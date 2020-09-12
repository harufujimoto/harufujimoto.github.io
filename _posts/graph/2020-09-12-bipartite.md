---
layout: page
title: "二部グラフ判定"
---

グラフを突っ込めば頂点を二色に彩色する。

is_bipartite()で、二部グラフかを取得し、二部だったらget()で彩色を取得する。色は0 or 1。

{% highlight cpp %}
template<class T> struct Bipartitle{
  int n;
  Graph<T> G;
  vector<int> col;
  bool flag = true;
  Bipartitle(Graph<T>& G):G(G),col(G.n,-1){
    n = G.n;
    for(int i = 0;i < n;i++){
      if(col[i] == -1) dfs(i,0);
    }
  }
  void dfs(int x,int c){
    col[x] = c;
    for(auto e : G[x]){
      if(col[e.to] == -1){
        dfs(e.to,c^1);
      }else if(col[e.to] == c){
        flag = false;
        return;
      }
    }
  }
  bool is_bipartite(){
    return flag;
  }
  vector<int> get(){
    return col;
  }
};

{% endhighlight %}
