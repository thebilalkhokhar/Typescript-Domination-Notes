# ✅ **1. Primitive Types vs Reference Types**

### **Primitive Types**

Ye values **directly memory me store** hoti hain. Inki copying by _value_ hoti hai.

Primitive types:

- **number**
- **string**
- **boolean**
- **bigint**
- **symbol**
- **null**
- **undefined**

👉 Primitive immutable hote hain — value change nahi hoti, balkay new value create hoti hai.

---

### **Reference Types**

Ye values **memory ke alag block me store** hoti hain. Variable me **reference/pointer** store hota hai.

Reference types:

- **object**
- **array**
- **function**
- **class instances**

👉 Copy by _reference_ hoti hai — yani dono variables same memory ko point karte hain.

---

# ✅ **2. Primitive Types in TS**

### **number**

All numeric values:

```ts
let age: number = 23;
let price: number = 199.99;
```

### **string**

Text values:

```ts
let name: string = "Bilal";
```

### **boolean**

True/false:

```ts
let isAdmin: boolean = false;
```

---

# ✅ **3. Array**

Array type define karne ke do tareeqe:

```ts
let nums: number[] = [1, 2, 3];

let names: Array<string> = ["Ali", "Bilal"];
```

---

# ✅ **4. Tuple**

Tuple = Fixed length + fixed type order

```ts
let user: [string, number] = ["Bilal", 23];
```

Order matter karta hai.

---

# ✅ **5. Enum**

Enum ka use values ko named constants dene ke liye hota hai.

```ts
enum Role {
  ADMIN,
  USER,
  GUEST,
}

let r: Role = Role.ADMIN;
```

Custom values bhi dein:

```ts
enum Status {
  SUCCESS = 200,
  NOT_FOUND = 404,
}
```

---

# ✅ **6. any**

`any` => Type checking band
**Dangerous**, but kabhi kabhi zaruri.

```ts
let data: any = 10;
data = "hello";
data = true;
```

---

# ✅ **7. unknown**

`unknown` safer alternative to `any`

Tum isko **pehle check kiye baghair use nahi** kar sakte.

```ts
let value: unknown;

value = "Bilal";

if (typeof value === "string") {
  console.log(value.toUpperCase()); // OK
}
```

---

# ✅ **8. null**

Intentional empty value:

```ts
let empty: null = null;
```

---

# ✅ **9. undefined**

Value assigned nahi hui:

```ts
let x: undefined = undefined;
```

---

# ✅ **10. void**

Functions that return **nothing**

```ts
function logMessage(msg: string): void {
  console.log(msg);
}
```

---

# ✅ **11. never**

Function **kabhi return nahi karta**

### Examples:

❌ always throws error
❌ infinite loop

```ts
function error(msg: string): never {
  throw new Error(msg);
}

function loopForever(): never {
  while (true) {}
}
```

---

# 📌 Quick Comparison Table (Super Helpful)

| Type          | Description                |
| ------------- | -------------------------- |
| **number**    | numeric values             |
| **string**    | text                       |
| **boolean**   | true/false                 |
| **array**     | list of same type values   |
| **tuple**     | fixed type + fixed length  |
| **enum**      | named constants            |
| **any**       | disable type checking      |
| **unknown**   | safer-any, must check type |
| **null**      | intentional empty          |
| **undefined** | unassigned                 |
| **void**      | no return                  |
| **never**     | never returns              |

---

---

# ⭐ 1. **Type Inference**

TypeScript khud se type **guess** kar leta hai, jise type inference kehte hain.

### Example:

```ts
let age = 23;
```

TS khud samajh jata hai:

```ts
// inferred as:
let age: number;
```

### Functions me inference:

```ts
function add(a: number, b: number) {
  return a + b; // return type inferred: number
}
```

### Kab inference fail hota hai?

```ts
let data; // data: any (dangerous)
```

Jab variable without value declare hota hai → TS gives it `any`.

---

# ⭐ 2. **Type Annotations**

Type ko manually specify karna = Type Annotation.

### Example:

```ts
let username: string = "Bilal";
let isAdmin: boolean = false;
let score: number = 99;
```

### Functions annotation:

```ts
function greet(name: string): string {
  return "Hello " + name;
}
```

