# CSS Best Practice

**1. Use where to group tag**
```css
// ❌ Don't 
main h1, main h2, main h3 {
  color: orange 
}

// ✅  Do 
main :where(h1, h2, h3){
 color: orange
}
```

**2. Use is to group behavior**
```css
// ❌ Don't 
button:focus, button:hover {
  color: orange 
}

// ✅  Do 
button :is(focus, hover){
 color: orange
}
```
