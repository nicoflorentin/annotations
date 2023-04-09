---
tags: [React]
title: '[React] Components Styling Options'
created: '2022-02-09T04:49:02.898Z'
modified: '2022-02-09T05:55:45.683Z'
---

# [React] Components Styling Options

## Inline CSS
- Dependencies: None
- Difficulty: Easy
- Approach: Worst

No creo que nadie necesite una introducción al CSS en línea. Esto es el estilo CSS enviado al elemento directamente usando el HTML o JSX. Puedes incluir un objeto JavaScript para CSS en los componentes de React, aunque hay algunas restricciones como el uso de camel casing en cualquier nombre de propiedad que contenga un guión. Puedes estilizar los componentes React de dos maneras usando objetos JavaScript como se muestra en el ejemplo.

**Example**
```js
import React from "react";

const spanStyles = {
  color: "#fff",
  borderColor: "#00f"
};

const Button = props => (
  <button style={{
    color: "#fff",
    borderColor: "#00f"
  }}>
    <span style={spanStyles}>Button Name</span>
  </button>
);
```

## Regular CSS

- Dependencies: None
- Difficulty: Easy
- Approach: Okay

El CSS regular es un enfoque común, posiblemente un paso mejor que el CSS en línea. Los estilos pueden importarse a cualquier número de páginas y elementos, a diferencia del CSS en línea, que se aplica directamente al elemento concreto. El CSS normal tiene varias ventajas, como la compatibilidad nativa con los navegadores (no requiere dependencias), no hay que aprender herramientas adicionales y no hay peligro de bloqueo de proveedores.

Puedes mantener cualquier número de hojas de estilo, y puede ser más fácil cambiar o personalizar los estilos cuando sea necesario. Pero el CSS normal puede ser un gran problema si estás trabajando en un proyecto más grande con muchas personas involucradas, especialmente sin una guía de estilo acordada para escribir CSS.

**Example**
```js
/* styles.css */

a:link {
  color: gray;
}
a:visited {
  color: green;
}
a:hover {
  color: rebeccapurple;
}
a:active {
  color: teal;
}
import React from "react";
import "styles.css";

const Footer = () => (
  <footer>
    &copy; 2020
    <a href="https://twitter.com/praveenscience">Find me on Twitter</a>
  </footer>
);

export default Footer;
```

**More Information**
You can read more about regular CSS usage of the W3C’s Learning CSS page. There are many playgrounds — such as JS Bin, JSFiddle, CodePen, and Repl.it — where you can try it out live and get the results in real time.

# CSS-in-JS

CSS-in-JS is a technique which enables you to use JavaScript to style components. When this JavaScript is parsed, CSS is generated (usually as a style element) and attached into the DOM.

There are several benefits to this approach. For example, the generated CSS is scoped by default, meaning that changes to the styles of a component won’t affect anything else outside that component. This helps prevent stylesheets picking up bloat as time goes by; if you delete a component, you automatically delete its CSS.

Another advantage is that you can leverage the power of JavaScript to interact with the CSS. For example, you can create your own helper functions in JavaScript and use them directly in your CSS to modify the code.

Next, we’ll look at two libraries that can be used to implement this in a React app.

**JSS**
- Dependencies: react-jss
- Difficulty: Easy
- Approach: Decent

JSS bills itself as “an authoring tool for CSS which allows you to use JavaScript to describe styles in a declarative, conflict-free and reusable way”. It’s framework agnostic, but when it comes to styling React components, React-JSS integrates JSS with React using the new Hooks API.

**Example**
```js
import React from "react";
import {render} from "react-dom";
import injectSheet from "react-jss";

// Create your styles. Since React-JSS uses the default JSS preset,
// most plugins are available without further configuration needed.
const styles = {
  myButton: {
    color: "green",
    margin: {
      // jss-expand gives more readable syntax
      top: 5, // jss-default-unit makes this 5px
      right: 0,
      bottom: 0,
      left: "1rem"
    },
    "& span": {
      // jss-nested applies this to a child span
      fontWeight: "bold" // jss-camel-case turns this into 'font-weight'
    }
  },
  myLabel: {
    fontStyle: "italic"
  }
};

// Define the component using these styles and pass it the 'classes' prop.
const Button = ({ classes, children }) => (
  <button className={classes.myButton}>
    <span className={classes.myLabel}>{children}</span>
  </button>
);

// Finally, inject the stylesheet into the component.
const StyledButton = injectSheet(styles)(Button);

const App = () => <StyledButton>Submit</StyledButton>
render(<App />, document.getElementById('root'))
```

**More Information**
You can learn more about this approach in the JSS official documentation. There’s also a way to try it out using their REPL (read-eval-print loop).

# Styled-Components

- Dependencies: styled-components
- Difficulty: Medium
- Approach: Decent

Styled-components is a further library that implements the above-mentioned CSS-in-JS technique. It utilizes tagged template literals — which contain actual CSS code between two backticks — to style your components. This is nice, as you can then copy/paste CSS code from another project (or anywhere else on the Web) and have things work. There’s no converting to camel case or to JS object syntax as with some other libraries.

