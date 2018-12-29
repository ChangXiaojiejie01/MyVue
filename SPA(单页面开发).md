

#### 认识SPA

##### SPA（Single Page Application） 单页面应用程序

​          概念： 一个web应用中只有一个页面组成

​          也就是说：将原来由多个页面配合完成的功能，现在使用一个页面来实现

##### MPA多页面应用程序（MPA Multiple Page Application）

​          概念： 一个web应用中有多个页面组成

##### 为什么要使用SPA？

​          1 加载内容更少，因为一些相同的页面部分（头部、侧边栏等）不需要重复加载

​          2 用户体验更好，可以通过 loading 效果，来告诉用户数据加载中

​          3 减少服务器压力，因为加载内容少了，服务器需要处理的内容少了，压力就小了

##### SPA的劣势？

 也就是 ajax 的劣势，是不利于： SEO（搜索引擎优化 百度）

​          服务端渲染

#### 如何使用SPA

##### 使用的技术点

​	1.ajax 使用ajax异步发送请求

​	2.哈希值 根据hash值来使用不同的功能

​	3.hashchange事件 当前hash值发生改变后，就会执行对应的处理函数

实现的思路：

​	1.在html页面中准备标签元素，并且设置href属性

​	2.使用axios发送请求，利用switch实现路由的功能

​	3.switch的判断值为location.hash，并将该过程封装成一个函数fn

​	4.给window注册hashchange事件，调用函数fn

```js
//html
  <div id="app">
    <ul>
      <li><a href="#/my">我的</a></li>
      <li><a href="#/find">发现</a></li>
      <li><a href="#/friend">朋友</a></li>
    </ul>
    <div class="text"></div>
  </div>

//js
let text = document.querySelector('.text');

let fn = ()=>{
    //判断location.hash的值
    switch (location.hash) {
        case "#/my":
            console.log('my');

            axios.get('./my.json').then(res=>{
                text.innerHTML=res.data.content
            });
            break;
        case "#/find":
            console.log('mfindy');

            axios.get('./find.json').then(res=>{
                text.innerHTML=res.data.content
            });
            break;
        case "#/friend":
            console.log('friend');

            axios.get('./friend.json').then(res=>{
                console.log(res.data.content);

                text.innerHTML=res.data.content
            });
            break;
        default:
            break;
    }
}
//初始化，刚进入页面调用一次
fn()
window.addEventListener('hashchange',fn);
```





