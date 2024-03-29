---
layout: post
title: Convex Hull
author-id: HBK_Wasi

tags: [Geometry] 
---

আজকে আমরা অনেকগুলো কার্তেসিয় স্থানাঙ্ক দেওয়া থাকলে সেটার কনভেক্স হাল বের করা শিখবো।

<font color="green"> কনভেক্স হাল:</font> ধরি আমাদের কাছে $$N$$ টা পয়েন্ট দেওয়া আছে। আমাদের উদ্দেশ্য হচ্ছে এমন ক্ষুদ্রতম <a href = "https://en.wikipedia.org/wiki/Convex_polygon">উত্তল বহুভুজ</a> তৈরি করা যেটার মধ্যে সবগুলো পয়েন্ট আছে। এটাকেই ওই পয়েন্টগুলোর কনভেক্স হাল বলা হয়।

<font color="green"> অ্যালগোরিদম: </font>এখানে আমি গ্রাহাম স্ক্যান অ্যালগোরিদম ব্যবহার করে কনভেক্স হাল কিভাবে তৈরি করতে হয় সেটা দেখাবো। গ্রাহাম স্ক্যান এ শুধু কম্পেরিজন, যোগ আর গুন ব্যবহার করেই $$ O(N logN) $$ এ কনভেক্স হাল বের করা যায়। কনভেক্স হাল বের করার জন্য এটিই সবচেয়ে ভালো কম্প্লেক্সিটি। এটা প্রমাণ করা যায় যে এটার চেয়ে ভালো কম্প্লেক্সিটিতে কনভেক্স হাল বের করা যায় না।

<h3> <font color="#100680"> Description </font> </h3>
এই অ্যালগোরিদমটি প্রথমেই "সবচেয়ে নিচে ও সবচেয়ে বামে" এর পয়েন্ট $$A$$ এবং "সবচেয়ে উপরে ও সবচেয়ে ডানে" এর পয়েন্ট $$B$$ খুঁজে বের করে। এটা স্পষ্ট যে $$A$$ আর $$B$$ দুটোই কনভেক্স হালে অন্তর্ভুক্ত হবে। কারণ যেহেতু এই দুইটি পয়েন্ট সবচেয়ে দূরে অবস্থিত, বাকি সবগুলো পয়েন্ট থেকে এমন ভাবে দুটি পয়েন্ট নেয়া সম্ভব হবে না যে পয়েন্টদুটোর সংযোগরেখা $$A$$ অথবা $$B$$ কে কনভেক্স হালের ভিতরের দিকে ফেলে।  

এখন আমরা $$A$$ ও $$B$$ এর সংযোজক একটা রেখা কল্পনা করি। এই রেখাটি সবগুলো পয়েন্টকে দু'টি সেটে ভাগ করে। ধরি, সেট দুটি $$S_1$$ও $$S_2$$ । $$S_1$$ হচ্ছে সেসব পয়েন্টগুলো যেগুলা $$AB$$ লাইনের উপরে আছে আর $$S_2$$ হচ্ছে সেই পয়েন্টগুলা যেগুলা $$AB$$ লাইনের নিচে আছে। যেই পয়েন্টগুলা $$AB$$ লাইনের মধ্যে পরেছে যেগুলাকে যেকোনো একটাতে রাখলেই হবে। $$A$$ আর $$B$$ পয়েন্ট দুটি উভয় সেটেই থাকবে। অ্যালগোরিদমটি প্রথমে $$S_1$$ সেটের পয়েন্টগুলা থেকে কনভেক্স হালের উপরের পার্ট টা তৈরি করে আর $$S_2$$ পয়েন্টগুলা থেকে কনভেক্স হালের নিচের পার্টটা তৈরি করে। তারপর দুইটা পার্টকে একসাথে জুড়ে দিলেই তৈরি হয়ে গেলো আমাদের সুন্দর কনভেক্স হাল। 😍

কিন্তু ওয়েট, এতো সোজা নাকি? কোথায় যেনো একটা গাফলা মনে হচ্ছে। হ্যাঁ। এখন উপরের পার্টের কনভেক্স হালটাই বা কিভাবে হবে 😨। 

উপায় কিন্তু আছে । 😀 উপরের সেটটা পাওয়ার জন্য আমরা প্রথমে $$x$$ কো-অর্ডিনেট দিয়ে সবগুলো পয়েন্ট কে সর্ট করব। কনভেক্স হালের উপরের পার্টের প্রথম পয়েন্ট টা হবে $$A$$ ও শেষ পয়েন্ট টা হবে $$B$$। আমরা দেখব যে বর্তমানে আমরা যে পয়েন্টে আছি সেটা $$B$$ কি না। যদি $$B$$ হয় তার মানে আমাদের কাজ শেষ। এখন আমাদের মাথায় এই চিন্তা টা আসতে পারে যে, আমরা শুধুমাত্র উপরের হাল টা বানানোর জন্য সব গুলো পয়েন্ট নিয়ে কাজ করছি। তাহলে তো এমন পয়েন্টগুলো চলে আসবে যেগুলো $$AB$$ লাইনের নিচে। তাহলে তো ঝামেলা $$!$$ ঝামেলা দূর করার জন্য আমরা $$A$$, $$P_{current}$$ এবং $$B$$ এর মধ্যে অরিয়েন্টেশন চেক করতে পারি। মানে যদি $$A  $$    ->  $$P_{current}$$   ->  $$B$$ পথটি ক্লক ওয়াইজ হয় তার মানে $$P_{current}$$ পয়েন্টটি $$AB$$ লাইনের উপরে আছে। তাহলে পয়েন্টটি $$S_1$$ সেটেই পড়বে। 

