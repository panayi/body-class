```
Meteor ================================================

'||     .|''''|, '||\   ||` '||'''|. .|''''|, '||\   ||`
 ||     ||    ||  ||\\  ||   ||   || ||    ||  ||\\  ||
 ||     ||    ||  || \\ ||   ||   || ||    ||  || \\ ||
 ||     ||    ||  ||  \\||   ||   || ||    ||  ||  \\||
.||...| `|....|' .||   \||. .||...|' `|....|' .||   \||.

 ============================================ body-class
```

Giving you `Blaze.addBodyClass` for **live live live** reactive class names on the body element.

Works automagically with [meteorhacks:flow-router](https://atmospherejs.com/meteorhacks/flow-router) & [iron:router](https://atmospherejs.com/iron/router) to add the current route name as a body class; useful for isolating your page specific css styles.

## It's super simple

```shell
meteor add london:body-class
```

Call `Blaze.addBodyClass(fn)` with a function and it's return value will be added as a class to the body.

If that function uses a reactive data source (Collection, Session, etc) then the body class will update when the dependencies change.

You can also just call `Blaze.addBodyClass('foo')` with a string to add a static class to the body.

## Examples

```javascript
Session.setDefault('state', 'alpha')

Blaze.addBodyClass(function() {
  return Session.get('state')
})
```
results in
```html
<body class="alpha">
```

The value from `Session.get('state')` is added as a class to the <body> element,
It will be updated whenever the value for `state` changes.


```javascript
// You can also add static classes
Blaze.addBodyClass('foo')

// Or some combination of the two...
Blaze.addBodyClass([
 'bar',
  function () { return Meteor.status().status }
])
```
results in

```html
<body class="foo bar connected">
```

Where `connected` will update to reflect the current connection state with the server.

So, remember kids:

- If [iron:router](https://atmospherejs.com/iron/router) is present, the current route is automatically added as a body class.
- If [meteorhacks:flow-router](https://atmospherejs.com/meteorhacks/flow-router) is present, the `name` property of the current route is automatically added as a body class.
- Calling `addBodyClass` multiple times is fine. They all end up as additional body classes.
- Duplicate classes are removed by virtue of using jQuery `addClass` to do the dirty work.
- For bonus points: add `Meteor.status().status` as a body class so you can visualize the connection health.

From the [meteorlondon](http://www.meteorlondon.com/) / [(╯°□°）╯︵ TABLEFLIP](http://tableflip.io) crew
