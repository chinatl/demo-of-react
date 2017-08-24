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
### 2.ReactDOM.render()
    ReactDOM.render(
        <h1>hello world</h1>,
        document.getElementById('app')
    )
ReactDOM.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。
### 3.JSX语法
    var arr = ['张三', '李四']
        ReactDOM.render(
            <div>
                { arr.map(function(v,i){
                    return <div key={i}>hello,{v}</div>
                })}
            </div> ,
            document.getElementById('app')
        )
上面代码体现了 JSX 的基本语法规则：遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析   
#### 注意: 如果返回多个html结构,必须要给标签家key值,否则会报错.
