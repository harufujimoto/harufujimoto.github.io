--
layout: page
title: "二項係数(Mod,Lucas's theorem)"
---
[edit](https://github.com/harufujimoto/harufujimoto.github.io/edit/master/_posts/math/2021-04-19-binom_lucas.md)

リュカの定理（Lucas's theorem)に基づいた、二項係数 binom(n,k) mod p で、n > p となるような場合に計算する。

{$ highlight cpp %}
template<class T>
T binom_lucas(T n, T k, T p) {
    auto f = [&](T n, T k) {
        if (n < 0 || k < 0 || n < k) return 0;
        T res = 1;
        for (int i = 1; i <= k; i++) {
            res = (res * T(n + 1 - i));
            res /= T(i);
            res %= p;
        }
        return res;
    };
    T res = 1;
    while (n) {
        res = res * f(n % p, k % p);
        n /= p;
        k /= p;
        res %= p;
    }
    return res;
}

{% endhighlight %}
