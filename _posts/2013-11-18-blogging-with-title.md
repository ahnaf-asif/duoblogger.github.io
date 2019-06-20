---
layout: post
title: Blogging with title
tags: [Test, Ipsum, Markdown, Portfolio]
---

# I am a BIG title

This is a very tiny tiny post with less than 250 letters.

Search should be working even for complicated escape symbols
```cpp
/** e==m*pow(c,2) **/
#include <bits/stdc++.h>
using namespace std;
#define DEBUG 1
#define LL long long
#define int long long
//#define OFFLINE 2585
#define pii pair<int, int>
#define SQR(n) (n*n)
#define pb push_back
//#define endl '\n'
#define yes cout << "YES" << endl
#define no cout << "NO" << endl
#define INF 100000000000
#define pi (acos(0.0) * 2.0)
#define time_start clock_t tStart = clock()
#define time_end (double)(clock() - tStart)/CLOCKS_PER_SEC
#define maxn 100009
#pragma GCC diagnostic warning "-std=c++11"
#define check(n, i) (int)(bool(!((n)&(1<<(i)))))
#define set(n, i) (((n)|(1<<(i))))
#define mod 100000
 
#define dbg(a) cout << #a << " = " << a << endl;
 
void faster(void)
{
    ios_base::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
}
 
int lcm(int a, int b)
{
    return (a*b) / __gcd(a, b);
}
 

int na, nb;
 
int mat[2][2], fib[2], matans[2][2];
 
void mul1(void)
{
    int mat00, mat01, mat10, mat11;
    mat00 = mat[0][0];
    mat01 = mat[0][1];
    mat10 = mat[1][0];
    mat11 = mat[1][1];
    mat[0][0] = ((mat00*mat00)%mod + (mat01*mat10)%mod)%mod;
    mat[0][1] = ((mat00*mat01)%mod + (mat01*mat11)%mod)%mod;
    mat[1][0] = ((mat10*mat00)%mod + (mat11*mat10)%mod)%mod;
    mat[1][1] = ((mat10*mat01)%mod + (mat11*mat11)%mod)%mod;
}
 
void mul3(int ara[][2])
{
    int matans00, matans01, matans10, matans11;
    matans00 = matans[0][0];
    matans01 = matans[0][1];
    matans10 = matans[1][0];
    matans11 = matans[1][1];
 
    matans[0][0] = ((matans00*ara[0][0])%mod + (matans01*ara[1][0])%mod)%mod;
    matans[0][1] = ((matans00*ara[0][1])%mod + (matans01*ara[1][1])%mod)%mod;
    matans[1][0] = ((matans10*ara[0][0])%mod + (matans11*ara[1][0])%mod)%mod;
    matans[1][1] = ((matans10*ara[0][1])%mod + (matans11*ara[1][1])%mod)%mod;
}
 
void mul2()
{
    int fib0 = fib[0];
    int fib1 = fib[1];
    fib[0] = ((matans[0][0]*fib0)%mod + (matans[0][1]*fib1)%mod)%mod;
    fib[1] = ((matans[1][0]*fib0)%mod + (matans[1][1]*fib1)%mod)%mod;
}

int fibo(int n)
{
    int y;
    if(!n) return 0;
    y=n-1;
    mat[0][0]=1;
    mat[0][1]=1;
    mat[1][0]=1;
    mat[1][1]=0;
    matans[0][0]=1;
    matans[0][1]=0;
    matans[1][0]=0;
    matans[1][1]=1;
    fib[0]=nb, fib[1]=na;
    while(y > 0)
    {
        if(y&1) mul3(mat);
        y /= 2;
        mul1();
    }
    mul2();
    return fib[0]%mod;
}
 
int bigmod(int base, int power)
{
    int ans=1;
    while(power > 0)
    {
        if(power&1) ans = (ans*base)%mod;
        power/=2;
        base *= base;
        base %= mod;
    }
    return ans;
}


int32_t main()
{
    #ifdef ONPC
      freopen("in.txt", "r", stdin);
      freopen("out.txt", "w", stdout);
    #endif
    faster();
    int t, t2, i, n, k, x, mud;
    cin >> t;t2=t;
    while(t--)
    {
      mud=1;
      cin >> na >> nb >> n >> k;
      while(k--) mud*=10;
      cout<< "Case "<<t2-t<<": "<<fibo(n)%mud <<endl;
    }
    return 0;
}

```