### When to use annotations?

✔ Value clear nahi
✔ Function parameters
✔ APIs se unknown response
✔ Complex objects (interfaces, types)

---

# ⭐ 3. **Interfaces**

Interface ka use **objects ke structure define karne** ke liye hota hai.

### Simple example:

```ts
interface User {
  id: number;
  name: string;
  isAdmin: boolean;
}

const bilal: User = {
  id: 1,
  name: "Bilal",
  isAdmin: false,
};
```

### Optional Properties (`?`)

```ts
interface Product {
  name: string;
  price: number;
  description?: string; // optional
}
```

### Readonly Properties

```ts
interface Car {
  readonly id: string;
  model: string;
}

const c: Car = { id: "A1", model: "Civic" };
// c.id = "B2"; ❌ error
```

### Functions inside interface

```ts
interface Person {
  name: string;
  speak(msg: string): void;
}

const p: Person = {
  name: "Ali",
  speak(msg) {
    console.log(msg);
  },
};
```

### Interface for Functions

```ts
interface SumFunc {
  (a: number, b: number): number;
}

const add: SumFunc = (x, y) => x + y;
```

---

# ⭐ Interface vs Type Alias (Quick 10-second clarity)

| Feature    | Interface            | Type Alias                          |
| ---------- | -------------------- | ----------------------------------- |
| Extendable | ✔ Yes (best for OOP) | ✔ Yes (but limited)                 |
| Merge-able | ✔ Yes                | ❌ No                               |
| Use-case   | Objects, classes     | Anything (union, tuple, primitives) |

Example merging (only interface):

```ts
interface A {
  x: number;
}
interface A {
  y: number;
}

const obj: A = { x: 1, y: 2 };
```

---

# ⭐ A small combined example (Inference + Annotations + Interface)

```ts
interface User {
  id: number;
  name: string;
  isAdmin?: boolean;
}

function createUser(name: string): User {
  return {
    id: Date.now(), // inferred number
    name, // inferred string
    isAdmin: false, // explicit boolean
  };
}

const u = createUser("Bilal");
```

TS khud inference karta hai but hum annotations se intent clear karte hain.

---

---

# ⭐ 1. **Type Aliases**

Type Alias = Kisi bhi type ko **custom naam** dena.
Primitive, array, object, function—kuch bhi type bana sakte ho.

### Basic Example:

```ts
type ID = number;
let userId: ID = 123;
```

### Object Type Alias:

```ts
type User = {
  id: number;
  name: string;
};
```

### Function Type Alias:

```ts
type Add = (a: number, b: number) => number;

const sum: Add = (x, y) => x + y;
```

Type aliases are more flexible than interfaces because these can hold **any type**, not just objects.

---

# ⭐ 2. **Extending Interfaces**

Interface extend karna = inheritance jaise.

### Example:

```ts
interface User {
  id: number;
  name: string;
}

interface Admin extends User {
  role: string;
}

const a: Admin = {
  id: 1,
  name: "Bilal",
  role: "super-admin",
};
```

✔ Reusability
✔ OOP-style structure
✔ Best for defining object models

---

# ⭐ 3. **Fundamentals of Type Aliases**

Type aliases ka power =
You can define:

✔ primitives
✔ objects
✔ functions
✔ tuples
✔ union
✔ intersection
✔ literal types
✔ anything

### Tuple alias:

```ts
type Point = [number, number];
const p: Point = [10, 20];
```

### Literal type alias:

```ts
type Status = "pending" | "success" | "failed";
let current: Status = "success";
```

### Object + optional + readonly:

```ts
type Product = {
  readonly id: number;
  name: string;
  price?: number;
};
```

---

# ⭐ 4. **Union Types**

Union = **multiple possible types**
(OR logic)

```ts
let value: number | string;

value = 10;
value = "Bilal";
```

### Union in type alias:

```ts
type ID = number | string;
let uid: ID = "xyz123";
```

### Union with objects:

```ts
type Dog = { bark: () => void };
type Cat = { meow: () => void };

type Pet = Dog | Cat;
```

👉 Must check before using (narrowing required):

```ts
function speak(pet: Pet) {
  if ("bark" in pet) pet.bark();
}
```

