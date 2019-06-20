---
layout: post
title: Hudai Checking
tags: [DP]
---

# Hello World

```c++
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
    
```
