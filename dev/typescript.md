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

## Type Guards (narrowing)
### as (type assertion)
- use only if necessary, type guards are better solution in most cases
- **be aware**: example of TS quirk [type guarding against null](https://stackoverflow.com/questions/57639697/typescript-type-guarding-against-null)
```TypeScript
const button = document.getElementById("og_btn") as HTMLButtonElement | null;
// outside of tsx
<HTMLButtonElement>document.getElementById("og_btn");

// non null assertion (!)
DoSomething(button!);
```

### typeof
- returns: `string`, `number`, `bigint`, `boolean`, `symbol`, `undefined`, `object` or `function`
- **be aware**: `null` is `object` (arrays and everything other then primitives is also `object`)
```TypeScript
if (typeof variable === "string") { /* narrow to string type */ }

```

### truthiness
- `0`, `NaN`, `""`, `0n`, `null` and `undefined` coerce to `false`
- **be aware**: empty string `""` will coerce to false, it might not be desired behaviour
```TypeScript
function printAll(strs: string | string[] | null) {
  if (strs && typeof strs === "object") {
    for (const s of strs) {
      // string[]
    }
  } else if (typeof strs === "string") {
    // string || ""
  }
}

// nullish coalescing operator (??): if left-hand side is null or undefined, return right-hand side (great for default values)
const nc = expression ?? 'whatever i want';
```

### equality
- **be aware**: loose equality `==` can be used to remove `null` and `undefined` at the same time
```TypeScript
function dumbFn(msg: string | null | undefined ) {
  if (msg != null) {
    // remove both 'null' and 'undefined' from the type.
  }
}
```

### in
- `property` in `object`
```TypeScript
type Employee = { something: () => void };
type Contractor = { anything: () => void };

function work(developer: Employee | Contractor) {
  if ("something" in developer) { ... }
}
```

### instanceof
```TypeScript
function work(developer: Employee | Contractor) {
  if (developer instanceof Contractor) { ... }
}
```

### is (type predicates)
- `parameter` is `Type`
- [assertion signatures](https://www.typescriptlang.org/docs/handbook/release-notes/typescript-3-7.html#assertion-functions)
```TypeScript
function isEmployee(developer: Employee | Contractor): developer is Employee {
  return (developer as Employee).something !== undefined;
}

// more useful example
function isString(x: unknown): x is string {
  return typeof x === 'string';
}
```

## Generics
- generics can infer type from passed runtime arguments [src](https://youtu.be/dLPgQRbVquo?t=264)
- use `extends` on function generics to put constraint (aka restrict) what can be passed in

### Arrays, Promises
```TypeScript
let arr: Array<number> = [1, 2, 3];
let promise: Promise<number> = getNumbers();
```

### Functions
```TypeScript
function someFunc<T, K extend keyof T>(p1: T, p2: K): T {}
const someFn = <T1, T2, T3>(p1: T1, p2: T2): T3 => {}
```

### Type Aliases
- example with default value for generic
```TypeScript
type ApiResponse<Data extends object = { status: number }> = {
  data: Data;
  message: string;
  doSomething(a: number): number;
};

type UserData = {
  id: number;
  name: string;
};

const res: ApiResponse<UserData> = {
  data: {
    id: 1,
    name: "user",
  },
  message: "msg",
  doSomething(a) {
    return a + a;
  },
};
```

### Interfaces
```TypeScript
// define property required in argument
interface Lengthwise {
  length: number;
}

function loggingIdentity<Type extends Lengthwise>(arg: Type): Type {
  console.log(arg.length); // use defined property
  return arg;
}
```

### keyof
- `keyof` operator takes an object type and produces a string or numeric literal union of its keys
```TypeScript
type Person = { developer: string; hired: boolean; salary: number };
type TK = keyof Person; // developer | hired | salary
type TV = Person[keyof Person]; // string | number | boolean
```

### typeof
```TypeScript
const arr = [{ developer: "amFrdWJ6", hired: true }, {...}];
type Person = typeof arr[number]; 
// type Person = { developer: string; hired: boolean; }
```

### conditional types
- **be aware**: optional properties are always treated as undefined

```TypeScript
type TypeNum = { id: number };
type TypeStr = { id: string };
type StrOrNum<Type extends number | string> = Type extends number
  ? TypeNum
  : TypeStr;

function getStrOrNum<Type extends number | string>(x: Type): StrOrNum<Type> {
  return { id: x } as StrOrNum<Type>;
}

// if object has property prop, return their type otherwise return never
type propOf<Type> = Type extends { prop: unknown } ? Type["prop"] : never;
type prop = propOf<{ prop: string }>;
//    ^? type X = string
```

```TypeScript
// example with infer
type Flatten<Type> = Type extends Array<infer Item> ? Item : Type;
type FlattenedType = Flatten<number | string[]>;
//    ^? type FlattenedType = string | number
```

```TypeScript
// work with optional props
type AddOptionalSuffix<Type> = Type extends { [Prop in keyof Type]: Type[Prop]; }
  ? {
    [Prop in keyof Type as `${Prop & string}${undefined extends Type[Prop]
      ? "Optional"
      : ""}`]: Type[Prop];
  }
: never;

// Distributive Conditional Types: conditional type will be applied to each member of that union
type Developer = { id: number; handsome?: boolean };
type Designer = { id: number; canCode?: boolean };
type OptPropsSuffix = AddOptionalSuffix<Developer | Designer>;
// type OptPropsSuffix = { ..., handsomeOptional?: ... } | { ..., canCodeOptional?: ... }
```

### mapped types
- modifiers: `-`, `+` for `readonly` and `?`
- remapping via `as`
```TypeScript
// recursively remove modifiers from object
type RemoveModifiers<T> = {
  -readonly [K in keyof T]-?: RemoveModifiers<T[K]>;
};

type ABTestSetting = {
  readonly id: string;
  readonly name: string;
  flags?: { 
    readonly flag: string; 
    state: boolean; 
    description?: string 
  };
};
type MutableABTest = RemoveModifiers<ABTestSetting>;
```

```TypeScript
// Key remapping via as
type AddCapOptPreffix<Type> = Type extends {
  [Prop in keyof Type]: Type[Prop];
}
  ? {
    [Prop in keyof Type as `${undefined extends Type[Prop]
      ? "optional"
      : ""}${Capitalize<Prop & string>}`]: Type[Prop];
  }
: never;
```

```TypeScript
// example with utility types
type RemoveProps<Type> = {
[Prop in keyof Type as Exclude<Prop, "id" | "salary">]: Type[Prop]
};
type Emp = {
  id: number;
  name: string;
  position: string;
  team: string;
  salary: number;
};
type E = RemoveProps<Emp>;
// type E = { name: string; position: string; team: string }
```

### Utility Types
#### Awaited<Type>
- Recursively unwraps Promises and returns their return type
```TypeScript
type A = Awaited<Promise<string>>;
// type A = string
type B = Awaited<Promise<Promise<number>>>;    
// type B = number
type C = Awaited<boolean | Promise<number>>;
// type C = number | boolean
```

#### Partial<Type>
- Constructs a type with all properties of Type set to optional
```TypeScript
type Original = { id: number };
type Optional = Partial<Original>;
// type Optional = { id?: number | undefined 
```

#### Required<Type>
- Constructs a type consisting of all properties of Type set to required
```TypeScript
type Original = { id?: number };
type Optional = Required<Original>;
// type Optional = { id: number }
```

#### Readonly<Type>
- Constructs a type with all properties of Type set to readonly
```TypeScript
type Original = { id: number };
type Optional = Readonly<Original>;
// type Optional = { readonly id: number }
```

#### Record<Keys, Type>
- Constructs an object type whose property keys are Keys and whose property values are Type (all defined TKeys has to be present in object)
```TypeScript
type TValue = { id: number; isDev: boolean };
type TKey = "amFrdWJ6" | "doggo";
const obj: Record<TKey, TValue> = {
  amFrdWJ6: { id: 0, isDev: true },
  doggo: { id: 1, isDev: false },
};
obj.amFrdWJ6;
```

#### Pick<Type, Keys>
- Constructs a type by picking the set of properties Keys (string literal or union of string literals) from Type.
```TypeScript
type Emp = { id: number; developer: string; isHired: boolean };
type HiredDevs = Pick<Emp, "id" | "developer">;
// type HiredDevs = { id: number; developer: string; }
```

#### Omit<Type, Keys>
- Constructs a type by picking all properties from Type and then removing Keys (string literal or union of string literals)
```TypeScript
type Emp = { id: number; developer: string; isHired: boolean };
type Devs = Omit<Emp, "id" | "isHired">;
// type Devs = { developer: string; }
```

#### Exclude<UnionType, ExcludedMembers>
- Constructs a type by excluding from UnionType all union members that are assignable to ExcludedMembers
```TypeScript
type T = Exclude<string | number | (() => void), Function>;
// type T = string | number
```

#### Extract<Type, Union>
- Constructs a type by extracting from Type all union members that are assignable to Union
```TypeScript
type T = Extract<string | number | (() => void), Function>;
// type T = () => void
```

#### NonNullable<Type>
- Constructs a type by excluding null and undefined from Type
```TypeScript
type T = NonNullable<string[] | number | null | undefined>;
// type T = number | string[]
```

#### Parameters<Type>
- Constructs a tuple type from the types used in the parameters of a function type Type
```TypeScript
// TODO
```

#### ConstructorParameters<Type>
- TODO
```TypeScript
// TODO
```

#### ReturnType<Type>
- Constructs a type consisting of the return type of function Type
```TypeScript
type T = ReturnType<() => string>;
// type T = string
type U = ReturnType<<X extends Y, Y extends number[]>() => X>;
// type U = number[]
```

#### InstanceType<Type>
- TODO
```TypeScript
// TODO
```

#### ThisParameterType<Type>
- TODO
```TypeScript
// TODO
```

#### OmitThisParameter<Type>
- TODO
```TypeScript
// TODO
```

#### ThisType<Type>
- TODO
```TypeScript
// TODO
```

#### Uppercase, Lowercase, Capitalize, Uncapitalize
- used with Template Literal Types

### TS upcoming
- [using](https://github.com/tc39/proposal-explicit-resource-management/commits/main/)