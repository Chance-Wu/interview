#### 1. 用法

---

> - `setInterval(code,millisec[,"lang"])` 方法可**按照指定的周期（以毫秒计）来调用函数或计算表达式**。
>
> - 会不停地调用函数，直到`clearInterval()`被调用或窗口被关闭。
>
> - 由 `setInterval()` 返回的 ID 值可用作 `clearInterval()` 方法的参数。
>
> ```jsx
> <!DOCTYPE html>
> <html lang="en">
>     <head>
>         <meta charset="UTF-8" />
>         <meta http-equiv="X-UA-Compatible" content="IE=edge" />
>         <meta name="viewport" content="width=device-width, initial-scale=1.0" />
>         <script src="https://cdn.staticfile.org/react/16.4.0/umd/react.development.js"></script>
>         <script src="https://cdn.staticfile.org/react-dom/16.4.0/umd/react-dom.development.js"></script>
>         <!-- 生产环境中不建议使用 -->
>         <script src="https://cdn.staticfile.org/babel-standalone/6.26.0/babel.min.js"></script>
>         <title>Document</title>
>     </head>
> 
>     <body>
>         <div id="root"></div>
>         <button onclick="stop()">停止时间</button>
> 
>         <script type="text/babel">
>             function tick() {
>                 const element = (
>                     <div>
>                         <h1>Hello, world!</h1>
>                         <h1>It is {new Date().toLocaleTimeString()}.</h1>
>                     </div>
>                 );
>                 ReactDOM.render(element,document.getElementById('root'));
>             }
> 
>             var id = setInterval(tick,1000);
> 
>             function stop() {
>                 clearInterval(id);
>             }
>         </script>
>     </body>
> </html>
> 
> ```



#### 2. 注意事项

---

>在动态加载页面中，一定要清理循环定时器。有时候重复设置定时器，严重的时候会导致内存泄漏，最终页面崩溃。



#### 3. 回调

---

>回调函数中会包含一些变量或者DOM元素，需要更加小心谨慎，考虑这些元素的释放。



#### 4. 存储方案

---

>（1）放在全局变量中，用之前判断，防止重复。
>
>```jsx
>var interval = null;//计时器
>var i = 0;
>function start(){//启动计时器函数
>  if(interval!=null){//判断计时器是否为空
>    clearInterval(interval);
>    interval=null;
>  }
>  interval = setInterval(overs,1000);//启动计时器，调用overs函数，
>}
>function overs(){
>  i++;
>  console.log(i); 
>}
>
>function stop(){        
>  clearInterval(interval);
>  interval = null;
>}
>```
>
>（2）暂存jquery变量中
>
>```jsx













