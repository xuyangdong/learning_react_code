# React 源码解读
<!-- TOC -->
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
* forEachChildren -> forEach
