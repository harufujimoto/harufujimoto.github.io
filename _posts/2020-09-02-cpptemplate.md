---
layout: post
title: "template CPP"
---

[edit](https://github.com/harufujimoto/harufujimoto.github.io/edit/master/_posts/2020-09-02-cpptemplate.md)

compile option
{% highlight bash %}
alias g='g++ main.cpp -std=c++17 -Wshadow -Wall -fsanitize=address -fsanitize=undefined -DLOCAL -D_GLIBCXX_DEBUG'
{% endhighlight %}

AtCoder,Codeforces : C++17対応

Google,AOJ : C++14 (構造化束縛とか使っちゃダメ）

そのほか：知らん

general


{% highlight cpp %}

#include<bits/stdc++.h>
#include<iomanip>
using namespace std;
#define REP(i,n) for(int i = 0;i < n;i++)
#define RNG(i,s,n) for(int i = s;i <= n;i++)
#define _RNG(i,e,s) for(int i = e;i >= s;i--)
#define mp make_pair
#define pb push_back
#define eb emplace_back
#define dup(x,y) (x + y - 1) / (y)
#define all(x) (x).begin(),(x).end()
#define rall(x) (x).rbegin(),(x).rend()
#define lb(x,key) lower_bound(all(x) , (key))
#define ub(x,key) upper_bound(all(x) , (key))
#define _size(v) int((v).size())

template<class T> bool chmax(T& a,T b){ if(a < b){ a = b; return true; }else return false; }
template<class T> bool chmin(T& a,T b){ if(a > b){ a = b; return true; }else return false; }

using ll = long long;
using ld = long double;
using vi = vector<int>;
using vl = vector<ll>;
using pi = pair<int,int>;
using pl = pair<ll,ll>;
using vpi = vector<pi>;
using vpl = vector<pl>;

#define debug(arr) cout << #arr << " = " << arr << '\n'
#define debug2(a,b) cout<<"["<<#a<<","<<#b<<"] = "<<"["<<a<<","<<b<<"]\n"
#define debug3(a,b,c) cout<<"["<<#a<<","<<#b<<","<<#c<<"] = "<<"["<<a<<","<<b<<","<<c<<"]\n"
template<class T> ostream &operator << (ostream& out, const vector<T>& arr) {
    cout << "{"; for (int i = 0; i < arr.size(); i++)cout << (!i ? "" : ", ") << arr[i]; cout << "}";
    return out;
}
template<class T> ostream &operator << (ostream& out, const vector<vector<T> >& arr) {
    cout << "{\n"; for (auto& vec : arr)cout << "  " << vec << ",\n"; cout << "}";
    return out;
}
template<class S,class T> ostream &operator << (ostream& out, const pair<S,T>& p){
    cout << "{" << p.first << "," << p.second << "}" << '\n';
    return out;
}
template<class T> istream &operator >> (istream& in, vector<T>& arr) {
    for (auto& i : arr)cin >> i; return in;
}
template<class S,class T> istream &operator >> (istream& in,pair<S,T>& p){
    cin >> p.first >> p.second; return in;
}

#define F first
#define S second
/////////////////////////////////////////////////////////////////////////
{% endhighlight %}

AtCoder

{% highlight cpp %}

int main(void){
  cin.tie(0);
  ios::sync_with_stdio(false);
  //cout << fixed << setprecision(20);
  
  return 0;
}

{% endhighlight %}

Codeforces

{% highlight cpp %}

void main2(){

}
int main(){
  cin.tie(0);
  ios::sync_with_stdio(false);
  //cout << fixed << setprecision(20);
  
  int tt;cin >> tt;
  while(tt--) main2();
  return 0;
}

{% endhighlight %}

Google

{% highlight cpp %}

void main2(){

}
int main(){
  cin.tie(0);
  ios::sync_with_stdio(false);
  //cout << fixed << setprecision(20);
  
  int tt;cin >> tt;
  for(int i=1;i<=tt;i++){
    cout << "Case #" << i << ": ";
    main2();
  }
}

{% endhighlight %}
