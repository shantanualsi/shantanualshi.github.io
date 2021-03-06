---
id: 40
title: 'Fault Tolerance in Distributed Systems: Distributed Consensus'
date: 2014-11-20T01:25:57+08:00
author: shantanualshi
layout: post
guid: http://shantanualshi.wordpress.com/?p=40
permalink: /2014/11/20/fault-tolerance-in-distributed-systems-distributed-consensus/
geo_latitude:
  - "1.352083"
geo_longitude:
  - "103.81983600000001"
geo_address:
  - Singapore
geo_public:
  - ""
categories:
  - Distributed Systems
tags:
  - Fault Tolerance
---
Back to writing after a while. Exam time! would try my best to stick around. Anyways, back to the topic-

Welcome the most sought after and esoteric topics in distributed systems- Distributed Consensus! A plethora of algorithms and their variants have been proposed to solve this problem. This is a very rigorous subject and we will scratch the surface in this article. Note that this article will cover the topic from a systems standpoint. We will remain silent on the algorithmic viewpoint for now.

First, lets see what do we mean by consensus. The fundamental problem in Distributed systems is that if a decision is to be made, all nodes in the system need to agree upon it. This is called consensus and is at the heart of many fault tolerance protocols. Let&#8217;s look at some examples &#8211; The decision on the final write ordering for eventual consistency, decision on the instruction order in replicated state machine, Distributed commit for transactions, other voting scenarios etc.

You can think of consensus in a variety of trivial applications. Decide on the majority in case of voting, or decide OK only if everyone is OK in the case of distributed commit, or decide on any proposal as in case of write ordering.

Okay, I assume you got a hang of what I&#8217;m talking about. Now let&#8217;s see the four common versions of Distributed consensus in case of failures. There are four versions of this problems.

**Version 1: Node Crash Failures; Channels are reliable; Timing is ****Synchronous**

Assume each node processes in lock-step rounds. One round is the time for receiving the input + local processing at the node + replying to the input. The consensus protocol for this scenario has been proved that consensus is deterministic only in the case when number of nodes is greater than _f+1_ where f is the number of nodes prone to crash.

Now, the notion of &#8217;round&#8217; can be implemented only because the Timing is Synchronous, in other words, the values are bounded. Ideally, you cannot bound the local processing time. Think of it as this way &#8211; a request to crack a complex password using brute force technique would take a long time. It&#8217;s still bound by a maximum value; however, not feasible enough to be considered for real world systems. Let&#8217;s make this clear &#8211; the notion of round has an implicit assumption that the local processing time is not _too high_ and is bounded by a value.

<figure id="attachment_43" aria-describedby="caption-attachment-43" style="width: 422px" class="wp-caption aligncenter">[<img class="wp-image-43" src="https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2014/11/distributed-consensus.png?resize=422%2C200" alt="Distributed Consensus Version 1" width="422" height="200" srcset="https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2014/11/distributed-consensus.png?zoom=2&resize=422%2C200 844w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2014/11/distributed-consensus.png?zoom=3&resize=422%2C200 1266w" sizes="(max-width: 422px) 100vw, 422px" data-recalc-dims="1" />](https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2014/11/distributed-consensus.png)<figcaption id="caption-attachment-43" class="wp-caption-text">Distributed Consensus Version 1 Example</figcaption></figure>

a,b,c are three processes. Remember &#8211; each process follows a lock step order (the horizontal dotted lines). Let&#8217;s say Process b gives input as 1 to a and c. b sends 1 to a, and immediately fails before it sends to c. Now, a has seen {1,2,3}, however c only has seen {2,3}. A consensus at this step is clearly incorrect. Hence, there has to be another round in order to establish consensus. That is, we need one extra round for each node failure. In general, we need f+1 rounds for f failures.

So how much rounds does the system have to make in order to make a consensus? Simple &#8211; it depends on the system designer or can be addressed using even more sophisticated algorithms. [See Early stopping consensus algorithms]

Okay, I know your mind will be filled with endless questions at this point of time. How much local processing time is too high? How does the system know the point of consensus? There are algorithms to address this. But I&#8217;ll stay away from those in this post.

**Version 2 : No node failures; Channels may drop messages; Timing is Synchronous (aka coordinated attack problem)**

There are two armies (nodes) A and B and want to attack at the same time. The goal is to reach an agreement whether to attack or not. If the decision is no, both A and B do not attack. If yes, both of them attack at the same time. There is a twist here &#8211; both A and B can communicate, however the messenger can die on the way, without getting delivered to the other army. Okay. now you know why this is called the coordinated attack problem.

