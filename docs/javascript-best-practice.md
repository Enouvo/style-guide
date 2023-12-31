# Javascript Best Practice 

**1. Use structuredClone to deep clone data**

```javascript
// ❌ Don't 
import { cloneDeep } from 'lodash-es';

const cloneData = cloneDeep(data);

// ✅  Do 
const cloneData = structuredClone(data);
```

**2. Use finally to remove duplication**

```javascript
// ❌ Don't 
const countNumberOfThings = things => {
  if (things) {
    logEvent()
    return null
  }
  if (things.length > 10) {
    logEvent()
    return many!
  }
  logEvent()
  return things.length
}

// ✅  Do
const countNumberOfThings = things => {
  try {
    if (things) {
      return null
    }
    if (things.length > 10) {
      return many!
    }
    return things.length
  } finally {
    logEvent()
  }
}
```

**3. Use extend to remove duplication property on class**
```javascript
// ❌ Don't
class Department {
  get totalAnnualCost() {...}
  get name() {...}
  get headCount() {...}
}

class Employee {
  get annualCost() {...}
  get name() {...}
  get id() {...}
}

// ✅  Do
class Party {
  get name() {...}
  get annualCost() {...}
}

class Department extends Party {
  get annualCost() {...}
  get headCount() {...}
}

class Employee extends Party {
  get annualCost() {...}
  get id() {...}
}
```
**4. Create a function with single responsibily**
```javascript
// Don't ❌
function createFile(name, isPublic) {
  if (isPublic) {
    fs.create(`./public/${name}`);
  } else {
    fs.create(name);
  }
}

// Do ✅
function createFile(name) {
  fs.create(name);
}

function createPublicFile(name) {
  createFile(`./public/${name}`);
}
```
**5. Use return first **
// Don't ❌
let label = null

if(user){
  label = user.getFullName()
} else if(product){
  label = product.getName()
}

// Do ✅
const label = (() => {
  if(user) return user.getFullName()
  if(product) return product.getName()
  return null
})()
```

