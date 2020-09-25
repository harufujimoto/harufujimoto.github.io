---
layout: page
title: "数列に対するクエリ・データ構造処理など"
---
[edit](https://github.com/harufujimoto/harufujimoto.github.io/edit/master/_posts/others/2020-09-25-arrays_query.md)

### [CF1420C2](https://codeforces.com/contest/1420/problem/C2)
- 部分列に対して、+,-,+,-,...としていく。部分列の総和の最大は？
- (a_i - a_(i+1)) + (a_(i+1) - a_(i+2)) としたときに、a_(i+1)が相殺される。落差の最大化みたいなことをしたいときに前から順番に見ていけば良い。
- 結局、max(a_(i+1) - a_i,0)を足し込んでいくのが最適。
