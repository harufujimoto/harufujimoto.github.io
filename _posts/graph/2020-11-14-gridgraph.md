---
layout:page
title: "generate grid graph"
---

[edit](https://github.com/harufujimoto/harufujimoto.github.io/edit/master/_posts/graph/2020-11-14-gridgraph.md)

depends on : graph template

{% highlight cpp %}
template<class T> struct GridGraphGenerate{
  int h,w;
  Graph<T> G;
  vector<vector<int>> grid;
  int get_id(int x,int y){
    return w * x + y;
  }
  GridGraphGenerate(int h,int w):h(h),w(w){
    G = Graph<T>((h+2)*(w+2));
    grid.assign(h+2,vector<int>(w+2,1));
  }
  void set_ng(int x,int y){
    grid[get_id(x,y)] = 0;
  }
  void build(int dir = 4){
    vector<int> dx = {1,0,-1,0,1,-1,-1,1};
    vector<int> dy = {0,-1,0,1,-1,-1,1,1};
    auto inside = [&](int x,int y)->bool{
      return x >= 0 && x < h && y >= 0 && y < w;
    };
    for (int i = 0; i < h; i++) {
      for (int j = 0; j < w; j++) {
        for (int d = 0; d < dir; d++) {
          int ni = i + dx[d]; 
          int nj = j + dy[d]; 
          if (inside(ni,nj) && grid[i][j] && grid[ni][nj]) {
            G.add_edge(get_id(i,j),get_id(ni,nj),1);
            G.add_edge(get_id(ni,nj),get_id(i,j),1);
          }
        }
      }
    }
  }
  Graph<T> get_graph(){
    return G; 
  }
};
{% endhighlight %}