---

# ⭐ 5. **Intersection Types**

Intersection = combine types
(AND logic)

```ts
type A = { a: number };
type B = { b: string };

type C = A & B;

const obj: C = { a: 1, b: "hello" };
```

👉 Ye **merge** karta hai.

### Real example: User + Timestamps

```ts
type User = { id: number; name: string };
type Timestamps = { createdAt: Date; updatedAt: Date };

type UserWithDates = User & Timestamps;
```

---

# ⭐ Union vs Intersection (Crystal Clear)

| Feature  | Union (`                  | `)                           | Intersection (`&`)     |
| -------- | ------------------------- | ---------------------------- | ---------------------- |
| Logic    | OR                        | AND                          |
| Meaning  | Value can be any one type | Value must satisfy all types |
| Example  | `number                   | string`                      | `{a} & {b}` → `{a, b}` |
| Use Case | Flexible inputs           | Combine models               |

---

# ⭐ Interface Extension vs Intersection

| Task                     | Interface Extend | Intersection Type      |
| ------------------------ | ---------------- | ---------------------- |
| Object inheritance       | ✔ Best           | ✔ Works                |
| Combine multiple objects | ✔                | ✔                      |
| Merge non-object types   | ❌               | ✔                      |
| Avoid conflicts          | ✔ safer          | ❌ can cause conflicts |

Example conflict in intersection:

```ts
type A = { x: number };
type B = { x: string };
type C = A & B; // ❌ x: never
```

---

# ⭐ Mini Practical Example (All concepts together)

```ts
// Base Interface
interface User {
  id: number;
  name: string;
}

// Extended Interface
interface Admin extends User {
  permissions: string[];
}

// Union Type
type UserType = "user" | "admin";

// Intersection Type
type Timestamped = {
  createdAt: Date;
  updatedAt: Date;
};

// Type Alias combining everything
type FullAdmin = Admin & Timestamped;

const bilal: FullAdmin = {
  id: 1,
  name: "Bilal",
  permissions: ["read", "write"],
  createdAt: new Date(),
  updatedAt: new Date(),
};
```

This uses:
✔ Interfaces
✔ Interface Extending
✔ Type Alias
✔ Intersection
✔ Union

Perfect real-world TS structure.

---

---

# ⭐ 1. **Introduction to Classes & Objects**

### **Class**

Blueprint/template hota hai jisme:

- properties
- methods
- constructors
- access modifiers
- logic

define hota hai.

### **Object**

Class ka actual instance (copy).

### Example:

```ts
class User {
  name: string = "Bilal";
  age: number = 23;

  greet() {
    console.log("Hello " + this.name);
  }
}

const u1 = new User();
u1.greet();
```

---

# ⭐ 2. **Fundamentals of Classes & Objects**

Class ke main parts:

- properties
- methods
- constructor
- `this` keyword
- access modifiers

---

# ⭐ 3. **Constructor**

Constructor tab run hota hai jab class ka object create hota hai.

```ts
class Car {
  brand: string;
  model: string;

  constructor(brand: string, model: string) {
    this.brand = brand;
    this.model = model;
  }
}

const c1 = new Car("Honda", "Civic");
```

---

# ⭐ 4. **this keyword**

`this` → current object ko refer karta hai.

```ts
class Student {
  name: string;

  constructor(name: string) {
    this.name = name; // this = object
  }

  intro() {
    console.log("I am " + this.name);
  }
}

const s = new Student("Bilal");
s.intro();
```

---

# ⭐ 5. **Public & Private Access Modifiers**

### **public** (default)

Har jagah accessible.

```ts
class User {
  public name: string = "Ali"; // optional 'public'
}
```

### **private**

Sirf class ke andar access.

```ts
class BankAccount {
  private balance: number = 0;

  deposit(amount: number) {
    this.balance += amount;
  }
}

const acc = new BankAccount();
// acc.balance ❌ ERROR
acc.deposit(100); // OK
```

---

# ⭐ 6. **Protected Access Modifier**

`protected` class ke andar + subclasses me accessible hota hai.

```ts
class Person {
  protected id: number = 101;
}

class Employee extends Person {
  showId() {
    console.log(this.id); // OK (protected allowed in child)
  }
}

const e = new Employee();
// e.id ❌ NOT accessible outside
```

