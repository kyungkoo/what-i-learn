# Hello World

기본적인 동작을 확인하기 위한 `html` 템플릿은 다음과 같다.

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>Example</title>
    </head>

    <body>
        <div id="app"></div>
        <!-- react.js path 설정 -->
        <script src="react.js"></script>
        <!-- react-dom.js path 설정 -->
        <script src="react-dom.js"></script>

        <script>
            // react code
        </script>
    </body>
</html>
```

`Hello World` 를 출력하기 위해서는 위의 `// react code` 부분에 아래 코드를 입력하도록 한다.

```javascript
ReactDOM.render(
    React.DOM.h1(null, "Hello World!"),
    document.getElementById("app")
);
```
