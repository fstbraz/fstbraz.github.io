---
layout: post
title: "DNS from Namecheap to Cloudflare on Github Pages"
date: 2015-08-29
excerpt: "Testing my website I've checked that first byte delivery it was a bit delayed, after identifying the problem, I have the idea of transfering the DNS to solve the problem. So, what's next is the analysis and the solution."
tags: [DNS, Namecheap, CloudFlare, Github Pages]
feature: /assets/img/fulls/02.jpg
comments: true
---

Testing my website [fausto.xyz](/) on [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/), I've checked that first byte delivery it was a bit delayed, after identifying the problem, I have the idea of transfering the DNS for [CloudFlare](https://www.cloudflare.com/) to solve the problem. So, what's next is the analysis and the solution.

### 1. What is the problem?

In a rapid analysis, we could see that exists is a 0.6 second delay on the first request to the server, (DNS Lookup), also that exists a second request.

![Screenshot]({{ site.url }}/assets/img/posts/webpage-legend.jpg)
![Screenshot]({{ site.url }}/assets/img/posts/webpage-test-1.jpg)

If we go deep in the analysis we see that the second request is a [302 redirect](https://en.wikipedia.org/wiki/HTTP_302).


### 2. 302 Redirects

After a quick search on Google, I found an [Analyzing the GitHub Pages Waterfall Chart](http://helloanselm.com/2014/github-pages-redirect-performance/) article, where [@helloanselm](https://twitter.com/helloanselm/) found that [Github Pages](https://pages.github.com/) redirects sites with a `A` DNS record configuration.

I'm using that configuration on [Namecheap](http://www.namecheap.com/?aff=89940), that doesn't support the `ALIAS` record, suggested on [Setting up a custom domain with Pages](https://help.github.com/articles/setting-up-a-custom-domain-with-github-pages/).

My other post completes all the information about this subject. -> [DNS configuration on GitHub Pages with Namecheap](http://fausto.xyz/DNS-configuration-on-Github-Pages-with-Namecheap.html).

For knowing more about an `ALIAS` you could also read -> [Why ALIAS-type DNS Records Break The Internet](https://iwantmyname.com/blog/2014/01/why-alias-type-records-break-the-internet.html) by [@norbu09](https://twitter.com/norbu09).


### 3. CloudFlare DNS configuration for GitHub Pages

After we get a free account, we have to add our website. 

![Screenshot]({{ site.url }}/assets/img/posts/cloudflare-add-site.png)

After CloudFlare import our DNS records, we have to delete the two `A` records, and replace for one `CNAME` that points for **username.github.io.**. Use **@** to reference the root of the domain.

![Screenshot]({{ site.url }}/assets/img/posts/cloudflare-add-record.png)

Now we should have two `CNAME` records.

![Screenshot]({{ site.url }}/assets/img/posts/cloudflare-cname-records.png)

After we modify the DNS records on CloudFlare, we have to transfer the DNS from Namecheap.


### 4. Transfering DNS from Namecheap to CloudFlare

We can start doing sign in on our [Namecheap](http://www.namecheap.com/?aff=89940) account, select the domain name, after that select the option **Transfer DNS to Webhost.** .

![Screenshot]({{ site.url }}/assets/img/posts/namecheap-dns-record.png)

Don't forget that the nameservers that I've used **gail.ns.cloudflare.com** and **hugh.ns.cloudflare.com**, could not be the nameservers that are assigned to your account by CloudFlare.


### 5. It works? 

After some days with the new DNS configurations from CloudFlare, I could say that I'm happy with the result. The 302 redirect is vanish and first byte time delivery is kicking ass.

![Screenshot]({{ site.url }}/assets/img/posts/webpage-legend.jpg)
![Screenshot]({{ site.url }}/assets/img/posts/webpage-test-2.jpg)

I don't know the way that this affects my website on GitHub Pages, but I know that CloudFlare ships with a DDoS protection, so I only could see advantages.

If you want to know more about all kind of DNS records, you can find good information in this article-> [Differences between the A, CNAME, ALIAS and URL records.](http://support.dnsimple.com/articles/differences-between-a-cname-alias-url/) by [DNSimple](https://dnsimple.com/)
