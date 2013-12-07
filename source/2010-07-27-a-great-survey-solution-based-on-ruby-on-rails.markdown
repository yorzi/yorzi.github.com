--- 
layout: post
title: A Great Survey Solution Based On Ruby on Rails
comments: true
categories: 
- gem
- Gem/Plugin
- plugin
- quiz
- rails
- Ruby On Rails
- survey solution
- surveyor
- Web Application
- Web2.0
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
I've been always looking for a powerful and flexible survey solution for a while, now I find it : <a href="http://github.com/breakpointer/surveyor">Surveyor</a>.

<strong>What's a Survey? </strong>
Here is a brief look at the similarities and differences between forms, surveys, questionnaires and quizzes.

Forms are a series of fields to be filled out by a user. Some forms are highly structured (such as a User form, or an Address form). Those highly structured forms can be created beforehand by a developer because they can map directly to models in the database. Other forms are highly unstructured, such as a questionnaire about your favorite types of food which are volatile. So form is simple structured format.

A Survey is a type of Form. Surveys are semi-structured data, in that we want to formulate the questions so they have “mineable” data, but they are not so structured as to be directly mappable to database tables (unless we desired to have one table per survey, do we?). Also If a survey field is not appropriately filled out (such as a misformatting), the user should be prompted to correct his/her answer. According to this needs, surveys should not prevent the user from completing them if they miss an answer, however. A Questionnaire is a type of Survey and meanwhile, a Quiz is also a type of Survey.

<strong>How To Set Up Surveys Via Surveyor?</strong>
There is already a clear manual for helping people to use Surveyor <a href="http://github.com/breakpointer/surveyor">here</a>. You can find most of what you want directly in <a href="http://wiki.github.com/breakpointer/surveyor/">Surveyor's official wiki</a>. However, I still want to share my experience on using Surveyor.

<strong>Install Surveyor.</strong>
As a plugin:
<pre>gem install haml
gem install fastercsv
script/plugin install git://github.com/breakpointer/surveyor.git -r 'tag v0.11.0'
</pre>
Or as a gem:
<pre># in environment.rb
config.gem "surveyor", :version => '~> 0.11.0', :source => 'http://gemcutter.org'
---
rake gems:install</pre>
Surveyor is relied on haml and fastercsv(this is for supporting export csv survey results)
Generate assets, run migrations:
<pre>script/generate surveyor
rake db:migrate</pre>
Try out the "kitchen sink" survey:
<code>rake surveyor FILE=surveys/kitchen_sink_survey.rb FIXTURES=surveys/fixtures
</code>
The rake surveyor task overwrites previous surveys by default, but can append instead:
<code>rake surveyor FILE=surveys/kitchen_sink_survey.rb FIXTURES=surveys/fixtures APPEND=true</code>

Now start your Rails server, you will see the demo survey "kitchen sink" on localhost:3000/surveys. This demo is pretty useful for you when you generate your own survey pattern. Because in kitchen sink demo, most of "Survey API" are there.

