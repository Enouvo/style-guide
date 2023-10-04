# React Best Practice 

**1. We may not need to put your `state` as a dependency**
```javascript
// ❌ Don't 
function FooComponent(){
  const [count, setCount] = useState(0);

  const increase = useCallback(() => setCount(count + 1), [count]);
  
  return <div>Count: {count}</div>
}

// ✅  Do 
function FooComponent(){
  const [count, setCount] = useState(0);

  const increase = useCallback(() => setCount(count => count + 1), []);
  
  return <div>Count: {count}</div>
}
```

