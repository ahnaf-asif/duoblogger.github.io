---
layout: post
title: Dp on Trees
author-id: asifthen00b
tags: [Dynamic Programming, Trees]

---

* [Introduction](#introduction)
* [Problem 1](#problem1)
  * [Variant 1](#problem1variant1)
* [Problem 2](#problem2)

## Introduction <a name="Introduction"></a>

আমরা আশা করি প্রাথমিক ডিপি বেশ ভালোভাবেই পারি, ডিপির স্টেট বেরকরতে পারি, ডিপি রিকার্শন বেরকরতে পারি। যদি তুমি না পারো তাহলে [এটি](https://duoblogger.github.io/2019/06/28/basic-dynamic-programming.html) দেখতে পারো। এরপর আমরা সামনের দিকে আগাবো। নরমাল ডিপি আমরা অ্যারে এর উপর করেছি। এবার একই জিনিস ট্রি এর উপর করবো। খুবই সাধারণ ব্যাপার। আমরা খুব কঠিনভাবে শুরু করবোনা অবশ্যই, তবে ট্রি ডিপির অনেক অনেক কঠিন প্রব্লেম আছে। আমরা আস্তে আস্তে সেগুলো সমাধান করতে শিখবো। কথা না বাড়িয়ে চলো শুরু করা যাক। 

### Pre-requirements

* [Basic Dynamic Programming](https://duoblogger.github.io/2019/06/28/basic-dynamic-programming.html)
* [Basic Graph Theory](http://www.shafaetsplanet.com/?p=143)
* [BFS](http://www.shafaetsplanet.com/?p=604)  ,  [Topsort](http://www.shafaetsplanet.com/?p=848)  ,  [DFS](http://www.shafaetsplanet.com/?p=973)
* [Different Definitions about trees](https://www.tutorialspoint.com/data_structures_algorithms/tree_data_structure.htm)

## Problem 1 <a name="problem1"></a>

> তোমাকে একটি ট্রি দেয়া আছে, তোমাকে ট্রি এর এমন দুটি নোড বের করতে হবে যাদের মধ্যকার দূরত্ব সবথেকে বেশি। তোমাকে আপাতত দুরত্ব বের করলেই হবে, নোড দুটি বের করার দরকার নেই। তুমি কি এটা বের করতে পারবে? 

এই প্রব্লেমটি ক্লাসিক প্রব্লেম। এই ম্যক্সিমাম ডিস্টেন্সকে ট্রির ডায়ামিটার বলে। এটার সলুশন নিজে বের করার চেষ্টা করো। না পারলে [এই টিউটোরিয়াল](http://www.shafaetsplanet.com/?p=521) থেকে দেখে নাও। 

এখন ধরে নিচ্ছি তোমরা দুটি DFS চালিয়ে কীভাবে ডায়ামিটার বের করতে হয় সেটা প্রমাণসহ বোঝো। তাহলে নিচের দিকে যাও, প্রব্লেমটাকে একটু কঠিন করে দিচ্ছি। 

### Variant 1 <a name="problem1variant1"></a>

এই ক্ষেত্রে ট্রি এর এজগুলোর কস্ট(cost) আছে, অর্থাৎ, ট্রি টি ওয়েটেড। তার উপর এজের ওয়েট নিগেটিভ হতে পারে। এবার ডায়ামিটার বের কর। নিচে সলুশন দেখার আগে চিন্তা করে দেখো। আমাদের আগের সলুশনটি কি কাজ করবে? কাজ করলে কেনো করবে? আর কাজ না করলে কেনো করবেনা? 

আমরা দুটি DFS দিয়ে কি করেছি? প্রথমে random নোড থেকে একটা DFS চালিয়ে সেখান থেকে সবথেকে দূরের নোডগুলো বের করেছি, তারপর সবথেকে দূরের যেকোনো একটি নোড থেকে আরেকবার DFS চালিয়েছি। তাতেই ম্যাক্সিমাম পেয়ে গেছি, তাই না? কিন্তু নিচের ট্রিতে প্রথম DFS টা $$e$$ থেকে চালালে কি হয় খেয়াল করো তো! 

![tree-dp-1]({{ "/assets/img/posts_images/tree_dp_2.png" | relative_url}})

দেখা যাবে প্রথম DFS এ e নোড থেকে d নোড সবথেকে দূরের। তাই দ্বিতীয় DFS টা d নোড থেকে চালিয়ে আমরা ম্যাক্সিমাম পাবো $$27$$ $$[path\space  ( d-e-b-a) ]$$  । কিন্তু আমরা যদি প্রথম DFS টা আন্য কোনো নোড থেকে চালাতাম, তাহলে ডায়ামিটার পেতাম $$28\ [path\ (a-b-c)]$$ । সুতরাং, আমরা এই ক্ষেত্রে প্রাথমিক DFS এ কোন নোডকে রুট ধরবো, তার উপর অনেক কিছু নির্ভর করবে। তাই এভাবে বের করা যাবেনা ডায়ামিটার। আসলে যাবে, আমরা সব নোড থেকে চালিয়ে দেখতে পারি, কিন্তু তাতে $$O(n^2)$$ সময় লেগে যাবে। তাই সেটা করা যাবেনা। তাহলে কী করা যায়? 

আমরা এখন ডিপির মতো চিন্তা করবো। আমরা প্রত্যেকটা নোডের জন্য বের করবো এই নোডের সাবট্রি এর মধ্যে এই নোড দিয়ে যায় এরকম সবথেকে বড় পাথ কোনটি। নিচের ছবিটি দেখ‌ো। 

![tree-dp-1]({{ "/assets/img/posts_images/tree_dp_3.png" | relative_url}})

ছবিতে ম্যাক্সিমাম পাথের সাইজ 21 । পাথটি হচ্ছে $$(4-7-6)$$

এখানে নোড $$1$$ এর সাবট্রির মধ্যে 1 দিয়ে যায় এরকম সবথেকে বড় পাথের সাইজ 20,  $$path(2-1-4-7-6)$$ । তাহলে আমরা যদি জানি যে প্রত্যেক নোডের জন্য ম্যাক্সিমাম পাথ কত, তাহলেই হয়ে যায়। ধর‌ $$dp(i)$$ মানে $$i$$ নোড দিয়ে $$i$$ এর সাবট্রির মধ্যকার ম্যাক্সিমাম পাথ। তাহলে $$ ans = max\left \{ dp(1),dp(2)....dp(n) \right \}$$ ।  কিন্তু আমরা এই ম্যাক্সিমাম কীভাবে বের করবো? এজন্য আমরা প্রত্যেক নোডে ম্যাক্সিমাম আর সেকেন্ড ম্যাক্সিমাম চেইন রেখে দিব। তাহলে এদের যোগফলই হবে ওই নোডের ম্যাক্সিমাম পাথ। এটা কেন হয়? চিন্তা করে দেখ। 

**<u>প্রমাণ:</u>** দেখ, প্রথমত চেইন দুটো আলাদা, তাই তাদের যোগ করলে নোড দিয়ে যায় এরকম একটা পাথ পাওয়া যাবে। এবার আমরা প্রমাণ করবো যে এই পাথই ম্যাক্সিমাম। ধরো আমাদের ম্যাক্সিমাম চেইন $$a$$ আর সেকেন্ড ম্যাক্সিমাম $$b$$ । তাহলে $$dp(node) = a+b$$ , তাই না? কিন্তু আমরা ধরে নিচ্ছি কথাটি ভুল এবং এমন দুটি চেইন $$(x,y)$$  পাওয়া যাবে যারা ম্যাক্সিমাম/সেকেন্ড ম্যাক্সিমাম না, তারপরেও $$x+y > a+b$$  হবে। এটা প্রমাণ করতে পারলে আমাদের সলুশন ভুল প্রমাণিত হবে, অন্যথায় নয়। 

এখন ধরে নিচ্ছি $$(x > y)$$ এবং $$(a > b)$$ । যেহেতু $$a$$ হচ্ছে ম্যাক্সিমাম সেহেতু $$x$$ ম্যাক্সিমাম না, তাই $$(a > x)$$ । আবার যেহেতু $$b$$ দ্বিতীয় সর্বোচ্চ এবং  $$(x  > y)$$, সেহেতু, $$(b > y)$$ হবে। এখন যদি  $$(a > x)$$ আর $$(b > y)$$ হয়, তাহলে $$(a+b > x+y)$$ হবে। অর্থাৎ, এরকম কোনো $$(x,y)$$ পাওয়া সম্ভব না, যেন  $$x+y > a+b$$ হয়। তাহলে প্রত্যেক নোডে ম্যাক্সিমাম আর সেকেন্ড ম্যাক্সিমাম চেইনের যোগফলই হচ্ছে ম্যাক্সিমাম পাথ। এখন এটার কোড কীভাবে করবো? খুবই সোজা। আমাদের ডিপি টেবিলে দুটো জিনিস রাখবো, একটা হচ্ছে পজিশন, আরেকটা হচ্ছে ম্যাক্স / সেকেন্ড ম্যাক্স। অর্থাৎ,$$dp[2][n]$$ । এখানে , 

$$dp[0][x] = second\max\left \{ chain(child_1),chain(child_2)...., chain(child_x) \right \} \\$$

$$dp[1][x] = max\left \{ chain(child_1),chain(child_2)...., chain(child_x) \right \}$$

কোড নিচে দিয়ে দিচ্ছি। তবো মনে রেখো, সবসময় কোড না দেখে নিজে চেষ্টা করবে, পারার পর মিলিয়ে দেখার জন্য কোড দিয়ে দিচ্ছি। আর যদি একেবারেই না পারো তাহলে প্রথম থেকে আবার পড়। 

 ```cpp
//dp[1][..] = maximum chain
//dp[0][..] = second maximum chain 
void dfs(int node,int parent){
    for(int v: graph[node]){
        if(v != parent){
            dfs(v,node);
            if(dp[1][node] < dp[1][v]){
                dp[0][node] = max(dp[1][node],dp[0][v]);
                dp[1][node] = dp[1][v];
            }
            else dp[0][node] = max{dp[0][node],dp[1][v],dp[0][v]};
        }
    }
}
int ans = 0;
for(int i = 1; i <= n;i++)ans = max(ans,dp[0][i]+dp[1][i]);
 ```

## Problem 2 <a name="problem2"></a>

> তোমাকে একটা ট্রি দেয়া আছে। ট্রি এর প্রত্যেকটা নোডে কিছু করে ভ্যালু আছে। তুমি এই ট্রি থেকে এমনভাবে কিছু নোড নিতে পারবে যেন তাদের ভ্যালুর যোগফল সর্বোচ্চ হয়। কিন্তু তুমি একই এজের(edge) একাধিক নোড নিতে পারবেনা। অর্থাৎ, ধরো নোড a থেকে b তো সরাসরি এজ আছে। তাহল তুমি  a আর b কে একসাথে নিতে পারবেনা, যেকোনো একটা নিতে হবে। তোমাকে সর্বোচ্চ যোগফল বের করতে হবে। 

এই প্রব্লেমটি সল্ভ করার আগে তুমি [এই প্রব্লেমটি](https://duoblogger.github.io/2019/06/28/basic-dynamic-programming.html#problem3) দেখে নাও। আ্যারে এর সলুশন বুঝতে পারলে তোমার জন্য এই প্রব্লেমটা বুঝতে কোনো সমস্যা হওয়ার কথা না। অ্যারেতে আগের ইন্ডেক্সের সাথে যেভাবে হিসাব করেছি, এখানে শুধু একটা নোডের চাইল্ডের সাথে হিসাবটা করবো। নিচের ছবিতে কিছুটা সিমুলেট করে দেখিয়েছি, ভালো করে খেয়াল করো, বুঝতে সুবিধা হতে পারে। 

![tree-dp-1]({{ "/assets/img/posts_images/tree_dp_1.png" | relative_url}})

ছবিটি খুব ভালো করে খেয়াল করলে বাকিটা বুঝতে অসুবিধা হবেনা। কোডটা নিজে করার চেষ্টা করো। আমি নিচে দিয়ে দিচ্ছি তাও। 

``` c++
void dfs(int node,int par){
    dp[0][node] = 0;
    dp[1][node] = cost[node];
    for(int v: graph[node]){
        if(v != par){
    		dfs(v,node);
            dp[0][node] += max({dp[1][v],dp[0][v],0});
            dp[1][node] += max(dp[0][v],0);
        }
    }
}
// print max(dp[0][1],dp[1][1]);
```

to be continued....



