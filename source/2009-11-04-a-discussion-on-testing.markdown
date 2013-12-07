--- 
layout: post
title: A discussion on testing
comments: true
categories:
- discussion
- rails
- ruby
- Ruby On Rails
- testing
- work
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
In this week code review meeting, I open a discussion about testing code of Ruby on Rails. Actually I think the test for a complex system is not that easy if you wanna do it gracefully, but it's still worth starting in small steps, that's what's important. I'd like to share the ideas people contributed, and the included contents are as following:
Andy:
<blockquote>
Tried something new for RoR testing yesterday, it's factory_girl(fixtures replacement solution. <a href='http://github.com/thoughtbot/factory_girl'>see more details</a>). In this week code review, I show the testing code, and also have questions about test:

1. How to make sure that you test all(99.5%) situations.
2. If you test before you code, how to control/ensure the function points properly?

feel free to comment here if you have any thoughts on it.
</blockquote>
I commented in front:
<blockquote>
My understanding of TEST:
It means we should "program"(with mock and stub) one more time in different rule(based on the testing framework) to make sure features working correctly. but there is still a big chance to make mistake in both side(twice programming), so non-structured testing does not work very well. idea?
</blockquote>
Then Guolei's view point:
<blockquote>
I don't think writing test code is "twice programming".
1. Test code should be very plain and very simple. Mock and stub do make it complex, but there's rarely case requiring mock and stub. If you find your test code is more complex that function code, then you are going wrong way.
2. Actually writing test code can not be called "program". It's more like you are telling computer what it should do. It's from the aspect of business logic, non with technique. So you should never make mistake when you get familiar with it, even so, it takes no time to fix it.
3. The value of test code shines when refactoring code and for complex logic. I think Andy's code is not a good example because the logic is so simple that there's more test code than function code.
</blockquote>
Gary's sample:
<blockquote>
Your test code is for a process. I would rather test a method one time, I this case I can try all possible input and test.
for example:
</blockquote>
<pre name="code" class="ruby">
describe "article?" do
    it "should figure out the page is article type" do
      2.times do
        @page.page_parts.create
      end
      @page.article?.should == true
    end
    it "should figure out the page is not article type" do
      2.times do
        @page.page_parts.create(:group_id => 0)
      end
      @page.article?.should == false
    end
  end
</pre>
Then I posted:
<blockquote>
Yeah.. I don't doubt about the value of writing test code, and I totally agree on what GL mentioned should be the basic principle of adding test code.

The problem is, when I wanna cover all the situations/cases, there is, so far, no good way than writing lots of cases for it. so how to ensure it covering all the test-needed points, specially the business logic?
It's not something about which skills(mock and stub) should be used somehow, it's about what should be test and how to make sure you fully test what you want to test.

For example in my test code, how to ensure it can fully test the Item model? if I missed points, is this test still believable? I know surely it should cover all situations as what we want, but how to make the coverage happened correctly? The test code may save my time and energy when refactoring or doing enhancement, but if it's not that correctly covering the case, does it still play an important role?

I am a bit confused of the way we are testing the system rather than writing test code for specific function, any more ideas?
</blockquote>
JP's response followed up:
<blockquote>
As previously mentioned, I think its best to look at tests as a future investment, not a "I cover every point". There are two types of "future investment"

1. Immediate future. You are about to write some code (function) and you know how you want it to work and what the different possibilities are. You write the test code first and then code the function. Now, as you code the function, it is much faster to see if it works (this is especially true for complex logic like the content inputting system).

2. Further future. You have a list of "known" situations/cases. You might modify the working code in the future and in the future you might forget what all these different situations/cases are - but you know what they are right now. So, you write test code. Now, if you modify the code in the future and the tests still pass, you can feel comfortable that the code you modified did not break any "known" conditions.
In both cases tests cannot find "unknown" cases...and I don't think this is the point.

Two specific cases come to mind where I felt I used test code really well:
a) Immediate Future: When first starting the Erlang queue system I wrote a number of test cases to simulate the trainer client's various conditions. This allowed me to write the erlang code and then run a bunch of cases on it really quickly which saved a lot of time (otherwise I would have had to do lots and lots of clicks on the Trainer Client). Unfortunately, once the queue system started integrating all of the other apps and connecting to FS I could no longer find a reasonable way to keep these test cases to work (as so many things would have to be stubbed).

a) Further future: The old, old carb.rb model. This was incredibly complex (even from the beginning). I wrote test code after writing that model. Then, a few months later, made significant changes to that model but was able to use that test code to insure I covered all the conditions (this was before Andy started working on it).
</blockquote>
Seven's response:
<blockquote>
I'm only on the first step of writing test code, but it do helps me free my hands and ears from testing calls with FreeSWITCH. Nice.
</blockquote>
My last response:
<blockquote>
I think I got what I want from above discussion, thanks to all for sharing your view points or samples.
</blockquote>
