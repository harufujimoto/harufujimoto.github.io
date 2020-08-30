---
layout: post
title: "UnionFind"
categories: datastructure
---

UnionFind木。

MAX_Nの値は適当に変える。2e6で'Runtime Error'を起こしていた気がする。

ufsize[]は自分の属する部分木のサイズを取得する。その時はufsize[find(x)]とかする？

TODO : 永続とか調べる

{% highlight cpp %}
struct UnionFind {
#define MAX_N 200000
	//UnionFind
	int par[MAX_N];
	int ufrank[MAX_N];
	int ufsize[MAX_N];
	UnionFind() {
		for (int i = 0; i < MAX_N; i++)
		{
			par[i] = i;
			ufrank[i] = 0;
			ufsize[i] = 1;
		}
	}
	int find(int x) {
		if (par[x] == x) return x;
		else return par[x] = find(par[x]);
	}
	void unite(int x, int y) {
		x = find(x);
		y = find(y);
		if (x == y) return;
		if (ufrank[x] < ufrank[y]) {
			par[ x] = y;
			int sx = ufsize[x], sy = ufsize[y];
			ufsize[x] = ufsize[y] = sx + sy;
		}
		else {
			par[y] = x;
			if (ufrank[x] == ufrank[y]) ufrank[x]++;
			int sx = ufsize[x], sy = ufsize[y];
			ufsize[x] = ufsize[y] = sx + sy;
		}
	}
	bool same(int x, int y) {
		return find(x) == find(y);
	}
};
{% endhighlight %}
