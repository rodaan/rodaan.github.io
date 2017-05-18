---
layout: post
title:  "Installing NodeJS and NPM on AWS"
date:   2016-10-24 00:11:43 -0700
categories: hackathons ec2 aws
---
This past weekend, I entered the Small Business Hackathon sponsored by Intuit with some friends. It was pretty fun. Food was great and there was a lot of cool swag.  

We ended up making a quick checkout and inventory management tool for nonprofit businesses such as Salvation Army and Goodwill. The tool was comprised of an inventory management dashboard and a mobile app that allowed users to take photos to catalog items quickly. When an item was scanned, the inventory would be quickly updated and the item would be displayed on the dashboard. When a customer of the nonprofit decided to buy an item, an employee of the nonprofit could take and photo and the tool would use image recognition to identify which item was being purchased.   

It was a cool idea but the app didn't end up working as well as we hoped as the image processing actually ended up taking a while to complete. Actually, while I'm writing this now, I realized what we could have done to exponentially speed up the process. Oh well.   

Anyways, the point of this article was to detail an issue I found when deploying a Node service on AWS.  

When I was working along setting up our backend web service, I decided to finish deployment to AWS once I had the basic Node server running. I have a lot of experience with the heartache of deploying applications AFTER development so I decided to get it over with early.  

So after trying to deploy the webapp, I discovered after sshing into my EC2 instance that it was missing one crucial factor to getting my application running: IT WAS MISSING NODE!  

So to save future Rodaan from wasting time again, I decided to make this post to highlight the steps to installing node on EC2:  

1. Install any updates to the EC2 instance:  
{% highlight bash %}
sudo yum update  
{% endhighlight %}

2. Install necessary tools to build node to the EC2 instance:  
{% highlight bash %}
sudo yum install gcc-c++ make  
sudo yum install openssl-devel  
{% endhighlight %}

3. Install git which you need to get the updated node binaries:  
{% highlight bash %}
sudo yum install git
{% endhighlight %}

4. Clone git repo with node binaries:  
{% highlight bash %}
git clone https://github.com/nodejs/node.git  
{% endhighlight %}

5. Decide which version of Node you want to install and "make" node (this may take 30 minutes or more):  
{% highlight bash %}
cd node  
git checkout v4.6.1  
./configure
make
sudo make install
{% endhighlight %}

6. Node that node is installed, add it to the superuser's path so you can actually use it to install more packages:  
{% highlight bash %}
sudo su  
vi /etc/sudoers  
{% endhighlight %}

7. On the VI editor go to the line that says (if you are new to VI, use the down keyboard arrow to do so):  
{% highlight bash %}
Defaults     secure_path = /sbin:/bin:/usr/sbin:/usr/bin  
{% endhighlight %}
and add this to the end of that line (use the right keyboard arrow to get to the end of the line):  
{% highlight bash %}
:/usr/local/bin  
{% endhighlight %}
Now you can save your changes by hitting ESC and typing:  
{% highlight bash %}
:wq!
{% endhighlight %}
You can now escape su mode (superuser mode) by typing:  
{% highlight bash %}
exit
{% endhighlight %}

8. Now download the npm binaries:  
{% highlight bash %}
git clone https://github.com/npm/npm.git  
{% endhighlight %}

9. Finally install npm:
{% highlight bash %}
cd npm  
sudo make install  
{% endhighlight %}

And there you have it! You've successfully installed node and npm! I hope this helps! If you have any questions feel free to email me! My next post will likely be one about permissions on Linux machines since I find myself dealing with them so often so keep a lookout for that!  

