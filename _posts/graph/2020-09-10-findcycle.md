---
layout: page
title: "グラフのサイクル検出"
---

グラフを突っ込んでdfs(0,0)を実行すると、頂点0からスタートするdfsで、サイクルの検出が行われる。

サイクルを一つ見つければよければその時点で終わりにすると楽。

まだverifyの余地があるのでいろいろやる

{% highlight cpp %}

template<class T> struct FindCycle{
  using vi = vector<int>;
  using vvi = vector<vi>;
  Graph<T> G;
  int n;
  vi col;
  int cy;
  vi mark;
  vi par;
  vvi cycles;
  FindCycle(Graph<T>& G):G(G){
    n=G.n;
    col.assign(n,0);
    cy=-1;
    mark.assign(n,-1);
    par.assign(n,0);
    cycles.assign(n,vi(0));
  }
  void dfs(int u,int p){
    cout << u << ' ' << p << endl;
    if(col[u]==2) return;
    if(col[u]==1){
      cy++;
      int cur = p;
      mark[cur] = cy;
      while(cur!=u){
        cur=par[cur];
        mark[cur]=cy;
      }
      return;
    }
    par[u]=p;
    col[u]=1;
    for(auto e:G[u]){
      int v=e.to;
      if(v==par[u]) continue;
      dfs(v,u);
    }
    col[u]=2;
  }
  vvi get_cycle(){
    for(int i=0;i<n;i++){
      if(mark[i]!=-1) cycles[mark[i]].push_back(i);
    }
    return cycles;
  }
};

{% endhighlight %}
