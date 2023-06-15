Here’s the full list of our tips and what to check to do a better React Code Review:

- Are there any **new *npm packages* added**?
- Check if there is no **functionality duplicates** like `date-fns` + `moment`.
- Also **check for imports**, as sometimes tree shaking is not working as you wish, and you could bundle the whole library and use just a single method like the below:

```
import _ from 'lodash';
//should became more precise import like:
import uniq from 'lodash/uniq';

```

- **If your app is using translations** – check if all new areas have also translations. If not, point that out and the developer should be aware of that in the future.

```
const NewComponent = () => {
  return (
    <div>
      New static text inside new component should be translated!
    </div>)
}

```

- **Check for missing or invalid types** if you are using TypeScript. All “**ANY**” types should also be fixed unless you have a really, really good explanation for not doing so. Below we have missing ***props types*** and ***any*** in the method.

```
const NewComponent = ({items, data}) => {
  const getItemId = (data: any) => data.id
  return (
    <div>
      {items.map(item => (
        <span key={getItemId(item)}>
          <h1>{item.title}</h1>
          <p>{item.description}</p>
        </span>))}
    </div>)
}
```

- **Check for variables, functions, and component names**. They should all declare what they are and what they do.
- **For boolean values, it’s good to have a prefix** `is/are/should` which declares their behaviour (`visible` => `isVisible`) and it will be harder to treat them as html properties.
- **Functions should declare what they do**, and if they return anything, they should have something like `get` – `getUsers`, if they are manipulating data, they should somehow tell what they are doing – `updateUsers` => `addUniqId`, `parseData` => `parseToAPIFormat` etc.
- **Check for weird logic patterns** (things you have never seen before). Sometimes when a developer takes too much time on a single task – they start to be really creative and create methods or flow that have no sense at all. You should help them here – to point that out and maybe help with a better solution.
- **Check for too complicated code chunks**. If someone is adding an ID into an array using 20 lines of code instead of 1, take some actions. Or when you are using some 3rd party packages like **lodash**, but the developer keeps writing all the methods by himself.
- **If you can’t understand what a specific chunk of code is doing** – we need to add a description comment there, or it’s just written incorrectly. In case the first option is viable – add a comment with a description. You can come back to this point in the future – and you still know what it does. If it’s incorrect – it needs fixing.
- **Check for hardcoded names, paths, and values**. Separate that kind of code, so you can easily change it in one place. Use paths instead. They are (in most cases) used in routing configuration and in every link and redirection. Also, separate types, date formats and everything that can be used in multiple places – to easily change them.
- **Check for backward compatibility issues** like changes in props from ***optional*** to ***required***. Or changes in some methods’ parameter types. If you made such a change with TypeScript – it should throw a compilation error. If you are using just JavaScript – you need to track that manually.
- **Check for code repetition**. If you’ve seen the same/similar logic in multiple places – point that out. Code should be reusable and if you will need to update that logic, you will have to update it in a single place. Not 3 of them.
- **Check for missing form validations** or incorrect form validations. I’ve never done an app that has a form without field validation.
- **Check for missing error handlers from API**. If a user receives 500 errors from API, will the user see a message with the correct info? Mostly about try/catch, and what is happening in a `catch` body?
- **Check for async methods** – can they be done in parallel, or do we need all the data in a sequence? Check if we actually wait for this data if we need it, or if we read from the promise object.
- **Sometimes you may notice potential bugs**. A big part of knowledge comes with experience. If you see something you’ve done in the past, but it caused errors – don’t make it happen again. Explain that you’ve been there, and you know the way out as you’ve made it work before.

# **COMMENTS IN REACT CODE REVIEW**

I think that a good way of segregating the comments is to categorize them.

For example, divide them into at least 3 groups:

- **MAJOR** – Comments that have a big impact on the code. They can break the app, create potential issues, don’t meet the criteria, have regression issues, etc. They are just comments that have to be fixed before merging.
- **MINOR** – In here we have some improvements – how we can make the code better and future-proof. Mostly about changing the implementation to a more readable code, more reusable or just better but won’t affect functionality (mostly) :). But if the developer has a good explanation about why it should stay this way – it’s fine to skip these.
- **OPTIONAL** – just syntax updates or something that won’t change the functionality at all. Like formatting issues or micro improvements.

Remember to communicate with your developer about the comments. That will speed up the process a lot.

Sometimes a simple *“Hi, I left a few comments in your PR, please let me know if you have any questions.”* is enough.

# **SUMMARY**

Remember – even if 10 people will review your code, it’s still your code, and you are responsible for it.

Setting up some rules will make cooperation much easier.

Don’t forget to point out good things too.

If you think that something is wrong, and you have an idea how to fix it – suggest that – that will speed the process up.

Don’t just add comments like *“change A to B”* – add a proper explanation of why it should be changed. For example: *“Please change the name from **“changeUserStatus”** to **“changeUserData”*** *as we are changing multiple fields in user – not just status.”*

And of course, be nice! There is no point in making the developer feel guilty, sad or worthless. Using correct language will change the sentence meaning like *“A to B”* – *“Can you change the name of A to B as it will be more readable”*. In other words, give a reason for each change.

Also, remember to communicate about the process status, whenever you want to discuss some solution, or you need some more answers.
