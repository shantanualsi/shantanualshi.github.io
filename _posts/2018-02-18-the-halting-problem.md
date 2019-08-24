---
id: 499
title: The Halting Problem
date: 2018-02-18T18:33:18+08:00
author: shantanualshi
layout: post
guid: https://shantanualshi.wordpress.com/?p=499
permalink: /2018/02/18/the-halting-problem/
timeline_notification:
  - "1518950000"
categories:
  - Computer Problems
tags:
  - computers
  - diagonalization
  - halting
  - loops
  - problems
  - turing
  - undecidability
---
<img class="alignnone size-full wp-image-500" src="https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-2-56-12-pm.png?resize=547%2C535" alt="Credits: XKCD" width="547" height="535" srcset="https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-2-56-12-pm.png?w=547 547w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-2-56-12-pm.png?resize=300%2C293 300w, https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-2-56-12-pm.png?resize=50%2C50 50w" sizes="(max-width: 547px) 100vw, 547px" data-recalc-dims="1" />

###### <span style="color:#808080;"><em>Picture Credits: xkcd</em></span>

Infinite Loops. We all know them.

A simple program like &#8211;

<pre><span style="color:#0000ff;">while </span>(<span style="color:#993300;">true</span>) {
  <span style="color:#0000ff;">System</span>.out.print("<span style="color:#339966;">Hello, world</span>");
}</pre>

will continue forever; whereas the program &#8211;

<pre><span style="color:#0000ff;">System</span>.out.print("<span style="color:#339966;">Hello, world</span>");</pre>

will execute that line and stop.

Sometimes, it is too obvious as in the example above. Other times, we have to rack our brains figuring out if any given program was entering in an infinite loop. Furthermore, in complicated programs, it is difficult to determine whether the program will not halt at all, or is just taking longer time to compute.

* * *

### 1. A Magic Machine

What if we had a magic machine which accepts any program _f_ and an any input _x._ 

Let&#8217;s check if such a machine can exist &#8211;

**<span style="text-decoration:underline;"><em>Step 1:</em></span>**

Imagine that such a Magic Machine (M) indeed does exist. Also, imagine we have an infinite amount of resources available to run such a machine.

This machine simply outputs &#8220;HALTS&#8221; if program our _f_ will exit after computing  or &#8220;NOT HALTS&#8221; if _f_ will enter an infinite loop while computing _f(x)._

<img class="aligncenter size-full wp-image-501" src="https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-19-30-pm.png?resize=552%2C171" alt="Screen Shot 2018-02-18 at 3.19.30 PM" width="552" height="171" srcset="https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-19-30-pm.png?w=552 552w, https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-19-30-pm.png?resize=300%2C93 300w" sizes="(max-width: 552px) 100vw, 552px" data-recalc-dims="1" /> 

As an example, let&#8217;s feed our magic machine to see what happens if _f_ is fed itself as an input. Let&#8217;s assume it says the program does not halt.

<img class=" size-full wp-image-502 aligncenter" src="https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-38-32-pm.png?resize=562%2C174" alt="Screen Shot 2018-02-18 at 3.38.32 PM.png" width="562" height="174" srcset="https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-38-32-pm.png?w=562 562w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-38-32-pm.png?resize=300%2C93 300w" sizes="(max-width: 562px) 100vw, 562px" data-recalc-dims="1" /> 

<span style="text-decoration:underline;"><em><strong>Step 2:</strong></em></span>

Build a Naughty Machine &#8220;N&#8221; that accepts one input. This machine enters an infinite loop if the input is &#8220;HALTS&#8221; and stops when the input is &#8220;NOT HALTS&#8221;. Basically, it does what it is not told to do. This should be easy to build.

<img class=" size-full wp-image-503 aligncenter" src="https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-46-48-pm.png?resize=362%2C106" alt="Screen Shot 2018-02-18 at 3.46.48 PM" width="362" height="106" srcset="https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-46-48-pm.png?w=362 362w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-46-48-pm.png?resize=300%2C88 300w" sizes="(max-width: 362px) 100vw, 362px" data-recalc-dims="1" /> 

_<span style="text-decoration:underline;"><strong>Step 3:</strong></span>_

Join the two machines together. Let&#8217;s call this bigger machine G.  Let&#8217;s call the joint program that they both execute as _g._ 

<img class=" size-full wp-image-504 aligncenter" src="https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-56-36-pm.png?resize=591%2C115" alt="Screen Shot 2018-02-18 at 3.56.36 PM" width="591" height="115" srcset="https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-56-36-pm.png?w=591 591w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-3-56-36-pm.png?resize=300%2C58 300w" sizes="(max-width: 591px) 100vw, 591px" data-recalc-dims="1" /> 

_<span style="text-decoration:underline;"><strong>Step 4:</strong></span>_

Let&#8217;s feed this new machine G with its own program g.

<img class=" size-full wp-image-507 aligncenter" src="https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-4-03-53-pm.png?resize=656%2C133" alt="Screen Shot 2018-02-18 at 4.03.53 PM" width="656" height="133" srcset="https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-4-03-53-pm.png?w=656 656w, https://i1.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-4-03-53-pm.png?resize=300%2C61 300w" sizes="(max-width: 656px) 100vw, 656px" data-recalc-dims="1" /> 

Let&#8217;s assume our Magic Machine outputs &#8220;NOT HALTS&#8221; when fed with g. That means that G is going in an infinite loop with this input. The naughty machine which is a part of G itself will negate that input print LULZ and then halt.

<p style="text-align:center;">
  <em><span style="color:#999999;"><span style="color:#000000;">G halted!  But our magic machine said G will not halt! </span><br /> </span></em>
</p>

We trusted our machine to determine correctly for all inputs. Our magic machine is a phony. It is not possible that such a machine exists.

* * *

### **2. The Halting Problem**

This is an overly simplified explanation of what is known as the halting problem. Turing proved that an algorithm to correctly determine whether a program will ever enter in an infinite loop or halt can never exist. As our example above, he stated that any such algorithm can be made to contradict itself and thus cannot be true.

Such problems that decide and output a binary true/false are known as decision problems or as Turing put it in German &#8211; <span class="_Tgc _s8w">Entscheidungsproblem</span>s. The Halting problem is one of the first examples of decision problem that is proved to be **_Undecidable_**.

* * *

### 3. Cantor&#8217;s Diagonalization

If you are still not convinced, the existence of such an algorithm can be disproved using a nice technique known as Cantor&#8217;s Diagonalization.

To start with, let&#8217;s again imagine such a machine exists. The machine outputs 0 if a program _f_  does not halt on any input _x_ and 1 if it does halt.

What we do know, and is proved, is that the number of programs is countably finite. What we can have is a matrix of two inputs to our machine and the cells denote 1 or 0 depending on whether the system halts or not.

Assume there are no more than 8 programs in the world and we check each program against all as in our matrix below. The programs are named by the letters A to H. The outputs 0 and 1 are just assumed outputs of the magic machine.

<img class=" size-full wp-image-508 aligncenter" src="https://i2.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-4-38-23-pm.png?resize=310%2C302" alt="Screen Shot 2018-02-18 at 4.38.23 PM" width="310" height="302" srcset="https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-4-38-23-pm.png?w=310 310w, https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-4-38-23-pm.png?resize=300%2C292 300w, https://i0.wp.com/blog.shantanualshi.com/wp-content/uploads/2018/02/screen-shot-2018-02-18-at-4-38-23-pm.png?resize=50%2C50 50w" sizes="(max-width: 310px) 100vw, 310px" data-recalc-dims="1" /> 

The matrix shows rows that represent programs and columns that are input to our programs. By convention we should have covered all possibilities to prove that our machine is correct.

Now, let&#8217;s pick up all the diagonal values of the matrix f(i) and invert them to g(i). You&#8217;ll notice that we did not test our machine for this input! It does not exist in our matrix.

If you add this to your set of inputs and run the diagonalization again, you&#8217;ll get another one! Each new input formed will differ in at least one bit.

You cannot just test the machine for all inputs! Such a machine cannot be built.

* * *

### 4. Significance

In addition of the relief to know that computers will not be able to outsmart human beings, the halting problem is extremely useful in the process of _reduction_. If any given problem P can be reduced to the halting problem, it can be proved that no solution exists for P and so is undecidable.

######