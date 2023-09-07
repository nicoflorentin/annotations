
### Plugins

By default you can't. However I use these simple lines in `tailwind.config.js` to give me `child` and `child-hover` options.

```xml
plugins: [
    function ({ addVariant }) {
        addVariant('child', '& > *');
        addVariant('child-hover', '& > *:hover');
    }
],
```

Then use like this

```xml
<div class="child:text-gray-200 child-hover:text-blue-500">...</div>
```

Which will give every child a gray textcolor, and a blue one on hover.

See [here](https://tailwindcss.com/docs/plugins#adding-variants) for more information on adding variants using a plugin

**Update** 4th of july 2022: Tailwind added an ad-hoc approach to target specific elements. You can now use `[&>*]:text-gray-200` or `[&>*:hover]:text-blue-500` to mimic the above behaviour. See the answer of @phum for more info!

