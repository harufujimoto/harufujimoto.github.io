---
layout: page
title: "2円の交点"
---

A1 - R1 , A2 - R2の対応。
最後の引数に、交点を格納するpair<V,V>を持たせる。

戻り値は、交点の個数。

{% highlight cpp %}
using ld = long double;
int crossing_points(V& A1,V& A2,ld R1,ld R2,pair<V,V>& p)
{
  int res;
  ld d , h , x;
  V v,B,H1,H2;
 
  v = A2 - A1;
  d = v.norm();
 
  if(d > (R1 + R2)) return 0;
  else if(d == (R1 + R2)) res = 1;
  else res = 2;
  
  x = (R1*R1 - R2*R2 + d*d) / (d*2.0);
  v.setlength(x);
  B = A1 + v;
  v.round(90,0);
  h = sqrt(R1*R1 - x*x);
  v.setlength(h);
  H1 = B + v;
  H2 = B - v;
  p = make_pair(H1,H2);
  return res;
}
{% endhighlight %}
