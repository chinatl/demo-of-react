# reack 语法的使用
### 1. HTML 模板
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
### 2. ReactDOM.render()
    ReactDOM.render(
        <h1>hello world</h1>,
        document.getElementById('app')
    )
ReactDOM.render 是 React 的最基本方法，用于将模板转为 HTML 语言，并插入指定的 DOM 节点。
### 3. JSX语法
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
#### 注意: 如果返回多个html结构,必须要给标签加key值,否则会报错.
### 4. 组件
     var Hello = React.createClass({
        render:function(){
            return <h1>hello {this.props.title}</h1>   
        }
    })
    ReactDOM.render(
        <Hello title='world'/>
     , document.getElementById('app')
    )
组件的用法与原生的 HTML 标签完全一致，可以任意加入属性，比如 hello 组件 ，就是 Hello 组件加入一个 title 属性，值为 world。组件的属性可以在组件类的 this.props 对象上获取.
#### 注意: 组件类的第一个字母要大写,否则会报错, 组件里面必须有个根标签, 添加组件属性，有一个地方需要注意，就是 class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。
### 5. this.props.children
     var NodeList = React.createClass({
        render:function(){
            return (
                <ol>
                    {React.Children.map(this.props.children,function(v){
                        return <lli>{v}</lli>
                    })}                        
                </ol>
            )
        }
    });
    ReactDOM.render(
        <NodeList>
            <span>hello</span>
            <span>world</span>
        </NodeList>,
        document.getElementById('app')
    )
this.props.children 属性。它表示组件的所有子节点
### 6. PropTypes的使用
    var Hello = React.createClass({
        render:function(){
            return (
                <h1>hello {this.props.title}</h1>  
            )
        },
        propTypes:{
            title:React.PropTypes.string.isRequired
        },
        getDefaultProps:function(){
            return {
                title: 'world'
            }
        }
    })
    ReactDOM.render(
        <Hello/>
        ,document.getElementById('app')
    )
组件类的PropTypes属性，就是用来验证组件实例的属性是否符合要求, 此外，getDefaultProps 方法可以用来设置组件属性的默认值。
### 7. 获取真实的dom节点
    var Hello = React.createClass({
        handleClick:function(){
            this.refs.myInput.focus();
            console.log(1)
        },
        render:function(){
            return (
             <div>
                    <input type='text' ref='myInput'/>   
                    <input type='button' value='点击' onClick={this.handleClick}/> 
             </div>  
            )
        },


    })
    ReactDOM.render(
        <Hello/>
        ,document.getElementById('app')
    )
通过ref获取dom节点,
#### 注意: onClick 事件中 click要大写
### this.state的使用
    var Hello = React.createClass({
        getInitialState:function(){
            return {
                title:'hello world'
            }
        },
        render:function(){
            return (
                <div>
                    <h1>{this.state.title}</h1>
                    <input type="button" onClick={this.handleClick} value='点击改变'/>
                </div>
            )
        },
        handleClick:function(){
            this.setState({
                title:'hello chinatl'
            })
        }
    })
    ReactDOM.render(
        <Hello/>
        ,document.getElementById('app')
    )
#### getInitialState 可以设置state的初始值 , 通过setState 来设置this.state 

### 生命周期 Mounting: 已插入真实DOM Updating 正在被重新渲染 Unmounting 已移出真实DOM

    
    