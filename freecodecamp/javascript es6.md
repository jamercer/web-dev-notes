# alternatives to `var`
## `let`
unlike `var`, when using `let`, a variable with the same name can only be declared once.
```javascript
var camper = 'James';
var camper = 'David';
console.log(camper); // logs 'David'

let camper = 'James';
let camper = 'David'; // throws an error
```

When you declare a variable with the ``let`` keyword inside a block, statement, or expression, its scope is limited to that block, statement, or expression.
```javascript
var printNumTwo;
for (var i = 0; i < 3; i++) {
  if (i === 2) {
    printNumTwo = function() {
      return i;
    };
  }
}
console.log(printNumTwo()); // returns 3

let printNumTwo;
for (let i = 0; i < 3; i++) {
  if (i === 2) {
    printNumTwo = function() {
      return i;
    };
  }
}
console.log(printNumTwo()); // returns 2
console.log(i); // returns "i is not defined"

function checkScope() {
  let i = 'function scope';
  if (true) {
    let i = 'block scope';
    console.log('Block scope i is: ', i);
  }
  console.log('Function scope i is: ', i);
  return i;
}
```
## `const`
`const` has all the awesome features that let has, with the added bonus that variables declared using const are read-only.
```javascript
const FAV_PET = "Cats";
FAV_PET = "Dogs"; // returns error
```
consts are written in all uppercase letters

objects (including arrays and functions) assigned to a variable using `const` are still mutable. Using the `const` declaration only prevents reassignment of the variable identifier.
```javascript
const s = [5, 6, 7];
s = [1, 2, 3]; // throws error, trying to assign a const
s[2] = 45; // works just as it would with an array declared with var or let
console.log(s); // returns [5, 6, 45]
```
`const` declaration alone doesn't really protect your data from mutation. To ensure your data doesn't change, JavaScript provides a function `Object.freeze` to prevent data mutation.

Once the object is frozen, you can no longer add, update, or delete properties from it. Any attempt at changing the object will be rejected without an error.
``` javascript
let obj = {
  name:"FreeCodeCamp",
  review:"Awesome"
};
Object.freeze(obj);
obj.review = "bad"; // will be ignored. Mutation not allowed
obj.newProp = "Test"; // will be ignored. Mutation not allowed
console.log(obj); 
// { name: "FreeCodeCamp", review:"Awesome"}
```

# Anonymous Functions

>lambda operator

```javascript
const myFunc = function() {
  const myVar = "value";
  return myVar;
}
```
can write an anonymous function with just `=>`
```javascript
const myFunc = () => {
  const myVar = "value";
  return myVar;
}
```
if there is no function body, only a return value, we can do this:
```javascript
const myFunc = () => "value";
```
you can pass arguments into an arrow function
```javascript
// doubles input value and returns it
const doubler = (item) => item * 2;
doubler(4); // returns 8
```
If an arrow function has a single parameter, the parentheses enclosing the parameter may be omitted.
```javascript
// the same function, without the parameter parentheses
const doubler = item => item * 2;
```
It is possible to pass more than one argument into an arrow function.
```javascript
// multiplies the first input value by the second and returns it
const multiplier = (item, multi) => item * multi;
multiplier(4, 2); // returns 8
```

# more function stuff
default parameters are a thing
```javascript
const greeting = (name = "Anonymous") => "Hello " + name;

console.log(greeting("John")); // Hello John
console.log(greeting()); // Hello Anonymous
```
## rest parameter
the rest parameter (`...`) you can create functions that take a variable number of arguments and stores them to an array
```javascript
function howMany(...args) {
  return "You have passed " + args.length + " arguments.";
}
console.log(howMany(0, 1, 2)); // You have passed 3 arguments.
console.log(howMany("string", null, [1, 2, 3], { })); // You have passed 4 arguments.
```
## spread operator
`...` is also the spread operator. which "expands" or "unpacks" an array
```javascript
const arr = [6, 89, 3, 45];
const maximus = Math.max(...arr); // returns 89

const arr1 = ['JAN', 'FEB', 'MAR', 'APR', 'MAY'];
let arr2;

//arr2 = ...arr1; // syntax error
arr2 = [...arr1]; // unpack array, then repackage array

console.log(arr2);
```
# destructuring assignment
## objects
you can destructure objects like this:
```javascript
const user = { name: 'John Doe', age: 34 };
// es5
const name = user.name; // name = 'John Doe'
const age = user.age; // age = 34
// es6
const { name, age } = user;
// name = 'John Doe', age = 34
```
the es6 destructuring syntax creates and assigns the name and age variables

you can also rename the variables you are assigning to
``` javascript
const { name: userName, age: userAge } = user;
// userName = 'John Doe', userAge = 34
```
you can access nested objects this way as well
``` javascript
const LOCAL_FORECAST = {
  today: { low: 64, high: 77 },
  tomorrow: { low: 68, high: 80 }
};
// es5
const lowToday = LOCAL_FORECAST.today.low;
const highToday = LOCAL_FORECAST.today.high;
// es6
const { today: { low: lowToday, high: highToday } } = LOCAL_FORECAST;
```
you can use destructuring in a funciton argument
``` javascript
const stats = {
  max: 56.78,
  min: -0.75,
  average: 35.85
};
//es5
const half = (stats) => (stats.max + stats.min) / 2.0; 
//es6
const half = ({max, min}) => (max + min) / 2.0; 
```

