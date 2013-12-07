--- 
layout: post
title: primary_key and foreign_key in Rails association
comments: true
categories:
- association
- belongs_to
- code
- has_many
- rails
- Ruby On Rails
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
The has_many and belongs_to association in Rails are with many optional parameters, they are actually the parameters for DB relationship, see more details by <a href="http://api.rubyonrails.org/classes/ActiveRecord/Associations/ClassMethods.html">clicking here</a>.

As a reminder to myself, I misunderstood the primary_key an foreign_key conditions in association, it should be set in both sides in some case, for instance:
<pre name="code" class="ruby">
class Student < ActiveRecord::Base
  has_many :trial_lessons, :foreign_key => :user_id, :primary_key => :profile_id
end
</pre>
Above code will let you invoke the student.trial_lessons, but if you want to use trial_lesson.student, you have to define the association as below:
<pre name="code" class="ruby">
class TrialLesson < ActiveRecord::Base
  belongs_to :student, :primary_key => :profile_id, :foreign_key => :user_id
end
</pre>
<blockquote><strong>Notice that</strong>: you actually set the same :primary_key and :foreign_key in both sides, it's because the DB relationship between these two Model can be described the same way..(it's only a way for me to remember the rule)</blockquote>
