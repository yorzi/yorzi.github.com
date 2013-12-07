--- 
layout: post
title: an A/B test solution in ROR
comments: true
categories:
- a/b-test
- EQenglish
- ielts
- landing-page
- ror
- routing
- Ruby On Rails
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
---
Last few days, I worked for a mission to add more flexible control to <a href="http://www.eqenglish.com">our website</a> landing pages. What I did is to add a "a/b" test feature for new landing pages, that means, if people have two designs and want to compare the results, they only release two versions of landing page, and then only get one url for the two versions of pages, after that the url will automatically redirect to different versions evenly, so that through Google analytics marketing people can easily decide which landing page is much better.

<strong>Landing pages A/B test solution:</strong>
<code lang="ruby">
class LandingsController < ApplicationController
  layout "layouts/blank"
  caches_page "ielts","ab_test"

  def ielts
    @landing_page = Landing.find_by_url_slug(params[:url_slug]) || Landing.valid_landings.first
    if @landing_page.ab_test?
      if not params[:channel].blank?
        redirect_to landing_ab_test_with_channel_path(["a","b"].rand,params[:url_slug],params[:channel])
      else
        redirect_to landing_ab_test_path(["a","b"].rand,params[:url_slug])
      end
    else
      render :layout => "layouts/landing_page"
    end
  end

  def ab_test
    @landing_page = Landing.find_by_url_slug(params[:type].to_s + "/" + params[:url_slug].to_s)
    (@landing_page = Landing.find_by_url_slug(params[:url_slug]) || Landing.valid_landings.first) if @landing_page.nil?
    render :layout => "layouts/landing_page"
  end
end
</code>
<strong>Routing:</strong>
<code lang="ruby">
   map.landing_trunk "ielts/:url_slug", :controller => "landings", :action => "ielts"
   map.landing_trunk_with_channel "ielts/:url_slug/:channel", :controller => "landings", :action => "ielts"
   map.landing_ab_test "ielts/sub/:type/:url_slug/", :controller => "landings", :action => "ab_test"
   map.landing_ab_test_with_channel "ielts/sub/:type/:url_slug/:channel", :controller => "landings", :action => "ab_test"
</code>

<strong>A/B test Sample:</strong>
<em>Suppose</em>:
              We release a type of landing page called : university
              And we have two kinds of different designs : called "a/university" and "b/university"
              Then we may release the landing page to many universities, such as "beida", "renda", "qinghua" etc.. they are different channels.

<em>Then we can</em>:
             Only release the url as "http://www.eqenglish.com/ielts/university" to any universities by following "/beida", "/renda", "/qinghua" etc...
             It should be like this "http://www.eqenglish.com/ielts/university/beida",  "http://www.eqenglish.com/ielts/university/renda"... etc.. (For client use)
             But in google analytics, you will see : "http://www.eqenglish.com/ielts/sub/a/university/beida"
                                                                  and : "http://www.eqenglish.com/ielts/sub/b/university/beida"  (For our analysis)

 It means, different landing page and different channel and ("a" or "b") will be in a unique URL for certain purpose. but for our client, they don't need to care about "a/b" test, system will redirect pages automatically.

Any involving comments are welcomed.
