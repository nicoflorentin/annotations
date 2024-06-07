
## Plugins

By default you can't. However I use these simple lines in `tailwind.config.js` to give me `child` and `child-hover` options.

```js
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

## Custom fonts
https://dev.to/dailydevtips1/using-google-fonts-in-a-tailwind-project-1jfo

```js
// ../tailwind.config.js

/** @type {import('tailwindcss').Config} */
export default {
  content: ["./index.html", "./src/**/*.{js,ts,jsx,tsx}"],
  theme: {
    extend: {
      colors: {
        primary: "#93C572",
        bone: '#DAD7CB'
      },
      fontFamily: {
	    //fuente con espacios
        espacios: ['"Press Start 2P"', "sans-serif"],
        consolas: ["consolas", "sans-serif"],
        inter: ['Inter', 'sans-serif']
      },
    },
  },
  plugins: [
    function ({ addVariant }) {
      addVariant("child", "& > *")
      addVariant("child-hover", "& > *:hover")
    },
  ],
}
```
```js
// ../index.css
@tailwind base;
@tailwind components;
@tailwind utilities;
  
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@700&display=swap");
@font-face {
  font-family: "rubik-mono-one";
  src: url("/src/assets/fonts/RubikMonoOne-Regular.ttf");
}
```

### Hide Scrollbar
https://dev.to/derick1530/how-to-create-scrollable-element-in-tailwind-without-a-scrollbar-4mbd

```js
//global index.css
@tailwind base;
@tailwind components;
@tailwind utilities;

// add the code bellow
@layer utilities {
      /* Hide scrollbar for Chrome, Safari and Opera */
      .no-scrollbar::-webkit-scrollbar {
          display: none;
      }
     /* Hide scrollbar for IE, Edge and Firefox */
      .no-scrollbar {
          -ms-overflow-style: none;  /* IE and Edge */
          scrollbar-width: none;  /* Firefox */
    }
  }
```