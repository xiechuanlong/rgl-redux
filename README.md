# Regular Redux
一个微型模块用于 [Regular](http://regularjs.github.io) 组件实现[Redux](http://redux.js.org).

[![build status](https://img.shields.io/travis/regularjs/rgl-redux/develop.svg?style=flat-square)](https://travis-ci.org/regularjs/rgl-redux) [![npm version](https://img.shields.io/npm/v/rgl-redux.svg?style=flat-square)](https://www.npmjs.com/package/rgl-redux)

```sh
npm install rgl-redux
```

## 运行要求
* regularjs 0.6.0-beta.1以上版本
* webpack+babel 用于构建基于ES6语法的应用

## 用法
`module/App.js`:
```js
import 'rgl-redux';
import './module/MyApp';
import { reducer } from './reducers'
import { createStore } from 'redux';

const AppContainer = Regular.extend({
  template: `
  <StoreProvider store={store}>
    <MyApp />
  </StoreProvider>
  `,
  config(data) {
    data.store = createStore(reducer);
  },
});
```

`components/MyComp.js`:
```js
import { connect } from 'rgl-redux';
import { changeFoo } from './actions';

const MyComp = Regular.extend({
  name: 'MyComp',
  template: '<div>{foo}</div><button on-click={this.onClick()}>Click Me!</button>',
  onClick() {
    this.$dispatch(changeFoo('bar'));
  }
});

export default connect({
  mapState(state) {
    return {
      foo: state.foo,
    };
  },
  dispatch: true,
})(MyComp);

```
## 示例项目
示例项目位于 `examples` 目录，克隆项目后，运行 `npm run example`
* [TodoApp 示例](examples/Todo)

## 文档

[https://regularjs.github.io/rgl-redux/](https://regularjs.github.io/rgl-redux/src/start.html)

## 路线图
### v0.2.0
* broadcast event: StoreProvider内的广播事件支持
* Complicated example: 更完整复杂的示例
* ActionMap: 一种简洁的方式实现dispatch -> action的映射


## License
MIT