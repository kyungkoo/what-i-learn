autoscale: true
slidenumbers: true

# 동시성 패턴

2016-09-20

---

## Case Studies

1. `Runner`

1. `Pool`

1. `Work`

---

## `Runner`

---

## Define `Runner` sturct

```go
// Runner 타입은 주어진 시간동안 일련의 작업을 수행한다.
type Runner struct {
	// 운영체제로부터 전달되는 인터럽트 신호를 수신하는 채널
	interrupt chan os.Signal
	// 처리가 종료되었음을 알리는 채널
	complete  chan error
	// 지정된 시간이 초과되었음을 알리는 채널
	timeout   <-chan time.Time
	// 인덱스 순서로 처리될 작업 목록을 저장하는 슬라이스
	tasks     []func(int)
}
```

---

## Define Errors

```go
// timeout 채널에서 값을 수신하면 ErrTimeout을 리턴한다.
var ErrTimeout = errors.New("시간을 초과했습니다.")

// 운영체제에서 인터럽트 이벤트를 수신하면 ErrInterrupt를 리턴한다.
var ErrInterrupt = errors.New("운영체제 인터럽트 신호를 수신했습니다.")
```

---

## Define `New` Function

```go
func New(d time.Duration) *Runner {
	return &Runner{
		interrupt: make(chan os.Signal, 1),
		complete:  make(chan error),
		timeout:   time.After(d),
	}
}
```

---

## Define `Add` Method

```go
// Runner 타입에 작업을 추가하는 메소드. 작업은 int형 ID를 매개변수로 전달받는다.
func (r *Runner) Add(tasks ...func(int)) {
	r.tasks = append(r.tasks, tasks...)
}
```

---

## Define `Start` Method

```go
func (r *Runner) Start() error {
	signal.Notify(r.interrupt, os.Interrupt) // 모든 종류의 인터럽트 신호룰 수신한다.

	go func() {
		r.complete <- r.run()     // 각 작업을 각기 다른 고루틴을 통해 실행한다.
	}()

	select {
	case err := <-r.complete:   // 작업 완료 신호를 수신한 경우
		return err
	case <-r.timeout:          // 작업 시간 초과 신호를 수신한 경우
		return ErrTimeout
	}
}
```

---

## Define `run` Method

```go
// 개별 작업을 실행하는 메소드
func (r *Runner) run() error {
	for id, task := range r.tasks {
		if r.gotInterrupt() { // OS 로 부터 인터럽트 신호를 수신했는지 확인
			return ErrInterrupt
		}

		task(id) // 작업을 실행
	}
	return nil
}
```

---

## Define `gotInterrupt` Method

```go
func (r *Runner) gotInterrupt() bool {
	select {
	case <-r.interrupt: // 인터럽트 이벤트가 발생하는 경우
		// 이후에 발생하는 인터럽트 신호를 더 이상 수신하지 않도록 한다.
		signal.Stop(r.interrupt)
		return true

	default:            // 작업을 계속해서 실행한다.
		return false
	}
}
```

---

## `createTask` Function

```go
func createTask() func(int) {
	return func(id int) {
		log.Printf("프로세서작업 #%d.", id)
		time.Sleep(time.Duration(id) * time.Second)
	}
}
```

---

## `main` Function

```go
const timeout = 3 * time.Second

r := runner.New(timeout)

r.Add(createTask(), createTask(), createTask())
```

---

## `main` Function

```go
if err := r.Start(); err != nil {
	switch err {
	case runner.ErrTimeout:
		log.Println("지정된 작업 시간을 초과했습니다.")
		os.Exit(1)
	case runner.ErrInterrupt:
		log.Println("운영체제 인터럽트가 발생했습니다.")
		os.Exit(2)
	}
}
```
---

## One More

---

## `error` 를 `const` 로 정의할 수는 없을까?

```go
const ErrTimeout = errors.New("시간을 초과했습니다.")
const ErrInterrupt = errors.New("운영체제 인터럽트 신호를 수신했습니다.")

```

<br />

- `const` 로 선언하면 **에러 발생**

```sh
const initializer errors.New("시간을 초과했습니다.") is not a constant
const initializer errors.New("운영체제 인터럽트 신호를 수신했습니다.") is not a constant
```

---

## Tips

1. `const` 에는 `const` 만 저장 할 수 있다.
1. `string` 은 `const` 타입이다.
1. `error` 는 `interface` 타입이다.

<br />

- **reference**
**[constant-errors](http://dave.cheney.net/2016/04/07/constant-errors)** (dave.cheney)

---

## Custom `err` package

```go
// Errors 타입 정의
type Errors string

// error interface 를 채용하기 위해 함수 선언
func (err Errors) Error() string {
	return string(err)
}
```

---

## Use `err.Errors`

```go
const (
	ErrTimeout = err.Errors("시간을 초과했습니다.")
	ErrInterrupt = err.Errors("운영체제 인터럽트 신호를 수신했습니다.")
)

switch err {
case runner.ErrTimeout:
	// do
case runner.ErrInterrupt:
	// do
}
```

---
