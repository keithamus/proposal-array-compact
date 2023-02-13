# proposal-array-compact

A proposal to create a more compact array, by discarding falsey values

```js
const array = [0, 1, false, 2, '', 3]

array.compact()
// =>  [1, 2 3]
```

## Champions

- Keith Cirkel ([@keithamus](https://github.com/keithamus/))

## Status

Current [Stage](https://tc39.es/process-document/): 0

## Motivation

Compacting an Array to only truthy values is a common operation. It's
usually handled by calling [`filter` with an identity function
(44k results)][filter_id]:

```js
array.filter(i => i)
```

or by passing the [`Boolean` value as a predicate function (133K results)][filter_b_pred]:

```js
array.filter(Boolean)
```

or a simple function returning the [`Boolean` value of just the first parameter (1K results)][filter_b]:

```js
array.filter(i => Boolean(i))
```

or even a simple function returning the [doubly-negated value of just the first parameter (18K results)][filter_double_negation]:

```js
array.filter(i => !!i)
```

All of these can be somewhat tricky to reason about, and the
various styles can be used in the same codebase to make matters
more confusing.

[Lodash includes `_.compact()`][lodash] which as a [standalone
dependency][lodash-npm] receives ~400,000 downloads per week.

[Sugar includes `.compact(all)`][sugar] which may cause
webcompat issues - as the `all` boolean (defaulting to false)
determines if elements removed should be falsey (when `true`)
or nullish (when `false`).

## Other languages

- [Ruby has a `.compact` method][ruby], which wil return an
  Array with all `nil` elements removed

## Polyfill

- None as of yet.

[filter_id]: https://cs.github.com/?scopeName=All+repos&scope=&q=%2F.filter%5C%28%5Ba-z%5D%5Cs*%3D%3E%5Cs*%5Ba-z%5D%5C%29%2F+%28language%3AJavaScript+OR+language%3ATypeScript%29
[filter_b_pred]: https://cs.github.com/?q=%2F.filter%5C(Boolean%5C)%2F%20(language%3AJavaScript%20OR%20language%3ATypeScript)&scopeName=All%20repos&scope=
[filter_b]: https://cs.github.com/?scopeName=All+repos&scope=&q=%2F.filter%5C%28%5Ba-z%5D%5Cs*%3D%3E%5Cs*Boolean%5C%28%5Ba-z%5D%5C%29%5C%29%2F+%28language%3AJavaScript+OR+language%3ATypeScript%29
[filter_double_negation]: https://cs.github.com/?scopeName=All+repos&scope=&q=%2F.filter%5C%28%5Ba-z%5D%5Cs*%3D%3E%5Cs*%21%21%5Ba-z%5D%5C%29%2F+%28language%3AJavaScript+OR+language%3ATypeScript%29
[lodash]: https://lodash.com/docs/4.17.15#compact
[lodash-npm]: https://www.npmjs.com/package/lodash.compact
[sugar]: https://sugarjs.com/docs/#/Array/compact
[ruby]: https://ruby-doc.org/core-2.7.0/Array.html#method-i-compact
