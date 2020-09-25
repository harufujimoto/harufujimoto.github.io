---
layout: page
title: "数列に対するクエリ・データ構造処理など"
---
[edit](https://github.com/harufujimoto/harufujimoto.github.io/edit/master/_posts/others/2020-09-25-arrays_query.md)

### [CF1420C2](https://codeforces.com/contest/1420/problem/C2)
- 部分列に対して、+,-,+,-,...としていく。部分列の総和の最大は？
- (a_i - a_(i+1)) + (a_(i+1) - a_(i+2)) としたときに、a_(i+1)が相殺される。落差の最大化みたいなことをしたいときに前から順番に見ていけば良い。
- 結局、max(a_(i+1) - a_i,0)を足し込んでいくのが最適。

### [CF1418D](https://codeforces.com/problemset/problem/1418/D)
- 数直線上にN個のゴミがある。これらのゴミを、ある位置にあるゴミを左右1ます隣に全部動かす、というムーブを繰り返してゴミの存在するマスを2つ以内にするために必要な最小の動作は何回？
- 観察：ゴミの場所の集合であって、それらを一つの位置に纏めようとするものについて、必要なムーブは、(集合のXの最大 - Xの最小）になる。
- よって、2つのセグメントを作って、右セグメントの左端と左セグメントの右端との距離を最大化すれば良い。
- 全ての位置をsetで持って、dist\[i] := X\[i+1] - X\[i]をmultisetで持ちながら管理すれば良い。
