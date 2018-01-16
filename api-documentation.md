# General
  
* [ng-dux](#module_ng-dux)
    * [.shallowCompare](#module_ng-dux.shallowCompare)
    * [.ngDux](#module_ng-dux.ngDux) : <code>string</code>

<a name="module_ng-dux.shallowCompare"></a>


## ng-dux.shallowCompare
shallow compare two objects

**Kind**: static constant of [<code>ng-dux</code>](#module_ng-dux)  
**Example**  
```js
 import {shallowCompare} from "ng-dux";
 
  const commonObject = {
    x: 1
  };
  const objA = {
    someProp: "nothing",
    anyProp: "something",
    someObject: commonObject
  };
  const objB = {
    someProp: "anything",
    anyProp: "something",
    someObject: commonObject
  };
  const objC = {
    anyProp: "something",
    someObject: commonObject,
    someProp: "nothing"
  };
 
  console.log(shallowCompare(objA, objB)); // false
  console.log(shallowCompare(objA, objC)); // true
  console.log(shallowCompare(objC, objB)); // false
 ```
<a name="module_ng-dux.ngDux"></a>

## ng-dux.ngDux : <code>string</code>
The module name

**Kind**: static constant of [<code>ng-dux</code>](#module_ng-dux)  
**Example**  
```js
 import {ngDux} from "ng-dux";
 
 angular.module("myExampleModule", [ngDux, ...otherDeps]);
 ```

* * *

# Injectable Services and Providers

  Use `ngDuxProvider` to configure your ngDux binding service.

**Kind**: global Angular Provider  
<a name="ngDuxProvider+setStore"></a>

## ngDuxProvider.setStore(store)
setStore is only available during the config phase of the angular application.
You might want to take care to set the store using the Provider in the config phase, since it can't be changed at a later point of time!
Use setStore(yourStore):
In case you want to reuse the store (eg. for binding
to react components), you can simply use ngDux.getStore()
to retrieve the same store instance that is being used in your
angular components. Using a different store instance for e.g. react components would lead to state, that won't stay in sync across angular and react components.
So:
If you want to integrate react components (or any other UI library/framework)
seamlessly into an AngularJS application, they NEED to use the same (!) instance of the store!

**Kind**: instance method of [<code>ngDuxProvider</code>](#ngDuxProvider)  

| Param | Type |
| --- | --- |
| store | [<code>ReduxStore</code>](https://redux.js.org) | 

**Example**  
```js
import {ngDux} from "ng-dux";

// import or create your redux store instance somewhere here...
// e.g.
 import {createStore} from "redux";
 const store = createStore(function reducer(state, action) {
   return {
     ...state,
     [action.type]: "was dispatched"
   };
 }, {
   //your default state
 });

angular.module("yourExampleAppModule", [ngDux]).config(["ngDuxProvider", function(ngDuxProvider) {
  ngDuxProvider.setStore(store);
}]);

```
  
* [ngDux](#ngDux)
    * _instance_
        * [.connect([mapStateToProps], [mapDispatchToProps], [shouldMapUpdate])](#ngDux+connect) ⇒ <code>Connector</code>
    * _static_
        * [.Connector](#ngDux.Connector) : <code>function</code>

**Kind**: global Angular Service  
**Requires**: <code>module:$rootScope</code>  
<a name="ngDux+connect"></a>

## ngDux.connect([mapStateToProps], [mapDispatchToProps], [shouldMapUpdate]) ⇒ <code>Connector</code>
creates a Connector function, that you can use to connect a controller instance with the provided mappings to a Redux store.
`ngDux#connect` the function returned is reuseable and can be passed to child components by their angular bindings, to reuse this mapping.

**Kind**: instance method of [<code>ngDux</code>](#ngDux)  
**Returns**: <code>Connector</code> - Connector  

| Param | Type | Description |
| --- | --- | --- |
| [mapStateToProps] | [<code>mapStateToProps</code>](#mapStateToProps) | Function that returns an Object with properties that were retrieved from the state. |
| [mapDispatchToProps] | [<code>mapDispatchToProps</code>](#mapDispatchToProps) | Function that returns an Object with functions to dispatch actions to the store. |
| [shouldMapUpdate] | [<code>shouldMapUpdate</code>](#shouldMapUpdate) | Decide whether the mapping should be recalculated and updated for a new state or not. |

<a name="ngDux.Connector"></a>

## ngDux.Connector : <code>function</code>
Function that will connect your Component controller instance to the store

**Kind**: static typedef of [<code>ngDux</code>](#ngDux)  

| Param | Type |
| --- | --- |
| bindingTargetInstance | [<code>BindingTarget</code>](https://docs.angularjs.org/guide/component#component-based-application-architecture) | 