Let&#8217;s get straight to the point. Solving this consensus problem has been proved IMPOSSIBLE irrespective of the overhead you are willing to tolerate. Yes, you read it right.

**Version 3 : Node crash failures; Channels are reliable; Timing is Asynchronous **

This corresponds to a real life scenario.Consider the Internet. The famous FLP theorem proves that it is IMPOSSIBLE to have a deterministic protocol in this case that always terminates. If correctness is preserved, then we can always find some scenario where the problem does not guarantee liveness, in other words it does not terminate.

In practice, the Paxos protocol works for number of nodes n ≥ 2f+1 where f is the number of crash failures possible. In this case, safety is always ensured (correctness). However, the protocol may enter into a livelock, which anyways always goes away eventually. Randomization can help to avoid livelock with probability 1. (Note that probability=1 DOES NOT mean &#8216;certainly&#8217;).

**Version 4 : Node Byzantine failures; Channels are reliable; Timing is Synchronous (aka The Byzantine Generals Problem)**

Here&#8217;s the model &#8211; There are n members in an army trying to reach a consensus. Now here among the n, there are f generals that always try to deviate the group from reaching a consensus. Each member has a 0 or 1 input &#8212; attack or retreat. The eventual goal of the group is that all non-faulty nodes eventually reach a consensus (termination), all non-faulty nodes eventually decide on the same value (agreement) and the eventual agreement is tied to the input the nodes provide (validity).

One of the application of this can be in the Replicated State machine (Linearizability).

The proved theorem in this scenario states &#8211; If _n ≤ 3f_ then the Byzantine consensus problem cannot be solved. There are protocols that exists for _n > 3f. _However, I&#8217;ll keep them out of scope of this article for now.

Okay, so we just now scratched the surface of the scenarios in case of distributed consensus. You might be wondering we have 3 different variables &#8211; Timing model (Synchronous/Asynchronous), Nodes (Reliable/Crash Failures/Byzantine Failures) and Channels (Reliable/ may drop messages). Quite normally, there are 2x3x2 = 12 possibilities right? Here&#8217;s the complete table for you &#8211;

<table style="height:683px;" width="781">
  <tr>
    <td width="156">
      <strong>Timing Model</strong>
    </td>
    
    <td width="156">
      <strong>Node</strong>
    </td>
    
    <td width="156">
      <strong>Channel</strong>
    </td>
    
    <td width="156">
      <strong>Comment</strong>
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Synchronous
    </td>
    
    <td width="156">
      Byzantine
    </td>
    
    <td width="156">
      Drops Messages
    </td>
    
    <td rowspan="6" width="156">
      Impossible to solve.
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Synchronous
    </td>
    
    <td width="156">
      Crash
    </td>
    
    <td width="156">
      Drops Messages
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Asynchronous
    </td>
    
    <td width="156">
      Byzantine
    </td>
    
    <td width="156">
      Drops Messages
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Asynchronous
    </td>
    
    <td width="156">
      Crash
    </td>
    
    <td width="156">
      Drops Messages
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Asynchronous
    </td>
    
    <td width="156">
      Reliable
    </td>
    
    <td width="156">
      Drops Messages
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Asynchronous
    </td>
    
    <td width="156">
      Byzantine
    </td>
    
    <td width="156">
      Reliable
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Asynchronous
    </td>
    
    <td width="156">
      Crash
    </td>
    
    <td width="156">
      Reliable
    </td>
    
    <td width="156">
      Version 4 (Impossible to solve)
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Synchronous
    </td>
    
    <td width="156">
      Reliable
    </td>
    
    <td width="156">
      Drops Messages
    </td>
    
    <td width="156">
       Version 2 (Impossible to solve)
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Synchronous
    </td>
    
    <td width="156">
      Byzantine
    </td>
    
    <td width="156">
      Reliable
    </td>
    
    <td width="156">
      Version 3 (Deterministic solution for n > 3f)
    </td>
  </tr>
  
  <tr>
    <td width="156">
      Synchronous
    </td>
    
    <td width="156">
      Crash
    </td>
    
    <td width="156">
      Reliable
    </td>
    
    <td width="156">
      Version 1 (Deterministic solution)
    </td>
  </tr>
</table>

Note that Crash failures are the most lenient types of failure. If Crash failures are impossible to solve, Byzantine failures are even more horrible! And also, if the channel is dropping messages, getting to a consensus is impossible no matter what.

To conclude, in this post I just introduced the general types of failures and the uncertain nature of distributed consensus in various scenarios.

This post was quite informal and I made some statements without introducing the formal proof and logic behind it. Proofs exists, but they are non-trivial, highly mathematical and beyond the scope of a simple explanation. Next post, I&#8217;ll write briefly about recovery.