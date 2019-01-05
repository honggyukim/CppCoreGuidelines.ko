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
### SL.3: 비표준 개체를 이름공간 `std` 에 추가하지 말라

##### 이유

`std` 이름 공간에 무언가를 추가하는 작업은 다른 표준을 따르는 코드의 의미를 변경할 수도 있으며
`std` 에 무언가를 추가하면 표준의 향후 버전에서 의도하지 않은 충돌을 일으킬 수 있다.

<a name="sl-safe"></a>
### SL.4: 타입 안전성을 지키면서 표준 라이브러리를 사용하라

##### 이유

명백하게도 이 룰을 지키지 않으면 미정의 동작(undefined behavior), 메모리 corruption, 그리고 다른 모든 종류의 나쁜 에러들을 일으킬 수 있다.

<a name="SS-con"></a>
## SL.con: Containers

???

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
