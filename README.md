const, let, var
---------------

`const` defines a constant, which value can't be changed

```js
const name = "Jonas";
// The following would throw an error:
//name = 42;
```

`let` defines changeable variables.

```js
let counter = 0;
counter = 42;
```

In contrast to `var`, `let` is block scoped.

```js
{
	let invisible = true;
}
// The following would throw an error, because the variable is not defined:
//console.log(invisible);
```

Whereas the same with `var` would work, since var is scoped
to the next enclosing function.

```js
{
	var visible = true;
}
console.log(visible); // -> true
```

String literals
---------------

Besides single (') and double quotes ("), ES2016 introduced
template strings via backtick quotes (`).

Template strings can directly contain variables:

```js
const name = 'Douglas';
console.log(`Hello ${name}.`);
```

Template strings can also include newlines:

```js
const truth = `No nasty
string concatenation
anymore.`;
```

Arrow functions
---------------

Arrow functions are a slightly shorter syntax
to declare unnamed functions. the following two
snippets are equal:

```js
const square = function(x) {
	return x * x;
};
const squareWithArrowFunction = (x) => {
	return x * x;
};
```

Besides a shorter syntax, they have a few
differences in their behvior.

Inside an arrow function `this` will always be the
same `this` as outside the function. This isn't
true for the old function syntax?

```js
const self = this;
const func = () => {
	assert(this === self); // -> always true
};
```

There is an even shorter syntax, if the arrow
function consists of just one statement and the
result of that statement should be returned.
In this case you can skip the curly braces:

```js
const square = (x) => x * x;
```

If the value you want to return is an object
literal you have to put parantheses around
the statement, so the curly braces won't be
mistaken for the function block:

```js
const getUser = () => ({ name: 'Max', age: 42 });
```

Default Parameters
------------------

A function (or arrow function) can specify default
values for several parameters.

```js
function multiply(x, y = 2) {
	return x * y;
}
```

If you now leave the parameter undefined or pass
`undefined` for the second parameter, it will now
have the value 2.

Enhanced Object Literals
------------------------

Object literals have a shorter syntax for some
common tasks.

You can set variables to the key with the same
name in a shorter way now:

```js
const name = 'Mustermann';
const firstName = 'Max';
// previously:
const person = {
	name: name,
	firstName: firstName
};
// now:
const person2 = {
	name, firstName
};
```

To attach an inline function to an object you
can now use a shorter syntax:

```js
// previously:
const obj = {
	toString: function() {
		// ...
	}
};
// now:
const obj = {
	toString() {
		// ...
	}
};
```

There is also support for calculating the key
of an entry from a variable by using squared
brackets:

```js
const obj = {
	[someVar + '42']: '...'
};
```

Destructuring
-------------

You can now easily destruct an array or object
into several variables with the new destructuring
syntax:

```js
const [x, y] = [1, 2];
// x == 1, y == 2
```

If you are not interested in some parts of the
array:

```js
const [x,,z] = [1, 2, 3, 4];
// x == 1, z == 3
```

Destructuring works also on objects:

```js
const props = {
	name: 'Max Mustermann',
	age: 42
};
const { name } = props;
// name == 'Max Mustermann'
```

If you want to use a different name for the variable
than the key name, you can set it directly during
destructuring.

```js
// const props as above
const { name, age: a } = props;
// name == 'Max Mustermann', a == 42
```

Spreading
---------
TODO

Klassen
-------

ES2015 introduced a new syntax to define classes, that
is more similar to the syntax other coding languages
use.

```js
class Person {

	// The constructor has always the name constructor
	constructor(name) {
		this.age = 0;
		this.name = name;
	}

	printAge() {
		console.log(this.age);
	}

}

const p = new Person('Max Mustermann');
p.printAge();
```

Classes support inheritance with a simple unified syntax:

```js
class Client extends Person {
	constructor(name, address) {
		super(name);
		this.address = address;
	}
}
```

import & export
---------------

A new and more complex import and export syntax became available with ES2015.

To export a something (variable, function, object, ...) from a file, use `export`:

```js
function multiply(x, y) { /* ... */ }

// Export an already existing object
export {multiply};
// export an inline defined object
export const PI_ROUNDED = 3;
```

This is a named export, exporting the object under its name. You can also change
the name that is used for exporting.

```js
function add(x, y) { /* .. */ }
function multiply(x, y) { /* .. */ }
export {add as sum, multiply as mul};
```

Each file can have one default export, for the "default" object one might wish
to import from that file. That object doesn't need to have a name - e.g. can be
an inline function - but can have a name, even though it won't be used in the export.

```js
export default function() {

}
```

To import from a file, you can use the syntax:

```js
// Using the name of a package to import from node_modules
import React from 'react';
// Using a file path will look up relative to the current file
import Client from './api/client.js';
```

Importing named members is using the curly braces syntax similar to
the export of it:

```js
import {add, multiply} from './math.js';
```

You can also specify a different name while importing:

```js
import {add as sum, multiply} from './math.js';
```

To import all exported members (named and default) from a module,
use the following syntax:

```js
import * as math from './math.js';
// math.add and math.multiply will be the named exports
// math.default will give access to the default export
```

You can also re-export the members of a module completely
or just specific named members - and optionally rename them:

```js
export * from './math.js';
export {sinus as sin, cosinus} from './advancedMath.js';
```


Promises
--------

A complete introductin to promises can be found at
[developers.google.com](https://developers.google.com/web/fundamentals/getting-started/primers/promises).
