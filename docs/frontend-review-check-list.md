# Frontend Review CheckList
Some rules mentioned below can be automatically checked using ESLint and tsconfig. We will attempt to list the rules that cannot be automatically checked. Please refer to [eslint-config-react](https://github.com/Enouvo/eslint-config-react) for more information on additional rules.
## Naming convention
### Follow S-I-D best practices
  - **Short**: must not take long to type and remember
  - **Intuitive**: must be read naturally, as close to the common speech as possible
  - **Descriptive**: must reflect what it does/possesses in the most efficient way
  ```javascript
    /* Bad */
  const a = 5 // "a" could mean anything
  const isPaginatable = a > 10 // "Paginatable" sounds extremely unnatural
  const shouldPaginatize = a > 10 // Made up verbs are so much fun!

  /* Good */
  const postCount = 5
  const hasPagination = postCount > 10
  const shouldPaginate = postCount > 10 // alternatively
  ```
- Avoid contractions, when they decrease readability of your code. Finding a short, descriptive name could be hard, but contractions is not an excuse for not doing so
```javascript
/* Bad */
function getUsrNme() {
 // ...
}

/* Good */
function getUserName() {
// ...
}
```
- Avoid context duplication, name should not duplicate the context in which it is defined. Always remove the context from a name if that doesn’t decrease its readability
```javascript
class EducationService {
 /* Bad: Method name duplicates the context (which is "EducationService") */
 getEducationCertificate(event) {
 // ...
 }

 /* Good:Reads nicely as `EducationService.getCertificate()` */
 getCertificate(event) {
 // ...
 }
}
```
- Reflect the expected output
```javascript
/* Bad */
const isEnabled = itemCount > 3
if(!isEnabled) {
 // ...
}

/* Good */
const isDisabled = itemCount <= 3
if(isDisabled) {
 // ...
}
```
### Folder Name
  - All folders should be named using **camelCase**
  - All folders of specific categories should be named as plurals
      - components*, enums, utils, services, models, contexts…*
### File Name
  - All files should be named using **camelCase** except **entities ( PascalCase )**
  - All files under one specific category folder should be named with post-fix **{specificCategoryName}** in the end
    - **components**: *Header.**components**.ts*
    - **decorators**: *header.**decorator**.ts*
    - **guards**: *global.**guard**.ts*
    - **handers**: *apiServer.**handler**.ts*
    - **contexts**: *company.**context**.ts*
    - **services**: *s3.**service**.ts*
    - **utils**: *date.**util**.ts*
    - **validators**: *contractValuatiion.**validator**.ts*
    - **models**: *user.**model**.ts*
    - **interfaces/dto** *user.**interface**.ts* or *user.**dto**.ts*
    - **resolvers**: contractValuation.**resolver**.ts
    - …
### CONST Variables for Repeated String Literals
If a string literal is being used constantly throughout the file, it’s a candidate for a const variable at the top. For example:
```javascript
if(user.instituteType === "school"){

}

// ...

const schoolGoing = users.map(u=>u.instituteType === "school");

// ...

{
  user.instituteType === "school"? <div>School</div>: null
}
```
The above could be changed to:
```javascript
const SCHOOL = "school";

if(user.instituteType === SCHOOL){

}

// ...

const schoolGoing = users.map(u=>u.instituteType === SCHOOL);

// ...

{
    user.instituteType === SCHOOL? <div>School</div>: null
}
```

### Spelling and Grammar Mistakes
Although not an English writing contest, for the sake of better readability and searchability, there should be minimal spelling errors in your variable, file, and directory names, and also in your static HTML text. Some examples:

```javascript
// misspelled variable names
const lable, univresity, schoolGongChildren, multPlayer, caculation;

// misspelled directory and file names
// /resorces /configration helpre.js

// grammatically incorrect HTML static text
<span>Your welcome</span>
```
One of the benefits of writing spelling and grammar mistake-free code is the ability to find something in the codebase with ease. You won’t have to waste time searching for the file “helper.js” and getting back “no results found”.

If you’re using visual studio code, you can install Code Spell Checker extension.


### Variable, File, and Directory Names Are Appropriate and Meaningful

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

## Code Style Guide

### Destructuring
Whether you’re importing different methods of a package or using props values, try to destructure your es6 code for cleanliness:

```javascript
import _ from "lodash";

// ....

_.forEach(
  //...
)
_.filter(
  //...
)
```

To

```javascript
import {forEach, filter} from "lodash";

// ....

forEach(
  //...
)
filter(
  //...
)
```
Similarly:

```javascript
const UserInfo = (props) =>
(<div>
  <div>
    First Name: {props.firstName}
  </div>
  <div>
    Second Name: {props.secondName}
  </div>
</div>)
```

To

```javascript
const UserInfo = ({
  firstName,
  lastName
}) =>
(<div>
  <div>
    First Name: {firstName}
  </div>
  <div>
    Second Name: {secondName}
  </div>
</div>)
```



### Methods/Functions
- Keep it short. A good function fits on a slide that people in the last row of a big room can comfortably read

- Return early from functions, to avoid deep nesting of if-statements
```javascript
// Bad 
function isPercentage(val) {
  if (val >= 0) {
    if (val < 100) {
      return true;
    } else {
      return false;
    }
  } else {
    return false;
  }
}

// Good
function isPercentage(val: number): boolean {
  if (val < 0 || val > 100) {
    return false;
  }

  return true;
} 

// Better
function isPercentage(val: number): boolean {
  const isInRange = val >= 0 && val <= 100;
  
  return isInRange; 
}
```
## Addition of New Package(s)
React applications, like others, are built on top of so many other useful packages/libraries. In an active development, you still need to add new packages. While code reviewing, pay special attention to the changes in package.json file. Consider the following points:

Is the new package absolutely necessary?
Is the new package rightly listed under “dependencies” or “devDependencies”?
The npm profile page for the library shows healthy downloads per week and frequent releases of new versions (a package with no new release for over a year is a red sign).
The license of the package is compatible with your needs. If the license is ISC or MIT, you’re probably good to go.


## TO BE DEFINED AND UPDATED CONSTANTLY

## References

For more best practices and conventions.

- [Airbnb React/JSX Style Guide](https://airbnb.io/javascript/react/#basic-rules)
- [Google JavaScript Style Guide](https://google.github.io/styleguide/jsguide.html)
- [ReactJS Code Review](https://www.techighness.com/post/react-js-code-review-checklist/)
