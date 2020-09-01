---
layout: post
title: "部分木の個数を数える
---

グラフのテンプレートを使う。kickstartで問題を誤解したときに書いたけど多分動く。

{% highlight cpp %}
template<class T>
long long __dfs(Graph<T>& G,vector<long long>& res,int x,int pre = -1){
  long long ans = 0;
  for(auto e : G[x]){
    if(e.to != pre){
      ans += __dfs(G,res,e.to,x);
    }
  }
  return res[x] = ans + 1;
}
template<class T>
vector<long long> CountSubtrees(Graph<T> G,int root){
  vector<long long> res(G.n,0);
  __dfs(G,res,root,-1);
  return res;
}
{% endhighlight %}
