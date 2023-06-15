# Frontend Review CheckList

## Variable, File, and Directory Names Are Appropriate and Meaningful

Depending on what kind of naming convention you follow, any new addition of variable, file or directory should adhere to that. You should also ensure that the name is making sense. For example:

`const firstName;`
is a better variable than:

`const fN;`
Take special note of naming parameters inside of methods such as each, map, filter etc.
```javascript
{
  users.map(user => <span>{user.firstName}</span>)
}
```
Here user is a way more informative name than:
```javascript
{
  users.map(item => <span>{item.firstName}</span>)
  // OR
  users.map(i => <span>{i.firstName}</span>)
}
```
Similarly, an informative and to-the-point directory and file name are always self-documenting and easier to reason about for others. E.g.:
```javascript
// /configJsonFiles
is more informative than

// /jsonFiles

// OR worse

// /files
```
