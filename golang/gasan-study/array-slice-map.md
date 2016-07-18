# Chapter4

## 배열 - 슬라이스 - 맵

---

## 배열 (Array)

- 동일한 타입이고
- 순차적이며
- 크기가 정해져 있다

---

## 배열 선언

```golang
// int 형 배열 선언
var intArr [3]int

// 각 인덱스에 값 추가
intArr[0] = 1
intArr[1] = 2
intArr[2] = 3
```

---

## 배열 선언 및 초기화

```golang
// 선언과 동시에 각 배열을 초기화 할 수 있다.
compile_languages := [2]string{"Go", "C"}

// 또는 초기화 하는 숫자에 배열 크기를 정의하도록 할 수 있다.
repl_languages := []string{"Scala", "Kotlin", "Swift"}
```

---
