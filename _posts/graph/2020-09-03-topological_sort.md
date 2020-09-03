---
layout: post
title: "トポロジカルソート"
---

使い方: コンストラクタにグラフを突っ込む。突っ込んだらtopologicalSort()関数を呼び出すと、トポロジカル順の添字配列が出力される。（上位の頂点が先に来る)

{% highlight cpp %}
#include "template.cpp"
template<class T> struct TopologicalSorting{
    Graph<T> G;
    TopologicalSorting(Graph<T>& G):G(G){}
    void topologicalSortUtil(int v,vector<bool>& visited,stack<int>& Stack);
    vector<int> topologicalSort();
};
template<class T>
void TopologicalSorting<T>::topologicalSortUtil(int v, vector<bool> &visited, stack<int> &Stack) {
    visited[v] = true;
    for(int i = 0;i < G[v].size();i++){
        int _to = G[v][i].to;
        if(!visited[_to]) topologicalSortUtil(_to,visited,Stack);
    }
    Stack.push(v);
}
template<class T>
vector<int> TopologicalSorting<T>::topologicalSort() {
    stack<int> Stack;
    vector<int> res;
    vector<bool> visited(G.n,false);
    for(int i = 0;i < G.n;i++){
        if(!visited[i]) topologicalSortUtil(i,visited,Stack);
    }
    while(Stack.size()){
        res.push_back(Stack.top());
        Stack.pop();
    }
    return res;
}


{% endhighlight %}
