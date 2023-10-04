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

**2. Prefer use if instead of nested ternary operator**
```javascript
// ❌ Don't 
render: (_, record) => {
	return (
		<div>
			{record.projectStatus.name === 'Published' ? (
				<b className="c-yellow">{record.projectStatus.name}</b>
			) : record.projectStatus.name === 'Started' ? (
				<b className="c-secondary-blue">{record.projectStatus.name}</b>
			) : record.projectStatus.name === 'Completed' ? (
				<b className="c-primary">{record.projectStatus.name}</b>
			) : (
				<b className="c-warning">{record.projectStatus.name}</b>
			)}
		</div>
	);
}

// ✅  Do 
const STATUS = {
	Published: 'Published',
  Started: 'Started',
  Completed: 'Completed'
}

render: (_, record) => {
  const name = record.projectStatus.name;
  const textClass = (() => {
    if (name === STATUS.Published) return 'c-yellow';
    if (name === STATUS.Started) return 'c-secondary-blue';
		if (name === STATUS.Completed) return 'c-primary'
    return 'c-warning';
  })();
  return <b className={textClass}>{name}</b>;
};
```

**3. Don't create a nested component**
```javascript
// ❌ Don't 
const Form = () => {
  const Input = (props) => <input type='text' {...props} />
  return (
    <>
        <Input
          key={index}
          value={value}
          onChange={(e) => onChange(e.target.value, index)}
        />
    </>
  );
};

// ✅  Do 
const Input = (props) => <input type='text' {...props} />

const Form = () => {
  return (
    <>
        <Input
          key={index}
          value={value}
          onChange={(e) => onChange(e.target.value, index)}
        />
    </>
  );
};
```
