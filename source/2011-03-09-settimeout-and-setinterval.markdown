--- 
layout: post
title: "JS note: setTimeout and setInterval"
comments: true
categories:
- JavaScript
- javascript
- js
- setInterval
- setTimeout
- UI/UE
status: publish
type: post
published: true
meta: 
  _edit_last: "1"
  aktt_notify_twitter: "no"
---
Yesterday, I discussed a JS issue with <a href="http://www.yakjuly.com/">Blade</a>, that I have to set up an automatic photo-switch effect on an existing page. I don't want to change anything except adding a piece of javascript for doing that job because this page is already messy up by another engineer. Blade suggested I should use <strong><a href="https://developer.mozilla.org/en/DOM/window.setTimeout">setTimeout</a></strong> for this effect.

<h4><strong>* Case Study</strong></h4>
The basic case is something like below(there are some other effects based on the structure and style, so don't affect others):
<code lang='html'>
<div id="tab_ls">
        <a class="active" id="haikou"></a>
	<a id="dalian"></a>  
        <a id="changsha"></a> 
</div>
	 
<div id="tab_con">
	<div style="display: block;" id="fk"> 	
		<div id="end"></div>
		<div id="ctt">
			<img src="http://www.2011roadshow.com/images/haikou.jpg">
                	<h3>会议城市：海口</h3>
			<p>时间：8月26日 14：00-18：00</p>
                	<p>地点：海口鑫源温泉大酒店</p>
	  	</div>
	</div>
        
	<div id="fk" style="display:none">
		<div id="end"></div>
	        <div id="ctt">
			<img src="http://www.2011roadshow.com/images/dalian.jpg">
                	<h3>会议城市：大连</h3>
			<p>时间：9月3日 14：00-18：00</p>
                	<p>地点：香洲花园酒店 </p>
		</div>
	</div>

	<div id="fk" style="display:none">
		<div id="end"></div>
	        <div id="ctt">
			<img src="images/changsha.jpg">
                	<h3>城市：长沙</h3>
			<p>时间：9月4日 14：00-18：00</p>
                	<p>地点：长沙潇湘华天大酒店</p>
		</div>
	</div>
</div>
</code>
Now the task is to write a js to roll the cities and regarding images, how to make it happen?
<h4>* Solution with <strong>setTimeout</strong></h4>
<code lang='javascript'>
<script type="text/javascript">
    var cities;
    var cityImages;
    var currentCity;
    var pause = false;
    var timer1;
    var timer2 ;
    
    function showNextImage()
    {	    	
    	if (pause) {
    		// do nothing
    	} else {
    		console.log("show next image");
    		console.log(currentCity);
    		if(cities.last() == currentCity) {
    			currentCity = currentCity.first();
    		} else {
    			currentCity = currentCity.next();
    		}
    		console.log(currentCity);
    		
    		var index = cities.index(currentCity);
    		console.log(index);
    		cityImages.hide();
    		console.log(cityImages.get(index));
    		$(cityImages.get(index)).show();
    		cities.removeClass("active")
    		currentCity.addClass("active");
    	}
    	timer1 = window.setTimeout("showNextImage()", 2000);
    }
    
	function repeatPlay()
	{	
		console.log("repeat play");
		showNextImage();
		if (timer2 != null){
			clearTimeout(timer2);
			timer2 = null;
		}
	}

  $(window).load(function(){
    cities = $("#tab_ls a");
    cityImages = $("#tab_con div#fk");
    currentCity = cities.first()
    console.log(cities);
    console.log("window load");
    repeatPlay();
    $("#tab_ls a").click(function(){
                clearTimeout(timer1);
		timer1 = null;
    		timer2 = window.setTimeout("repeatPlay()", 6000);
	});
  });
</script>
</code>
Actually, you can figure out this effect with <strong><a href="https://developer.mozilla.org/en/window.setInterval">setInterval</a></strong> as well. The difference between setTimeout and setInterval is how many times you want to run the function which is set as their parameters. setTimeout will execute the function only once when time is out. But setInterval execute the function repeatedly in certain interval which is set as a parameter.

Every time you should remember to clear the Timeout or Interval after finish your job through <strong><a href="https://developer.mozilla.org/en/DOM/window.clearTimeout">clearTimeout</a></strong> and <strong><a href="https://developer.mozilla.org/en/DOM/window.clearInterval">clearInterval</a></strong>. 

I have linked the regarding references for the four methods about, you should read the document and related samples to know more details.

More Resources:
<a href="http://hi.baidu.com/ruhaole/blog/item/af905fefc2dad33aadafd57a.html">如何在jQuery中使用 setInterval，setTimeout</a>
<a href="http://cn.dydou.cn/wyzz/2010/0710/13733.html">jQuery：Tab切换功能的集合</a>
