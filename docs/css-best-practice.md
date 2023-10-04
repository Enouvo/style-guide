# CSS Best Practice

**1. Use where to group tag**
```javascript
// ❌ Don't 
main h1, main h2, main h3 {
  color: orange 
}

// ✅  Do 
main :where(h1, h2, h3){
 color: orange
}
```
