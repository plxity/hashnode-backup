## Memoized Selector - Using 'Reselect' with ReactJS and Redux

## Introduction
Hello everyone 👋, I am back with another blog where I'll be explaining a bit about '[Reselect](https://www.npmjs.com/package/reselect)'. It is an NPM module which can be used along with React and Redux to improve the performance of the application. 🚀

### Back story
While contributing to [Processing Organisation](https://github.com/processing) (An OpenSource Organisation) I was working on an issue which involved 'Reselect' and to solve that [issue](https://github.com/processing/p5.js-web-editor/pull/1657)  I had to learn a bit about it.


![undraw_code_inspection_bdl7.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606558520395/k7RyE_K9K.png)

### Let's Go

Suppose you are building a component in ReactJS which involves managing multiple states with help of Redux. If a component is updated the whole state tree is calculated again and it is rerendered. This update in state tree can be an expensive call at times if the state tree is very large.
Using 'Reselect' can help us to prevent unnecessary recalculations and re-rendering of the component which improves the performance indirectly. 

### Code Snipet - Example
Suppose your React component looks something like -

`Containers/PersonList.js`
```
import { connect } from 'react-redux'

const sortByName = (names, filter) => {
  switch (filter) {
    case 'ASCE':
      return  {Logic for ordering the names array in ascending order}
    case 'DESC':
      return {Logic for ordering the names array in descending order}
    default: 
      return names;
  }
}

const mapStateToProps = (state) => {
  return {
   names: sortByName(state.names, state.filterOrder),
   cities: state.cities
  }
}

const mapDispatchToProps = (dispatch) => {
  return {
   addNewCity: (city) => {
      dispatch(addNewCity(city))
    }
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(PersonList)

```

So whenever there is a change in a state tree, `mapStateToProps` is called again and the component is rendered.

For example, if a new city is added state tree will be calculated again, the component will rerender, the `mapStateToProps` will be called and `sortByName` function will run again. This can lead to performance issue if the `names` list is huge. It will be called again even if there is no change in the `names` array or the `filter`.


We can solve this problem by using 'Reselect'. It helps us to create a memoized selector.

Code snippet -
`Selector/index.js`

```
import { createSelector } from 'reselect'

const getSortingFilter = (state) => state.filterOrder
const getNames = (state) => state.names

export const getSortedNames = createSelector(
  [ getSortingFilter, getNames ],
  (filter, names) => {
    switch (filter) {
    case 'ASCE':
      return  {Logic for ordering the names array in ascending order}
    case 'DESC':
      return {Logic for ordering the names array in descending order}
    default:
      return names;
   }
  }
)

```
In `createSelector` function I have used two parameters which are `getSortingFilter` and `getNames` which gives the filter and the names array from the state tree respectively. 

`Names` will only be re-calculated when there is a change in the `Names` array or `filter` parameter (As specified in the `createSelector` function). You can add any number of parameters in the `createSelector` function.

```
const getSortingFilter = (state) => state.filterOrder
const getNames = (state) => state.names
```
Now let's change our `PersonList` component -

`Containers/PersonList.js`
```
import { connect } from 'react-redux';
import { getSortedNames } from '../selectors/index.js';
// Import the function which we created just now in selector/index.js;

const mapStateToProps = (state) => {
  return {
   names: getSortedNames(state),
   // Change sortByName to getSortedNames
   cities: state.cities
  }
}

const mapDispatchToProps = (dispatch) => {
  return {
   addNewCity: (city) => {
      dispatch(addNewCity(city))
    }
  }
}

export default connect(mapStateToProps, mapDispatchToProps)(PersonList)

```

Now what happens is even if a new city is added and there is no change in the `names` or `filter` property and `mapStateToProps` is called again. The names array won't be calculated again because we have used a memoized selector. It will return the cached result.


Initially, when the component renders for the first time `mapStateToProps` is called for the first time and `getSortedNames` also gets called.  After that, It caches the result for `names`. So whenever the state tree changes and `getSortedNames` gets called, It will check if there is any change in the `names` or `filter`. If there is no change it will return the cached result hence saving time in recalculating the `names` array again. If there is a change it will be calculated again and that result will be cached. You can read more about 'Reselect' from [here](https://github.com/reduxjs/reselect).

That's it for this blog. 
Thank you for reading. 😃

Connect to me on [Twitter](https://twitter.com/apoorv_taneja), [Github](https://github.com/plxity) and [LinkedIn](https://www.linkedin.com/in/apoorvtaneja/) for more tech related stuff.

Happy Learning ⚡️

