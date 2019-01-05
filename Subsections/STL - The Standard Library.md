<a name="S-stdlib"></a>
# STL: The Standard Library
STL: 표준 라이브러리

단순히 언어 자체만 사용하게 되면 모든 작업이 더디게 되고(어떤 언어라도), 반면 적절한 라이브러리를 사용하게 되면 어떤 작업도 상당히 단순해진다. 

> Using only the bare language, every task is tedious (in any language).
> Using a suitable library any task can be reasonably simple.

표준 라이브러리는 해가 갈 수록 꾸준히 성장하고 있다.
현재는 표준에 있는 설명이 언어 자체의 기능들보다 더 커졌다.
그래서 가이드라인의 이 라이브러리 섹션이 결국에는 다른 섹션 모두의 합과 같거나 더 많은 양을 기술할것으로 보인다.

> The standard library has steadily grown over the years.
> Its description in the standard is now larger than that of the language features.
> So, it is likely that this library section of the guidelines will eventually grow in size to equal or exceed all the rest

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

* [SL.1: Use libraries wherever possible](#Rsl-lib)
* SL.1: 가능한 곳 어디에서든 라이브러리를 사용하라
* [SL2.: Prefer the standard library to other libraries](#Rsl-sl)
* SL.2: 다른 라이브러리보다는 표준 라이브러리를 우선적으로 사용하라
* [SL.3: Do not add non-standard entities to namespace `std`](#sl-std)
* SL.3: 비표준 개체를 이름공간 `std` 에 추가하지 말라
* [SL.4: Use the standard library in a type-safe manner](#sl-safe)
* SL.4: 타입 안전성을 지키면서 표준 라이브러리를 사용하라
* ???

<a name="Rsl-lib"></a>
### SL.1:  가능한 곳 어디에서든 라이브러리를 사용하라(Use libraries wherever possible)

**Reason**

처음부터 다시 만들지 말고 시간을 절약하라.
다른 사람이 이미 완료한 일을 중복해서 하지 말라.
다른 사람들이 향후 개선을 하게 되면 그 혜택을 누릴 수 있다.
또한 내가 직접 개선함으로서 다른 사람들을 도울 수 있다.

> Save time. Don't re-invent the wheel.
> Don't replicate the work of others.
> Benefit from other people's work when they make improvements.
> Help other people when you make improvements.

<a name="Rsl-sl"></a>
### SL.2: 다른 라이브러리보다는 표준 라이브러리를 우선적으로 사용하라(Prefer the standard library to other libraries)

**Reason**

많은 사람들이 표준 라이브러리를 알고 있으므로 스스로 작성한 코드나 다른 라이브러리 보다 더 안정적이고, 더 잘 관리되고, 더 광범위한 곳에 사용할 수 있다.

> More people know the standard library.
> It is more likely to be stable, well-maintained, and widely available than your own code or most other libraries.

<a name="sl-std"></a>
### SL.3: 비표준 개체를 이름공간 `std` 에 추가하지 말라(Do not add non-standard entities to namespace `std`)

**Reason**

`std` 이름 공간에 무언가를 추가하는 작업은 다른 표준을 따르는 코드의 의미를 변경할 수도 있으며
`std` 에 무언가를 추가하면 표준의 향후 버전에서 의도하지 않은 충돌을 일으킬 수 있다.

> Adding to `std` may change the meaning of otherwise standards conforming code.
> Additions to `std` may clash with future versions of the standard.

<a name="sl-safe"></a>
### SL.4: 타입 안전성을 지키면서 표준 라이브러리를 사용하라(Use the standard library in a type-safe manner)

**Reason**

명백하게도 이 룰을 지키지 않으면 미정의 동작(undefined behavior), 메모리 corruption, 그리고 다른 모든 종류의 나쁜 에러들을 일으킬 수 있다.

> Because, obviously, breaking this rule can lead to undefined behavior, memory corruption, and all kinds of other bad errors.


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