---

# ⭐ 7. **Optional Properties**

Properties jo hon bhi sakti hain aur nahi bhi.

```ts
class User {
  name: string;
  age?: number; // optional

  constructor(name: string, age?: number) {
    this.name = name;
    this.age = age;
  }
}

const u1 = new User("Bilal");
const u2 = new User("Ali", 23);
```

---

# ⭐ 8. **Parameter Properties**

Constructor parameters ko directly property banane ka shortcut.

Instead of:

```ts
class User {
  name: string;

  constructor(name: string) {
    this.name = name;
  }
}
```

Shortcut:

```ts
class User {
  constructor(public name: string) {}
}

const u = new User("Bilal");
```

Works with:

- public
- private
- protected
- readonly

Example:

```ts
class Product {
  constructor(
    private id: number,
    public title: string,
    protected price: number
  ) {}
}
```

---

# ⭐ 9. **Getters & Setters**

Getter → property ko read karne ka safe way
Setter → restricted write logic

```ts
class Employee {
  private _salary: number = 0;

  get salary() {
    return this._salary;
  }

  set salary(amount: number) {
    if (amount < 0) {
      throw new Error("Invalid salary");
    }
    this._salary = amount;
  }
}

const e = new Employee();
e.salary = 50000;
console.log(e.salary);
```

✔ Controlled access
✔ Validation
✔ Clean syntax

---

# ⭐ 10. **Static Members**

Static ⇒ class-level property/method
Ye object par nahi, class par directly call hota hai.

```ts
class MathUtil {
  static PI = 3.14;

  static square(num: number) {
    return num * num;
  }
}

console.log(MathUtil.PI);
console.log(MathUtil.square(5));
```

Object banane ki zarurat nahi.

---

# ⭐ 11. **Abstract Classes**

Abstract = incomplete class
→ Directly object nahi banta
→ Must be extended
→ Abstract methods ko child class implement karta hai

```ts
abstract class Shape {
  abstract area(): number; // no body
}

class Circle extends Shape {
  constructor(public radius: number) {
    super();
  }

  area(): number {
    return Math.PI * this.radius * this.radius;
  }
}

const c = new Circle(5);
console.log(c.area());
```

✔ Base structure
✔ Force child classes to implement required methods

---

# ⭐ Mini Project Example (All Concepts Combined)

```ts
abstract class User {
  constructor(
    public name: string,
    protected email: string,
    private password: string
  ) {}

  abstract getRole(): string;

  get maskedEmail() {
    return this.email.replace(/(.{3}).+(@.+)/, "$1***$2");
  }
}

class Admin extends User {
  static systemUsers = 0;

  constructor(name: string, email: string, password: string) {
    super(name, email, password);
    Admin.systemUsers++;
  }

  getRole() {
    return "admin";
  }
}

const bilal = new Admin("Bilal", "bilal@example.com", "12345");

console.log(bilal.maskedEmail);
console.log(bilal.getRole());
console.log(Admin.systemUsers);
```

This example covers:
✔ Classes
✔ Objects
✔ Constructor
✔ this
✔ public, private, protected
✔ Parameter properties
✔ Getter
✔ Static properties
✔ Abstract class
✔ Method overriding

---

---

# ⭐ **1. Introduction to Functions (TypeScript)**

TS functions JS jaise hi hote hain, bas hum **types** define kar sakte hain.

### Basic example:

```ts
function add(a: number, b: number): number {
  return a + b;
}
```

### Arrow Function

```ts
const greet = (name: string): string => {
  return "Hello " + name;
};
```

### Void function (no return)

```ts
function log(msg: string): void {
  console.log(msg);
}
```

---

# ⭐ **1.1 Rest Parameters**

Jab arguments unknown hon → `...rest` use hota hai.

```ts
function sum(...nums: number[]) {
  return nums.reduce((a, b) => a + b, 0);
}

console.log(sum(1, 2, 3, 4)); // 10
```

✔ Rest hamesha **array** return karta hai
✔ Type define karna zaroori hai

---

# ⭐ **1.2 Function Overloading**

