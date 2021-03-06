```js
const renderer = TestUtils.createRenderer();
renderer.render(<MyComponent />);

// Extra props and children from the render are ignored
expect(renderer, 'to have rendered', <div className="parent" />);

// The span "two" is missing here, but it is ignored.
expect(renderer, 'to have rendered',
   <div id="main">
      <span>one</span>
      <span>three</span>
  </div>
);

// The following assertion will fail, as 'four' does not exist
expect(renderer, 'to have rendered',
   <div id="main">
      <span>one</span>
      <span>four</span>
  </div>
);
```

If you want to check for an exact render, use `'to have exactly rendered'`.

Alternatively, if you don't care about extra props, but want to check that there are no extra child nodes, use `'to have rendered with all children'`
Note that `exactly` implies `with all children`, so you using both options is not necessary.

Normally wrappers (elements that simply wrap other components) are ignored. This can be useful if you have higher order
components wrapping your components, you can simply ignore them in your tests (they will be shown greyed out 
if there is a "real" error).  If you want to test that there are no extra wrappers, simply add 
`with all wrappers` to the assertion.


```js

// The span "two" is missing here, as is `className="parent"`
// The missing span will cause an assertion error, but the extra prop will be ignored
// due to `to have rendered with all children` being used

expect(renderer, 'to have rendered with all children',
   <div id="main">
      <span>one</span>
      <span>three</span>
  </div>
);
```

```js

// The span "two" is missing here, as is `className="parent"`
// This will cause an assertion error,
// due to `to have exactly rendered` being used

expect(renderer, 'to have exactly rendered',
   <div id="main">
      <span>one</span>
      <span>three</span>
  </div>
);
```

