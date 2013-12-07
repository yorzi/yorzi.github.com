--- 
layout: post
title: Comparing Equality (==, eql?, equal?) and Case Equality (===) in Ruby
comments: true
categories: 
- ==
- ===
- case
- eql?
- Ruby
- ruby
- Ruby On Rails
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
In weekly code review, GL mentioned a weird issues :
<code lang="ruby">
def self.test(obj)
    case obj.class
    when Student, TrialPlan
      puts "1"
    when Call
      puts "2"
    else
      puts "3"
    end
end
</code>
This doesn't behave as expected. When we run test(Student.first), it prints out "3"!

but this works fine.
<code lang="ruby">
def self.test(obj)
    case obj.class.to_s
    when "Student", "TrialPlan"
      puts "1"
    when "Call"
      puts "2"
    else
      puts "3"
    end
end
</code>

Then I searched around for explaining this, I found the <em>case statement</em> in Ruby is very different with what in other languages. Ruby implements the Case statement according to its special operator "===", which is not the same as "==".

what's difference? See below explainations:
<a href="http://www.skorks.com/2009/08/how-a-ruby-case-statement-works-and-what-you-can-do-with-it/">how-a-ruby-case-statement-works-and-what-you-can-do-with-it/</a>
<a href="http://blog.mustmodify.com/2008/11/ruby-case-statement-comparison-feature.html">ruby-case-statement-comparison-feature.html</a>
