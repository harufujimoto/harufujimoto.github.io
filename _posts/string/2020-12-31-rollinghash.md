---
layout: post
title: "Rolling Hash"
---
{% highlight cpp %}
struct RollingHash{
  using i64 = int64_t;
  vector<i64> MOD = {1000000007,1000000009,998244353};
  vector<i64> Hash[3],value;
  i64 b = 1000007;
  int la,lb;
  void add(i64& a,i64 b,i64 mod){
    a += b;
    if(a < 0){
      a += mod*((-a + mod - 1) / mod);
    }
    a %= mod;
  }
  void mult(i64& a,i64 b,i64 mod){
    a *= b;
    if(a < 0){
      a += mod*((-a + mod - 1) / mod);
    }
    a %= mod;
  }
  vector<i64> get_hashvalue(string a){
    vector<i64> res(3,0);
    for(int i=0;i<3;i++){
      i64 tmp=1,mod=MOD[i];
      for(int j=la-1;j>=0;j--){
        add(res[i],1LL*(a[j]-'a')*tmp,mod);
        mult(tmp,b,mod);
      }
    }
    return res;
  }
  RollingHash(string p,string t){
    la = p.length();
    lb = t.length();
    assert(lb >= la);
    value = get_hashvalue(p);
    for(int i=0;i<3;i++){
      i64 mod = MOD[i];
      Hash[i].assign(lb-la+1,0);
      i64 h=1;
      for(int i=0;i<la;i++)mult(h,b,mod);
      i64 tmp=1;
      for(int j=la-1;j>=0;j--){
        add(Hash[i][0],1LL*(t[j] -'a')*tmp,mod);
        mult(tmp,b,mod);
      }
      for(int j=la;j<lb;j++){
        i64 val = Hash[i][j-la];
        mult(val,b,mod);
        add(val,-h*(t[j-la]-'a'),mod);
        add(Hash[i][j+1-la],val,mod);
        add(Hash[i][j+1-la],1LL*(t[j]-'a'),mod);
      }
    }
  }
  RollingHash(string t,int size){
    la = size;
    lb = t.length();
    assert(lb >= la);
    for(int i=0;i<3;i++){
      i64 mod = MOD[i];
      Hash[i].assign(lb-la+1,0);
      i64 h=1;
      for(int i=0;i<la;i++)mult(h,b,mod);
      i64 tmp=1;
      for(int j=la-1;j>=0;j--){
        add(Hash[i][0],1LL*(t[j] -'a')*tmp,mod);
        mult(tmp,b,mod);
      }
      for(int j=la;j<lb;j++){
        i64 val = Hash[i][j-la];
        mult(val,b,mod);
        add(val,-h*(t[j-la]-'a'),mod);
        add(Hash[i][j+1-la],val,mod);
        add(Hash[i][j+1-la],1LL*(t[j]-'a'),mod);
      }
    }
  }
  vector<int> search(){
    vector<int> res;
    for(int j=0;j<lb-la+1;j++){
      int ok=1;
      for(int i=0;i<3;i++){
        ok &= (value[i] == Hash[i][j]);
      }
      if(ok) res.push_back(j);
    }
    return res;
  }
};

{% endhighlight %}
