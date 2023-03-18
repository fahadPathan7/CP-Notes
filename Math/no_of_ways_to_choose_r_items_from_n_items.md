# No. of ways to choose r items from n items


### Index
- [Basic discussion](#basic-discussion)
- [Code segment to find modular multiplicative inverse](#code-segment-to-find-modular-multiplicative-inverse)
- [Calculating nCr](#calculating-ncr)
- [Resources to follow](#resources-to-follow)
- [Problems to practice](#problems-to-practice)

<br>

### Basic discussion

This is a combinatorics problem.<br>We need to calculate under a modulus value.

The ans is **nCr**<br><br>

> **nCr = n! / (n - r)! * r!**

<br>
Firstly, we need to calculate the value of n! and (n - r)! * r! differently. <br>
then we will use modular multiplicative inverse to get the result.

let, divisor = (n - r)! * r!<br>
now we need the modular multiplicative inverse of the divisor.

if divisor and mod are co-prime (gcd(divisor, mod) = 1),
then, according to extended euclidean algorithm we know,

**a * x + b * y = gcd(a, b)**

now, divisor * x + mod * y = gcd(divisor, mod). but the gcd is 1 (as divisor and mod are co-prime). so,

**divisor * x + mod * y = 1**

If we take modulu of mod from the both sides, (~= means congruence)

**divisor * x ~= 1 (modulus mod)**

So, x is the modular multiplicative inverse of the divisor. we can get the value of x by using extended euclidean algorithm.

<br>

### Code segment to find modular multiplicative inverse

```c++
int extendedEuclid(int a, int b, int& x, int& y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int x1, y1;
    int gcd = extendedEuclid(b, a % b, x1, y1);
    x = y1;
    y = x1 - (a / b) * y1;
    return gcd;
}
int modInverse(int A, int M) {
    // A is the divisor and M is the mod
    int x, y; // x is the mmi of A
    int gcd = extendedEuclid(A, M, x, y);
    if (gcd != 1) return -1; // modular multiplicative inverse is not possible
    return (x % M + M) % M; // to avoid negative number
}
```

<br>

### Calculating nCr

now we have the the factorial of n (factN) and mmi of divisor (mmiDivisor).<br>
So, the result would be, **(factN * mmiDivisor) % mod**

code segment. assuming that divisor and mod are co-prime here.
```c++
#include <bits/stdc++.h>
using namespace std;

#define mod 1000003

vector<int> fact(1000001);

void factorial() {
    fact[0] = 1;
    for (ll i = 1; i <= 1000000; i++) {
        fact[i] = (fact[i - 1] * i) % mod;
    }
}
int extendedEuclid(int a, int b, int& x, int& y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    int x1, y1;
    int gcd = extendedEuclid(b, a % b, x1, y1);
    x = y1;
    y = x1 - (a / b) * y1;
    return gcd;
}
int modInverse(int A, int M) {
    int x, y; // x is the mmi of A(divisor)
    int gcd = extendedEuclid(A, M, x, y);
    return (x % M + M) % M; // adding M to avoid negative result
}

int main() {
    factorial(); // calculating the factorial values first
    int n, r; // r items to choose from n items
    cin >> n >> r;
    int divisor =  (fact[n - r] * fact[r]) % mod; // (n - r)! * r!
    int res = (fact[n] * modInverse(divisor, mod));
    cout << res << endl;
}
```

<br>

### Resources to follow
- [geeksforgeeks](https://www.geeksforgeeks.org/multiplicative-inverse-under-modulo-m/)

<br>

### Problems to practice
- [Combinations](https://lightoj.com/problem/combinations)

