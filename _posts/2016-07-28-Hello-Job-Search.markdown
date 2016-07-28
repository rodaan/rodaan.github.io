---
layout: post
title:  "Hello Job Search!"
date:   2016-07-28 00:11:43 -0700
categories: job search
---
Hi everyone! 

So I'm currently job searching, but as soon as I'm done, I'll be looking to be updating this blog whenever I come across an interesting problem or topic.

So to keep things short, my name is Rodaan and I'm a software engineer who likes solving problems. I am currently interested in machine learning, natural language processing, and cybersecurity.

This is the current problem I'm working on (it's much more complicated than this but you get the point!):

{% highlight javascript %}
let hired = false;
while(!hired){
	const lead = searchForJob();
	const interview = applyForJob(lead);
	let offer = false;
  if(interview){
    offer = doInterview(interview);
  }
  if(offer){
  	hired = true;
  	console.log('Finished!')
  }
}
#=> prints 'Finished' to console when hired and Rodaan celebrates.
{% endhighlight %}

Check out some of my work on github. I'll also keep my portfolio updated with things I've created that are presentable!
