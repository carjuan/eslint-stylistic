# jsx-sort-props

Enforce props alphabetical sorting.

Some developers prefer to sort props names alphabetically to be able to find necessary props easier at the later time. Others feel that it adds complexity and becomes burden to maintain.

## Rule Details

This rule checks all JSX components and verifies that all props are sorted alphabetically. A spread attribute resets the verification. The default configuration of the rule is case-sensitive.

Examples of **incorrect** code for this rule:

::: incorrect

```jsx
/* eslint @stylistic/jsx-sort-props: "error" */

<Hello lastName="Smith" firstName="John" />;
```

:::

Examples of **correct** code for this rule:

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: "error" */

<Hello firstName="John" lastName="Smith" />;
<Hello tel={5555555} {...this.props} firstName="John" lastName="Smith" />;
```

:::

## Rule Options

```js
...
"@stylistic/jsx-sort-props": [<enabled>, {
  "callbacksLast": <boolean>,
  "shorthandFirst": <boolean>,
  "shorthandLast": <boolean>,
  "multiline": "ignore" | "first" | "last",
  "ignoreCase": <boolean>,
  "noSortAlphabetically": <boolean>,
  "reservedFirst": <boolean>|<array<string>>,
  "locale": "auto" | "any valid locale"
}]
...
```

### `ignoreCase`

When `true` the rule ignores the case-sensitivity of the props order.

Examples of **correct** code for this rule

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "ignoreCase": true }] */

<Hello name="John" Number="2" />;
```

:::

### `callbacksLast`

When `true`, callbacks must be listed after all other props, even if `shorthandLast` is set :

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "callbacksLast": true }] */

<Hello tel={5555555} onClick={this._handleClick} />
```

:::

### `shorthandFirst`

When `true`, short hand props must be listed before all other props, but still respecting the alphabetical order:

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "shorthandFirst": true }] */

<Hello active validate name="John" tel={5555555} />
```

:::

### `shorthandLast`

When `true`, short hand props must be listed after all other props (unless `callbacksLast` is set), but still respecting the alphabetical order:

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "shorthandLast": true }] */

<Hello name="John" tel={5555555} active validate />
```

:::

### `multiline`

Enforced sorting for multiline props

- `ignore`: Multiline props will not be taken in consideration for sorting.

- `first`: Multiline props must be listed before all other props (unless `shorthandFirst` is set), but still respecting the alphabetical order.

- `last`: Multiline props must be listed after all other props (unless either `callbacksLast` or `shorthandLast` are set), but still respecting the alphabetical order.

Defaults to `ignore`.

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "multiline": "first" }] */

<Hello
  classes={{
    greetings: classes.greetings,
  }}
  active
  validate
  name="John"
  tel={5555555}
/>
```

:::

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "multiline": "last" }] */

<Hello
  active
  validate
  name="John"
  tel={5555555}
  classes={{
    greetings: classes.greetings,
  }}
/>
```

:::

### `noSortAlphabetically`

When `true`, alphabetical order is **not** enforced:

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "noSortAlphabetically": true }] */

<Hello tel={5555555} name="John" />
```

:::

### `reservedFirst`

This can be a boolean or an array option.

When `reservedFirst` is `true`, the default reserved props are [`children`, `dangerouslySetInnerHTML` (only for DOM components), `key`, `ref`]. These props must be listed before all other props, but still respecting the alphabetical order:

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "reservedFirst": true }] */

<Hello key={0} ref={johnRef} name="John">
  <div dangerouslySetInnerHTML={{__html: 'ESLint Plugin React!'}} ref={dangerDivRef} />
</Hello>
```

:::

If given as an array, the array's values will override the default list of reserved props.
These props will respect the order specified in the array:

::: incorrect

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "reservedFirst": ["v-if", "v-for"] }] */

<App a v-for={i in list} v-if={list} b />
```

:::

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "reservedFirst": ["v-if", "v-for"] }] */

<App v-if={list} v-for={i in list} a b />
```

:::

With `reservedFirst: ["key"]`, the following will **not** warn:

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "reservedFirst": ["key"] }] */

<Hello key={'uuid'} name="John" ref={johnRef} />
```

:::

### `reservedLast`

This can be an array option. These props must be listed after all other props.
These will respect the order specified in the array:

::: incorrect

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "reservedLast": ["v-slot"] }] */

<App v-slot={{ foo }} onClick={onClick} />
```

:::

::: correct

```jsx
/* eslint @stylistic/jsx-sort-props: ["error", { "reservedLast": ["v-slot"] }] */

<App onClick={onClick} v-slot={{ foo }} />
```

:::

### `locale`

Defaults to `"auto"`, meaning, the locale of the current environment.

Any other string provided here may be passed to [`String.prototype.localeCompare`](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/String/localeCompare) - note that an unknown or invalid locale may throw an exception and crash.

## When Not To Use It

This rule is a formatting preference and not following it won't negatively affect the quality of your code. If alphabetizing props isn't a part of your coding standards, then you can leave this rule off.
