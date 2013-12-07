--- 
layout: post
title: Polymorphic association in factory_girl
comments: true
categories:
- factory girl
- Gem/Plugin
- polymorphic
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
I tried factroy_girl yesterday to work with rspec framework, It's excellent way to support testing, however, the polymorphic association in factroy_girl almost defeated me.
The factory definition in my code is as:
<pre name='code' class='ruby'>
Factory.define :item do |i|
    i.status 0
    i.related_with_id 1
    i.association :unit
end

Factory.define :study_record do |sr|
    sr.association :content, :factory => :item
    sr.add_attribute :interaction_id
    sr.add_attribute :finished_at
end
</pre>
Then I did this:
<pre name="code" class="ruby">

    @item = Factory(:item)
    @study_record = Factory(:study_record)
    @item.study_records << @study_record

</pre>
But actually, this does not work to associate @study_record with @item, the problem is that @study_record.content is totally a new instance of Item rather than @item. It seems that "<<" doesn't work in this case.
The right way to do so:
<pre name="code" class="ruby">

     @item = Factory(:item)
    @study_record = Factory(:study_record, :content => @item)

</pre>
Polymorphic association works, and it's better than the fixtures solution indeed.
