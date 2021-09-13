# 浅析MVC

MVC模式（Model–view–controller）是软件工程中的一种软件架构模式，把软件系统分为三个基本部分：模型（Model）、视图（View）和控制器（Controller）。

## MVC三个对象

* 模型（Model） - 用于封装与应用程序的业务逻辑相关的数据以及对数据的处理方法，会有一个或多个视图监听此模型。一旦模型的数据发生变化，模型将通知有关的视图。
```javascript
Model层
Model = {
    data:{需要用到的数据}，
    create()：{增数据}，
    delete()：{删数据}，
    update(): {更新数据}，
    get(): {获取数据}
}
```
* 视图（View） - 是它在屏幕上的表示，描绘的是model的当前状态。当模型的数据发生变化，视图相应地得到刷新自己的机会。
```javascript
View层
View = {
    el:null,
    html:`内容`
    init(){初始化页面}
    render(){刷新页面}
}
```
* 其它（Controller）- 定义用户界面对用户输入的响应方式，起到不同层面间的组织作用，用于控制应用程序的流程，它处理用户的行为和数据model上的改变。
```javascript
const c = {
  init(container) {
        v.init()//初始化View
        v.render()//第一次渲染页面
        c.autoBindEvents()//自动的事件绑定
        eventBus.on('m:update',()=>{v.render()}//当enentsBus触发'm:update'是View刷新
    },
  events: {事件 },   //事件以哈希表的方式记录存储
  add() {具体实现},
  minus() {具体实现},
  mul() {具体实现},
  div() {具体实现},
  autoBindEvents() {自动绑定事件}
}
```

## EventBus

EventBus是消息传递的一种方式，基于一个消息中心，订阅和发布消息的模式。

### API
* on : 监听事件
* trigger(emit) : 触发事件
* off：取消监听
```javascript
//订阅消息
class EventBus {
    constructor() {
        this._eventBus = $(window)
    }
    on(eventName, fn) {
        return this._eventBus.on(eventName, fn)
    }
    trigger(eventName, data) {
        return this._trigger.trigger(eventName, data)
    }
    off(eventName, fn) {
        return this._eventBus.off(eventName, fn)
    }
}
```

## 表驱动编程

表驱动法就是一种编程模式，从表里面查找信息而不使用逻辑语句。事实上，凡是能通过逻辑语句来选择的食物，都可以通过查找表来选择。对简单的情况而言，使用逻辑语句更为容易和直白，但随着逻辑链的越来越复杂，查表法也愈发显得更具有吸引力。

### 优点

> 1.提高了程序的可读性。一个消息如何处理,只要看一下驱动表就知道,非常明显。
> 2.减少了重复代码。这种方法的代码量肯定比第一种少。为什么?因为它把一些重复的东西...
> 3.增强可扩展性，更容易修改
> 4.降低复杂度，通过把程序逻辑的复杂度转移到人类更容易处理的数据中来，从而方便操作
> 5.主干清晰

## 模块化

模块化是一种处理复杂系统分解为更好的可管理模块的方式。每个模块完成一个特定的子功能，所有的模块按某种方法组装起来，成为一个整体，完成整个系统所要求的功能。

模块具有以下几种基本属性：接口、功能、逻辑、状态，功能、状态与接口反映模块的外部特性，逻辑反映它的内部特性。

### 优势

> 1.避免命名冲突（减少命名空间污染）
> 2.灵活架构，焦点分离，方便模块间组合、分解
> 3.多人协作互不干扰
> 4.高复用性和可维护性