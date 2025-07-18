---
title: indent
rule_type: layout
outline: deep
---

# indent

There are several common guidelines which require specific indentation of nested blocks and statements, like:

```js
function hello(indentSize, type) {
    if (indentSize === 4 && type !== 'tab') {
        console.log('Each next indentation will increase on 4 spaces');
    }
}
```

These are the most common scenarios recommended in different style guides:

- Two spaces, not longer and no tabs: Google, npm, Node.js, Idiomatic, Felix
- Tabs: jQuery
- Four spaces: Crockford

## Rule Details

This rule enforces a consistent indentation style. The default style is `4 spaces`.

## Options

This rule has a mixed option:

For example, for 2-space indentation:

```json
{
    "indent": ["error", 2]
}
```

Or for tabbed indentation:

```json
{
    "indent": ["error", "tab"]
}
```

Examples of **incorrect** code for this rule with the default options:

::: incorrect

```js
/* eslint @stylistic/indent: "error" */

if (a) {
  b=c;
  function foo(d) {
    e=f;
  }
}
```

:::

Examples of **correct** code for this rule with the default options:

::: correct

```js
/* eslint @stylistic/indent: "error" */

if (a) {
    b=c;
    function foo(d) {
        e=f;
    }
}
```

:::

This rule has an object option:

