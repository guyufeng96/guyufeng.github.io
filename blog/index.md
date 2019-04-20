# Welcom to Yufeng Gu's Blog!
<head>
<h2>
	<li><a href="/">Home</a></li>
		        	<li><a href="/about">About</a></li>
	        		<li><a href="/cv">CV</a></li>
	        		<li><a href="/blog">Blog</a></li>
<body>
<h3>
{% for post in site.posts %}
<li><span>{{ post.date | date_to_string }}</span> » <a href="{{ post.url }}" title="{{ post.title }}">{{ post.title }}</a></li>
	  {% endfor %}
		<li>31 Mar 2019 » <a href="{{site.baseurl}}/homework/hw2.pdf">An overview on the bootstrap.</a><br/>
		<li>18 Mar 2019 » <a href="{{site.baseurl}}/homework/hw1.pdf">Discriminative & generative: a preliminary study.</a><br/>
		<li>17 Jan 2019 » <a href="{{site.baseurl}}/article/High-Speed Rail, Housing Prices and Regional Disparities - Evidence from China.pdf">High-speed rail, husing prices and regional disparities - evidence from China.</a>

<footer>
	    		<ul>
	        		<li><a href="mailto:guyf96@qq.com">Email</a></li>
	        		<li><a href="https://github.com/guyufeng96">github.com/guyufeng96</a></li>
				</ul>
			</footer>
