#redux
>redux是一个独立模块，而且也非常小，它并没有什么复杂的api，只是提供一种思想。我们写react，redux并不是必须加的，对于以展示为主、逻辑简单的大可不必使用，对于逻辑复杂，父子、兄弟之间通信频繁的，建议使用，会节省效率，而且applyMiddleWare还可以加logger，输出每次state变化的过程原因，方便我们查找问题。

####什么时候用它比较好呢：
* 某个组件的状态，需要共享
* 某个状态需要在任何地方都可以拿到
* 一个组件需要改变全局状态
* 一个组件需要改变另一个组件的状态

####Redux 的设计思想很简单
* Web 应用是一个状态机，视图与状态是一一对应的
* 所有的状态，保存在一个对象里面

解读以上两点：一个 State 对应一个 View。只要 State 相同，View 就相同。你知道 State，就知道 View 是什么样，反之亦然。State 的变化，会导致 View 的变化。但是，用户接触不到 State，只能接触到 View。所以，State 的变化必须是 View 导致的。Action 就是 View 发出的通知，表示 State 应该要发生变化了。理解了这个，对于理解下面的provider\connect有帮助。

####state
* 状态，需要什么用什么，没必要把所有state都给了一个组件

#### action
* view发出的通知，告诉store要改变的state，可以是一个对象，也可以是一个函数，如果是函数必须返回一个对象

#### store
* store.dispatch : 发出一个action，通知store
* subscribe：监听state变化
* getState: 获取当前state

#### reducer
* view dispatch 一个action后，告诉要来改变state，怎么改变呢，处理逻辑在reducer上
* Reducer 函数最重要的特征是，它是一个纯函数。也就是说，只要是同样的输入，必定得到同样的输出。
* 默认通过Object.assign

> 一般一个reducer对应state中的一个key，这样颗粒化后，操作更简单。最后可以用combineReducers来合并reducer,所以combineReducer里面的名字定义会和state对应起来，若要重命名，用as

#### 中间件 applyMiddleware
* 我们知道reducer是纯函数，不适合写逻辑，state更不用说了，那只有action了
* 中间件就是一个函数，对store.dispatch方法进行了改造，在发出 Action 和执行 Reducer 这两步之间，添加了其他功能。
* 中间件在createStore传入，createStore参数依次是reducer(必传)、inintialState(选传)、applyMiddleware(选传 )
* ##### redux-thunk
异步中间件，因为我们改变state时，可能需要一个异步的操作，比如ajax，根据返回值来改变，这时就需要它。


> ###### bindActionCreators
这个一般是在connect的参数mapDispatchToProps中使用，当你在组件中要dispatch一个action时，需要用store的dispatch，这样较多时比较麻烦，用这个方法后，会对dispatch(action1())做一个封装，你直接可以this.props.action1()调用。




-------------


# react-redux
>react-redux只是对redux的一个封装，便于react使用，它提供了provider、connect
#### connect
> 组件可以分为两类：UI 组件（presentational component）和容器组件（container component）。
* ui组件主要是展示、内部逻辑运算
* 容器组件主要用来与外部通信

connect就是来作为容器组件，它把我们自己的组件封装一层，需要向上传递state时(mapDispatchToProps)、或父级兄弟传递过来state时(mapStateToProps)，需要经过它

#### provider
* 在根组件外面包了一层，这样一来，App的所有子组件就默认都可以拿到state了。
它的原理是React组件的context属性

##### react-router-redux中间件
router改变时对应相应的state 

#### redux-actions
* createAction(s): 实际上它就是用来创建action的，自动返回一个符合redux规范的action(必须有type参数，payload是error object，会自动返回error:true)
* handleAction(s)：处理action，实际就是封装reducer的。handleAction(type, reducer, defaultState)



-----------
原先项目没有用到redux，后来发展有些属性得组件间传来传去，而且有时变化都不知道怎么变的，所以才引入redux，现已加入项目代码中，抽时间我再补个小例子。



> 相关推荐： 
> 
> 阮一峰：http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_one_basic_usages.html



> api: http://cn.redux.js.org/docs/api/bindActionCreators.html
> https://redux-actions.js.org/docs/api/handleAction.html
