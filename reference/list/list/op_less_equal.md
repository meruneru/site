# operator<=
* list[meta header]
* std[meta namespace]
* function template[meta id-type]

```cpp
namespace std {
  template <class T, class Allocator>
  bool operator<=(const list<T, Allocator>& x, const list<T, Allocator>& y);
}
```

## 概要
`list`において、左辺が右辺以下かを判定する。


## 戻り値
`!(x > y)`


## 計算量
線形時間


## 例
```cpp example
#include <iostream>
#include <list>

int main ()
{
  std::list<int> ls1 = {1, 2, 3};
  std::list<int> ls2 = {4, 5, 6};

  std::cout << std::boolalpha;

  std::cout << (ls1 <= ls2) << std::endl;
}
```


### 出力
```
true
```