## arrays
idk we can do fucky shit with arrays i guess
```javascript
const [a, b] = [1, 2, 3, 4, 5, 6];
console.log(a, b); // 1, 2

const [a, b,,, c] = [1, 2, 3, 4, 5, 6]; // commas skip indexes
console.log(a, b, c); // 1, 2, 5

let a = 8, b = 6;
[b,a] = [a,b]; // b and a are swapped
```
the following is similar to `Array.prototype.slice()`
```javascript
const [a, b, ...arr] = [1, 2, 3, 4, 5, 7];
console.log(a, b); // 1, 2
console.log(arr); // [3, 4, 5, 7]
```

Variables `a` and `b` take the first and second values from the array and `arr` gets the rest of the values in the form of an array. The rest element only works correctly as the last variable in the list. As in, you cannot use the rest parameter to catch a subarray that leaves out the last element of the original array.

# Template Literal

Template literals allow you to create multi-line strings and to use string interpolation features to create strings

use backticks ``` ` ``` to wrap the string, can write multi-line strings without \n

`${variable-name}` is used to insert a string variable instead of using `+` for concatenation 
```javascript
const person = {
  name: "Zodiac Hasbro",
  age: 56
};

// Template literal with multi-line and string interpolation
const greeting = `Hello, my name is ${person.name}!
I am ${person.age} years old.`;

console.log(greeting); // prints
// Hello, my name is Zodiac Hasbro!
// I am 56 years old.
```

# consise literal declarations
idk this is confusing
``` javascript
// you dont have to do this
const getMousePosition = (x, y) => ({
  x: x,
  y: y
});
// you can just do this
const getMousePosition = (x, y) => ({ x, y });
```
stores the value of the variable to a property named the same as the variable

# Concise Declarative Functions
when creating functions in objects you can create functions like this:
```javascript
const bicycle = {
  gear: 2,
  setGear(newGear) {
    this.gear = newGear;
  }
};
// instead of this
const bicycle = {
  gear: 2,
  setGear: function(newGear) {
    this.gear = newGear;
  }
};
```

# Classes
a different way of creating objects. looks like classes from c based languages but is really just a javascript object??? idk.

classes have constructors that initialize stuff
```javascript
class Vegetable { constructor(name) {this.name = name;}}

const carrot = new Vegetable('carrot');
console.log(carrot.name); // Should display 'carrot'
```

getter and setter methods can be used to modify private variables

```javascript
class Thermostat {
  constructor(fahrenheit) {this.fahrenheit  = fahrenheit;}
  get temperature() {return 5.0/9.0 * (this.fahrenheit - 32);}
  set temperature(celsius) {this.fahrenheit = celsius * 9.0 / 5.0 + 32;}
}

const thermos = new Thermostat(76); // Setting in Fahrenheit scale
let temp = thermos.temperature; // 24.44 in Celsius
thermos.temperature = 26;
temp = thermos.temperature; // 26 in Celsius
```

# Modules (import & export)

code can be reused by making it a module (set its type attrib to "module")
```javascript
<script type="module" src="index.js"></script>
```
A script that uses this module type can now use the import and export features
```javascript
export const add = (x, y) => { return x + y; }
// or
const add = (x, y) => { return x + y; }
export { add };
// can export multiple things
export { add, subtract };
```
functions that have been exported from one script can be imported into another
```javascript
import { add, subtract } from './math_functions.js';
add(2,2) // 4
subtract(2,1) // 1
```

The static import statement is used to import read only live bindings which are exported by another module.

you can use ```import * as``` to import every exported function from a file
```javascript
import * as myMathModule from "./math_functions.js";
myMathModule.add(2,3);
myMathModule.subtract(5,3);
```
default export lets you do stuff? can be anonynous and renamed on import?/??
```javascript
export default function add(x, y) {
  return x + y;
}

export default function(x, y) {
  return x + y;
}
```
```javascript
import add from './my-module.js';
```
The imported value, ```add```, is not surrounded by curly braces. ```add``` here is simply a variable name for whatever the default export of the ```math_functions.js``` file is.

# Javascript Promise
used with asynchronous bs. When the task completes, you either fulfill your promise or fail to do so.

```Promise``` is a constructor function, so you need to use the ```new``` keyword to create one.
```javascript
const myPromise = new Promise((resolve, reject) => { });
```
promise should receive a function with ```resolve``` and ```reject``` as parameters. (in this example) The example above uses strings for the argument of these functions, but it can really be anything. Often, it might be an object, that you would use data from, to put on your website or elsewhere.

A promise has three states: ```pending```, ```fulfilled```, and ```rejected```
```javascript
const makeServerRequest = new Promise((resolve, reject) => {
  // responseFromServer represents a response from a server
  let responseFromServer;
    
  if(responseFromServer) {
    resolve("We got the data");
  } else {  
    reject("Data not received");
  }
});

makeServerRequest.then(result => { console.log(result); });
makeServerRequest.catch(error => { console.log(error); });
```
The ```then``` method is executed immediately after your promise is fulfilled with ```resolve```

```catch``` is the method used when your promise has been rejected. It is executed immediately after a promise's ```reject``` method is called