Ek hi function ke **multiple signatures**.
Actual implementation **ek hi** hoti hai.

### Example:

```ts
function combine(a: number, b: number): number;
function combine(a: string, b: string): string;

function combine(a: any, b: any) {
  return a + b;
}

console.log(combine(10, 20));
console.log(combine("Bilal", " Ahmad"));
```

✔ Overloads strict types allow karte hain
✔ Implementation generic hoti hai (any ya union)

---

# ⭐ **2. Generics**

Generics = **type ko parameter bana dena**
Jab type vary kare, to generics best hote hain.

### Generic Function:

```ts
function identity<T>(value: T): T {
  return value;
}

identity<number>(10);
identity<string>("Bilal");
```

### Generic Array:

```ts
let items: Array<string> = ["a", "b"];
```

### Generic Interface:

```ts
interface ApiResponse<T> {
  data: T;
  status: number;
}

const r: ApiResponse<string> = {
  data: "Success",
  status: 200,
};
```

### Generic Class:

```ts
class Box<T> {
  constructor(public value: T) {}
}

const b = new Box<number>(10);
```

---

# ⭐ **3. Modules in TypeScript**

Modules hotay hain files jinme **export** aur **import** hota hai.

### File1: utils.ts

```ts
export function add(a: number, b: number) {
  return a + b;
}
```

### File2: main.ts

```ts
import { add } from "./utils";

console.log(add(5, 10));
```

### Default export:

```ts
export default class User {}
```

### Import default:

```ts
import User from "./User";
```

TS automatically JS me compile hoke ES modules generate karta hai.

---

# ⭐ **4. Type Assertions**

Type assertion = TypeScript ko batana ke “trust me, mujhe pata hai”.

2 ways:

### ✔ `as` syntax

```ts
let input = document.getElementById("username") as HTMLInputElement;
console.log(input.value);
```

### ✔ angle bracket syntax:

```ts
let value = <number>(<unknown>"10");
```

⚠ Assertion runtime me type change nahi karta
Sirf compiler ko hint deta hai.

---

# ⭐ **5. Type Guards**

Type Guards = runtime checks that narrow types **inside if blocks**.

Used with:
✔ `typeof`
✔ `instanceof`
✔ `in` operator
✔ custom type guards

---

## ⭐ 5.1 `typeof` Type Guard

```ts
function printValue(val: string | number) {
  if (typeof val === "string") {
    console.log(val.toUpperCase());
  } else {
    console.log(val.toFixed(2));
  }
}
```

---

## ⭐ 5.2 `instanceof`

```ts
class User {}
class Admin {}

function checkRole(obj: User | Admin) {
  if (obj instanceof Admin) {
    console.log("Admin");
  }
}
```

---

## ⭐ 5.3 `in` operator (best for objects)

```ts
type Dog = { bark: () => void };
type Cat = { meow: () => void };

function speak(animal: Dog | Cat) {
  if ("bark" in animal) {
    animal.bark();
  } else {
    animal.meow();
  }
}
```

---

# ⭐ 5.4 Custom Type Guard (Professional Use)

```ts
type User = { type: "user"; name: string };
type Admin = { type: "admin"; privileges: string[] };

function isAdmin(u: User | Admin): u is Admin {
  return u.type === "admin";
}

function check(u: User | Admin) {
  if (isAdmin(u)) {
    console.log(u.privileges);
  }
}
```

✔ TS ko explicitly bataya jaata hai
✔ Best practice for complex apps

---

# ⭐ Complete Mini Project (All Concepts Together)

```ts
// 1. Generic Response
interface Response<T> {
  success: boolean;
  data: T;
}

// 2. Function with Generics + Overloading
function getItem(id: number): Response<string>;
function getItem(id: string): Response<number>;

function getItem(id: any): any {
  if (typeof id === "number") {
    return { success: true, data: "Item-" + id };
  }
  return { success: true, data: id.length };
}

// 3. Type Guard
function isString(x: any): x is string {
  return typeof x === "string";
}

// 4. Use in App
function process(item: number | string) {
  if (isString(item)) {
    console.log("String:", item.toUpperCase());
  } else {
    console.log("Number:", item.toFixed());
  }
}

console.log(getItem(10));
process("bilal");
```