- `"ignoredNodes"` can be used to disable indentation checking for any AST node. This accepts an array of [selectors](https://eslint.org/docs/latest/extend/selectors). If an AST node is matched by any of the selectors, the indentation of tokens which are direct children of that node will be ignored. This can be used as an escape hatch to relax the rule if you disagree with the indentation that it enforces for a particular syntactic pattern.
- `"SwitchCase"` (default: 0) enforces indentation level for `case` clauses in `switch` statements
- `"VariableDeclarator"` (default: 1) enforces indentation level for `var` declarators; can also take an object to define separate rules for `var`, `let` and `const` declarations. It can also be `"first"`, indicating all the declarators should be aligned with the first declarator.
- `"outerIIFEBody"` (default: 1) enforces indentation level for file-level IIFEs. This can also be set to `"off"` to disable checking for file-level IIFEs.
- `"MemberExpression"` (default: 1) enforces indentation level for multi-line property chains. This can also be set to `"off"` to disable checking for MemberExpression indentation.
- `"FunctionDeclaration"` takes an object to define rules for function declarations.
  - `parameters` (default: 1) enforces indentation level for parameters in a function declaration. This can either be a number indicating indentation level, or the string `"first"` indicating that all parameters of the declaration must be aligned with the first parameter. This can also be set to `"off"` to disable checking for FunctionDeclaration parameters.
  - `body` (default: 1) enforces indentation level for the body of a function declaration.
  - `returnType` (default: 1) enforces indentation level for the return type of a function declaration.
- `"FunctionExpression"` takes an object to define rules for function expressions.
  - `parameters` (default: 1) enforces indentation level for parameters in a function expression. This can either be a number indicating indentation level, or the string `"first"` indicating that all parameters of the expression must be aligned with the first parameter. This can also be set to `"off"` to disable checking for FunctionExpression parameters.
  - `body` (default: 1) enforces indentation level for the body of a function expression.
  - `returnType` (default: 1) enforces indentation level for the return type of a function expression.
- `"StaticBlock"` takes an object to define rules for class static blocks.
  - `body` (default: 1) enforces indentation level for the body of a class static block.
- `"CallExpression"` takes an object to define rules for function call expressions.
  - `arguments` (default: 1) enforces indentation level for arguments in a call expression. This can either be a number indicating indentation level, or the string `"first"` indicating that all arguments of the expression must be aligned with the first argument. This can also be set to `"off"` to disable checking for CallExpression arguments.
- `"ArrayExpression"` (default: 1) enforces indentation level for elements in arrays. It can also be set to the string `"first"`, indicating that all the elements in the array should be aligned with the first element. This can also be set to `"off"` to disable checking for array elements.
- `"ObjectExpression"` (default: 1) enforces indentation level for properties in objects. It can be set to the string `"first"`, indicating that all properties in the object should be aligned with the first property. This can also be set to `"off"` to disable checking for object properties.
- `"ImportDeclaration"` (default: 1) enforces indentation level for import statements. It can be set to the string `"first"`, indicating that all imported members from a module should be aligned with the first member in the list. This can also be set to `"off"` to disable checking for imported module members.
- `"flatTernaryExpressions": true` (`false` by default) requires no indentation for ternary expressions which are nested in other ternary expressions.
- `"offsetTernaryExpressions": true` (`false` by default) requires indentation for values of ternary expressions.
- `"offsetTernaryExpressionsOffsetCallExpressions": true` (`true` by default), handles an edge case for call expressions nested in ternary. It's only effective when `offsetTernaryExpressions` is set to `true`.
- `"ignoreComments"` (default: false) can be used when comments do not need to be aligned with nodes on the previous or next line.
- `"tabLength"` (default: 4) when using tabbed indentation, the indentation used to calculate the insertion value of the template string

Level of indentation denotes the multiple of the indent specified. Example:

- Indent of 4 spaces with `VariableDeclarator` set to `2` will indent the multi-line variable declarations with 8 spaces.
- Indent of 2 spaces with `VariableDeclarator` set to `2` will indent the multi-line variable declarations with 4 spaces.
- Indent of 2 spaces with `VariableDeclarator` set to `{"var": 2, "let": 2, "const": 3, "using": 3}` will indent the multi-line variable declarations with 4 spaces for `var` and `let`, 6 spaces for `const`, `using` and `await using` statements.
- Indent of tab with `VariableDeclarator` set to `2` will indent the multi-line variable declarations with 2 tabs.
- Indent of 2 spaces with `SwitchCase` set to `0` will not indent `case` clauses with respect to `switch` statements.
- Indent of 2 spaces with `SwitchCase` set to `1` will indent `case` clauses with 2 spaces with respect to `switch` statements.
- Indent of 2 spaces with `SwitchCase` set to `2` will indent `case` clauses with 4 spaces with respect to `switch` statements.
- Indent of tab with `SwitchCase` set to `2` will indent `case` clauses with 2 tabs with respect to `switch` statements.
- Indent of 2 spaces with `MemberExpression` set to `0` will indent the multi-line property chains with 0 spaces.
- Indent of 2 spaces with `MemberExpression` set to `1` will indent the multi-line property chains with 2 spaces.
- Indent of 2 spaces with `MemberExpression` set to `2` will indent the multi-line property chains with 4 spaces.
- Indent of 4 spaces with `MemberExpression` set to `0` will indent the multi-line property chains with 0 spaces.
- Indent of 4 spaces with `MemberExpression` set to `1` will indent the multi-line property chains with 4 spaces.
- Indent of 4 spaces with `MemberExpression` set to `2` will indent the multi-line property chains with 8 spaces.

### tab

Examples of **incorrect** code for this rule with the `"tab"` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", "tab"] */

if (a) {
     b=c;
function foo(d) {
           e=f;
 }
}
```

:::

Examples of **correct** code for this rule with the `"tab"` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", "tab"] */

if (a) {
	b=c;
	function foo(d) {
		e=f;
	}
}
```

:::

### ignoredNodes

The following configuration ignores the indentation of `ConditionalExpression` ("ternary expression") nodes:

Examples of **correct** code for this rule with the `4, { "ignoredNodes": ["ConditionalExpression"] }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 4, { "ignoredNodes": ["ConditionalExpression"] }] */

var a = foo
      ? bar
      : baz;

var a = foo
                ? bar
: baz;
```

:::

The following configuration ignores indentation in the body of IIFEs.

Examples of **correct** code for this rule with the `4, { "ignoredNodes": ["CallExpression > FunctionExpression.callee > BlockStatement.body"] }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 4, { "ignoredNodes": ["CallExpression > FunctionExpression.callee > BlockStatement.body"] }] */

(function() {

foo();
bar();

})();
```

:::

All AST node types can be found at [ESTree](https://github.com/estree/estree) specification. You can use [AST Explorer](https://ast-explorer.dev/) with the espree parser to examine AST tree of a code snippet.

### SwitchCase

Examples of **incorrect** code for this rule with the `2, { "SwitchCase": 1 }` options:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "SwitchCase": 1 }] */

switch(a){
case "a":
    break;
case "b":
    break;
}
```

:::

Examples of **correct** code for this rule with the `2, { "SwitchCase": 1 }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "SwitchCase": 1 }] */

switch(a){
  case "a":
    break;
  case "b":
    break;
}
```

:::

### VariableDeclarator

Examples of **incorrect** code for this rule with the `2, { "VariableDeclarator": 1 }` options:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "VariableDeclarator": 1 }] */

var a,
    b,
    c;
let d,
    e,
    f;
const g = 1,
    h = 2,
    i = 3;
using j = foo(),
    k = bar(),
    l = baz();
await using j = foo(),
    k = bar(),
    l = baz();
```

:::

Examples of **correct** code for this rule with the `2, { "VariableDeclarator": 1 }` options:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "VariableDeclarator": 1 }] */

