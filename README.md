#### how to install

```
npm i react-eventproxy
```

#### function api

eventProxy 中总共有 on、one、off、trigger 这 4 个函数：  
* on、one：on 与 one 函数用于订阅者监听相应的事件，并将事件响应时的函数作为参数，on 与 one 的唯一区别就是，使用 one 进行订阅的函数，只会触发一次，而 使用 on 进行订阅的函数，每次事件发生相应时都会被触发。
* trigger：trigger 用于发布者发布事件，将除第一参数（事件名）的其他参数，作为新的参数，触发使用 one 与 on 进行订阅的函数。
* off：用于解除所有订阅了某个事件的所有函数。

#### how to use
```
import eventProxy from '../eventProxy'

class Parent extends Component{
  render() {
    return (
      <div>
        <Child_1/>
        <Child_2/>
      </div>
    );
  }
}
// componentDidUpdate 与 render 方法与上例一致
class Child_1 extends Component{
  componentDidMount() {
    setTimeout(() => {
      // 发布 msg 事件
      eventProxy.trigger('msg', 'end');
    }, 1000);
  }
}
// componentDidUpdate 方法与上例一致
class Child_2 extends Component{
  state = {
    msg: 'start'
  };

  componentDidMount() {
  	// 监听 msg 事件
    eventProxy.on('msg', (msg) => {
      this.setState({
        msg
      });
    });
  }

  render() {
    return <div>
      <p>child_2 component: {this.state.msg}</p>
      <Child_2_1 />
    </div>
  }
}

```

