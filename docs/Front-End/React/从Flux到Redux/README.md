# 从Flux到Redux

* [Flux](#flux)
    * [创建一个Flux应用](#创建一个flux应用-▲)
    * [Flux的优势](#flux的优势-▲)
    * [Flux的不足](#flux的不足-▲)
* [Redux](#redux)


# <p align="center">Flux</p>

###### [<p align="right">back to top ▲</p>](#从flux到redux)
在MVC( Model-View-Controller）的世界里，React相当于V（也就是View）的部分，只涉及页面的渲染，一旦涉及应用的数据管理部分，还是交给Model和Controller。

MVC框架提出的数据流很理想，用户请求先到达Controller，由Controller调用Model获得数据，然后把数据交给View，**但是，在实际框架实现中，总是允许View和Model可以直接通信**：

![MVC的缺点](../../../images/flux_mvc_1.png)

* 服务器端MVC框架往往就是每个请求就只在Controller-Model-View三者之间走一圈，结果就返回给浏览器去渲染或者其他处理了，然后这个请求生命周期的Controller-Model-View就可以回收销毁了，这是一个严格意义的单向数据流；
* 对于浏览器端MVC框架，存在用户的交互处理，界面渲染出来之后，Model和View依然存在于浏览器中，这时候就会诱惑开发者为了简便，让现存的Model和View直接对话。

> 对于MVC框架，为了让数据流可控，Controller应该是中心，当View要传递消息给Model时，应该调用Controller的方法，同样，当Model要更新View时，也应该通过Controller引发新的渲染。

### **Flux的特点：更严格的数据流控制。**

![Flux的单向数据流](../../../images/flux_1.png)

__一个Flux应用包含四个部分：__
* __Dispatcher (MVC-Controller)__，处理动作分发，维持Store之间的依赖关系；
* __Store (MVC-Model)__，负责存储数据和处理数据相关逻辑；
* __Action (对应给MVC框架的用户请求)__，驱动Dispatcher的JavaScript对象；
* __View (MVC-View)__，视图部分，负责显示用户界面。

> 当需要扩充应用所能处理的“请求”时，MVC方法需要增加新的Controller，而Flux则是增加新的Action。


## 创建一个Flux应用 [▲](#从flux到redux)
**1、Dispatcher**
```js
// src/AppDispatcher.js
import {Dispatcher} from 'flux';
export default new Dispatcher();
// Dispatcher存在的作用是用来派发action
```
**2、action**
> action代表一个“动作”，是一个普通的JavaScript对象，代表一个动作的纯数据。action对象不自带方法，就是纯粹的数据。

```js
// 定义action通常需要两个文件，
// ActionTypes定义action的类型，
// Actions定义action的构造函数（也称为action Creator）。

// 分成两个文件的主要原因是在Store中会根据action类型做不同操作，
// 也就有单独导入action类型的需要。

// src/ActionTypes.js
export const INCREMENT = 'increment';
export const DECREMENT = 'decrement';

// src/Actions.js
// 出于业界习惯，这个文件被命名为Actions.js，
// 但是里面定义的并不是action对象本身，
// 而是能够产生并派发action对象的函数。
import * as ActionTypes from './ActionTypes.js';
import AppDispatcher from './AppDispatcher.js';

export const increment = (counterCaption) => {
    AppDispatcher.dispatch({
        // action对象必须有一个字符串类型的type字段，代表这个action对象的类型。
        type: ActionTypes.INCREMENT,
        counterCaption: counterCaption
    });
};

export const decrement = (counterCaption) => {
    AppDispatcher.dispatch({
        type: ActionTypes.DECREMENT,
        counterCaption: counterCaption
    });
};
// Actions.js导出两个action构造函数increment和decrement，
// 当这两个函数被调用的时候，创造了对应的action对象，
// 并立即通过AppDispatcher.dispatch函数派发出去。
```

**3、Store**
> Store是一个对象，存储应用状态，同时还要接受Dispatcher派发的动作，根据动作来决定是否要更新应用状态。

```js
// src/stores/CounterStore.js
import AppDispatcher from '../AppDispatcher.js';
import * as ActionTypes from '../ActionTypes.js';
import {EventEmitter} from 'events';

const CHANGE_EVENT = 'changed';

const counterValues = {
    'First': 0,
    'Second': 10,
    'Third': 30
};

// 当Store的状态发生变化的时候，需要通知应用的其他部分（View）做必要的响应。
// 应该用消息的方式建立Store和View的联系。
// 因此我们让CounterStore扩展了EventEmitter.prototype，
// 等于让CounterStore成了EventEmitter对象。
// 一个EventEmitter实例对象支持下列相关函数：
// 1.emit(事件名称)，广播一个特定事件；
// 2.on(事件名称, 处理函数)，增加一个挂在这个EventEmitter对象特定事件上的处理函数；
// 3.removeListener(事件名称, 处理函数)，和on相反，
// 删除挂在这个EventEmitter对象特定事件上的处理函数。

// CounterStore对象的emitChange、addChangeListener和removeChangeListener函数，
// 就是利用EventEmitter上述的三个函数完成对CounterStore状态更新的广播、添加监听函数和删除监听函数等操作。
const CounterStore = Object.assign({}, EventEmitter.prototype, {
    // CounterStore还提供一个getCounterValues函数，
    // 用于让应用中其他模块可以读取当前的计数值，
    // 当前的计数值存储在文件模块级的变量counterValues中。
    getCounterValues: function(){
        // 严格来说，getCountervalue这样的getter函数应该返回一个不可变（Immutable）数据，
        // 这样调用者即使通过getCounterValues获得了当前计数值对象，
        // 也不能够修改这个对象从而扰乱其他代码的使用。 
        return counterValues;
        // 为简单起见，这里我们并不使用Immutable。
    },
    emitChange: function(){
        this.emit(CHANGE_EVENT);
    },
    addChangeListener: function(callback){
        this.on(CHANGE_EVENT, callback);
    },
    removeChangeListener: function(callback){
        this.removeChangeListener(CHANGE_EVENT, callback);
    }
});

// 上面实现的Store只有注册到Dispatcher实例上才能真正发挥作用。

// 当通过register函数把一个回调函数注册到Dispatcher之后，
// 所有派发给Dispatcher的action对象，都会传递到这个回调函数中来，
// 回调函数要做的，就是根据唯一的一个参数action对象来决定改如何更新自己的状态。
CounterStore.dispatchToken = AppDispatcher.register((action) => {
    if(action.type === ActionTypes.INCREMENT){
        counterValues[action.counterCaption]++;
        CounterStore.emitChange();
    }else if(action.type === ActionTypes.DECREMENT){
        counterValues[action.counterCaption]--;
        CounterStore.emitChange();
    }
});
// 如果action.type是INCREMENT，就根据action对象字段counterCaption确定是哪个计数器，
// 把counterValues上对应的字段做加一操作；
// 如果action.type代表DECREMENT，就做对应的减一的操作。

// 无论加一减一，最后都要调用CounterStore.emitChange函数，
// 假如有调用者通过Counter.addChangeListner关注了CounterStore的状态变化，
// 这个emitChange函数调用就会引发监听函数的执行。
```

```js
// src/stores/SummaryStore.js
import AppDispatcher from '../AppDispatcher.js';
import * as ActionTypes from '../ActionTypes.js';
import CounterStore from './CounterStore.js';
import {EventEmitter} from 'events';

const CHANGE_EVENT = 'changed';

function computeSummary(counterValues){
    let summary = 0;
    for(const key in counterValues){
        if(counterValues.hasOwnProperty(key)){
            summary += counterValues[key];
        }
    }
    return summary;
}

const SummaryStore = Object.assign({}, EventEmitter.property, {
    // SummaryStore没有存储自己的状态，
    // 当getSummary被调用时，直接从CounterStore里获取状态计算。
    // 可见，虽然名为Store，但并不表示一个Store必须要存储什么东西，
    // Store只是提供获取数据的方法，Store提供的数据完全可以由另一个Store计算得来。
    getSummary: function(){
        return computeSummary(CounterStore.getCounterValues());
    },

    emitChange: function(){
        this.emit(CHANGE_EVENT);
    },

    addChangeListener: function(callback){
        this.on(CHANGE_EVENT, callback);
    },

    removeChangeListener: function(callback){
        this.removeListener(CHANGE_EVENT, callback);
    }
});

// Dispatcher的register函数，只提供了注册一个回调函数的功能，
// 但不能让调用者在register时选择只监听某些action。
// 当一个动作被派发的时候，Dispatcher只是简单地把所有注册的回调函数全都调用一遍，
// 至于这个动作是不是对方关心的，Flux的Dispatcher不关心，而是要求每个回调函数去鉴别。
// 这个设计让Flux的Dispatcher逻辑最简单化，Dispatcher的责任越简单，就越不会出现问题。
//  由回调函数全权决定如何处理action对象，也是非常合理的。
SummaryStore.dispatchToken = AppDispatcher.register((action) => {
    if((action.type === ActionTypes.INCREMENT) || (action.type === ActionTypes.DECREMENT)){
        // 可以认为Dispatcher调用回调函数的顺序完全是无法预期的，
        // 不要假设它会按照我们期望的顺序逐个调用。

        // Dispatcher的waitFor可以接受一个数组作为参数，
        // 数组中每个元素都是一个Dispatcher.register函数的返回结果，即dispatchToken。
        // waitFor函数告诉Dispatcher,当前的处理必须要暂停，
        // 直到dispatchToken代表的那些已注册回调函数执行结束才能继续。
        AppDispatcher.waitFor([CounterStore.dispatchToken]);
        // JavaScript是单线程的语言，不存在线程之间的等待，
        // waitFor函数当然并用多线程实现的，
        // 只是在调用waitFor时，把控制权交给Dispatcher，
        // 让Dispatcher检查dispatchToken代表的回调函数有没有被执行，
        // 如果已经执行，就直接继续，
        // 如果还没执行，就调用dispatchToken代表的回调函数之后waitFor才返回。

        SummaryStore.emitChange();
    }
});

export default SummaryStore;
```

**4、View**

> Flux框架下，View并不是说必须要使用React，View本身是一个独立的部分，可以用任何一种UI库来实现。

存在于Flux框架中的React组件需要实现以下几个功能：
* 创建时要读取Store上状态来初始化组件内部状态；
* 当Store上状态发生变化时，组件要立刻同步更新内部状态保持一致；
* View如果要改变Store状态，必须且只能派发action。

```js
// src/views/CounterPanel.js
import React, {Component} from 'react';
import Counter from './Counter.js';
import Summary from './Summary.js';

const style = {
    margin: '20px'
};

class ControlPanel extends Component{
    render(){
        return (
            <div style={style}>
                <Counter caption="First" />
                <Counter caption="Second" />
                <Counter caption="Third" />
                <hr/>
                <Summary />
            </div>
        );
    }
}

export default ControlPanel;
```

```js
// src/views/Counter.js
import React, {Component, PropTypes} from 'react';
import * as Actions from '../Actions.js';
import CounterStore from '../stores/CounterStore.js';

const buttonStyle = {
    margin: '10px'
};

class Counter extends Component{
    constructor(props){
        super(props);

        this.onChange = this.onChange.bind(this);
        this.onClickIncrementButton = this.onClickIncrementButton.bind(this);
        this.onClickDecrementButton = this.onClickDecrementButton.bind(this);

        this.state = {
            count: CounterStore.getCounterValues()[props.caption]
        }
    }

    shouldComponentUpdate(nextProps, nextState){
        return (nextProps.caption !== this.props.caption) || (nextState.count !== this.state.count);
    }

    componentDidMount(){
        CounterStore.addChangeListener(this.onChange);
    }

    componentWillUnmount(){
        CounterStore.removeChangeListener(this.onClick);
    }

    onChange(){
        const newCount = CounterStore.getCounterValues()[this.propss.caption];
        this.setState({count: newCount});
    }

    onClickIncrementButton(){
        Actions.increment(this.props.caption);
    }

    onClickDecrementButton(){
        Actions.decrement(this.props.caption);
    }

    render(){
        const {caption} = this.props;
        return (
            <div>
                <button style={buttonStyle} onClick={this.onClickIncrementButton}>+</button>
                <button style={buttonStyle} onClick={this.onClickDecrementButton}>-</button>
                <span>{caption} count: {this.state.count}</span>
            </div>
        )
    }
}
```

```js
// src/views/Summary.js
import React, {Component} from 'react';
import SummaryStore from '../stores/SummaryStore.js';

class Summary extends Component{
    constructor(props){
        super(props);
        this.onUpdate = this.onUpdate.bind(this);
        this.state = {
            sum: SummaryStore.getSummary()
        }
    }

    componentDidMount(){
        SummaryStore.addChangeListener(this.onUpdate);
    }

    componentWillUnmount(){
        SummaryStore.removeChangeListener(this.onUpdate);
    }

    onUpdate(){
        this.setState({
            sum: SummaryStore.getSummary()
        })
    }

    render(){
        return (
            <div>Total Count: {this.state.sum}</div>
        );
    }
}

export default Summary;
```

## Flux的优势 [▲](#从flux到redux)

> Flux的架构下，应用的状态被放在Store中，React组件只是扮演View的作用，被动根据Store的状态来渲染。React组件依然有自己的状态，但是已经完全沦为Store组件的一个映射，而不是主动变化的数据。

**“单向数据流”的管理方式**

在Flux的理念里，如果要改变界面，必须改变Store中的状态，如果要改变Store中的状态，必须派发一个action对象，这就是规矩。在这个规矩之下，想要追溯一个应用的逻辑就变得非常容易。

**MVC最大的问题就是无法禁绝View和Model之间直接对话**，Flux中的View对应于MVC中的View，Flux中的Store对应于MVC中的Model，在Flux中，Store只有get方法，没有set方法，根本不可能直接去修改其内部状态，View只能通过get方法获取Store的状态，无法直接去修改状态，如果View想要修改Store状态，只有派发一个action对象给Dispatcher。

**这看起来是一个“限制”，但却是一个很好的“限制”，杜绝了数据流混乱的可能。**

**在Flux体系下，驱动界面改变始于一个动作的派发，除此之外，别无他法。**


## Flux的不足 [▲](#从flux到redux)

1. Store之间依赖关系 
    1. 在Flux体系中，如果两个Store之间有逻辑依赖关系，就必须要用Dispatcher的waitFor函数；
    2. CounterStore必须要把注册回调函数时产生的dispatchToken公之于众；
    3. SummaryStore必须要在代码里建立对CounterStore的dispatchToken的依赖。

    **最好的依赖管理是根本不让依赖产生。**
2. 难以进行服务器端渲染
    > 如果要在服务器端渲染，输出不是一个DOM树，而是一个全是HTML的字符串。

    > 在Flux体系中，有一个全局的Dispatcher，然后每一个Store都是一个全局唯一的对象，和一个浏览器网页只服务于一个用户不同，在服务器端要同时接受很多用户的请求，如果每个Store都是全局唯一的对象，那不同请求的状态肯定就乱套了。
3. Store混杂了逻辑和状态
    > Store封装了数据和处理数据的逻辑，用面向对象的思维来看，这是一件好事。但是，当我们需要动态替换一个Store的逻辑时，只能把这个Store整体替换掉，那也就无法保持Store中存储的状态。


# <p align="center">Redux</p>

###### [<p align="right">back to top ▲</p>](#从flux到redux)

### Redux基本原则
1. 唯一数据源（Single Source of Truth）
    
    **应用的状态数据应该只存储在唯一的一个Store上**
    > 如果状态数据分散在多个Store中，容易造成数据冗余；虽然Dispatcher的waitFor方法可以保证多个Store之间的更新顺序，但这又产生了不同Store之间的显式依赖关系，这种依赖关系的存在增加了应用的复杂度，容易带来新的问题。
2. 保持状态只读（State is read-only）
    * 要修改Store的状态，必须要通过派发一个action对象完成，这点和Flux没什么区别；
    * 要驱动用户界面渲染，就要改变应用的状态，但是改变状态的方法不是去修改状态上值，而是创建一个新的状态对象返回给Redux，由Redux完成新的状态的组装。
3. 数据改变只能通过纯函数完成（Changes are made with pure functions）
    
    __Redux=Reducer+Flux__
    
    在Redux中，每个reducer的函数签名如下所示：

    __reducer(state, action)__

    state是当前的状态，action是接收到的action对象，reducer函数要做的事情，就是根据state和action的值产生一个新的对象返回。

    reducer必须是纯函数，即函数的返回结果必须完全由参数state和action决定，而且不产生任何副作用，也不能修改参数state和action对象。