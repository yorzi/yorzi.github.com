--- 
layout: post
title: find_in_batches is not working
comments: true
categories:
- bug
- find_in_batches
- rails
- rake
- Ruby On Rails
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
Days ago, I came across a situation in which <a href="http://api.rubyonrails.org/classes/ActiveRecord/Batches/ClassMethods.html">find_in_batches</a> does not work correctly, the sample code is as below:
<code lang="ruby">
#NOT WORKING AS EXPECTED.
namespace :studycenter do
  desc 'generate item extra items'
  task :update_extra_items => :environment do
    puts "starting at #{@time = Time.now}......"
    Item.find_in_batches(:conditions => {:content_type => "Scenario"}) do |items|
      items.each do |item|
        begin
          if item.extra_items.blank?
            item.related_lessons.each do |extra|
              @item = ItemExtraItem.create({:item_id => item.id, :extra_item_id => extra.id})
              puts "=============================================#{@item.id}"
            end
          end
          puts "finished item with ID:#{item.id}"
        rescue Exception => e
          puts "something wrong happened!! item with ID:#{item.id}"
          next
        end
      end
      puts "------------------spent #{(Time.now - @time)/60} minutes!"
    end
    puts "finished at #{Time.now}, totally, spent #{(Time.now - @time)/60} minutes!"
  end
end
</code>
Then I refactor this task, so I can migrate data which generated day by day.
<code lang="ruby">
#WORKING WELL
namespace :studycenter do
  desc 'generate item extra items'
  task :update_extra_items => :environment do
    puts "starting at #{@time = Time.now}......"
    (1..300).each do |n|
      items = Item.all(:conditions => ["content_type = 'Scenario' and items.created_at >= ? and items.created_at < ?",("2010-03-13".to_date - n.days), ("2010-03-13".to_date - (n-1).days) ])
      items.each do |item|
        begin
          if item.extra_items.blank?
            item.related_lessons.each do |extra|
              @item = ItemExtraItem.create({:item_id => item.id, :extra_item_id => extra.id})
              puts "=============================================#{@item.id}"
            end
          end
          puts "finished item with ID:#{item.id}"
        rescue Exception => e
          puts "something wrong happened!! item with ID:#{item.id}"
          next
        end
      end
      puts "------------------spent #{(Time.now - @time)/60} minutes!"
    end
    puts "finished at #{Time.now}, totally, spent #{(Time.now - @time)/60} minutes!"
  end
end
</code>
Do you know why find_in_batches is not working here?
PS:  item.related_lessons is an item array, so the item and its related lesson are all the same class.

<strong>Answer</strong>: In find_in_batches loop, the specific Class only has a range of its instances(e.g. 1~1000), so item.related_lessons can not find the item(e.g. 1001) out of the range..
