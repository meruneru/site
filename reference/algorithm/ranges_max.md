# max
* algorithm[meta header]
* std::ranges[meta namespace]
* function template[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std::ranges {
  template<class T, class Proj = identity,
           indirect_strict_weak_order<projected<const T*, Proj>> Comp = ranges::less>
  constexpr const T& max(const T& a, const T& b, Comp comp = {}, Proj proj = {}); // (1)

  template<copyable T, class Proj = identity,
           indirect_strict_weak_order<projected<const T*, Proj>> Comp = ranges::less>
  constexpr T max(initializer_list<T> r, Comp comp = {}, Proj proj = {});         // (2)

  template<input_range R, class Proj = identity,
           indirect_strict_weak_order<projected<iterator_t<R>, Proj>> Comp = ranges::less>
    requires indirectly_copyable_storable<iterator_t<R>, range_value_t<R>*>
  constexpr range_value_t<R> max(R&& r, Comp comp = {}, Proj proj = {});          // (3)
}
```
* identity[link /reference/functional/identity.md]
* indirect_strict_weak_order[link /reference/iterator/indirect_strict_weak_order.md]
* projected[link /reference/iterator/projected.md]
* ranges::less[link /reference/functional/ranges_less.md]
* initializer_list[link /reference/initializer_list/initializer_list.md]
* input_range[link /reference/ranges/input_range.md]
* indirectly_copyable_storable[link /reference/iterator/indirectly_copyable_storable.md]
* iterator_t[link /reference/ranges/iterator_t.md]
* range_value_t[link /reference/ranges/range_value_t.md]

## 概要
同じ型の2つの値、もしくは範囲によるN個の値のうち、最大値を取得する。

## 戻り値
比較 [`invoke`](/reference/functional/invoke.md)`(comp, `[`invoke`](/reference/functional/invoke.md)`(proj, *i), `[`invoke`](/reference/functional/invoke.md)`(proj, *j))` によって最大と判断された最初の値

## 備考
- 等価な要素が 2 つ以上あった場合には、最も左の要素を返す。

## 例
```cpp example
#include <array>
#include <algorithm>
#include <functional>

int main()
{
  constexpr int result1 = std::ranges::max(2, 3);
  static_assert(result1 == 3);

  constexpr int result2 = std::ranges::max(2, 3, std::ranges::greater());
  static_assert(result2 == 2);

  constexpr int result3 = std::ranges::max({1, 2, 3});
  static_assert(result3 == 3);

  constexpr std::array<int, 3> a = {1, 2, 3};

  constexpr int result4 = std::ranges::max(a, std::ranges::greater());
  static_assert(result4 == 1);
}
```
* std::ranges::max[color ff0000]
* std::ranges::greater[link /reference/functional/greater.md]

### 出力
```
```

### 備考
Windows環境においては、`<windows.h>`をインクルードすると`max`という名前の関数マクロが定義され、`std::ranges::max()`と衝突してしまうという問題がある。

この解決策として以下の2つの方法がある：

- `<windows.h>`をインクルードするまでに`#define NOMINMAX`を行う。これで`max`マクロが定義されなくなる。
- `std::ranges::max()`を呼び出す際に、`(std::ranges::max)(a, b);`のように関数名をカッコで囲んで使用する。これで、名前解決において`std::ranges::max()`関数が必ず使用される。

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): 10.1.0
- [ICC](/implementation.md#icc): ??
- [Visual C++](/implementation.md#visual_cpp): 2019 Update 10

## 参照
- [N4861 25 Algorithms library](https://timsong-cpp.github.io/cppwp/n4861/algorithms)
