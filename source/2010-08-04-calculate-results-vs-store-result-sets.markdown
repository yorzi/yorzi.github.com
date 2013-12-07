--- 
layout: post
title: calculate results VS. store result sets
comments: true
categories:
- case-study
- database
- db
- db optimization
- Deployment
- instant calculate
- Mysql
- result set
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  _wp_old_slug: ""
---
Firstly, what's the results in title? For example, the results may be learners who will be alive in coming two weeks, or the results may be study times of one learner, etc. Generally, results should be some data coming from analyzing other data.

Here my question is, how can we get certain results much faster and easily?

<strong>Case 1:</strong>
We want to pick up a name list, all people in the list should be under certain condition, say, condition A, condition B, condition C, so normally, we just select the results which obey the rule(condition). Right? It depends.

If name list is always dynamically different in condition A,B,C, it's really hard to store the results set, we have to calculate instantly to make sure the results is accurate.

If name list is very difficult to figure out in condition A,B,C, we should store the stable part of the result set, so that we will not get stuck when calculate tons of data very time.

<strong>Case 2.</strong>
We want to show study times of a learner, how can we do that? Should we store the study times as one attributor of study record or should we just make one study record as one-time study? Obviously, it depends on the complication of study record and the definition of one-time study. 

In our case, one study record is instantly changed when it's in different status, so storing study times in study record is not a good idea because the results might be locked when status changes. But if we calculate study times based on its status, it will be more reliable and accurate. and also it will not be locked when status is with exception.

<strong>Conclusion:</strong>
To store result set, is a way to cache results, but some times it's not easy to maintain the result sets, for instance, if there are too many conditions when getting a results set, it's always in heavy load to update result sets, you have to listen to every condition level changes. If the situation is complex, remember to cache your result set and maintain it carefully.

To calculate results instantly lets you ignore the real data, you just need to use the rule carefully, that will be more accurate, because you very time select what the rule defines. However the disadvantage is, when the data sets is large, you have to pay more to do that instantly, so you want to do a cron job or just cache the stable part of previous result sets.  
