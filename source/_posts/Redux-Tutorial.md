---
title: Redux Tutorial
date: 2020-04-26 08:04:13
tags:
---
## A First Look at `Redux`
![image](https://blog.codecentric.de/files/2017/12/Bildschirmfoto-2017-12-01-um-08.53.32.png)
On the left hand side, you see a tree of React components. Once a component initiates a state change, this change needs to be propagated to all other components that rely on the changed data.

This is where Redux comes in handy. Redux is a predictable state container for JavaScript apps. The state is kept in one store and components listen to the data in the store that they are interested in.

**Flux pattern**
Redux implements the Flux pattern that manages the data flow in your application. The view components subscribe to the store and react on changes. Components can dispatch actions that describe what should happen. The Reducers receive these actions and update the store. A detailed explanation of the four parts of the flux pattern in Redux is given in the next sections.
![image](https://image.slidesharecdn.com/reduxdataflowwithangular-170623072558/95/redux-data-flow-with-angular-24-638.jpg?cb=1498202795)
![image](https://img-blog.csdn.net/20180814194906342?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl8zODY0MjMzMQ==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
- **Actions** are payloads of information that send data from your application to your store. They are the only source of information for the store. You send them to the store using `store.dispatch()`.
- **Reducers** specify how the application's state changes in response to actions sent to the store. Remember that actions only describe what happened, but don't describe how the application's state changes.
we defined the actions that represent the facts about “what happened” and the reducers that update the state according to those actions.
- The **Store** is the object that brings them together. The store has the following responsibilities:
    - Holds application state;
    - Allows access to state via getState();
    - Allows state to be updated via dispatch(action);
    - Registers listeners via subscribe(listener);
    - Handles unregistering of listeners via the function returned by subscribe(listener)

**Data Flow**
The data lifecycle in any Redux app follows these 4 steps:

**1. You call `store.dispatch(action)`.**
**2. The Redux store calls the reducer function you gave it.**
**3. The root reducer may combine the output of multiple reducers into a single state tree.**
**4. The Redux store saves the complete state tree returned by the root reducer.**

## Initialize the First Program
1. 
```shell script
npm install -g create-react-app
```
2. 
```shell script
`somewhere:`
 mkdir ReduxDemo   
 cd ReduxDemo      
 create-react-app demo01  
 cd demo01   
 npm  start  
```
3. 
```javascript
import React from 'react';
import ReactDOM from 'react-dom'
import TodoList from './TodoList'

ReactDOM.render(<TodoList/>,document.getElementById('root'))
```
4. Structure:
<img id="d01" src="d01.png" width="250" height="350"/>


5. Create TodoList.js
```javascript
import React, { Component } from 'react';
class TodoList extends Component {
    render() { 
        return ( 
            <div>Hello World</div>
         );
    }
}
export default TodoList;
```
6. Install AntDesign
```shell script
npm install antd --save
```

## Create UI with AntDisign
1. Import components(Input, Button, List) and css in TodoList.js
```javascript
import React, { Component } from 'react'
import 'antd/dist/antd.css'
import {Input, Button, List} from 'antd'

const data=[
    '早8点开晨会，分配今天的代码任务',
    '早9点和项目经理开需求沟通会',
    '中午12 点和客户吃饭'
]

class TodoList extends Component {
    
    render() { 
        return ( 
            <div style={{margin:'10px'}}>
                <div>
                    <Input
                        placeholder='Write Somethind'
                        style={{width:'250px', marginRight:'10px'}}
                    />
                    <Button type="primary">增加</Button>
                </div>
                <div style={{margin:'10px', width:'300px'}}>
                    <List
                        bordered
                        dataSource={data}
                        renderItem={item=>(<List.Item>{item}</List.Item>)}
                    />
                </div>
            </div>
         );
    }
}
 
export default TodoList;
```
2. result:
<img id="d12" class="glyphicon-align-left" src="d12.png">

## Create store and reducer in Redux
1. install Redux
```shell script
npm install --save redux
```
2. create `index.js` and `reducer.js` in store
<img id="d13" src="d13.png">
index.js
```javascript
import {createStore} from 'redux'
import reducer from './reducer'
const store = createStore(reducer)
export default store
```
  reducer.js
```javascript
const defaultState = {
    inputValue: 'Write Somethine',
    List: [
        '早8点开晨会，分配今天的代码任务',
        '早9点和项目经理开需求沟通会',
        '中午12 点和客户吃饭'
    ]
}
export default (state = defaultState, action) => {
    return state
}
```
  TodoList.js
```javascript
import React, { Component } from 'react'
import 'antd/dist/antd.css'
import {Input, Button, List} from 'antd'
import store from './store'

const data=[
    '早8点开晨会，分配今天的代码任务',
    '早9点和项目经理开需求沟通会',
    '中午12 点和客户吃饭'
]

class TodoList extends Component {
    
    constructor(props){
        super(props)
        console.log(store.getState())
        this.state = store.getState()
    }

    render() { 
        return ( 
            <div style={{margin:'10px'}}>
                <div>
                    <Input
                        placeholder={this.state.inputValue}
                        style={{width:'250px', marginRight:'10px'}}
                    />
                    <Button type="primary">增加</Button>
                </div>
                <div style={{margin:'10px', width:'300px'}}>
                    <List
                        bordered
                        dataSource={this.state.List}
                        renderItem={item=>(<List.Item>{item}</List.Item>)}
                    />
                </div>
            </div>
         );
    }
}
 
export default TodoList;
```
  result
  <img id="d14" src="d14.png">


## Install Redux dev Extention from Google Chrom
`index.js`
```javascript
import {createStore} from 'redux'
import reducer from './reducer'
const store = createStore(
    reducer,
    window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
    )
export default store
```
  result:
  <img id="d15" src="d15.png">


1. Add onChange, storeChange, clickBrn in `TodoList.js`
```javascript
import React, { Component } from 'react'
import 'antd/dist/antd.css'
import {Input, Button, List} from 'antd'
import store from './store'

class TodoList extends Component {
    
    constructor(props){
        super(props)
        this.state = store.getState()
        this.changeInputValue=this.changeInputValue.bind(this)
        this.storeChange=this.storeChange.bind(this)
        this.clickBtn=this.clickBtn.bind(this)
        store.subscribe(this.storeChange)
        
    }

    render() { 
        return ( 
            <div style={{margin:'10px'}}>
                <div>
                    <Input
                        placeholder={this.state.inputValue}
                        style={{width:'250px', marginRight:'10px'}}
                        onChange={this.changeInputValue}
                        value={this.state.inputValue}
                    />
                    <Button 
                    type="primary"
                    onClick={this.clickBtn}
                    >增加</Button>
                </div>
                <div style={{margin:'10px', width:'300px'}}>
                    <List
                        bordered
                        dataSource={this.state.List}
                        renderItem={item=>(<List.Item>{item}</List.Item>)}
                    />
                </div>
            </div>
         );
    }
    changeInputValue(e){
        const action = {
            type: 'changeInput',
            value: e.target.value
        }
        store.dispatch(action)
    }
    storeChange(){
        this.setState(store.getState())
    }
    clickBtn(){
        const action = {type: 'addItem'}
        store.dispatch(action)
    }
}
 
export default TodoList;
```
  `reducer.js`
  ```javascript
const defaultState = {
    inputValue: 'Write Something',
    List: [
        '早8点开晨会，分配今天的代码任务',
        '早9点和项目经理开需求沟通会',
        '中午12 点和客户吃饭'
    ]
}
export default (state = defaultState, action) => {
    
    //reducer只能接受state，不能改变state
    if(action.type ==='changeInput'){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        newState.inputValue = action.value
        return newState
    }
    if(action.type === 'addItem'){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        if (newState.inputValue  != ''){
            newState.List.push(newState.inputValue)
            newState.inputValue=''
            return newState
        }
        
    }
    if(action.type === 'deleteItem'){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        newState.List.splice(action.index, 1)
        return newState
    }
    return state
}
```
2. add deleteItem in TodoList.js
```javascript
import React, { Component } from 'react'
import 'antd/dist/antd.css'
import {Input, Button, List} from 'antd'
import store from './store'

class TodoList extends Component {
    
    constructor(props){
        super(props)
        this.state = store.getState()
        this.changeInputValue=this.changeInputValue.bind(this)
        this.storeChange=this.storeChange.bind(this)
        this.clickBtn=this.clickBtn.bind(this)
        store.subscribe(this.storeChange)
        
    }

    render() { 
        return ( 
            <div style={{margin:'10px'}}>
                <div>
                    <Input
                        placeholder={this.state.inputValue}
                        style={{width:'250px', marginRight:'10px'}}
                        onChange={this.changeInputValue}
                        value={this.state.inputValue}
                    />
                    <Button 
                    type="primary"
                    onClick={this.clickBtn}
                    >增加</Button>
                </div>
                <div style={{margin:'10px', width:'300px'}}>
                    <List
                        bordered
                        dataSource={this.state.List}
                        renderItem={(item, index)=>(<List.Item onClick={this.deleteItem.bind(this, index)}>{item}</List.Item>)}
                    />
                </div>
            </div>
         );
    }
    changeInputValue(e){
        const action = {
            type: 'changeInput',
            value: e.target.value
        }
        store.dispatch(action)
    }
    storeChange(){
        this.setState(store.getState())
    }
    clickBtn(){
        const action = {type: 'addItem'}
        store.dispatch(action)
    }
    deleteItem(index){
        const action={
            type:'deleteItem',
            index
        }
        store.dispatch(action)
    }
}
 
export default TodoList;
```
## Tips for Redux
1. add `actionType.js` in store
```javascript
export const CHANGE_INPUT = 'changeInput'
export const ADD_ITEM = 'addItem'
export const DELETE_ITEM = 'deleteItem'
```
  `TodoList.js`
  ```javascript
import React, { Component } from 'react'
import 'antd/dist/antd.css'
import {Input, Button, List} from 'antd'
import store from './store'
import { CHANGE_INPUT, ADD_ITEM, DELETE_ITEM } from './store/actionType'

class TodoList extends Component {
    
    constructor(props){
        super(props)
        this.state = store.getState()
        this.changeInputValue=this.changeInputValue.bind(this)
        this.storeChange=this.storeChange.bind(this)
        this.clickBtn=this.clickBtn.bind(this)
        store.subscribe(this.storeChange)
        
    }

    render() { 
        return ( 
            <div style={{margin:'10px'}}>
                <div>
                    <Input
                        placeholder={this.state.inputValue}
                        style={{width:'250px', marginRight:'10px'}}
                        onChange={this.changeInputValue}
                        value={this.state.inputValue}
                    />
                    <Button 
                    type="primary"
                    onClick={this.clickBtn}
                    >增加</Button>
                </div>
                <div style={{margin:'10px', width:'300px'}}>
                    <List
                        bordered
                        dataSource={this.state.List}
                        renderItem={(item, index)=>(<List.Item onClick={this.deleteItem.bind(this, index)}>{item}</List.Item>)}
                    />
                </div>
            </div>
         );
    }
    changeInputValue(e){
        const action = {
            type: CHANGE_INPUT,
            value: e.target.value
        }
        store.dispatch(action)
    }
    storeChange(){
        this.setState(store.getState())
    }
    clickBtn(){
        const action = {type: ADD_ITEM}
        store.dispatch(action)
    }
    deleteItem(index){
        const action={
            type: DELETE_ITEM,
            index
        }
        store.dispatch(action)
    }
}
 
export default TodoList;
```
  `reducer.js`
  ```javascript
import { CHANGE_INPUT, ADD_ITEM, DELETE_ITEM } from './actionType'

const defaultState = {
    inputValue: 'Write Something',
    List: [
        '早8点开晨会，分配今天的代码任务',
        '早9点和项目经理开需求沟通会',
        '中午12 点和客户吃饭'
    ]
}
export default (state = defaultState, action) => {
    
    //reducer只能接受state，不能改变state
    if(action.type === CHANGE_INPUT){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        newState.inputValue = action.value
        return newState
    }
    if(action.type === ADD_ITEM){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        if (newState.inputValue  != ''){
            newState.List.push(newState.inputValue)
            newState.inputValue=''
            return newState
        }
        
    }
    if(action.type === DELETE_ITEM){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        newState.List.splice(action.index, 1)
        return newState
    }
    return state
}
```
2. create `actionCreator.js` in store
```javascript
import { CHANGE_INPUT, ADD_ITEM, DELETE_ITEM} from './actionType'

export const changeInputAction = (value) => ({
        type: CHANGE_INPUT,
        value
})
export const addItemAction = () => ({
    type: ADD_ITEM,
})
export const deleteItemAction = (index) => ({
    type: DELETE_ITEM,
    index
})
```
  `TodoList.js`
  ```javascript
import React, { Component } from 'react'
import 'antd/dist/antd.css'
import {Input, Button, List} from 'antd'
import store from './store'
import { changeInputAction, addItemAction, deleteItemAction } from './store/actionCreator'

class TodoList extends Component {
    
    constructor(props){
        super(props)
        this.state = store.getState()
        this.changeInputValue=this.changeInputValue.bind(this)
        this.storeChange=this.storeChange.bind(this)
        this.clickBtn=this.clickBtn.bind(this)
        store.subscribe(this.storeChange)
        
    }

    render() { 
        return ( 
            <div style={{margin:'10px'}}>
                <div>
                    <Input
                        placeholder={this.state.inputValue}
                        style={{width:'250px', marginRight:'10px'}}
                        onChange={this.changeInputValue}
                        value={this.state.inputValue}
                    />
                    <Button 
                    type="primary"
                    onClick={this.clickBtn}
                    >增加</Button>
                </div>
                <div style={{margin:'10px', width:'300px'}}>
                    <List
                        bordered
                        dataSource={this.state.List}
                        renderItem={(item, index)=>(<List.Item onClick={this.deleteItem.bind(this, index)}>{item}</List.Item>)}
                    />
                </div>
            </div>
         );
    }
    changeInputValue(e){
        const action = changeInputAction(e.target.value)
        store.dispatch(action)
    }
    storeChange(){
        this.setState(store.getState())
    }
    clickBtn(){
        const action = addItemAction()
        store.dispatch(action)
    }
    deleteItem(index){
        const action=deleteItemAction(index)
        store.dispatch(action)
    }
}
 
export default TodoList;
```
## Split UI and Business Ligic
1. Create TodoListUI.js using `imrc` and `ccc` shortcut
  move UI from TodoList.js to TodoListUI.js
  `TodoListUI.js`
  ```javascript
import React, { Component } from 'react';
import 'antd/dist/antd.css'
import {Input, Button, List} from 'antd'

class TodoListUI extends Component {
    constructor(props) {
        super(props);
        this.state = {  }
    }
    render() { 
        return ( <div style={{margin:'10px'}}>
        <div>
            <Input
                placeholder={this.props.inputValue}
                style={{width:'250px', marginRight:'10px'}}
                onChange={this.props.changeInputValue}
                value={this.props.inputValue}
            />
            <Button 
            type="primary"
            onClick={this.props.clickBtn}
            >增加</Button>
        </div>
        <div style={{margin:'10px', width:'300px'}}>
            <List
                bordered
                dataSource={this.props.List}
                renderItem={(item, index)=>(
                <List.Item 
                    onClick={() => {this.props.deleteItem(index)}}>
                    {item}
                </List.Item>)}
            />
        </div>
    </div> );
    }
}
 
export default TodoListUI;
```
  `TodoList.js`
   ```javascript
import React, { Component } from 'react'
import store from './store'
import { changeInputAction, addItemAction, deleteItemAction } from './store/actionCreator'
import TodoListUI from './TodoListUI'

class TodoList extends Component {
    
    constructor(props){
        super(props)
        this.state = store.getState()
        this.changeInputValue=this.changeInputValue.bind(this)
        this.storeChange=this.storeChange.bind(this)
        this.deleteItem=this.deleteItem.bind(this)
        this.clickBtn=this.clickBtn.bind(this)
        store.subscribe(this.storeChange)
        
    }

    render() { 
        return ( 
            <TodoListUI 
                inputValue={this.state.inputValue} 
                changeInputValue={this.changeInputValue}
                clickBtn={this.clickBtn}  
                List={this.state.List}
                deleteItem={this.deleteItem}
            />
         );
    }
    changeInputValue(e){
        const action = changeInputAction(e.target.value)
        store.dispatch(action)
    }
    storeChange(){
        this.setState(store.getState())
    }
    clickBtn(){
        const action = addItemAction()
        store.dispatch(action)
    }
    deleteItem(index){
        const action=deleteItemAction(index)
        store.dispatch(action)
    }
}
 
export default TodoList;
```
## Stateless Components
`TodoListUI.js`
  ```javascript
import React from 'react';
import 'antd/dist/antd.css'
import {Input, Button, List} from 'antd'

const TodoListUI = (props) => {
    return ( <div style={{margin:'10px'}}>
    <div>
        <Input
            placeholder={props.inputValue}
            style={{width:'250px', marginRight:'10px'}}
            onChange={props.changeInputValue}
            value={props.inputValue}
        />
        <Button 
        type="primary"
        onClick={props.clickBtn}
        >增加</Button>
    </div>
    <div style={{margin:'10px', width:'300px'}}>
        <List
            bordered
            dataSource={props.List}
            renderItem={(item, index)=>(
            <List.Item 
                onClick={() => {props.deleteItem(index)}}>
                {item}
            </List.Item>)}
        />
    </div>
</div> );
}
 
export default TodoListUI;
```
## Axios-Retrieve Data from Backend
1. 
```shell script
npm install --save axios
```

2. Create componentDidMoint() to get data
```javascript
import React, { Component } from 'react'
import store from './store'
import { changeInputAction, addItemAction, deleteItemAction } from './store/actionCreator'
import TodoListUI from './TodoListUI'
import axios from 'axios'

class TodoList extends Component {
    
    constructor(props){
        super(props)
        this.state = store.getState()
        this.changeInputValue=this.changeInputValue.bind(this)
        this.storeChange=this.storeChange.bind(this)
        this.deleteItem=this.deleteItem.bind(this)
        this.clickBtn=this.clickBtn.bind(this)
        store.subscribe(this.storeChange)
        
    }

    render() { 
        return ( 
            <TodoListUI 
                inputValue={this.state.inputValue} 
                changeInputValue={this.changeInputValue}
                clickBtn={this.clickBtn}  
                List={this.state.List}
                deleteItem={this.deleteItem}
            />
         );
    }

    componentDidMount(){
        axios.get('https://www.easy-mock.com/mock/5cfcce489dc7c36bd6da2c99/xiaojiejie/getList').then((res)=>{
            const data = res.data
            const action = getListAction(data)
            store.dispatch(action)
        })
    }

    changeInputValue(e){
        const action = changeInputAction(e.target.value)
        store.dispatch(action)
    }
    storeChange(){
        this.setState(store.getState())
    }
    clickBtn(){
        const action = addItemAction()
        store.dispatch(action)
    }
    deleteItem(index){
        const action=deleteItemAction(index)
        store.dispatch(action)
    }
}
 
export default TodoList;
```
  result:
  ![image](day01.png)
  easy-mock:
  ```shell script
https://easy-mock.com/project/5eac19cbd933d175e8597106
```
3. `actionType.js`
```javascript
export const CHANGE_INPUT = 'changeInput'
export const ADD_ITEM = 'addItem'
export const DELETE_ITEM = 'deleteItem'
export const GET_LIST = 'getList'

```
4. `actionCreator.js`
```javascript
import { CHANGE_INPUT, ADD_ITEM, DELETE_ITEM, GET_LIST} from './actionType'

export const changeInputAction = (value) => ({
        type: CHANGE_INPUT,
        value
})
export const addItemAction = () => ({
    type: ADD_ITEM,
})
export const deleteItemAction = (index) => ({
    type: DELETE_ITEM,
    index
})
export const getListAction = (data) => ({
    type: GET_LIST,
    data
})

```
5. `reducer.js`
```javascript
import { CHANGE_INPUT, ADD_ITEM, DELETE_ITEM, GET_LIST } from './actionType'

const defaultState = {
    inputValue: 'Write Something',
    List: []
}
export default (state = defaultState, action) => {
    
    //reducer只能接受state，不能改变state
    if(action.type === CHANGE_INPUT){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        newState.inputValue = action.value
        return newState
    }
    if(action.type === ADD_ITEM){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        if (newState.inputValue  !== ''){
            newState.List.push(newState.inputValue)
            newState.inputValue=''
            return newState
        }
        
    }
    if(action.type === DELETE_ITEM){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        newState.List.splice(action.index, 1)
        return newState
    }

    if(action.type === GET_LIST){
        let newState = JSON.parse(JSON.stringify(state))//深度拷贝state
        newState.List = action.data.data.List
        return newState
    }
    return state
}
```

## Redux-thunk
1. 
```shell script
npm install --save redux-thunk
```

2. `index.js`
```javascript
import {createStore, applyMiddleware, compose} from 'redux'
import reducer from './reducer'
import thunk from 'redux-thunk'
const composeEnhancers = window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__ ? window.__REDUX_DEVTOOLS_EXTENSION_COMPOSE__({}):compose

const enhancer = composeEnhancers(applyMiddleware(thunk))

const store = createStore(
    reducer, enhancer)
export default store
```
3. `TodoList.js`
```javascript
import React, { Component } from 'react'
import store from './store'
import { getTodoList, changeInputAction, addItemAction, deleteItemAction } from './store/actionCreator'
import TodoListUI from './TodoListUI'


class TodoList extends Component {
    
    constructor(props){
        super(props)
        this.state = store.getState()
        this.changeInputValue=this.changeInputValue.bind(this)
        this.storeChange=this.storeChange.bind(this)
        this.deleteItem=this.deleteItem.bind(this)
        this.clickBtn=this.clickBtn.bind(this)
        store.subscribe(this.storeChange)
        
    }

    render() { 
        return ( 
            <TodoListUI 
                inputValue={this.state.inputValue} 
                changeInputValue={this.changeInputValue}
                clickBtn={this.clickBtn}  
                List={this.state.List}
                deleteItem={this.deleteItem}
            />
         );
    }

    componentDidMount(){
        const action = getTodoList()
        store.dispatch(action)
    }

    changeInputValue(e){
        const action = changeInputAction(e.target.value)
        store.dispatch(action)
    }
    storeChange(){
        this.setState(store.getState())
    }
    clickBtn(){
        const action = addItemAction()
        store.dispatch(action)
    }
    deleteItem(index){
        const action=deleteItemAction(index)
        store.dispatch(action)
    }
}
 
export default TodoList;
```
4. `actionCreator.js`
```javascript
import { CHANGE_INPUT, ADD_ITEM, DELETE_ITEM, GET_LIST} from './actionType'
import axios from 'axios'

export const changeInputAction = (value) => ({
        type: CHANGE_INPUT,
        value
})
export const addItemAction = () => ({
    type: ADD_ITEM,
})
export const deleteItemAction = (index) => ({
    type: DELETE_ITEM,
    index
})
export const getListAction = (data) => ({
    type: GET_LIST,
    data
})
export const getTodoList = () => {
    return (dispatch) => {
        axios.get('https://easy-mock.com/mock/5eac19cbd933d175e8597106/Demo02/getList').then((res)=>{
            const data = res.data
            const action = getListAction(data)
            dispatch(action)
        })
    }
}

```
## Using React-Redux to simplify Code
1. 
```shell script
npm install --save react-redux
```
2. Create new demo02
  `index.js`
  ```javascript
import React from 'react';
import ReactDOM from 'react-dom'
import TodoList from './TodoList'

ReactDOM.render(<TodoList/>,document.getElementById('root'))
```

  `TodoList.js`
  ```javascript
import React, { Component } from 'react';
import store from './store'
class TodoList extends Component {
    constructor(props) {
        super(props);
        this.state = store.getState()
    }
    render() { 
        return ( <div>
            <div>
                <input value={this.state.inputValue}/>
                <button>提交</button>
            </div>
            <div>
                <li>Wenyong</li>
            </div>
        </div> );
    }
}
 
export default TodoList;
```
  `index.js` under store folder
  ```javascript
import { createStore } from 'redux'
import reducer from './reducer'

const store = createStore(reducer)

export default store
```
  `reducer.js`
  ```javascript
const defaultState = {
    inputValue : 'Wenyong',
    list : []
}

export default (state = defaultState, action) => {
    return state
}
```
  structure:
  <img id = "day02" src="day02.png">


## Provider and Connect in React-Redux
1. Import Provider in `index.js`
```javascript
import React from 'react';
import ReactDOM from 'react-dom'
import TodoList from './TodoList'
import { Provider } from 'react-redux'
import store from './store'

const App = (
  <Provider store = {store}>
    <TodoList />
  </Provider>
)

ReactDOM.render(App ,document.getElementById('root'));



```
2. import connect
  `TodoList.js`
  ```javascript
import React, { Component } from 'react';
import { connect } from 'react-redux'

class TodoList extends Component {
    constructor(props) {
        super(props);
    }
    render() { 
        return ( <div>
            <div>
                <input value={this.props.inputValue}/>
                <button>提交</button>
            </div>
            <div>
                <li>Wenyong</li>
            </div>
        </div> );
    }
}

const stateToProps = (state) => {
    return {
        inputValue : state.inputValue
    }
}
 
export default connect(stateToProps, null)(TodoList);
```

## Change Store State Value
1. `TodoList.js`
```javascript
import React, { Component } from 'react';
import { connect } from 'react-redux'

class TodoList extends Component {
    
    render() { 
        return ( <div>
            <div>
                <input value={this.props.inputValue} onChange={this.props.inputChange}/>
                <button>提交</button>
            </div>
            <div>
                <li>Wenyong</li>
            </div>
        </div> 
        );
    }

}

const stateToProps = (state) => {
    return {
        inputValue : state.inputValue
    }
}

const dispatchToProps = (dispatch) => {
    return {
        inputChange(e) {
            let action = {
                type : 'change_input',
                value : e.target.value
            }
            dispatch(action)
        }
    }
}
 
export default connect(stateToProps, dispatchToProps)(TodoList);
```
2. `reducer.js`
```javascript
const defaultState = {
    inputValue : 'Wenyong',
    list : []
}

export default (state = defaultState, action) => {
    if (action.type === 'change_input') {
        let newState = JSON.parse(JSON.stringify(state)) 
        newState.inputValue = action.value
        return newState
    }
    return state
}
```
3. Create add_item
  `TodoList.js`
  ```javascript
import React, { Component } from 'react';
import { connect } from 'react-redux'

class TodoList extends Component {
    
    render() { 
        return ( <div>
            <div>
                <input value={this.props.inputValue} onChange={this.props.inputChange}/>
                <button onClick= {this.props.clickButton}>提交</button>
            </div>
            <ul>
                {
                    this.props.list.map((item, index)=>{
                    return (<li key={index}>{item}</li>)
                    })
                }
            </ul>
        </div> 
        );
    }

}

const stateToProps = (state) => {
    return {
        inputValue : state.inputValue,
        list : state.list
    }
}

const dispatchToProps = (dispatch) => {
    return {
        inputChange(e) {
            let action = {
                type : 'change_input',
                value : e.target.value
            }
            dispatch(action)
        },
        clickButton() {
            let action = {type : 'add_item'}
            dispatch(action)
        }
    }
}
 
export default connect(stateToProps, dispatchToProps)(TodoList);
```
  `reducer.js`
  ```javascript
const defaultState = {
    inputValue : 'Wenyong',
    list : []
}

export default (state = defaultState, action) => {
    if (action.type === 'change_input') {
        let newState = JSON.parse(JSON.stringify(state)) 
        newState.inputValue = action.value
        return newState
    }
    if (action.type === 'add_item') {
        let newState = JSON.parse(JSON.stringify(state)) 
        newState.list.push(newState.inputValue)
        newState.inputValue = ''
        return newState
    }
    return state
}
```

<style>
#d12 {
    width: 50%;
    height: 50%;
    border: 1px solid #ddd;
    display: inline-block;
}
#d13 {
    width: 40%;
    height: 40%;
    border: 1px solid #ddd;
    display: inline-block;
}
#d14 {
    width: 50%;
    height: 50%;
    border: 1px solid #ddd;
    display: inline-block;
}
#d01 {
    width: 40%;
    height: 40%;
    border: 1px solid #ddd;
    display: inline-block;
}
#day02 {
    width: 40%;
    height: 40%;
    border: 1px solid #ddd;
    display: inline-block;
}
</style>