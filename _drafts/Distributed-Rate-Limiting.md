---
id: 668
title: Distributed Rate Limiting
date: 2018-11-11T19:41:49+08:00
author: shantanualshi
layout: post
guid: http://blog.shantanualshi.com/?p=668
permalink: /?p=668
categories:
  - Distributed Systems
tags:
  - Distributed Systems
  - Load Balancing
  - Rate Limiting
---
You are a software architect for an online publishing startup like Medium.com. Your startup expects over 20K registered users over the next 5 years and you&#8217;ve laid down your architecture carefully to handle the load.  <figure class="wp-block-image">

<img src="https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-1.png" alt="" class="wp-image-674" srcset="https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-1.png?w=1778 1778w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-1.png?resize=300%2C131 300w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-1.png?resize=768%2C334 768w, https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-1.png?resize=1024%2C446 1024w" sizes="(max-width: 1000px) 100vw, 1000px" data-recalc-dims="1" /> </figure> 

The client hits a load balancer. Depending on the User ID, the load balancer is configured to direct the request to appropriate web server. The setup is running perfect, until due to some reason, Server A dies. 

No problem, our load balancer is smart enough to know Server A is down and starts distributing Server A&#8217;s traffic to other servers equally. Server B is now handling users from 5001-10000 along with 1-1666. Server C is handling 10001-15000 along with 1667-3333 and so on. <figure class="wp-block-image">

<img src="https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-2.png" alt="" class="wp-image-675" srcset="https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-2.png?w=1756 1756w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-2.png?resize=300%2C116 300w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-2.png?resize=768%2C297 768w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/11/image-2.png?resize=1024%2C395 1024w" sizes="(max-width: 1000px) 100vw, 1000px" data-recalc-dims="1" /> </figure> 

In no time, you realise that Server B was already on the verge of failure. Due to to the additional load, Server B dies! 

Your load balancer tries to split B&#8217;s load on to other servers. Effectively now, servers C and D are handling 200% of their initial load! As an upshot, Server C dies! 

Server D is on flames!

Your system is experiencing **_cascading failures._**

<blockquote class="wp-block-quote">
  <p>
    <em>A </em><strong><em>cascading failure</em></strong><em> is a process in a system of interconnected parts in which the failure of one or few parts can trigger the failure of other parts and so on. </em>
  </p>
</blockquote>

<hr class="wp-block-separator" />

You don&#8217;t want this to happen again. Server A failed because 

Congratulations, your API is experiencing what is popularly known as the **_thundering herd problem. _**

<blockquote class="wp-block-quote">
  <p>
    <em>In the simplest terms, when many users make a request to the same piece of data at the same time, a thundering herd problem is triggered. Thus the system thrashes briefly while a herd of processes thunders through. This problem usually occurs in a highly concurrent environment with many users.</em>
  </p>
</blockquote>