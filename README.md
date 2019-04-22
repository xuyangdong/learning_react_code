# React 源码解读
[TOC]
## React模块API
### ReactElement的定义
* ReactElement是React的一个工厂方法，返回的是一个object，这个object就是ReactElement的实例，该实例有一下几个属性（排除了__dev__模式的属性）
  * $$typeof: JS Symbols -> REACT_ELEMENT_TYPE，判断一个Object是不是ReactElement的依据就是判断Symbo.for('react.element')
  * type: 内置的html标签，React Component
  * ref:
  * props:
### React.createElement
### React.Children模块提供的方法
#### React.Children的定义
* this.props.children:没有定义具体的类型，可以是任何类型，包括：string，object，function，array

#### React.Children.forEach

* forEachChildren 别名 forEach
* 先排除this.props.children为null的场景
* 从对象池中获取一个对象用于保存遍历children的上下文以及执行的具体的遍历函数，即forEach的回调函数
  * getPooledTraverseContext:React用一个数组保存了最多10个对象，用于缓存回调函数以及上下文对象，减少对象创建的消耗
* 遍历操作
  * 如果children是undefined或者boolean类型，不调用callBack，返回0
  * 如果children是string或者number类型，调用callback，
  * 如果children是object且$$typeof是REACT_ELEMENT_TYPE/REACT_PORTAL_TYPE调用callback
  * 递归：
    * 如果Array.isArray(children)：按照数组的方式for循环去递归：深度优先
    * 如果children是可迭代对象：[Symbol.iterator]属性是一个生成器工厂，那么采用迭代器的方式去深度优先
    * 如果children是一个普通对象，不支持对象作为children类型
* 释放对象
