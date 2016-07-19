autoscale: true
slidenumbers: true

# Go 언어 포인터

2016-07-19

---

## 포인터 변수 선언

1. 타입 앞에 `*`을 추가하여 포인터 변수로 선언
1. `new`를 사용하여 포인터 변수를 초기화
1. 선언과 초기화를 동시에...

```go
var ptrInt *int
ptrInt = new(int)

var ptrStr *string = new(string)
ptrFloat := new(float64) // := 를 이용하여 초기화 가능
```

---

## 포인터 변수 접근

1. 포인터 변수는 해당 포인터의 주소값을 갖는다.
1. 포인터 변수의 값에 접근하기 위해서는 변수명 앞에 `*`를 붙여 접근한다.

```go
var ptrInt *int = new(int)
fmt.Println(*ptrInt) // 0
// *를 사용하여 포인터 변수의 값에 접근한다.
*ptrInt = 20
fmt.Println(*ptrInt) // 20
```

---

## 포인터 주소값 접근

1. 포인터 변수는 해당 포인터의 주소를 가지고 있다.
2. 일반 변수의 경우에는 `&`를 사용하여 해당 변수의 주소값에 접근할 수 있다.

```go

intVal := 20
ptrInt := &intVal
// 동일한 주소값을 갖는다.
fmt.Println(&intVal) // 0xc8200701c0
fmt.Println(ptrInt)  // 0xc8200701c0

```

---

## 함수 매개변수로 기본 값 전달

`Value Type` 변수는 함수 내부에서 변경해도 외부에 영향을 미치지 못한다.

```go
func changeValueTypeToTwo(number int) {
	number = 2
}

num := 20
fmt.Println(num) 					// 20
changeIntValueToTwo(number)
fmt.Println(num) 					// 20
```

---

## 함수 매개변수로 포인터 전달

포인터 인자를 전달하게 되면 함수 내부에서 변경한 값이 외부 변수에도 영향을 미친다.

```go
func changePointerTypeToTwo(number *int) {
	*number = 2
}

num := 20
fmt.Println(&num) 					// 20
changeIntValueToTwo(number)
fmt.Println(num) 					// 2
```

---

## 포인터 연산

Go 언어 에서는 포인터 연산이 불가능 하다.

```go
var ptrInt *int = new(int)
ptrInt++

// invalid operation: ptrInt++ (non-numeric type *int)
```
