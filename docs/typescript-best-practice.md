# Best practice when use Typescript

**1. Prefer `unknown` to `any`**

```tsx
{
  // 👎 Bad
  function main(value: any) {
    value();
  }

  // TS doesn't notice the error, and this code crashes at runtime
  main(1);
}

{
  function main1(value: unknown) {
    // ❌ Object is of type 'unknown'.
    value();
  }

  // 👍 Good
  function main2(value: unknown) {
    if (typeof value === 'function') {
      // ✅
      value();
    }
  }
}
```

**2. Don’t use non-primitive boxed objects**

```tsx
{
  // 👎 Bad
  function toString(num: Number) {
    return num.toString();
  }
}

{
  // 👍 Good
  function toString(num: number) {
    return num.toString();
  }
}
```

**3. Use constant enums whenever possible**

```tsx
{
  // 👎 Bad
  enum Enum {
    X,
    Y,
  }

  const x = Enum.X;
  console.log(x);

  // ✨ Compiled JavaScript code.
  // var Enum = void 0;
  // (function (Enum) {
  //   Enum[(Enum['X'] = 0)] = 'X';
  //   Enum[(Enum['Y'] = 1)] = 'Y';
  // })(Enum || (Enum = {}));
  // var x = Enum.X;
  // console.log(x);
}

{
  // 👍 Good
  const enum Enum {
    X,
    Y,
  }

  const x = Enum.X;
  console.log(x);

  // ✨ Compiled JavaScript code.
  // var x = 0; /* X */
  // console.log(x);
}
```

**4. Optimized with the latest features**

```tsx
{
  // Optional chaining (?.)
  // Deep property values can be read without having to check every reference for validity.
  interface Person {
    name?: string;
  }

  const p1: Person = {};

  // string | undefined
  const firstName = p1?.name;

  // ✨ Compiled JavaScript code.
  // var p1 = {};
  // var firstName = p1 === null || p1 === void 0 ? void 0 : p1.name;
}

{
  // Nullish coalescing operator (??)
  // Returns the right operand when the left operand is `null` or `undefined`, otherwise returns the left operand.
  interface Person {
    name?: string;
  }

  const p1: Person = {};

  // string
  const firstName = p1?.name ?? 'A';

  // ✨ Compiled JavaScript code.
  // var p1 = {};
  // var firstName = (_a = p1 === null || p1 === void 0 ? void 0 : p1.name) !== null && _a !== void 0 ? _a : 'A';
}
```

**5. Flexible use of advanced utility types**
```tsx
{
  interface PersonInfo {
    age: number;
    height: number;
  }

  type PersonName = 'A' | 'B';

  // ✨ Record<Keys, Type>
  const persons: Record<PersonName, PersonInfo> = {
    A: { age: 1, height: 2 },
    B: { age: 1, height: 2 },
  };

  // ✨ Omit<Type, Keys>
  const p1: Omit<PersonInfo, 'height'> = {
    age: 1,
  };

  // ✨ ReturnType<Type>
  const p2: ReturnType<() => PersonInfo> = {
    age: 1,
    height: 2,
  };

  // ...
}
```
