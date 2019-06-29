---
layout: post
title: Dp on Trees
author-id: asifthen00b
tags: [Dynamic Programming, Trees]

---

## Table Of Contents

* [Introduction](introduction)
* [Problem 1](#problem1)
* [Problem 2](#problem2)

## Introduction <a name="introduction"></a>

আমরা আশা করি প্রাথমিক ডিপি বেশ ভালোভাবেই পারি, ডিপির স্টেট বেড় করতে পারি, ডিপি রিকার্শন বেড় করতে পারি। যদি তুমি না পারো তাহলে [এটি](https://duoblogger.github.io/2019/06/28/basic-dynamic-programming.html) দেখতে পারো। এরপর আমরা সামনের দিকে আগাবো। নরমাল ডিপি আমরা অ্যারে এর উপর করেছি। এবার একই জিনিস ট্রি এর উপর করবো। খুবই সাধারণ ব্যাপার। আমরা খুব কঠিনভাবে শুরু করবোনা অবশ্যই, তবে ট্রি ডিপির অনেক অনেক কঠিন প্রব্লেম আছে। আমরা আস্তে আস্তে সেগুলো সমাধান করতে শিখবো। কথা না বাড়িয়ে চলো শুরু করা যাক। 

### Pre-requirements

* [Basic Dynamic Programming](https://duoblogger.github.io/2019/06/28/basic-dynamic-programming.html)
* [Basic Graph Theory](http://www.shafaetsplanet.com/?p=143)
* [BFS](http://www.shafaetsplanet.com/?p=604)  ,  [Topsort](http://www.shafaetsplanet.com/?p=848)  ,  [DFS](http://www.shafaetsplanet.com/?p=973)
* [Different Definitions about trees](https://www.tutorialspoint.com/data_structures_algorithms/tree_data_structure.htm)

## Problem 1 <a name="problem1"></a>

> তোমাকে একটি ট্রি দেয়া আছে, তোমাকে ট্রি এর এমন দুটি নোড বেড় করতে হবে যাদের মধ্যকার দূরত্ব সবথেকে বেশি। তোমাকে আপাতত দুরত্ব বেড় করলেই হবে, নোড দুটি বেড় করার দরকার নেই। তুমি কি এটা বেড় করতে পারবে? 

এই প্রব্লেমটি ক্লাসিক প্রব্লেম। এই ম্যক্সিমাম ডিস্টেন্সকে ট্রির ডায়ামিটার বলে। এটার সলুশন নিজে বেড় করার চেষ্টা করো। না পারলে [এই টিউটোরিয়াল](http://www.shafaetsplanet.com/?p=521) থেকে দেখে নাও। 

## Problem 2 <a name="problem2"></a>

> তোমাকে একটা ট্রি দেয়া আছে। ট্রি এর প্রত্যেকটা নোডে কিছু করে ভ্যালু আছে। তুমি এই ট্রি থেকে এমনভাবে কিছু নোড নিতে পারবে যেন তাদের ভ্যালুর যোগফল সর্বোচ্চ হয়। কিন্তু তুমি একই এজের(edge) একাধিক নোড নিতে পারবেনা। অর্থাৎ, ধরো নোড a থেকে b তো সরাসরি এজ আছে। তাহল তুমি  a আর b কে একসাথে নিতে পারবেনা, যেকোনো একটা নিতে হবে। তোমাকে সর্বোচ্চ যোগফল বেড় করতে হবে। 

এই প্রব্লেমটি সল্ভ করার আগে তুমি [এই প্রব্লেমটি](https://duoblogger.github.io/2019/06/28/basic-dynamic-programming.html#problem3) দেখে নাও। আ্যারে এর সলুশন বুঝতে পারলে তোমার জন্য এই প্রব্লেমটা বুঝতে কোনো সমস্যা হওয়ার কথা না। অ্যারেতে আগের ইন্ডেক্সের সাথে যেভাবে হিসাব করেছি, এখানে শুধু একটা নোডের চাইল্ডের সাথে হিসাবটা করবো। নিচের ছবিতে কিছুটা সিমুলেট করে দেখিয়েছি, ভালো করে খেয়াল করো, বুঝতে সুবিধা হতে পারে। 

![tree-dp-1]({{ "/assets/img/posts_images/tree_dp_1.png" | relative_url}})

ছবিটি খুব ভালো করে খেয়াল করলে বাকিটা বুঝতে অসুবিধা হবেনা। কোডটা নিজে করার চেষ্টা করো। আমি নিচে দিয়ে দিচ্ছি তাও। 

``` c++
void dfs(int node,int par){
    dp[0][node] = 0;
    dp[1][node] = cost[node];
    for(auto v: graph[node]){
        if(v != par){
    		dfs(v,node);
            dp[0][node] += max({dp[1][v],dp[0][v],0});
            dp[1][node] += max(dp[0][v],0);
        }
    }
}
// print max(dp[0][1],dp[1][1]);
```









