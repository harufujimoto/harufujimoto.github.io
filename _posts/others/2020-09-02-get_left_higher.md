---
layout: post
title: "配列：自分より大きい要素で自分に最も近い値のテーブルをO(N)で求める"
---

stackを用いる。

この時、値そのものはans,場所はIDに格納されている。どっちも欲しかったらpairにして返す。

{% highlight cpp %}
template<class T>
vector<int> getLeftHigher(vector<T>& a,int n){
  stack<pair<T,int>> S;
  vector<int> ans(n,-1);
  vector<int> ID(n,-1);
  for(int i = 0;i < n;i++){
    while(!S.empty() && S.top().first <= a[i]) // smaller : >=
      S.pop();
    if(S.empty())
      ans[i] = -1;
    else
      ans[i] = S.top().first,ID[i] = S.top().second;
      
    S.emplace(a[i],i);
  }
  //return ans;
  return ID;
}
template<class T>
vector<int> getRightHigher(vector<T>& a,int n){
  stack<pair<T,int>> S;
  vector<int> ans(n,-1),ID(n,-1);
  for(int i = n-1;i >= 0;i--){
    while(!S.empty() && S.top().first <= a[i]) // smaller : >=
      S.pop();
    if(S.empty())
      ans[i] = -1,ID[i] = -1;
    else
      ans[i] = S.top().first,ID[i] = S.top().second;
    S.emplace(a[i],i);
  }
  //return ans;
  return ID;
}
{% endhighlight %}

{% highlight cpp %}
template<class T>
vector<int> getLeftLower(vector<T>& a,int n){
  stack<pair<T,int>> S;
  vector<int> ans(n,-1);
  vector<int> ID(n,-1);
  for(int i = 0;i < n;i++){
    while(!S.empty() && S.top().first >= a[i]) // smaller : >=
      S.pop();
    if(S.empty())
      ans[i] = -1;
    else
      ans[i] = S.top().first,ID[i] = S.top().second;
      
    S.emplace(a[i],i);
  }
  //return ans;
  return ID;
}
template<class T>
vector<int> getRightLower(vector<T>& a,int n){
  stack<pair<T,int>> S;
  vector<int> ans(n,-1),ID(n,-1);
  for(int i = n-1;i >= 0;i--){
    while(!S.empty() && S.top().first >= a[i]) // smaller : >=
      S.pop();
    if(S.empty())
      ans[i] = -1,ID[i] = -1;
    else
      ans[i] = S.top().first,ID[i] = S.top().second;
    S.emplace(a[i],i);
  }
  //return ans;
  return ID;
}
{% endhighlight %}

// verified : google kick start 2020-D-d.
