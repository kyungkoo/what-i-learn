# Chapter4

## 배열 - 슬라이스 - 맵

---

## 배열 (Array)

- 동일한 타입이고
- 순차적이며
- 크기가 정해져 있다

---

## 배열 선언

```go
// int 형 배열 선언
var intArr [3]int

// 각 인덱스에 값 추가
intArr[0] = 1
intArr[1] = 2
intArr[2] = 3
```

---

## 배열 선언 및 초기화

선언과 동시에 각 배열을 초기화 할 수 있다.
또한 초기화 하는 숫자에 배열 크기를 정의 하도록 할 수 있다.

```go
compile_langs := [2]string{"Go", "C"}

repl_langs := [...]string{"Scala", "Kotlin", "Swift"}
```

---

## 배열의 부분 초기화

배열은 선언 시 해당 타입으로 초기화 된다.
부분 초기화를 하게되면 선언하지 않은 부분은 기본값으로 초기화 된다.

```go
languages := [3]string{0:"Java", 2:"Python"}
// languages[0] => Java
// languages[1] => ""(빈 문자열)
// languages[2] => Python
```

---

## 슬라이스 (Slice)

- 배열이 가지고 있는 기능은 기본적으로 제공한다.
- 배열과는 달리 동적으로 크기를 조절할 수 있다.
- 내부적으로는 배열의 포인터를 참조하고 있기 때문에 배열이 가지고 있는 문제에 대한 해결책이 될 수 있다.

---

## 슬라이스 소스 코드

[src/runtime/slice.go](https://golang.org/src/runtime/slice.go)

```go
type slice struct {
    array unsafe.Pointer
    len   int
    cap   int
}
```

슬라이스 소스코드를 살펴보면, 내부적으로 `array`의 포인터를 참조하고 있음을 짐작 할 수 있다.

---

## 슬라이스 정의

배열과는 달리 `[]`

```go

```