var a,
  b,
  c;
let d,
  e,
  f;
const g = 1,
  h = 2,
  i = 3;
using j = foo(),
  k = bar(),
  l = baz();
await using j = foo(),
  k = bar(),
  l = baz();
```

:::

Examples of **correct** code for this rule with the `2, { "VariableDeclarator": 2 }` options:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "VariableDeclarator": 2 }] */

var a,
    b,
    c;
let d,
    e,
    f;
const g = 1,
    h = 2,
    i = 3;
using j = foo(),
    k = bar(),
    l = baz();
await using j = foo(),
    k = bar(),
    l = baz();
```

:::

Examples of **incorrect** code for this rule with the `2, { "VariableDeclarator": "first" }` options:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "VariableDeclarator": "first" }] */

var a,
  b,
  c;
let d,
  e,
  f;
const g = 1,
  h = 2,
  i = 3;
using j = foo(),
  k = bar(),
  l = baz();
await using j = foo(),
  k = bar(),
  l = baz();
```

:::

Examples of **correct** code for this rule with the `2, { "VariableDeclarator": "first" }` options:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "VariableDeclarator": "first" }] */

var a,
    b,
    c;
let d,
    e,
    f;
const g = 1,
      h = 2,
      i = 3;
using j = foo(),
      k = bar(),
      l = baz();
await using j = foo(),
            k = bar(),
            l = baz();
```

:::

Examples of **correct** code for this rule with the `2, { "VariableDeclarator": { "var": 2, "let": 2, "const": 3, "using": "first" } }` options:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "VariableDeclarator": { "var": 2, "let": 2, "const": 3, "using": "first" } }] */

var a,
    b,
    c;
let d,
    e,
    f;
const g = 1,
      h = 2,
      i = 3;
using j = foo(),
      k = bar(),
      l = baz();
await using j = foo(),
            k = bar(),
            l = baz();
```

:::

### outerIIFEBody

Examples of **incorrect** code for this rule with the options `2, { "outerIIFEBody": 0 }`:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "outerIIFEBody": 0 }] */

(function() {

  function foo(x) {
    return x + 1;
  }

})();

if (y) {
console.log('foo');
}
```

:::

Examples of **correct** code for this rule with the options `2, { "outerIIFEBody": 0 }`:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "outerIIFEBody": 0 }] */

(function() {

function foo(x) {
  return x + 1;
}

})();

if (y) {
  console.log('foo');
}
```

:::

Examples of **correct** code for this rule with the options `2, { "outerIIFEBody":  "off" }`:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "outerIIFEBody": "off" }] */

(function() {

function foo(x) {
  return x + 1;
}

})();

(function() {

  function foo(x) {
    return x + 1;
  }

})();

if (y) {
  console.log('foo');
}
```

:::

### MemberExpression

Examples of **incorrect** code for this rule with the `2, { "MemberExpression": 1 }` options:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "MemberExpression": 1 }] */

foo
.bar
.baz()
```

:::

Examples of **correct** code for this rule with the `2, { "MemberExpression": 1 }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "MemberExpression": 1 }] */

foo
  .bar
  .baz();
```

:::

### FunctionDeclaration

Examples of **incorrect** code for this rule with the `2, { "FunctionDeclaration": {"body": 1, "parameters": 2, "returnType": 1} }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "FunctionDeclaration": {"body": 1, "parameters": 2, "returnType": 1} }] */

function foo(bar,
  baz,
  qux) {
    qux();
}

function foo(a: string)
: a is 'a' {
  return bar()
}
```

:::

Examples of **correct** code for this rule with the `2, { "FunctionDeclaration": {"body": 1, "parameters": 2, "returnType": 1} }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "FunctionDeclaration": {"body": 1, "parameters": 2, "returnType": 1} }] */

function foo(bar,
    baz,
    qux) {
  qux();
}

function foo(a: string)
  : a is 'a' {
  return bar()
}
```

:::

Examples of **incorrect** code for this rule with the `2, { "FunctionDeclaration": {"parameters": "first"} }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, {"FunctionDeclaration": {"parameters": "first"}}] */

function foo(bar, baz,
  qux, boop) {
  qux();
}
```

:::

Examples of **correct** code for this rule with the `2, { "FunctionDeclaration": {"parameters": "first"} }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, {"FunctionDeclaration": {"parameters": "first"}}] */

function foo(bar, baz,
             qux, boop) {
  qux();
}
```

:::

### FunctionExpression

Examples of **incorrect** code for this rule with the `2, { "FunctionExpression": {"body": 1, "parameters": 2, "returnType": 1} }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "FunctionExpression": {"body": 1, "parameters": 2, "returnType": 1} }] */

