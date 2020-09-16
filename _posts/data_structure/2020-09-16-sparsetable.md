---
layout: page
title: "Sparse Table"
---

配列の区間最小値を前計算O(NlogN) , クエリO(1)で求める。

ただし配列には変更が加えられない。

コンストラクタにvectorを突っ込むと前計算を始める。あとはquery(l,r) で \[l,r)の区間最小を計算する。

{% highlight cpp %}
template<class T>
struct SparseTable {
    vector<T> arr;
    vector<vector<T>> dat;
    int N;

    SparseTable() {}

    SparseTable(vector<T> &arr) : arr(arr), N(arr.size()) {
        dat.assign(N + 1, vector<T>(N + 1, 0));
        for (int i = 0; i < N; i++) dat[i][0] = arr[i];
        for (int j = 1; (1 << j) <= N; j++) {
            for (int i = 0; (i + (1 << j) - 1) < N; i++) {
                if (dat[i][j - 1] < dat[i + (1 << (j - 1))][j - 1]) {
                    dat[i][j] = dat[i][j - 1];
                } else {
                    dat[i][j] = dat[i + (1 << (j - 1))][j - 1];
                }
            }
        }
    }

    // get min [L,R)
    T query(int L, int R) {
        int j = (int) log2(R - L);
        if (dat[L][j] <= dat[R - (1 << j)][j])
            return dat[L][j];
        else
            return dat[R - (1 << j)][j];
    }

};

{% endhighlight %}