<strong>Survey Sample</strong>
Well, let's create our first survey. I paste my first as below, we can take a look at the way Surveyor support.
<code lang='ruby'>
#/surveys/salon_survey.rb
survey "欢迎您访问Idapted技术沙龙活动调查问卷！" do

  section "[Rails系统重构最佳实践]@beta-salon 2010/07/24" do
    # A label is a question that accepts no answers
    label "<b>希望您填写自己的个人信息，我们会为您提供最快速和专业的Ruby on Rails技术活动资讯！</b>"

    # When :pick isn't specified, the default is :none (no checkbox or radio button)
    q_1 "请填写您的姓名(中英文名均可)"
    a_1 :string
    
    q_3 "请填写您的电话(如果我们有更多后续的技术交流活动，我们会发短信通知您:))"
    a_3 :string

    q_3 "请填写您的邮箱(如果我们有更多后续的技术交流活动，我们也会发邮件通知您:))"
    a_3 :string

    # A basic question with checkboxes
    # "question" and "answer" may be abbreviated as "q" and "a"
    q_2 "我们公司(Idapted)的产品涉及到以下几种技术，请选择您喜欢的主题，我们的研发团队会根据大家的反馈继续开展相关技术交流活动！", :pick => :any
    a_1 "Ruby on Rails"
    a_2 "Flex/Flash"
    a_3 "VoIP/FreeSwitch"
    a_4 "Erlang"
    a_5 "Titanium/iPhone/iTouch/iPad Development"

    # A dependent question, with conditions and rule to logically join them  
    # the question's reference identifier is "2a", and the answer's reference_identifier is "1"
    # question reference identifiers used in conditions need to be unique on a survey for the lookups to work
    q_2a "请简单说明为什么您对所选择的技术感兴趣:)"
    a_1 "说明：", :text
    dependency :rule => "A or B or C or D"
    condition_A :q_2, "==", :a_1
    condition_B :q_2, "==", :a_2
    condition_C :q_2, "==", :a_3
    condition_D :q_2, "==", :a_4
    condition_E :q_2, "==", :a_5

    q_4 "您使用Ruby on Rails开发有多长时间了？", :pick => :one, :display_type => :slider
    ["刚开始", "半年", "一年", "两年", "两年以上"].each{|level| a level}
    
    # Surveys, sections, questions, groups, and answers also take a custom css class for covenience in custom styling
    q_6 "请介绍一下您自己的工作和感兴趣的技术", :custom_class => 'address'
    a :text, :custom_class => 'mapper'
    # validations can use regexp values
    validation :rule => "A"
    condition_A "=~", :regexp => /[0-9a-zA-z\. #]/
  end
end
</code>
In above sample, I create a "survey", then I also create a "section" inside a survey. Yeah, you can define many section for a survey to make the whole survey being like a wizard, that's pretty interesting. In on survey, there are more than 15 types of question, you can define a survey as using plain English, what you should obey is to refer to Kitchen Sink sample, it means you can only define a question type according to the certain rule, don't worry, the rule is simple.

Once you finished defining the survey, it means you now have a ruby file, say salon_survey.rb, you should run the following commend in your terminal to migrate all your survey items into your application, remember the append command, it will let you not to delete previous survey which stored in the same application.
<pre>rake surveyor FILE=surveys/salon_survey.rb FIXTURES=surveys/fixtures APPEND=true</pre>
Wow, you now have your new survey list in the Survey root path after you restart your server. I guess you will like it.

<strong>Customize Survey</strong>
All go well so far, But, there is a big weakness of this survey solution if you only use it as above. Because the Surveyor doesn't support any easy way to manage the survey results. You should add the administration side in your application by yourself. I will also give you some hints on doing this.

Before your create management part for survey results, I remind you take a look at the survey configure file where you can do some really simple config for specific survey, such as define welcome page and finish page, or the survey title you want to customize. It's something as below:
<code lang='ruby'>
# Initializers/surveyor.rb
# Loaded once. Restart your app (even in development) to apply changes made here
Surveyor::Config.run do |config|
  config['default.relative_url_root'] = "surveys" #nil # "surveys"
  config['default.title'] = "EQ英语(Idapted) 技术沙龙调查问卷" #nil # "You can take these surveys:"
  config['default.layout'] = "surveyor_custom" # "surveyor_default"
  config['default.index'] = nil#:welcome_pages_path #:welcome_pages_path # "/surveys" # or :index_path_method
  config['default.finish'] =  :thankyou_pages_path # "/surveys" # or :finish_path_method
  config['use_restful_authentication'] = false # set to true to use restful authentication
  config['extend'] = %w(survey surveyor_helper surveyor_controller) #%w()
end
</code>

<strong>Survey Results Statistics</strong>
OK, last hints about adding management part of survey, here we should know clearly what's the survey's structure. So what's Survey's data structure? It's like this:
<pre>
# Survey structure
Survey-------Section1---------Question1---------Many Answers(From different user)
                                      ---------Q2
                                      ---------Q3
                                      ---------More Question
          -------Section2
          -------More Sections

#Response Structure. Each User Has one unique <strong>ResponseSet</strong>
ResponseSet---------Response1
                    ---------Response2
                    ---------More Responses
</pre>
So you can display all results as you need. I do it as below:
<code lang='ruby'>
#results_controller.rb
class Admin::ResultsController < Admin::BaseController
  layout "results"
  
  def index
    @surveys = Survey.all
  end
  
  def show
    @survey = Survey.find(params[:id])
    @response_sets = @survey.response_sets
    @questions = SurveySection.find_by_survey_id(params[:id]).questions
  end
end

#View show.html.erb
<table class="list_table">
  <tr>
    <th>ID</th>
    <th>Code</th>
	<% @questions.each do |question| %>
		<% next if question.display_order == 1 %>
		<th><%= "[" +question.display_order.to_s + "]" + question.text  %></th>
	<% end %>
  </tr>

<% @response_sets.each do |r_set| %>
  <tr>
    <td><%=h r_set.id %></td>
    <td><%=h r_set.access_code %></td>
	<% @questions.each do |question| %>
		<% next if question.display_order == 1 %>
		<td><%= display_response(r_set,question) %></td>
	<% end %>
  </tr>
<% end %>
</table>

#results_helper.rb
module Admin::ResultsHelper
  def display_response(r_set,question)
    sets = r_set.responses.select{|r| r.question.display_order == question.display_order}
	  	if sets.size == 0
  			return "-"
  		elsif sets.size == 1
  			return (sets.first.string_value || sets.first.text_value || show_answer(sets.first))
  		else
  		  txt = ""
        sets.each do |set|
          txt << show_answer(set) + "<br/>"
        end
        return txt
     end
  end
  
  def show_answer(set)
     set.answer.text
  end
end
</code>

God, I really make a long post, hope you can find something useful, feel free to contact me if you have any confusion.