var foo = function(bar,
  baz,
  qux) {
    qux();
}

const foo = function(a: string)
: a is 'a' {
  return bar()
}
```

:::

Examples of **correct** code for this rule with the `2, { "FunctionExpression": {"body": 1, "parameters": 2, "returnType": 1} }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "FunctionExpression": {"body": 1, "parameters": 2, "returnType": 1} }] */

var foo = function(bar,
    baz,
    qux) {
  qux();
}

const foo = function(a: string)
  : a is 'a' {
  return bar()
}
```

:::

Examples of **incorrect** code for this rule with the `2, { "FunctionExpression": {"parameters": "first"} }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, {"FunctionExpression": {"parameters": "first"}}] */

var foo = function(bar, baz,
  qux, boop) {
  qux();
}
```

:::

Examples of **correct** code for this rule with the `2, { "FunctionExpression": {"parameters": "first"} }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, {"FunctionExpression": {"parameters": "first"}}] */

var foo = function(bar, baz,
                   qux, boop) {
  qux();
}
```

:::

### StaticBlock

Examples of **incorrect** code for this rule with the `2, { "StaticBlock": {"body": 1} }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "StaticBlock": {"body": 1} }] */

class C {
  static {
      foo();
  }
}
```

:::

Examples of **correct** code for this rule with the `2, { "StaticBlock": {"body": 1} }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "StaticBlock": {"body": 1} }] */

class C {
  static {
    foo();
  }
}
```

:::

Examples of **incorrect** code for this rule with the `2, { "StaticBlock": {"body": 2} }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "StaticBlock": {"body": 2} }] */

class C {
  static {
    foo();
  }
}
```

:::

Examples of **correct** code for this rule with the `2, { "StaticBlock": {"body": 2} }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "StaticBlock": {"body": 2} }] */

class C {
  static {
      foo();
  }
}
```

:::

### CallExpression

Examples of **incorrect** code for this rule with the `2, { "CallExpression": {"arguments": 1} }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "CallExpression": {"arguments": 1} }] */

foo(bar,
    baz,
      qux
);
```

:::

Examples of **correct** code for this rule with the `2, { "CallExpression": {"arguments": 1} }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "CallExpression": {"arguments": 1} }] */

foo(bar,
  baz,
  qux
);
```

:::

Examples of **incorrect** code for this rule with the `2, { "CallExpression": {"arguments": "first"} }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, {"CallExpression": {"arguments": "first"}}] */

foo(bar, baz,
  baz, boop, beep);
```

:::

Examples of **correct** code for this rule with the `2, { "CallExpression": {"arguments": "first"} }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, {"CallExpression": {"arguments": "first"}}] */

foo(bar, baz,
    baz, boop, beep);
```

:::

### ArrayExpression

Examples of **incorrect** code for this rule with the `2, { "ArrayExpression": 1 }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "ArrayExpression": 1 }] */

var foo = [
    bar,
baz,
      qux
];
```

:::

Examples of **correct** code for this rule with the `2, { "ArrayExpression": 1 }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "ArrayExpression": 1 }] */

var foo = [
  bar,
  baz,
  qux
];
```

:::

Examples of **incorrect** code for this rule with the `2, { "ArrayExpression": "first" }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, {"ArrayExpression": "first"}] */

var foo = [bar,
  baz,
  qux
];
```

:::

Examples of **correct** code for this rule with the `2, { "ArrayExpression": "first" }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, {"ArrayExpression": "first"}] */

var foo = [bar,
           baz,
           qux
];
```

:::

### ObjectExpression

Examples of **incorrect** code for this rule with the `2, { "ObjectExpression": 1 }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "ObjectExpression": 1 }] */

var foo = {
    bar: 1,
baz: 2,
      qux: 3
};
```

:::

Examples of **correct** code for this rule with the `2, { "ObjectExpression": 1 }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "ObjectExpression": 1 }] */

var foo = {
  bar: 1,
  baz: 2,
  qux: 3
};
```

:::

Examples of **incorrect** code for this rule with the `2, { "ObjectExpression": "first" }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, {"ObjectExpression": "first"}] */

var foo = { bar: 1,
  baz: 2 };
```

:::

Examples of **correct** code for this rule with the `2, { "ObjectExpression": "first" }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, {"ObjectExpression": "first"}] */

var foo = { bar: 1,
            baz: 2 };
