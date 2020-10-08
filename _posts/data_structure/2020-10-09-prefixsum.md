---
layout: page
title: "累積和"
---

多分動くと思うけどちょっと自信ない

{% highlight cpp %}
/*
    last updated : 2020.8.10
 */
template<class T> struct Cumulative{ // 一次元累積和
    int N;
    vector<T> c;
    vector<T> a;
    Cumulative(vector<T> a):a(a){
        N = a.size() + 1;
        c = vector<T>(N,0);
        build();
    }
    void build(){
        for(int i = 1;i <= N;i++){
            c[i] = c[i-1] + a[i];
        }
    }
    T query(int i,int j){//[i,j)を返す
        return c[j] - c[i];
    }
};

template<class T> struct Cumulative2D { // 二次元累積和
    int N,M;
    vector<vector<T> > Dat; 

    Cumulative2D(int N,int M):N(N),M(M){//aの配列size
        Dat = vector<vector<T> >(N+1,vector<T>(M+1,0));
    }
    void add(int i,int j,T x){ //a[i][j] = xをDat[i+1][j+1]に加算する
        Dat[i+1][j+1] += x;
    }
    void build(){//累積和テーブルを作成する
        for(int j = 1;j <= M;j++){ Dat[0][j] += Dat[0][j-1]; }
        for(int i = 1;i <= N;i++){ Dat[i][0] += Dat[i-1][0]; }
        for(int i = 1;i <= N;i++){
            for(int j = 1;j <= M;j++){
                Dat[i][j] += (Dat[i-1][j] + Dat[i][j-1] - Dat[i-1][j-1]);
            }
        }
    }
    T query(int i,int j,int k,int l){ //[(i,j) , (k,l))
        return Dat[k][l] - Dat[k][j] - Dat[i][l] + Dat[i][j];
    }
};
{% endhighlight %}
