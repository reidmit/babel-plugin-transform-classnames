# babel-plugin-classnames

A Babel plugin that optimizes the composition of class names in React components (or anywhere, really). It lets you write code similarly to how you would with the popular [classnames](https://github.com/JedWatson/classnames) library, but this "library" is optimized away at build time.

Input:

```js
import cn from 'babel-plugin-transform-classnames';

function MyComponent(props) {
  return (
    <div
      className={cn('hello', 'world', something, {
        always: true,
        never: false,
        wow: props.test,
        big: props.size > 100
      })}
    />
  );
}
```

Output:

```js
function MyComponent(props) {
  return (
    <div
      className={
        'hello world ' +
        (something || '') +
        ' always' +
        (props.test ? ' wow' : '') +
        (props.size > 100 ? ' big' : '')
      }
    />
  );
}
```

This removes your dependency on a library like `classnames` and means that no extra work is done to join your class names together at runtime.
