# react-kbone

使用 [preact](https://github.com/preactjs/preact) 多端开发(小程序和Web)，基于 [kbone](https://github.com/wechat-miniprogram/kbone) 的 element 和 render。

## 特性

* 与 taro 编译型不同，react-kbone 支持完整 JSX 语法，任意位置任意方式书写 JSX
* 使用最好的 react web 框架 preact，轻量迅速（react 不是最好的 react web 框架） 
* 一站式接入，webpack、es2018+、babel7+、jsx、hot reload、cli，你想要的都有
* 由于 3kb preact 加持，生成出的包大小超级小！！

## 一套语法多端运行

```jsx
import { h, Component } from 'preact'
import './index.css'

class Counter extends Component {
  state = { count: 1 }

  sub = () => {
    this.setState({ count: --this.state.count })
  }

  add = () => {
    this.setState({ count: ++this.state.count })
  }

  clickHandle = () => {
    if ("undefined" != typeof wx && wx.getSystemInfoSync) {
      wx.navigateTo({
        url: '../log/index?id=1'
      })
    } else {
      location.href = 'log.html'
    }
  }

  render({ }, { count }) {
    return (
      <div>
        <button onClick={this.sub}>-</button>
        <span>{count}</span>
        <button onClick={this.add}>+</button>
        <div onClick={this.clickHandle}>跳转</div>
      </div>
    )
  }
}

export default Counter
```

## 快速开始

```js
npm i omi-cli -g
omi init-mpreact my-app
cd my-app
npm start        //开发小程序
npm run web      //开发 web
npm run build    //发布 web
```

> 也支持一条命令 `npx omi-cli init-mpreact my-app` (npm v5.2.0+)

## 目录说明

```
├─ build
│  ├─ mp     //微信开发者工具指向的目录，用于生产环境
│  ├─ web    //web 编译出的文件，用于生产环境
├─ config
├─ public
├─ scripts
├─ src
│  ├─ assets
│  ├─ components    //存放所有组件
│  ├─ log.js        //入口文件，会 build 成  log.html
│  └─ index.js      //入口文件，会 build 成  index.html
```

## License

MIT 