Styled-components also removes the mapping between components and styles. As can be read in their documentation, this means that when you’re defining your styles, you’re actually creating a normal React component that has your styles attached to it. This makes your code more succinct and easy to follow, as you end up working with a Layout component, as opposed to a div with a class name of “layout”.

Props can be used to style styled components in the same way that they are passed to normal React components. Props are used instead of classes in CSS and set the properties dynamically.

Example

import React from "react";
import styled, { css } from "styled-components";

const Button = styled.button`
  cursor: pointer;
  background: transparent;
  font-size: 16px;
  border-radius: 3px;
  color: palevioletred;
  margin: 0 1em;
  padding: 0.25em 1em;
  transition: 0.5s all ease-out;
  ${props =>
    props.primary &&
    css`
      background-color: white;
      color: green;
      border-color: green;
    `};
`;

export default Button;

**More Information**
Styled-components has detailed documentation, and the site also provides a live editor where you can try out the code. Get more information on styled-components at styled-components: Basics.

# CSS Modules

- Dependencies: css-loader
- Difficulty: Tough (Uses Loader Configuration)
- Approach: Better

If you’ve ever felt like the CSS global scope problem takes up most of your time when you have to find what a particular style does, or if getting rid of CSS files leaves you nervously wondering if you might break something somewhere else in the code base, I feel you.

CSS Modules solve this problem by making sure that all of the styles for a component are in one single place and apply only to that particular component. This certainly solves the global scope problem of CSS. Their composition feature acts as a weapon to represent shared styles between states in your application. They are similar to mixins in Sass, which makes it possible to combine multiple groups of styles.

**Example**
```js
import React from "react";
import style from "./panel.css";

const Panel = () => (
  <div className={style.panelDefault}>
    <div className={style.panelBody}>A Basic Panel</div>
  </div>
);

export default Panel;
.panelDefault {
  border-color: #ddd;
}
.panelBody {
  padding: 15px;
}
```
Please note that, if you’re using Create React App, it supports CSS Modules out of the box. Otherwise, you’ll need webpack and a couple of loaders that enable webpack to bundle CSS files. Robin Wieruch has a great tutorial on this.

# Sass & SCSS

- Dependencies: node-sass
- Difficulty: Easy
- Approach: Best

Sass claims that it’s the most mature, stable, and powerful professional-grade CSS extension language in the world. It’s a CSS preprocessor, which adds special features such as variables, nested rules and mixins (sometimes referred to as “syntactic sugar”) into regular CSS. The aim is to make the coding process simpler and more efficient. Just like other programming languages, Sass allows the use of variables, nesting, partials, imports and functions, which add super powers to regular CSS.

There are a number of ways that a Sass stylesheet can be exported and used in a React project. As you might expect, Create React App supports Sass out of the box. If you’re using webpack, you’ll need to use the sass-loader, or you could just use the sass --watch command.

We look at how to use Sass with Create React App at the end of this article.

**Example**
```css
$font-stack: 'Open Sans', sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}
```

**More Information**
Learn more about using and installing Sass with a variety of programming languages from their official documentation at Sass: Syntactically Awesome Style Sheets. If you want to try something out, there’s a service called SassMeister – The Sass Playground! where you can play around with different features of Sass and SCSS.

# Less

- Dependencies: less, less-loader
- Difficulty: Easy
- Approach: Good

Less (Leaner Style Sheets) is an open-source, dynamic preprocessor style sheet language that can be compiled into CSS and run on the client side or server side. It takes inspiration from both CSS and Sass and is similar to SCSS. A few notable differences include variables starting with an @ sign in Less and with a $ in Sass.

**Example**
```css
@pale-green-color: #4D926F;

#header {
  color: @pale-green-color;
}
h2 {
  color: @pale-green-color;
}

```

**More Information**
You can get started with Less from the official documentation, and there’s LESSTESTER, a Less Sandbox that converts your Less code into CSS.

# Stylable

- Dependencies: stylable, @stylable/webpack-plugin
- Difficulty: Difficult
- Approach: Better

If you’re not the biggest fan of CSS-in-JS, then Stylable might be for you. It’s a preprocessor that enables you to scope styles to components so they don’t leak and clash with other styles elsewhere in your app. It comes with several handy features — such as the ability to define custom pseudo-classes — so that you can apply styles to your components based on state. It is also inspired by TypeScript, with the project’s home page stating:

We want to give CSS a type system — to do for CSS what TypeScript does for JavaScript.

When it comes to integrating Stylable with React, they offer a handy guide. There’s also the create-stylable-app project, which will initialize a React-based web application with Stylable as its styling solution.

**Example**
```css
@namespace "Example1";

/* Every Stylable stylesheet has a reserved class called root
that matches the root node of the component. */
.root {
  -st-states: toggled, loading;
}
.root:toggled { color: red; }
.root:loading { color: green; }
.root:loading:toggled { color: blue; }
/* CSS output*/
.Example1__root.Example1--toggled { color: red; }
.Example1__root.Example1--loading { color: green; }
.Example1__root.Example1--loading.Example1--toggled { color: blue; }
```

**More Information**
Stylable has much more to offer. The official documentation on getting started provides detailed explanation.



