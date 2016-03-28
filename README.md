# Lesson 6.2 - Block Scoped Variables

Let's explore block scoped variables shall we? Block scoped variables are
simply variables that are local to the block in which they were defined. Let's
explore this a bit with some code samples.

## The Basics

If we were to use `var` to declare a variable in this snippet, everything would
be just fine:

```js
for (var i = 0; i < 3; i++) {
  var j = i * i
}

console.log(j) // This will print '4', and is fine
```

But let's say we use `let` to declare that variable:

```js
for (let i = 0; i < 3; i++) {
  let j = i * i
}

console.log(j) // This will throw, because let is local to the `for` loop.
```

This is a subtle difference, but an important one. This really helps to keep
variables scoped to their local block, and avoids confusion for other developers
(and yourself).

## Nested Scopes

Scoping also works in situations where the blocks are nested:

```js
function foo() {
  let bar = 'Hello World!';

  return function() {
    return bar;
  }
}
```

In this example, the returned function has access to the `bar` variable because
it was declared in the outer scope. The functioned that is returned from the
`foo` function has access to all variables declared in the scope of the `foo`
function.

However, this will throw an error:

```js
function foo() {
  for (let i = 0; i < 3; i++) {
    let j = i;
  }

  return j; // This is not allowed, as j was declared inside a different scope
}
```

Taking this one step farther, we can do something like this:

```js
let j = 0;

function foo() {
  for (let i = 0; i < 3; i++) {
    j += i;
  }
}

foo()
console.log(j)
-> 6
```

This isn't very good programming practice, but it clearly demonstrates how
nested scoping works. The `j` variable is available in all child scopes.

## Scoping with switch statements

Scoping also applies to switch statements. Adding curly braces to your `case`
statements will encapsulate them in their own scope.

```js
let i = 10;
let foo = 'BAR';

switch (i) {
  case 10:
    let foo = 'It's 10!';
}
```

This will throw an error because you are attempting to redefine the `foo`
variable. The `foo` variable is still in scope inside of that case statement.
However, if we rewrite that like this:

```js
let i = 10;
let foo = 'BAR';

switch (i) {
  case 10: {
    let foo = 'It's 10!';
  }
}
```

This is perfectly acceptable, because we have created an isolated scope for
the case statement.

## Wrapping up

Anything inside curly braces ({}) is considered to be inside of a block, and
you can create a block all by itself:

```js
{
  // This is inside of an isolated block scope
  let foo = 1;
}

console.log(foo); // `foo` is undefined in this scope
```

Constants behave in exactly the same way as `let` when it comes to scoping.
It is for this reason that it is preferred to use `const` and `let` over `var`
as often as possible.

## Moving on
Easy! Block scoped variables are a simple concept, and using the right type
of variable declarations is crucial to writing good, clean code. Let's move
on and discuss block scoped functions!
