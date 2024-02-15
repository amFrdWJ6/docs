# TypeScript

## Docs
- [TypeScript.org](https://www.typescriptlang.org/)
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)

### Useful links
- [typehero.dev](https://typehero.dev/)
- [tsdoc.dev: type documentation for npm packages](https://tsdocs.dev/)
- [TotalTypeScript](https://www.totaltypescript.com/)
- [JavaScript.info](https://javascript.info/)
- [Do's & Don'ts](https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html)

## Basics
### Variables
`var`, `let` & `const`

```TypeScript
var a   = 'A'; // function || global scope
let b   = 'B'; // block scope
const c = 'C'; // block scope; cannot change reference, but internal state is mutable
```

### Types
#### Primitives
- `string`, `number`, `bigint`, `boolean`
- `undefined`, `null`
- [`symbol`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Symbol): a primitive type for unique identifiers
```TypeScript
let happiness: boolean; // type annotation
const name = "string"; // infered as string
```

#### Other
- `any`: effectively turns off type checking, avoid it
- `unknown`: use instead of `any`, use type guards for narrowing
- `never`: when throwing error or narrowing types to point, where options were exhausted
- `void`

#### Aliases, Interface, Union
```TypeScript
type TypeAlias = {
  mutable: string;
  readonly immutable: string;
  unionString: string | string[];
  optional?: string;
};

interface MCFaceInter {
  // pretty much same as type alias, but:
  // - interface can describe only object shapes
  // - interface is easily extendable (type aliases only via intersections)
}

// The Discriminated Union
type A = {
  commonProperty: "A";
  A_specificProperty: string;
}

type B = {
  commonProperty: "B";
  B_uniqueProperty: string;
}

function switchDiscriminatedUnion(param: A | B) {
  switch (param.commonProperty) {
    case "A":
      return param.A_specificProperty;
    case "B":
      return param.B_uniqueProperty;
    default:
      const _never: never = param;
      return _never;
  }
}
```

### Arrays, Tuples, Maps/Sets
- prefer Map/Set before object/arrays (performance, safety, non-string key, order preserved, uniqueness)
```TypeScript
const myArr = Array<string>; // or string[];
let myTuple = [string, number]; // array with predefined length and types

let myMap = new Map<number, string>([
  [1, 'first'], [2, 'second']
]);
// methods: .set(), .get(), .has(), .delete(), .clear(), .size
// iter: myMap.keys() || .values() || .entries()
let mapFromObject = new Map(Object.entries({'a': 1}));
let objectFromMap = Object.fromEntries([
  [1, 'first'], [2, 'second']
]);

let mySet = new Set<number>([1, 2, 3, 3]) // .size === 3
// methods: .add(), .delet(), .has(), .clear(), .size
// iter: for..of (same as Map) || .forEach()
```

### Functions
```TypeScript
async function fnName(a: <type || type alias>): <return type> {}
let arrowFn = async (a: <type || type alias>): <return type> => {}
let anonFn = function (a: <type || type alias>): <return type> {}
```

### Enums
- provide explicit `string` values for `enum`s
- enum does not exists in JavaScript
```TypeScript
enum AccountRole {
  Guest = "guest",
  Member = "member",
  Admin = "admin",
};

const isAdmin = (user.role === AccountRole.Admin);
```
