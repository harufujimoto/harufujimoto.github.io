---
layout: post
title: "(1 << k)個上の親を求める（ダブリング）"
---

LCAを求めるときに使うやつ。でも他でも使い道はある

{% highlight cpp %}
template<class T>
vector<vector<int>> calc_parent(Graph<T> G,int root) // directed graph & know root
{
  int n = G.n;
  vector<vector<int>> par(n,vector<int>(20));
  for(int i = 0;i < n;i++){
    if(G[i].size() != 0){
      for(auto e : G[i]){
        par[e.to][0] = i;
      }
    }
    par[root][0] = root;
  }
  for(int i = 0;i < n;i++){
    for(int j = 1;j < 20;j++){
      par[i][j] = par[par[i][j-1]][j-1];
    }
  }
  return par;
}
{% endhighlight %}
