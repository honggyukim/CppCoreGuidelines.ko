<a name="S-stdlib"></a>
# SL: 표준 라이브러리(The Standard Library)

단순히 언어 자체만 사용하게 되면 모든 작업이 더디게 되고(어떤 언어라도), 반면 적절한 라이브러리를 사용하게 되면 어떤 작업도 상당히 단순해진다.

표준 라이브러리는 해가 갈 수록 꾸준히 성장하고 있다.
현재는 표준에 있는 설명이 언어 자체의 기능들보다 더 커졌다.
그래서 가이드라인의 이 라이브러리 섹션이 결국에는 다른 섹션 모두의 합과 같거나 더 많은 양을 기술할것으로 보인다.

C++ 표준 라이브러리 구성에 대한 요약:

> C++ Standard-library component summary:

* [SL.con: Containers](#SS-con)
* [SL.str: String](#SS-string)
* [SL.io: Iostream](#SS-io)
* [SL.regex: Regex](#SS-regex)
* [SL.chrono: Time](#SS-chrono)
* [SL.C: The C Standard Library](#SS-clib)

표준 라이브라리 규칙 요약:

> Standard-library rule summary:

* [SL.1: 가능한 곳 어디에서든 라이브러리를 사용하라](#Rsl-lib)
* [SL.2: 다른 라이브러리보다는 표준 라이브러리를 우선적으로 사용하라](#Rsl-sl)
* [SL.3: 비표준 개체를 이름공간 `std` 에 추가하지 말라](#sl-std)
* [SL.4: 타입 안전성을 지키면서 표준 라이브러리를 사용하라](#sl-safe)
* ???

<a name="Rsl-lib"></a>
### SL.1:  가능한 곳 어디에서든 라이브러리를 사용하라

##### 이유

처음부터 다시 만들지 말고 시간을 절약하라.
다른 사람이 이미 완료한 일을 중복해서 하지 말라.
다른 사람들이 향후 개선을 하게 되면 그 혜택을 누릴 수 있다.
또한 내가 직접 개선함으로서 다른 사람들을 도울 수 있다.

<a name="Rsl-sl"></a>
### SL.2: 다른 라이브러리보다는 표준 라이브러리를 우선적으로 사용하라

##### 이유

많은 사람들이 표준 라이브러리를 알고 있으므로
스스로 작성한 코드나 다른 라이브러리 보다 더 안정적이고, 더 잘 관리되고, 더 광범위한 곳에 사용할 수 있다.

<a name="sl-std"></a>
### SL.3: 비표준 개체를 이름공간 `std`에 추가하지 말라

##### 이유

`std` 이름 공간에 무언가를 추가하는 작업은 다른 표준을 따르는 코드의 의미를 변경할 수도 있으며
`std` 에 무언가를 추가하면 표준의 향후 버전에서 의도하지 않은 충돌을 일으킬 수 있다.

<a name="sl-safe"></a>
### SL.4: 타입 안전성을 지키면서 표준 라이브러리를 사용하라

##### 이유

명백하게도 이 룰을 지키지 않으면 미정의 동작(undefined behavior), 메모리 corruption, 그리고 다른 모든 종류의 나쁜 에러들을 일으킬 수 있다.

## <a name="SS-con"></a>SL.con: Containers

???

컨테이너 규칙 요약:

* [SL.con.1: C 의 배열을 사용하기보다 STL 의 `array` 나 `vector` 를 사용하라](#Rsl-arrays)
* [SL.con.2: 다른 컨테이너를 사용할 이유가 있지 않는다면 STL `vector` 를 기본으로 사용하라](#Rsl-vector)
* [SL.con.3: 경계조건에서 발생하는 에러를 피하라](#Rsl-bounds)
*  ???

### <a name="Rsl-arrays"></a>SL.con.1: C 의 배열을 사용하기보다 STL 의 `array`나 `vector`를 사용하라

##### 이유

C 배열은 덜 안전하고 `array`나 `vector`에 비해 가지는 장점이 없다.
고정된 길이의 배열에는 `std::array`를 사용하라. 이는 함수에 전달될때 포인터 전달에 비해 나빠지는 것이 없으며 자기 자신의 크기를 알 수 있다.
또한, 원래의 배열과 같이 스택에 할당되는 `std::array`는 자기 자신의 요소들 또한 스택에 보관한다.
가변길이 배열의 경우, `std::vector`를 사용하라. 이는 자신의 크기를 변경할 수 있으며 메모리 할당을 자체적으로 관리해준다.

##### 예제

    int v[SIZE];                        // BAD

    std::array<int, SIZE> w;             // ok

##### 예제

    int* v = new int[initial_size];     // BAD, owning raw pointer
    delete[] v;                         // BAD, manual delete

    std::vector<int> w(initial_size);   // ok

##### 노트

컨테이너에 대한 비소유 참조(non-owning references)의 경우 `gsl::span`를 사용하라.

##### 노트

Comparing the performance of a fixed-sized array allocated on the stack against a `vector` with its elements on the free store is bogus.
You could just as well compare a `std::array` on the stack against the result of a `malloc()` accessed through a pointer.
For most code, even the difference between stack allocation and free-store allocation doesn't matter, but the convenience and safety of `vector` does.
People working with code for which that difference matters are quite capable of choosing between `array` and `vector`.

##### Enforcement

* Flag declaration of a C array inside a function or class that also declares an STL container (to avoid excessive noisy warnings on legacy non-STL code). To fix: At least change the C array to a `std::array`.

### <a name="Rsl-vector"></a>SL.con.2: 다른 컨테이너를 사용할 이유가 있지 않는다면 STL `vector` 를 기본으로 사용하라

##### 이유

`vector`와 `array`는 다음의 세 가지 장점을 제공하는 유일한 표준 컨테이너들이다.
- 가장 빠른 범용 접근(random access, including being vectorization-friendly)
- 가장 빠른 일반적인 접근 패턴(begin-to-end or end-to-begin is prefetcher-friendly)
- 가장 적은 공간 부담(contiguous layout has zero per-element overhead, which is cache-friendly)

일반적인 경우 컨테이너로부터 요소를 추가하고 제거할 필요가 있는 경우 기본적으로 `vector`를 사용하고,
만약 컨테이너의 크기를 변경할 일이 없다면 `array`를 사용하라.

만약 다른 컨테이너가 더 적절해 보인다면, 예를 들어 O(log N) 검색 성능을 위해 `map`을 사용하거나, 요소들 중간에 효율적으로 삽입을 하고 싶은 경우는 `list`를 사용할 수 있다.  그렇지 않다면 몇 KB 의 크기까지는 보통의 경우에 `vector`가 더 나은 성능을 보일 수 있다.

##### Note

`string` should not be used as a container of individual characters. A `string` is a textual string; if you want a container of characters, use `vector</*char_type*/>` or `array</*char_type*/>` instead.

##### Exceptions

If you have a good reason to use another container, use that instead. For example:

* If `vector` suits your needs but you don't need the container to be variable size, use `array` instead.

* If you want a dictionary-style lookup container that guarantees O(K) or O(log N) lookups, the container will be larger (more than a few KB) and you perform frequent inserts so that the overhead of maintaining a sorted `vector` is infeasible, go ahead and use an `unordered_map` or `map` instead.

##### Note

To initialize a vector with a number of elements, use `()`-initialization.
To initialize a vector with a list of elements, use `{}`-initialization.

    vector<int> v1(20);  // v1 has 20 elements with the value 0 (vector<int>{})
    vector<int> v2 {20}; // v2 has 1 element with the value 20

[Prefer the {}-initializer syntax](#Res-list).

##### Enforcement

* Flag a `vector` whose size never changes after construction (such as because it's `const` or because no non-`const` functions are called on it). To fix: Use an `array` instead.

### <a name="Rsl-bounds"></a>SL.con.3: 경계조건에서 발생하는 에러를 피하라

##### 이유

할당된 요소들의 범위를 넘어서 읽거나 쓰는 경우에 나쁜 에러나 원치 않은 결과 및 사고 또는 보안 침해를 일으킬 수 있다.

##### Note

The standard-library functions that apply to ranges of elements all have (or could have) bounds-safe overloads that take `span`.
Standard types such as `vector` can be modified to perform bounds-checks under the bounds profile (in a compatible way, such as by adding contracts), or used with `at()`.

Ideally, the in-bounds guarantee should be statically enforced.
For example:

* a range-`for` cannot loop beyond the range of the container to which it is applied
* a `v.begin(),v.end()` is easily determined to be bounds safe

Such loops are as fast as any unchecked/unsafe equivalent.

Often a simple pre-check can eliminate the need for checking of individual indices.
For example

* for `v.begin(),v.begin()+i` the `i` can easily be checked against `v.size()`

Such loops can be much faster than individually checked element accesses.

##### Example, bad

    void f()
    {
        array<int, 10> a, b;
        memset(a.data(), 0, 10);         // BAD, and contains a length error (length = 10 * sizeof(int))
        memcmp(a.data(), b.data(), 10);  // BAD, and contains a length error (length = 10 * sizeof(int))
    }

Also, `std::array<>::fill()` or `std::fill()` or even an empty initializer are better candidate than `memset()`.

##### Example, good

    void f()
    {
        array<int, 10> a, b, c{};       // c is initialized to zero
        a.fill(0);
        fill(b.begin(), b.end(), 0);    // std::fill()
        fill(b, 0);                     // std::fill() + Ranges TS

        if ( a == b ) {
          // ...
        }
    }

##### Example

If code is using an unmodified standard library, then there are still workarounds that enable use of `std::array` and `std::vector` in a bounds-safe manner. Code can call the `.at()` member function on each class, which will result in an `std::out_of_range` exception being thrown. Alternatively, code can call the `at()` free function, which will result in fail-fast (or a customized action) on a bounds violation.

    void f(std::vector<int>& v, std::array<int, 12> a, int i)
    {
        v[0] = a[0];        // BAD
        v.at(0) = a[0];     // OK (alternative 1)
        at(v, 0) = a[0];    // OK (alternative 2)

        v.at(0) = a[i];     // BAD
        v.at(0) = a.at(i);  // OK (alternative 1)
        v.at(0) = at(a, i); // OK (alternative 2)
    }

##### Enforcement

* Issue a diagnostic for any call to a standard-library function that is not bounds-checked.
??? insert link to a list of banned functions

This rule is part of the [bounds profile](#SS-bounds).

**TODO Notes**:

* Impact on the standard library will require close coordination with WG21, if only to ensure compatibility even if never standardized.
* We are considering specifying bounds-safe overloads for stdlib (especially C stdlib) functions like `memcmp` and shipping them in the GSL.
* For existing stdlib functions and types like `vector` that are not fully bounds-checked, the goal is for these features to be bounds-checked when called from code with the bounds profile on, and unchecked when called from legacy code, possibly using contracts (concurrently being proposed by several WG21 members).




## STL.str: String

???

## STL.io: Iostream

???

### STL.???: Use character-level input only when you have to; _expr.low_.

### STL.???: When reading, always consider ill-formed input; _expr.low_.

## STL.regex: Regex

???

## STL:c: The C standard library

### STL.???: C-style strings

### STL.???: printf/scanf
