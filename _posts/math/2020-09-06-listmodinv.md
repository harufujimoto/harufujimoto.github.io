---
post: page
title: "逆元O(N)列挙"
---

[edit](https://github.com/harufujimoto/harufujimoto.github.io/edit/master/_posts/math/2020-09-06-listmodinv.md)

{% highlight cpp %}
vector<mint> list_mod_inverse(ll n = 1000010){
  vector<mint> inv(n+1,1);
  for(int i=2;i<=n;i++)inv[i]=inv[MOD%i]*(mint)(MOD-MOD/i);
  return inv;
}
{% endhighlight %}

{% highlight cpp %}
vector<ll> list_mod_inverse(ll n, ll m)
{
    vector<ll> inv(n + 1);
    inv[1] = 1;
    for (int i = 2; i <= n; ++i)
        inv[i] = inv[m % i] * (m - m / i) % m;
    return inv;
}

{% endhighlight %}
