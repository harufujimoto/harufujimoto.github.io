---
layout: page
title: "点,円"
---

# 点（ベクトル）クラス

ld dot(V b) : 内積。

ld det(V b) : 外積。

ld norm() : ノルムを取得する。

V& setlength(ld len) : ベクトルのノルムをlenに変更する。

void round(ld deg,bool argument = false) : ベクトルを回転させる。度数で入力する場合argumentはfalseのまま、ラジアンで入力する時trueにする。

ld getarg() : 偏角を取得。



{% highlight cpp %}
struct V{
using ld = long double;
 
    const ld EPS = 1E-12;
    const ld PI = 3.141592653589793238462643;
    ld x,y;
 
    ld add(ld a,ld b){
        if(abs(a+b) < EPS * (abs(a) + abs(b)))return 0;
        else return a + b;
    }
    ///////////////////////////////////////////////////
    V(){}
    V(ld x,ld y):x(x),y(y){}
    V &operator = (const V& anot){
      if(this != &anot){
        x = anot.x;
        y = anot.y;
      }
      return (*this);
    }
 
    V operator + (V anot){
      return V(add(x , anot.x) , add(y , anot.y));
    }
    V operator - (V anot){
      return V(add(x , -anot.x) , add(y , -anot.y));
    }
    V operator * (ld d){
      return V(x * d , y * d);
    }
 
    bool  operator<(V& b){return getarg() > b.getarg();}
    
    ld dot(V b){return add(x * b.x,y * b.y);}
    ld det(V b){return add(x * b.y , -y * b.x);}
    
    ld norm(){return sqrt(add(x*x , y*y));}
    void normalize(){
      ld n = (*this).norm();
      ld nx = x / n;
      ld ny = y / n;
      this->x = nx,this->y = ny;
    }
    V& setlength(ld len){
      ld ratio = len / (*this).norm();
      this->x *= ratio;
      this->y *= ratio;
      return (*this);
    }
 
    void round(ld deg,bool argument = false){//弧度法で入力する時はargument = true
        ld arg = (argument ? deg : PI*(deg/180.0)) ;
        ld nx = add(x * cos(arg) , -y * sin(arg));
        ld ny = add(x * sin(arg) , y * cos(arg));
        this->x = nx , this->y = ny;
    }
 
    ld getarg(){
        return atan2(y,x);// [PI,-PI]
    }
 
    friend ostream& operator<<(ostream& os,V& p){
        os << fixed << setprecision(10);
        os << "(" << p.x << "," << p.y << ")";
        return os;
    }
};
{% endhighlight %}

