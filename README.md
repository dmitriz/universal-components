# universal-components
Write UI components that work with any framework any DOM library


## The Web has Fragmentation problem

Everyone speaks about "reusable" UI components, yet most UI libraries are framework-specific, must be used exactly as intended, not modular, require hard configuration, fragile etc.

Does it really have to be that way and what is the alternative?


## An Alternative from Ideal World

In an ideal world with no boundaries, all UI components are composed from small general purpose universal lego-block-style pure functions. Functions producing nodes from pure data and functions transforming nodes. You want to change the font size? Here:

```js
// data last Ramda style
setFontSize(size, node)

// fluent style
node.setFontSize(size)
```

Which are themselves derived from their universal style setter `setStyle`:

```js
setFontSize = fontSize => node => setStyle({fontSize})
```

And now you never need to hard code font sizes inside your buttons!
All sizes and spaces should be exposed as functional parameters in the most general 


The same goes to applying any other style.

Want to set gap space between the children blocks which [semantically belongs to parent even if the CSS currently forces you to set margins onto children](https://medium.com/@taion/the-problem-with-css-in-js-circa-mid-2016-14060e69bf68), just write

```js
const setChildrenGap = gap => node =>
    node.children.filter(notLast).setMarginRight(gap)
```

And done. 

### And frameworks? 

Why should your component depend on a framework?
The DOM is just plain JSON node tree! 
It looks exactly the same in any framework or no framework.

Why not keep the framework-specific element creator factories as simple parameters of your component?

```js
// use it inside React
const MyComp = createMyComp(React.createElement)

// or Inferno
const MyComp = createMyComp(Inferno.createElemet)

// or Mithril
const MyComp = createMyComp(m)

// or Angular
const MyComp = createMyComp(Angular.createElement)

// or Snabbdom
const MyComp = createMyComp(require('snabbdom/h'))

// or nothing
const MyComp = createMyComp(require('hyperscript'))
```

I can't say it better than @sindresorhus about reusable modules:
https://github.com/sindresorhus/ama/issues/10#issuecomment-117766328

Then how about writing UI nodes or fancy UI components, styled or not, in the same way as @sindresorhus writes his modules? :)
