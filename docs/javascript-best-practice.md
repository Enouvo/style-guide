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
