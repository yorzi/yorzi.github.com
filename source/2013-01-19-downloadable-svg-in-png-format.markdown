---
layout: post
title: "Downloadable SVG in PNG Format"
date: 2013-01-19 16:08
comments: true
categories: 
- svg
- highcharts
- downloading
- charting
---
Recently, I worked on some interesting features, we use [Highcharts] and/or [Raphaeljs] to build complex charts, including bar chart, scatter chart or heat map, etc. In an extreme sample, we build a complicated one-page charting engine by which user is able to compose a group of conditions and then render a meaningful chart according to what are selected. It's pretty cool. 

Meanwhile, client is willing to download these generated charts on individual chart level. They also want to have an ability to share the individual chart as a link or even as a piece of HTML code. What's the best solution to add these functionalities? Well, we did try many solutions for the features, let me show you how we make it finally.
 
#### Start from a HTML template

<script src="https://gist.github.com/4443672.js"></script>

Above HTML code is the generated content on my page, I will mainly explain the solution based on it. Here is also a sample SVG file: [sample.svg], you can use it to go through the whole senario if you want to experiment by yourself.

#### Deal with SVG via HTML5 Canvas

HighCharts and Rapheal are JS libaries by which you are able to generate complex [SVG] charts, normally, people can not download a svg file directly, and it's also not a popular image format for sharing around. We'd better convert it to a PNG or JPG image, as PNG and JPG format is downloadable from web page. I will take PNG format as a sample in this post.

How to convert a SVG image to a PNG image? Mainly, you can do the convertion job from server side. There is a SVG toolkit provided by Apache which is named as [Batik]. But I don't like this solution, it's a bit comoplex to install Batik and make it work with Ruby on Rails. I'd like to work the convertion out via pure javascript. Yes, use [canvg] to move all SVG information to a HTML5 Canvas object.

<script src="https://gist.github.com/4452589.js"></script>

Using the HTML5 canvas element, you can create all sorts of cool graphics client-side on the fly using Javascript. There is a neat function on the the canvas object called toDataURL(). This functions encodes the image data as a base64 encoded PNG file and returns it as a [data: URI]. By using the data:URI string, you can make it a downloadable PNG file. 

There is also a libary to help you do so, it's [Canvas2Image] that can convert canvas to image as BMP, PNG or JPEG format.

<script src="https://gist.github.com/4467012.js"></script> 

#### Customize default filename while downloading

Canvas2Image lib will implement a pop out window to allow you download the data:URI as a PNG image file with a default name `download`, which is not acceptable by our client, I have to figure out a way to customize the downloadable filename. 

<script src="https://gist.github.com/4467156.js"></script>

It might be easy if you just want to cover your Chrome or Firefox user, as there is a `download` attribute for `<a>` tag, when you set it as something like `<a src='the data:uri string' download='test.png'>` then you will get the default filename in this the case when you click the download link.

I am not lucky, I have to cover IE9 at least. So I need to push the data:uri to server, then I can render the data with specific headers(see below code), that will make the downloadable file with a customized file name.

<script src="https://gist.github.com/4467051.js"></script>

Pay attention to above ```html2canvas([$(".hidden_container")[0]],{ … })``` parts. It helps to convert whole HTML code to a canvas based on [html2canvas] lib, that's our case as we have to wrap up some HTML code out side the the charts.

#### A trick to overcome IE9 issue

When you work on IE9, the canvg fails to translate the SVG to Canvas, it seems IE9's `DOMParser()` is not able to parse the SVG successfully. After some search from Google, we found only one line code will resove the SVG parser issue. Just replace some invalid string in SVG data as below: 

<script src="https://gist.github.com/4467165.js"></script>

#### Conclusion

To summarize this post, you are suggested to use several JS libs above to convert ```SVG``` to ```Canvas```, then convert ```Canvas``` to ```PNG``` file, if you also want to customize a piece of HTML code out side the SVG chart, then you are able to convert ```HTML``` to ```Canvas```, then again from ```Canvas``` to ```PNG```, when you want to set a customized filename for the generated PNG file, you have to send the data:uri string onto server side, then rewrite the response headers, all these handling will implement a downloading feature for you.

 
[html2canvas]: http://html2canvas.hertzen.com/ 
[sample.svg]: https://gist.github.com/4443811
[data: URI]: http://en.wikipedia.org/wiki/Data:_URI_scheme
[Canvas2Image]: http://www.nihilogic.dk/labs/canvas2image/
[canvg]: http://code.google.com/p/canvg/
[Raphaeljs]: http://raphaeljs.com/
[Highcharts]: http://www.highcharts.com/
[SVG]: http://www.w3.org/TR/SVG11/
[Batik]: http://xmlgraphics.apache.org/batik/#download