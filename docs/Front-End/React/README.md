# React

## UI = render(data)

## prop
***prop(property的简写)是从外部传递给组件的数据，一个React组件通过定义自己能够接受的prop就定义了自己的对外公共接口。***

当外部世界要传递一些数据给React组件，一个最直接的方式就是通过prop；同样，React组件要反馈数据给外部世界，也可以用prop，因为prop的类型不限于纯数据，也可以是函数，函数类型的prop等于让父组件交给了子组件一个回调函数，子组件在恰当的实际调用函数类型的prop，可以带上必要的参数，这样就可以反过来把信息传递给外部世界。


```js
import React, {Component} from 'react';
// 在使用JSX的范围内必须要有React
// 即使代码中并没有直接使用React
// 因为JSX最终会被转译成依赖于React的表达式
import PropTypes from 'prop-types';
// prop是组件的对外接口，使用propTypes让组件声明自己的接口规范

class Counter extends Component{
    constructor(props){
        super(props);
        
        this.onClickIncrementButton = this.onClickIncrementButton.bind(this);
        this.onClickDecrementButton = this.onClickDecrementButton.bind(this);
        // 在构造函数中给成员函数绑定了当前this的执行环境
        // 因为ES6方法创造的React组件类并不自动给我们绑定this到当前实例对象
        
        this.state = {
            count: props.initValue
        }
        // 通常在组件类构造函数的结尾处初始化state
        // 组件的state必须是一个JavaScript对象
        // 不能是string或者number这样的简单数据类型
        // 即使要存储的只是一个数字类型的数据，也只能把它存作state某个字段对应的值
    }
    
    onClickIncrementButton(){
        this.setState({count: this.state.count + 1});
    }
    onClickDecrementButton(){
        this.setState({count: this.state.count - 1});
    }
    // 改变组件state必须使用this.setState函数，不能直接修改this.state
    // 直接修改this.state的值，虽然事实上改变了组件的内部状态，但没有驱动组件进行重新渲染
    // this.setState()首先改变this.state的值，然后驱动组件经历更新过程，这样才有机会让this.state里新的值出现在界面上
    
    render(){
        const {caption} = this.props;
        // ES6的解构赋值（destructuring assignment）语法从this.props中获得了名为caption的prop值
        
        return (
            <div>
                <button style={buttonStyle} onClick={this.onClickIncrementButton}>+</button>
                <button style={buttonStyle} onClick={this.onClickDecrementButton}>-</button>
            </div>
        );
    }
}

Counter.propTypes = {
    caption: PropTypes.string.isReauired,
    initValue: PropTypes.number
};
// 这不只是声明，而且是一种限制
// 在运行时和静态代码检查时，都可以根据propTypes判断外部世界是否正确地使用了组件的属性
// propTypes检查只是一个辅助开发的功能，并不会改变组件的行为
// 没有propTypes定义，组件依然能够正常工作
// 即使在上面propTypes检查出错的情况下，组件依旧能工作

// 定义类的propTypes要占用一些代码空间
// propTypes检查要消耗CPU计算资源
// 在产品环境下做propTypes检查在最终用户的浏览器Console中输出错误信息没什么意义
// 所以最好的方式是，开发者在代码中定义propTypes，避免在开发过程中犯错，但在发布产品代码时，去掉propTypes，这样最终部署到产品环境的代码就会更优
// babel-react-optimize具有这个功能，但应该确保只在发布产品代码时使用它

Counter.defaultProps = {
    initValue: 0
};
// propTypes声明中initValue没有用isRequired要求必须有值
// 我们需要在代码中判断所给initValue值是否存在，如果不存在就给一个默认的初始值
// this.state = {
//     count: props.initValue || 0
// }
// 这样的判断逻辑充斥在我们组件的构造函数中并不美观且容易遗漏
// 可以用React的defaultProps功能让代码更加易懂

export default Counter;
```
***给this.props赋值是React.Component构造函数的工作之一***

如果一个组件需要定义自己的构造函数，一定要记得在构造函数的第一行通过super调用父类也就是React.Component的构造函数。如果在构造函数中没有调用super(props)，那么组件实例被构造之后，类实例的所有成员函数就无法通过this.props访问到父组件传递过来的props值。

## state
***state代表组件的内部状态。由于React组件不能修改传入的prop，所以需要记录自身数据变化，就要使用state。***

## prop与state的对比
* prop定义外部接口，state记录内部状态；
* prop的赋值在外部世界使用组件时，state的赋值在组件内部；
* 组件不应该改变prop的值，而state存在的目的就是让组件来改变的。

