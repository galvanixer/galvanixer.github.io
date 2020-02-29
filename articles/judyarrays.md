---
title: Judy Arrays
layout: blog-single
date: Thu Jan  2 17:54:55 CET 2020
title_image: '/assets/images/blog/judyarrays/ja_top.png'
author: Tanul Gupta
category: ['Julia', 'Computer Science']
tags: ['Julia', 'Computer Science']
---

<H2>Introduction</H2>
<p>
I wanted to simulate the time evolution of quantum systems containing 100 or more qubits. This is a humongous task for any classical computer, but even we get a good enough system, we are still limited by datatypes that can store (key, value) pairs with more than 264 keys. Even Hash tables are unable to resolve this issue. This led us to search for associative arrays that can satisfy the following requirements:</p>

<ul>
	<li>Sparse arrays with dynamic or unbounded indexes (0, 1, 2, .... n).</li>
	<li>Fast search and retrieval</li>
	<li>Fast counting and sorting</li>
	<li>Memory efficient</li>
	<li>Nearly linear performance from very small to very large populations</li>
</ul>

All these requirements are fulfilled by JudyArrays, and that's why I undertook this journey to understand the working of this peculiar data type. Roughly speaking, **Judy Arrays** are highly optimized **256-ary [radix trees][rt].** Unlike most other associative arrays, Judy arrays use no hashing, leverage compression on their keys, and can efficiently represent sparse data.

## History
JudyArray was developed by Douglas Baskins and his team in Hewlett Packard (HP), and it is named after his sister.

## Benefits 
1. __Memory Efficient__  
Being dynamic, Judy arrays can grow or shrink as elements are inserted or removed from the array. Hence, the memory used by Judy arrays is nearly proportional to the number of elements stored.
2. __Speed__  
Judy arrays are designed to minimize the number of expensive [cache-line][cl] fills from RAM. A cache miss is a failed attempt to read or write a piece of data in the cache, which results in the main memory (RAM) access with much longer latency. Therefore, a cache miss should be avoided as often as possible. This is precisely what the complex algorithm behind Judy arrays achieve. Due to these cache optimizations, Judy arrays are fast, especially for very large datasets.

## When to use Judy array?
1. Large and sparse data sets.
2. Semi-sequential data sets.
3. General low latency requirement. 

## Algorithm
Will be updated. 

## Implementations available
1. The original implementation of Judy Array was written by Douglas Baskins at HP. This implementation is the fastest, but quite complex to understand the algorithm. It is available as a [Judy Array API library][jl] written in C.
2. Author Karl Malbrain with assistance from Jan Weiss rewrote Douglas's [Judy Arrays within 1250 lines of code][ja1250].
3. [Tanmay Mohapatra][author:tm] wrote a Julia package that acts as a wrapper on top of the original C API written by Douglas. As this wrapper was written in Julia 0.6, it is now deprecated.
4. [Tanul Gupta][author:ta] wrote a Julia package named [JudyDicts][git:jd] taking inspiration from [Tanmay's][author:tm] deprecated package. This new Julia package works in Julia 1.0.

## Future
We are working on a standalone Julia package based on Karl Malbrain's implementation. Let's hope we can work it out as soon as possible.

[git:jd]:https://github.com/galvanixer/JudyDicts.jl
[author:ta]:https://github.com/galvanixer
[author:tm]:https://github.com/tanmaykm
[ja1250]:https://code.google.com/archive/p/judyarray/
[jl]:http://judy.sourceforge.net/index.html
[rt]:https://en.wikipedia.org/wiki/Radix_tree
[cl]:https://en.wikipedia.org/wiki/Cache-line
