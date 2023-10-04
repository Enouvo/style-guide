# Javascript Best Practice 

❌ Don't 
```javascript
import { cloneDeep } from 'lodash-es';

const cloneData = cloneDeep(data);
```

✅  Do 
```javascript
const cloneData = structuredClone(data);
```