## 组件的生命周期
* **装载过程（Mount）**，组件第一次在DOM树中渲染的过程
    * constructor
        * 并不是每个组件都需要定义自己的构造函数
        * 无状态的React组件往往不需要定义构造函数
        * 一个React组件需要构造函数，往往是为了下面的目的：
            1. 初始化state
            2. 绑定成员函数的this环境
    * ~~getlnitialState~~
    * ~~getDefaultProps~~
        ```js
        const Sample = React.createClass({
            getInitialState: function(){
                return {foo: 'bar'};
            },
            getDefaultProps: function(){
                return {sampleProp: 0};
            }
        });
        ```
        > getlnitialState的返回值用来初始化组件的this.state，getDefaultProps的返回值可以作为props的初始值。
        
        > 这两个函数只在React.createClass方法创造的组件类中才会用到，在ES6的方法定义的React组件中根本不会用到。
        
        > React.createClass已经被Facebook官方逐渐废弃，强烈建议不再要使用React.createClass。
        
        > getlnitialState只出现在装载过程中，在一个组件的整个生命周期过程中只被调用一次，不要在里面放置预期会被多次执行的代码。

    * componentWillMount
        * 通常不用定义componentWillMount函数
        > componentWilJMount发生在“将要装载”时，这个时候没有任何渲染出来的结果，即使调用this.setState修改状态也不会引发重新绘制。
        
        > 换句话说，所有可以在componentWillMount 中做的事情，都可以提前到constructor中做，可以认为这个函数存在的主要目的就是为了和componentDidMount对称。
        
    * render
        * render函数是React组件中最重要的函数
        > 一个React组件可以忽略其他所有函数都不实现，但是一定要实现 render 函数，因为所有 React 组件的父类 React.Component类对除render之外的生命周期函数都有默认实现。
        
        * render函数并不做实际的谊染动作
        > 它只返回一个JSX描述的结构，最终由React来操作渲染过程。
        
        * 组件在某些情况下选择没有东西可画
        > 那就让render函数返回一个null或者false，等于告诉React，这个组件这次不需要渲染任何DOM元素。
        
    * componentDidMount
        * render函数被调用完之后，componentDidMount函数并不是会被立刻调用。
        > componentDidMount被调用的时候，render函数返回的东西已经引发了渲染，组件已经被“装载”到了DOM树上。
        
        ```nohighlight
        enter constructor: First
        enter componentWillMount First
        enter render First
        enter constructor: Second
        enter componentWillMount Second
        enter render Second
        enter constructor: Third
        enter componentWillMount Third
        enter render Third
        enter componentDidMount First
        enter componentDidMount Second
        enter componentDidMount Third
        ```
        > 之所以会有上面的现象，是因为render函数本身并不往DOM树上渲染或者装载内容，它只是返回一个JSX表示的对象，然后由React库来根据返回对象决定如何渲染。
        
        > 而React库肯定是要把所有组件返回的结果综合起来，才能知道该如何产生对应的DOM修改。所以，只有React库调用所有组件的render函数之后，才有可能完成装载，这时候才会依次调用各个组件的componentDidMount函数作为装载过程的收尾。
        
        * componentWillMount可以在服务器端被调用，也可以在浏览器端被调用；而componentDidMount只能在浏览器端被调用，在服务器端使用React的时候不会被调用。

        * componentDidMount被调用的时候，组件已经被装载到DOM树上了，可以放心获取渲染出来的任何DOM。
