---
layout: post
title:  "Big O and it's value"
date:   2017-06-20 17:35:23 +0000
---


## What is Big O?
Big O is a mathamatical notation used to express the limiting factor in the grouth of a asymptotic function as it approtches infinity. Generally expressed as `O(n)`

In plain english this means that `O` is a function that describes how another function performs as its input (defined as `n`) grows. For example, `O(n * 2)` would mean that what ever size `n` is the amount of work is double that. So if the size of work `n` is 50, this function would do 100 units of work. Here is a graph showing how some common Big O functions scale over time:

![](https://i.stack.imgur.com/WcBRI.png)

As you can see small changes in how much work is being done can matter a whole lot as the input scales even to 1,000.

## Where did the constants go
One inportant thing to realize about Big O is that there is no constants defined in the notation. So for example if you have some code that takes the input and saves it to a disk that is a constant amount of work (whatever the input that work will be the same), Even tough this operation can take several times longer to perform on a 5400 RPM drive than on a NVME SSD, as far as the code is concerned this timing is irrelivent to how it will scale over time and as such is thrown out. (this is called a `O(1)` operation

## The value of using Big O
For most applications Big O is not a very important day to day concern, as the inputs are generally under 1,000/sec on one execution path. However, for thouse who care about how well their application scales (and many executives do) then using Big O can give important insights into what is really going on under the hood.
