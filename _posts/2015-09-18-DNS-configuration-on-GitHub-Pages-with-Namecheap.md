---
layout: post
title: "DNS configuration on GitHub Pages with Namecheap"
date: 2015-09-18
excerpt: "After submitting my site to GitHub and check that everything works, I didn't know how to point to my recently purchased domain. To accomplish that, I did some research hoping that other confused people can configure their on GitHub domain through this post."
tags: [DNS, Namecheap, Github Pages]
feature: /assets/img/fulls/01.jpg
comments: true
---

After submitting my site to GitHub and check that everuthing works in [fstbraz.github.io](/), I didn't know how to point to my recently purchased domain.
To accomplish that, I did some research hoping that other confused people can configure their [Namecheap](http://www.namecheap.com/?aff=89940) on GitHub domain through this post.

### 1. Add CNAME file in your repository.

 Create a new file on the root. Save with the name `CNAME`, without extension.

> yourdomain.com


### 2. Find your Host Records.

Sign in on Namecheap, select your domain and go to **All Host Records**. 

![Screenshot]({{ site.url }}/assets/img/posts/namecheap-hosts.png)


### 3. DNS Configuration.

**3.1**. Configure the @ (used to instance the name of the domain that points to the DNS), **IP Address/URL** to `192.30.252.153` and the **Record Type** for `A (Address)` with **TTL** .

**3.2**. Configure the **www** (the www subdomain), **IP Address/URL** for `username.github.io.` (with a dot) and the **Record Type** for `CNAME (Alias)` with **TTL** at `1800`.

**3.3**. In **SUB-DOMAIN SETTINGS** add one `@` on the first field, and duplicate the option from the step 3.1, on **IP Adress/URL** we can go with `192.30.252.154`.

![Screenshot]({{ site.url }}/assets/img/posts/namecheap-hosts-name.png)

**3.4**. Save it, and we are rockin! Don't forget that this changes can take time, because of the DNS propagation.

If you have no idea what a DNS is, you can check [this](https://support.google.com/a/answer/48090?hl=en) guide from Google.