যদি $$P_{current}$$ পয়েন্টটি $$S_1$$ সেটেই থাকে, তাহলে আমরা পয়েন্ট $$P_{current}$$ এবং এই পর্যন্ত বানানো কনভেক্স হালের শেষ পয়েন্ট $$hull_{last}$$ এবং তার আগের পয়েন্ট $$hull_{last-1}$$ গুলো নিবো। এবার $$hull_{last-1}$$ -> $$hull_{last}$$ ও $$hull_{last}$$ -> $$P_{current}$$ এই দুটি রেখা আঁকবো। এই রেখা দুটি $$hull_{last}$$ বিন্দুতে ছেদ করে। এখন আমরা রেখাদ্বয় দ্বারা উৎপন্ন কোণটি চেক করবো। যদি এই কোণটি ক্লকওয়াইজ হয়, আমরা বর্তমান পয়েন্ট টিকে হালে যুক্ত করে দিতে পারি। আর এন্টি-ক্লকওয়াইজ হলে আমরা হালের লাস্ট পয়েন্টটিকে ডিলিট করে দিব। এবং $$P_{current}$$ পয়েন্টটিকে হালে যুক্ত করবো। কারণ, $$hull_{last-1}$$ এবং $$P_{current}$$ রেখাটি সেক্ষেত্রে $$hull_{last}$$ পয়েন্টটিকে কাভার করতে পারবে। 

একই লজিকে আমরা হালের নিচের  অংশটুকুও তৈরি করে ফেলতে পারি। এক্ষেত্রে শুধু ক্লকওয়াইজ আর এন্টি-ক্লকওয়াইজ এর ব্যবহারটা উল্টে যাবে। আগের ক্ষেত্রে  ক্লক ওয়াইজ হলে যুক্ত করে দিতাম এবং এন্টি ক্লকওয়াইজ হলে ডিলিট করে দিতাম।  নিচের হাল বানানোর ক্ষেত্রে এন্টি ক্লকওয়াইজ হলে যুক্ত করে দিতে হবে এবং ক্লকওয়াইজ হলে ডিলিট করে দিতে হবে।
এবার, উপরের আর নিচের হালটা যুক্ত করে দিলেই তৈরি হয়ে গেল আমাদের সুন্দর কনভেক্স হাল। এটার $$C$$++ ইম্প্লেমেন্টেশন করা যেতে পারে এভাবে ।

<h3 > <font color="#100680">Implementation</font> </h3>
```cpp
struct pt {
    double x, y;
};

bool cmp(pt a, pt b) {
    return a.x < b.x || (a.x == b.x && a.y < b.y);
}

bool cw(pt a, pt b, pt c) {
    return a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y) < 0;
}

bool ccw(pt a, pt b, pt c) {
    return a.x*(b.y-c.y)+b.x*(c.y-a.y)+c.x*(a.y-b.y) > 0;
}

void convex_hull(vector<pt>& a) {
    if (a.size() == 1)
        return;

    sort(a.begin(), a.end(), &cmp);
    pt p1 = a[0], p2 = a.back();
    vector<pt> up, down;
    up.push_back(p1);
    down.push_back(p1);
    for (int i = 1; i < (int)a.size(); i++) {
        if (i == a.size() - 1 || cw(p1, a[i], p2)) {
            while (up.size() >= 2 && !cw(up[up.size()-2], up[up.size()-1], a[i]))
                up.pop_back();
            up.push_back(a[i]);
        }
        if (i == a.size() - 1 || ccw(p1, a[i], p2)) {
            while(down.size() >= 2 && !ccw(down[down.size()-2], down[down.size()-1], a[i]))
                down.pop_back();
            down.push_back(a[i]);
        }
    }

    a.clear();
    for (int i = 0; i < (int)up.size(); i++)
        a.push_back(up[i]);
    for (int i = down.size() - 2; i > 0; i--)
        a.push_back(down[i]);
}
```

<h3> <font color="100680">Practice Problems</font></h3>
- [Kattis - Convex Hull](https://open.kattis.com/problems/convexhull)
- [Kattis - Keep the Parade Safe](https://open.kattis.com/problems/parade)
- [Timus 1185: Wall](http://acm.timus.ru/problem.aspx?space=1&num=1185)
- [Usaco 2014 January Contest, Gold - Cow Curling](http://usaco.org/index.php?page=viewproblem2&cpid=382)

