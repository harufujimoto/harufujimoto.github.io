---
layout: post
title: "template CPP"
---

[edit](https://github.com/harufujimoto/harufujimoto.github.io/edit/master/_posts/2020-09-02-cpptemplate.md)

general


{% highlight cpp %}

#include<bits/stdc++.h>
using namespace std;
 
#define REP(i,n) for(int i = 0;i < n;i++)
#define mp make_pair
#define pb push_back
#define eb emplace_back
#define all(x) (x).begin(),(x).end()

template<class T> bool chmax(T& a,T b){ if(a < b){ a = b; return true; }else return false; }
template<class T> bool chmin(T& a,T b){ if(a > b){ a = b; return true; }else return false; }
 
using ll = long long;
using ld = long double;
using vi = vector<int>;
using vl = vector<ll>;
using Pi = pair<int,int>;
using Pl = pair<ll,ll>;
using vpi = vector<Pi>;
using vpl = vector<Pl>;
 
void lyn(){
  cin.tie(0);
  ios::sync_with_stdio(false);
}
 
#define debug(arr) cout << #arr << " = " << arr << '\n'
#define debug2(a,b) cout << "[" << #a << "," << #b << "] = " << "[" << a << "," << b << "]" << '\n'
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


{% endhighlight %}

Codeforces

{% highlight cpp %}

void main2(){

}
int main(){
  cin.tie(0);
  ios::sync_with_stdio(false);// interactiveでは使わない！
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
  ios::sync_with_stdio(false);// interactiveでは使わない！
  //cout << fixed << setprecision(20);
  
  int tt;cin >> tt;
  for(int i=1;i<=tt;i++){
    cout << "Case #" << i << ": ";
    main2();
  }
}

{% endhighlight %}
