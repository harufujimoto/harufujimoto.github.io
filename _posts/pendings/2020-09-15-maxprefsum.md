---
layout: page
title: "最大累積和(O(NlogN))"
---
[edit](https://github.com/harufujimoto/harufujimoto.github.io/blob/master/_posts/pendings/2020-09-15-maxprefsum.md)

セグメント木を使って「左端を固定した時の最大累積和」を求める

テストケースだと 実際の答えに+1されてしまう、そもそも動いてるのか怪しい（正統性も微妙）

kickstart 2019 round B - c

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

#define maxn 100010
#define INF (1LL << 55)
int N,S;
ll a[maxn];

int M;
ll sum[2*maxn],maxpref[2*maxn];

void init()
{
  M = 1;
  while(M <= N) M *= 2;
  fill(sum,sum + 2*M - 1,0);
  fill(maxpref,maxpref + 2*M - 1,-INF);
}
void update(int k,ll x)
{
  k += M - 1;
 // cout << "bef : sum[" << k << "] = " << sum[k] << '\n';
  sum[k] = x;
 // cout << "aft : sum[" << k << "] = " << sum[k] << '\n';
  maxpref[k] = x;
  while(k > 0)
  {
    k = (k - 1) / 2;
    sum[k] = sum[2*k+1] + sum[2*k+2];
    maxpref[k] = max(maxpref[2*k+1],sum[2*k+1]+maxpref[2*k+2]);
  }
}
ll get_sum(int a,int b,int k,int l,int r)
{
  if(r <= a || b <= l) return 0;
  if(a <= l && r <= b) return sum[k];
  else
  {
    ll vl = get_sum(a,b,k*2+1,l,(l+r)/2);
    ll vr = get_sum(a,b,k*2+2,(l+r)/2,r);
    return vl + vr;
  }
}
ll query(int a,int b,int k,int l,int r)
{
  if(r <= a || b <= l) return -INF;
  if(a <= l && r <= b) return maxpref[k];
  else
  {
    ll vl = query(a,b,k*2+1,l,(l+r)/2);
    ll vr = get_sum(a,b,k*2+1,l,(l+r)/2) + query(a,b,k*2+2,(l+r)/2,r);
    //cout << l << ',' << r << endl;
    //cout << "vl : " << vl << " , vr : " << vr << endl;
    return max(vr,vl) - 1;
  }
}
ll query(int a,int b)
{
  return query(a,b,0,0,M);
}

void main2()
{
  cin >> N >> S;
  REP(i,N) cin >> a[i];
  init();
  
  vector<int> last(100010,-1),cnt(100010,0),_next(N,-1);
  REP(i,N)
  {
    int v = a[i];
    int l = last[v];
    if(l == -1)
    {
      last[v] = i;
      cnt[i] = 1;
    }else{
      cnt[i] = cnt[l] + 1;
      _next[l] = i;
      last[v] = i;
    }
  }
  
  REP(i,N)
  {
    int v = 0;
    if(cnt[i] <= S) v = 1;
    else if(cnt[i] == S + 1) v = -S;
    debug2(i,v);
    update(i,v);
  }
  
  ll ans = -LONG_MAX;
  REP(i,N)
  {
    chmax(ans , query(i,N));
    
  
}

void testing()
{
  N = 8;
  init();
  cout << "M = " << M << endl;
  update(0,4);
  update(1,5);
 // REP(i,M) debug2(i,make_pair(sum[i],maxpref[i]));
  update(2,3);
  update(3,13);
  update(4,-33);
  update(5,400);
  update(6,-3);
  cout << query(0,8) << endl;
  exit(0);
}

int main()
{
  cin.tie(0);
  ios::sync_with_stdio(false);
  
  //testing();
  
  int tt;cin >> tt;
  for(int i=1;i<=tt;i++){
    cout << "Case #" << i << ": ";
    main2();
  }
}


{% endhighlight %}