* **更新过程（Update）**，当组件被重新渲染的过程
    > 组件被装载到DOM树上之后，用户在网页上可以看到组件的第一印象，但是要提供更好的交互体验，就要让该组件可以随着用户操作改变展现的内容，当props或者state被修改的时候，会引发组件的更新过程。

    * componentWillReceiveProps(nextProps)
        * 只要父组件的render函数被调用，在render函数里面被渲染的子组件就会经历更新过程，不管父组件传给子组件的props有没有改变，都会触发子组件的componentWillReceiveProps函数。

        * componentWillReceiveProps(nextProps)把传入的参数nextProps和this.props作对比。nextProps是这一次渲染传入的props值，this.props是上一次渲染时的props值，只有两者有变化时才会调用this.setState更新state。

        * 通过this.setState触发的更新过程不会调用该函数。
        > 因为componentWillReceiveProps(nextProps)根据nextProps计算是否通过this.setState更新state，如果this.setState导致componentWillReceiveProps(nextProps)再次被调用，那就形成了死循环。

    > this.forceUpdate()，每个React组件都可以通过forceUpdate函数强行引发一次重新绘制。

    * shouldComponentUpdate(nextProps, nextState)
        * render函数决定了该渲染什么，shouldComponentUpdate函数决定了一个组件什么时候不需要渲染。

        * render和shouldComponentUpdate，也是React生命周期函数中仅有的两个要有返回结果的函数。
        > render函数的返回结果用于构造DOM对象，shouldComponentUpdate函数返回一个布尔值，告诉React库这个组件在这次更新过程中是否要继续。

        * 通过this.setState函数引发更新过程，并不是立刻更新组件的state值。
        > 在执行到函数shouldComponentUpdate时，this.state依然是this.setState函数执行之前的值，所以我们要做的实际上就是在nextProps、nextState、this.props和this.state中互相比对。

    * componentWillUpdate
    > 如果组件的shouldComponentUpdate函数返回true，React就会依次调用对应组件的componentWillUpdate、render和componentDidUpdate函数。

    * render
    * componentDidUpdate
        * 无论更新过程发生在服务器端还是浏览器端，componentDidUpdate函数都会被调用。
        > 和装载过程的componentDidMount函数不同，componentDidUpdate函数并不是只在浏览器端才执行。

        > 在介绍componentDidMount函数时，我们说到可以利用componentDidMount函数执行其他UI库的代码，如jQuery代码。当React组件被更新时，原有的内容被重新绘制，这时候就需要在componentDidUpdate函数中再次调用jQuery代码。

        > 使用React做服务器端渲染时，基本不会经历更新过程，因为服务器端只需要产出HTML字符串，一个装载过程就足够产出HTML了，所以正常情况下服务器端不会调用componentDidUpdate函数，如果调用了，说明我们的程序有错误，需要改进。

* **卸载过程（Unmount）**，组件从DOM中删除的过程
    > React组件的卸载过程只涉及一个函数componentWillUnmount，当React组件要从DOM树上删除掉之前，对应的componentWillUnmount函数会被调用，所以这个函数适合做一些清理性的工作。

    * componentWillUnmount
        * componentWillUnmount中的工作往往和componentDidMount有关。
        > 在componentDidMount中用非React的方法创造的一些DOM元素，如果撒手不管可能会造成内存泄露，那就需要在componentWillUnmount中把这些创造的DOM元素清理掉。

## 组件通过prop向外传递数据
* 父组件通过prop传递数据给子组件
* 组件的prop可以是任何JavaScript对象
> 函数可以被看做一种对象，既可以像其他对象一样作为prop的值从父组件传递给子组件，又可以被子组件作为函数调用。

```js
import React, { Component, PropTypes } from 'react';

class Counter extends Component {
    ...
}

Counter.propTypes = {
    caption: PropTypes.string.isRequired,
    initValue: PropTypes.number,
    onUpdate: PropTypes.func
    // React虽然有PropType能够检查prop的类型
    // 但没有任何机制来限制prop的参数规格
    // 参数的一致性只能靠开发者来保证
};

Counter.defaultProps = {
    initValue: 0,
    onUpdate: f => f //什么都不做的函数
};

export default Counter;
```

## React组件state和prop的局限
* 使用state存储状态的缺点：数据的冗余和重复

    子组件和父组件的数据可能发生重复

    ![组件状态不一致](../../images/react_state_1.png)
    > 数据如果出现重复，带来的一个问题就是如何保证重复数据一致，如果数据存多份而且不一致，那就很难决定到底使用哪个数据作为正确结果了。
* 利用prop在组件之间传递信息也会遇到问题

    ![组件状态不一致](../../images/react_prop_1.png)
    > 在一个包含三级或者三级以上组件结构应用中，顶层的祖父级组件想要传递一个数据给最低层的子组件，如果用prop的方式，就只能通过父组件中转。也许中间那一层父组件根本用不上这个prop，但是依然需要支持这个prop，扮演好搬运工的角色，只因为子组件用得上，这明显违反了低耦合的设计要求。


## 列表 & Keys

Keys 帮助 React 识别哪些元素改变了，比如被添加或删除。因此你应当给数组中的每一个元素赋予一个确定的标识。

## 事件系统

Virtual DOM 在内存中以对象的形式存在，在这些对象上添加事件非常简单。

React 基于 Virtual DOM 实现了一个 SyntheticEvent （合成事件）层，我们所定义的事件处理器会接收到一个 SyntheticEvent 对象的实例，它完全符合 W3C 标准，不存在任何 IE 上的兼容问题，且与原生的浏览器事件一样拥有同样的接口，同样支持事件的冒泡机制，可以使用 stopPropagation() 和 preventDefault() 来中断它。

所有事件都自动绑定到最外层上。如果需要访问原生事件对象，可以使用 nativeEvent 属性。

