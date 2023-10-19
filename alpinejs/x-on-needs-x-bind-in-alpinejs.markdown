# Everything in AlpineJS requires an x-data directive

To use a simple click handler you might just drop in a `@click` directive:

```js
<div>
    <button @click="alert('Hello')">Click me</button>
</div>
```

This won’t work. It needs to be declared inside an `x-data` directive:

```js
<div x-data>
    <button @click="alert('Hello')">Click me</button>
</div>
```

This seems incredibly obvious in hindsight. It’s even described in the documentation:

> Everything in Alpine starts with the x-data directive.

Source: [Alpine.js documentation](https://alpinejs.dev/directives/data)

I think my confusion was that all the examples I read included bound data. There is an example that specifically handles using [Alpine without data](https://alpinejs.dev/essentials/state#data-less-alpine) but my mental model had `x-data` being required only for data. It’s actually required for context, with the bound data being optional context.











