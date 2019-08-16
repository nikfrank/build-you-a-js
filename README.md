# build you a js, write everything from js in order to understand it

to master each of the features we use in js, we will implement their API from primitives

then you'll understand how to use them better!


### .forEach

here I'll use curried functions instead of prototype lexical scoping

```js
const forEach = array=> callback => {
  for(let i=0; i<array.length; i++)
  callback(array[i], i, array);
};

forEach([1, 2, 3], n => console.log(n));
// log: 1, log: 2, log: 3
```




### .map

here I'll use curried functions instead of prototype lexical scoping

```js
const map = array=> mapping => {
  let result = [];
  for(let i=0; i<array.length; i++)
    result.push( mapping(array[i], i, array) );
    
  return result;
};

map([1, 4, 9])( x => x ** 1.5 ); // [1, 8, 27]
```




### .filter

here I'll use curried functions instead of prototype lexical scoping

```js
const filter = array=> predicate => {
  let result = [];
  for(let i=0; i<array.length; i++)
    predicate(array[i], i, array) && result.push(array[i]);
    
  return result;
};

filter([1, 2, 3, 4, 8])( x => !~(''+Math.log2(x)).indexOf('.') )
// [1, 2, 4, 8]
```


### .reduce

here I'll use curried functions instead of prototype lexical scoping

```js
const reduce = array=> (reducer, accumulator) => {
  
  for(let i=0; i<array.length; i++)
    accumulator = reducer( accumulator, array[i], i, array );
    
  return accumulator;
};

reduce([1, 4, 9])( (a, x) => a + x ** 1.5, 0 ); // 36
```



### Promisify

```js
const promisify = apiWithNodeCallback => (...args)=>
  (new Promise((resolve, reject)=>

    apiWithNodeCallback( ...args.slice(0, -1), (err, res)=>
      err ? reject(err) : resolve(res)
    )

  ));
```



### Promise

```js
const Promise = thunk=> {
  let callbacks;

  const p = {
    then: callback => (callbacks.push({ then: callback }), p),
    catch: callback => (callbacks.push({ catch: callback }), p),
  };
  
  const runCbs = next => v => {
    for(let i=0; i<callbacks.length; i++){
      if( next in callbacks[i] ){
        try {
          v = callbacks[i][state](v);
          next = 'then';
          
          // if v is a promise, runCbs on its callbacks
          
        } catch(e) {
          v = e;
          next = 'catch';
        }
      }
    }
    
    if( next === 'catch' ){
      console.error( v );
      throw 'Exception Unhandled in Promise';
    }
  };
  
  thunk(runCbs('then'), runCbs('catch'));
}
```



This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