```

:::

### ImportDeclaration

Examples of **correct** code for this rule with the `4, { "ImportDeclaration": 1 }` option (the default):

::: correct

```js
/* eslint @stylistic/indent: ["error", 4, { "ImportDeclaration": 1 }] */

import { foo,
    bar,
    baz,
} from 'qux';
```

:::

::: correct

```js
/* eslint @stylistic/indent: ["error", 4, { "ImportDeclaration": 1 }] */

import {
    foo,
    bar,
    baz,
} from 'qux';
```

:::

Examples of **incorrect** code for this rule with the `4, { "ImportDeclaration": "first" }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 4, { "ImportDeclaration": "first" }] */

import { foo,
    bar,
    baz,
} from 'qux';
```

:::

Examples of **correct** code for this rule with the `4, { "ImportDeclaration": "first" }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 4, { "ImportDeclaration": "first" }] */

import { foo,
         bar,
         baz,
} from 'qux';
```

:::

### flatTernaryExpressions

Examples of **incorrect** code for this rule with the default `4, { "flatTernaryExpressions": false }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 4, { "flatTernaryExpressions": false }] */

var a =
    foo ? bar :
    baz ? qux :
    boop;
```

:::

Examples of **correct** code for this rule with the default `4, { "flatTernaryExpressions": false }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 4, { "flatTernaryExpressions": false }] */

var a =
    foo ? bar :
        baz ? qux :
            boop;
```

:::

Examples of **incorrect** code for this rule with the `4, { "flatTernaryExpressions": true }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 4, { "flatTernaryExpressions": true }] */

var a =
    foo ? bar :
        baz ? qux :
            boop;
```

:::

Examples of **correct** code for this rule with the `4, { "flatTernaryExpressions": true }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 4, { "flatTernaryExpressions": true }] */

var a =
    foo ? bar :
    baz ? qux :
    boop;
```

:::

### offsetTernaryExpressions

Examples of **incorrect** code for this rule with the default `2, { "offsetTernaryExpressions": false }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "offsetTernaryExpressions": false }] */

condition
  ? () => {
      return true
    }
  : () => {
      false
    }
```

:::

Examples of **correct** code for this rule with the default `2, { "offsetTernaryExpressions": false }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "offsetTernaryExpressions": false }] */

condition
  ? () => {
    return true
  }
  : condition2
    ? () => {
      return true
    }
    : () => {
      return false
    }
```

:::

Examples of **incorrect** code for this rule with the `2, { "offsetTernaryExpressions": true }` option:

::: incorrect

```js
/* eslint @stylistic/indent: ["error", 2, { "offsetTernaryExpressions": true }] */

condition
  ? () => {
    return true
  }
  : condition2
    ? () => {
      return true
    }
    : () => {
      return false
    }
```

:::

Examples of **correct** code for this rule with the `2, { "offsetTernaryExpressions": true }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "offsetTernaryExpressions": true }] */

condition
  ? () => {
      return true
    }
  : condition2
    ? () => {
        return true
      }
    : () => {
        return false
      }
```

:::

### offsetTernaryExpressionsOffsetCallExpressions

> This option is only effective when `offsetTernaryExpressions` is set to `true`.

Since v2.12.0, we [introduced a fix](https://github.com/eslint-stylistic/eslint-stylistic/pull/625) to call expressions handling inside ternary. With the new version, the rule now expect the following code to be correct:

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "offsetTernaryExpressions": true }] */

condition
  ? gerUser({
      name: 'foo',
      age: 20,
    })
  : condition2
    ? gerUser({
        id: 'bar',
      })
    : undefined
```

:::

Due to the new fix introduced changes to some existing codebase, we introduced this `offsetTernaryExpressionsOffsetCallExpressions` option to toggle the behaviors. It's set to `true` by default, where you can set it to `false` to use the previous behavior.

::: correct

```js
/* eslint @stylistic/indent: ["error", 2, { "offsetTernaryExpressions": true, "offsetTernaryExpressionsOffsetCallExpressions": false }] */

condition
  ? gerUser({
    name: 'foo',
    age: 20,
  })
  : condition2
    ? gerUser({
      id: 'bar',
    })
    : undefined
```

:::

### ignoreComments

Examples of additional **correct** code for this rule with the `4, { "ignoreComments": true }` option:

::: correct

```js
/* eslint @stylistic/indent: ["error", 4, { "ignoreComments": true }] */

if (foo) {
    doSomething();

// comment intentionally de-indented
    doSomethingElse();
}
```

:::

## Compatibility

- **JSHint**: `indent`
- **JSCS**: [validateIndentation](https://jscs-dev.github.io/rule/validateIndentation)
