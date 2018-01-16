# ngDux - Introduction

ngDux was created to overcome deficits of the existing AngularJS-Redux \(_ng-redux_\) binding implementation.  
The need to share a store instance between AngularJS and React components is one of the main reasons for this reinvention of the wheel.

---

The existing _ng-redux_ implementation allows only for creating a Redux store instance inside the ng-redux bindings configuration. There is no way of accessing the store instance object directly or to provide an existing store instance to the _ng-redux_ bindings.

**ngDux** leaves the creation and configuration of the store instance up to the developer, to allow the use of a shared store instance between AngularJs and React \(just like **react-redux** does\).

To make selectors and mappings reuseable between AngularJS and React components, we tried to resemble the react-redux `connect()` API as close as possible. If you ever worked with **react-redux**, you will probably feel familiar with using  **ngDux**.

