# React/JSX 编码规范

## Component: stateless > Class > React.createClass

- 优先考虑使用stateless创建可复用组件

```javascript
  function Hello({hello}) {
    return <div>{hello}</div>
  }
  export default Hello
```

- 组件拥有内部的 state 或 refs 时,使用class.注意:内部方法需要绑定this

```javascript
  class Hello extends React.Component {
    constructor(props) {
      super(props)
      this.state = {
        // initialState
      }
      this.handleOnChange = this.handleOnChange.bind(this)
    }

    handleOnChange() {
      console.log(this.refs.username)
    }

    render() {
      return (
        <input type="text" ref="username" onChange={this.handleOnChange} />
      )
    }
  }
```

## 命名

- 引用命名: React组件使用大驼峰命名, 引用实例采用驼峰命名

```javascript
  import HelloWorld from './HelloWorld'

  const helloWorld = <HelloWorld />
```

- 文件命名: 如果在components根目录, 则文件名与组件名相同. 如果文件在单独目录, 则文件名为index.js, 目录名与组件名相同

## 对齐

- 组件属性对齐规范

```javascript
  // 如果组件的属性不多, 则写在一行
  <Foo bar="bar" />

  // 多行属性采用缩进
  <Foo
    bar="bar"
    baz="baz"
  />
```

## 引号

- JSX标签属性使用双引号, js的string还是用单引号

```javascript
  <Foo bar="bar" />

  <Foo style={{backgroundColor: '#eee'}} />
```

## 属性

- 属性使用驼峰命名

```javascript
  <Foo userName="hello" />
```

- 当属性值等于`true`的时候, 省略该属性的赋值

```javascript
  <Foo hidden />
```

## 括号

- 用括号包裹多行JSX标签

```javascript
  render() {
    return (
      <MyComponent className="container">
        <MyChild />
      </MyComponent>
    )
  }
```

## 方法

- 不要在render方法中bind(this), 应该在constructor中绑定. 因为render会执行很多次

- 组件的内部方法不需要使用`_`前缀. 因为都是内部方法...
