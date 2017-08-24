# reack 语法的使用
### 1.HTML 模板
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Document</title>
        <script src="./build/react.js"></script>
        <script src="./build/react-dom.js"></script>
        <script src="./build/browser.min.js"></script>
    </head>
    <body>
        <div id="app"></div>
        <script type="text/babel">
            /*这是写代码*/
        </script>
    </body>
    </html>
上面代码一共用了三个库： *react.js* 、*react-dom.js* 和 *Browser.js* ，
它们必须首先加载。其中，*react.js* 是 *React* 的核心库，*react-dom.js*
是提供与 *DOM* 相关的功能，*Browser.js* 的作用是将 *JSX* 语法转为 *JavaScript* 语法，
这一步很消耗时间，实际上线的时候，应该将它放到服务器完成。
### ReactDOM.render()
    ReactDOM.render(
        <h1>hello world</h1>,
        document.getElementById('app')
    )
ReactDOM.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。

