{
  "name": "build-you-a-js",
  "version": "0.1.0",
  "private": true
}

# build you a js, write everything from js in order to understand it

### .filter

```js

const filter = array=> predicate => {
  let result = [];
  for(let i=0; i<array.length; i++)
    predicate(array[i]) && result.push(array[i]);
    
  return result;
};
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
