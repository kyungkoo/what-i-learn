# `IntelliJ` 에서 `Go` 프로젝트 환경 설정 하기

<!-- ![Figure0](./img/figure0.jpg) -->

`IntelliJ` 는 plugin 을 사용하면 여러 기능을 추가할 수 있다. [`Go Plugin`](https://github.com/go-lang-plugin-org/go-lang-idea-plugin)을 사용하면 `IntelliJ` 에서도 `Go`를 사용할 수 있다.

`IntelliJ` 를 실행한 다음 우측 하단의 `Configure`->`Plugins`을 선택한다.

![Figure1](./img/figure1.jpg)


하단의 `Browse repositories...`를 선택한다.

![Figure2](./img/figure2.jpg)

입력창에 `go`를 입력하면 다음과 같이 `Go` 플러그인이 검색될 것이다 . 이를 선택하여 설치 한 다음 `IntelliJ`를 재 실행 하자.

![Figure3](./img/figure3.jpg)



![Figure4](./img/figure4.jpg)

![Figure5](./img/figure5.jpg)

![Figure6](./img/figure6.jpg)

![Figure7](./img/figure7.jpg)

![Figure8](./img/figure8.jpg)

![Figure9](./img/figure9.jpg)

![Figure10](./img/figure10.jpg)

프로젝트의 구조는 다음과 같다.

```shell
.
├── GoWithIntellij.iml
└── src
    └── MyGo
        ├── main.go
        └── vendor
            └── printer
                └── printer.go
```
