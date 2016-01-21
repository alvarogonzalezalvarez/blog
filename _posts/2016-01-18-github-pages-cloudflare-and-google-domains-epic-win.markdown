---
layout: post
title:  "Github Pages, Cloudflare and Google Domains: Epic Win"
description: "Combine Github Pages, Cloudflare and Google Domains in a perfect way: SSL, Caching, Naked Custom Domains and Email Forwarding for free!"
date:   2016-01-21 19:13:05 +0100
author: Álvaro González Álvarez
categories: ['Web Technologies']
imageprev: /img/github-pages-cloudflare-google-domains.png
comments: true
published: true
---
As you probably already know, you can create your own website using a __Github Repository__. The only thing you need is a new repository named **_username_.github.io**, where _username_ is your username on Github. Once created, as soon as you push your html files to the repository, your site will be up and running; you can check it out by typing in your browser `http://yourusername.github.io`. Easy, right?

Now that we have our site online, there are two things you should know about __Github Pages__:

1. It doesn't support `SSL`.
2. If you want to configure an __apex__ or a __naked__ domain as a `Custom Domain`, you will lose the benefits of Github's CDN.

But don't worry, we are going to solve these two points and gain even more features by combining __Github Pages__ with __Cloudflare__.

#__1 - Cloudflare: First Steps__#

Firstly, you need to have a domain name purchased. In this guide we will be using __Google Domains__, as it's incredibly easy to combine with __Cloudflare__ and __Github Pages__. Let's begin: 

1. Create a [Cloudflare's free acount][cloudflare-free].
2. When asked, enter your site URL. Cloudflare will assign to you two DNS name servers that you will have to configure in your Google Domains account.

#__2 - Google Domains: DNS Setup__#

Log into your __Google Domains__ account and follow the steps below:

1. If you want to, you can go to `Configure email` and configure an `Alias Email Address`.
2. Go to `Configure DNS` and select `Use custom name servers`. Now, enter the two DNS name servers that Cloudflare assigned to your site previously.
3. Copy or take a screenshot of your data below `Email forward`. In the next step, we will configure these entries on our Cloudflare account.

![Google Domains Email Forwarding](https://alvarogonzalezalvarez.com/blog/img/google-domains-email-forwarding-dns.png){: .jekyll-image }

#__3 - Cloudflare: Improving your Website__#

####__3.1 - Configuring a Naked Domain__####

Log into your __Cloudflare__ account and go to `DNS`. We will add two `DNS Records` in order to configure a __Naked Domain__ (http://example.com) for our __Github Page__ as follows (replace 'alvarogonzalezalvarez.com' with 'yourdomainname.com' and 'alvarogonzalezalvarez.github.io' with '_yourgithubusername_.github.io'):

![Naked Domain on Cloudflare for Github Pages](https://alvarogonzalezalvarez.com/blog/img/naked-domain-cloudflare-github-pages.png)

####__3.2 - Configuring Email Forwarding__####

Now we are going to add the entries that we copied before from our __Google Domains__ account (again, don't forget to replace 'alvarogonzalezalvarez.com' with 'yourdomainname.com'):

![Email Forwarding for Google Domains in Cloudflare](https://alvarogonzalezalvarez.com/blog/img/email-forwarding-google-domains-cloudflare.png)

Note that these last DNS settings could take several hours to propagate.

####__3.3 - Forcing SSL__####

As we stated before, __Github Pages__ doesn't support https, but don't panic; on __Cloudflare__, go to `Page Rules` and create a rule as follows (yes, I know you've already got it, but just in case, don't forget to replace alvarogonzalezalvarez.com with yourdomainname.com :D):

![SSL and https for Github Pages using Cloudflare](https://alvarogonzalezalvarez.com/blog/img/ssl-https-github-pages-cloudflare.png)

####__3.4 - Other Improvements: Caching, Minification, IPv6 Compatibility...__####

There are also other features that you can enable with your Cloudflare's free account:

1. Caching: Inside `Page Rules`, you can create a rule to cache everything and speed up your website.
2. Inside `Speed`, I would recommend to activate __JavaScript__, __CSS__ and __HTML__ __Minification__.
3. Go to `Network` and enable __IPv6 Compatibility__.

Feel free to explore and find out other useful settings.

#__4 - Github Pages: Creating the CNAME File__#

And finally, the last step. Go to your Github repository: **_username_.github.io**, create a file named `CNAME` and add a single line that specifies your naked custom domain (example.com). For example:

{% highlight ruby %}
example.com
{% endhighlight %}

Now, fire up your browser and test `https://yoursite.com`!

#__CONCLUSION__#

Congratulations. You have just created a website with the following features:

+ A solid and free web hosting.
+ SSL support.
+ Naked Custom Domain with the benefits of Github's CDN (www.yoursite.com will 301 redirect to https://yoursite.com).
+ Email Forwarding.
+ Automatic Javascript, CSS and HTML Minification.
+ IPv6 Compatibility.
+ Full caching.

Enjoy!

[cloudflare-free]: https://www.cloudflare.com/a/sign-up