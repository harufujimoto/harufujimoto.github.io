---
layout: post
title: "template CPP"
---

[edit](https://github.com/harufujimoto/harufujimoto.github.io/edit/master/_posts/2020-09-02-cpptemplate.md)

Codeforces

{% highlight cpp %}

void main2(){

}
int main(){
  cin.tie(0);
  ios::sync_with_stdio(false);
  
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
  
  int tt;cin >> tt;
  for(int i=1;i<=tt;i++){
    cout << "Case #" << i << ": ";
    main2();
  }
}

{% endhighlight %}