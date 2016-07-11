# 테스트 코드를 작성하는 방법

1. 파일명 뒤에 `_test`를 추가한다.
파일명이 `calculator.go`인 경우, 테스트 코드명은 `calculator_test.go`가 된다. `_test` 를 붙이지 않으면 테스트 파일로 인식하지 않는다.

2. 테스트 코드의 함수명은 `Example`로 시작해야 한다.
3. 결과값이 나오는 구간 밑에 `// Output:` 을 추가하고 그 밑에 예상되는 결과값을 주석으로 입력한다.

calculator.go
```golang
package calculator

fun AddInt(first, second int) {  
    return first + second
}
```

calculator_test.go
```golang
package calculator

import (
	"fmt"

	"github.com/kyungkoo/calculator"
)

func ExampleAddInt() {
	fmt.Println(calculator.AddInt(1, 2))
	// Output:
	// 3
}
```

위 코드에서는 테스트 파일명을 `calculator_test.go`로 하였고 테스트하는 함수명이 `ExampleAddInt`로 `Example`로 시작한다.
`fmt.Println()`을 사용하여 함수의 결과값을 출력하고, 그 밑에 `// Output:`과 `// 3`을 입력하여 예상되는 출력값을 명시해 놓는다.

테스트를 수행하기 위해 `Shell`에서 아래 커맨드를 입력한다.
```shell
go test calculator_test.go calculator.go
```

**참고**
- [`디스커버리 GO`](http://www.hanbit.co.kr/media/books/book_view.html?p_code=B5279497767) 3장.