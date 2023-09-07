With the upgraded Create React App released recently, we got a lot of new tools to play with. Sass is one that I’m excited to have built in, since we used to have to make .scss files compile and write to .css files right in our folder structure. You may be concerned about using Sass in React. Isn’t it a smarter way to write styles with CSS-in-JS libraries like styled-components or aphrodite? I believe that adding Sass support to Create React App will be a big help for React beginners.

Here are some steps to follow:

- Let’s start by installing the Create React App. You can do that by running npm install -g create-react-app globally or using npx create-react-app to download and invoke it immediately so your installed package won’t be anywhere in your globals. You can find out more about npx here.
- Create a new React project with create-react-app app-name and then change into that directory.
- Install the node-sass dependency using npm install node-sass --save. This will compile your scss to css.
- That’s it — we’re done. We can test the configuration by changing our src/App.css file to src/App.scss file and updating src/App.js to import it. Then we can try out some cool Sass/SCSS features.

## Common Examples
Here’s a way to use variables in SCSS:

```css
$blue: #004BB4;
$ubuntu-font: 'Ubuntu', 'Arial', 'Helvetica', sans-serif;
$nunito-font: 'Nunito', 'Arial', 'Helvetica', sans-serif;
```

Once you’ve created the variables, you can use them wherever you need to, like this:

```css
h1 {
  font: $ubuntu-font;
  color: $blue;
}
a {
  font: $nunito-font;
  background-color: $blue;
  padding: 6px;
}
```
When you compile your SCSS files, the Sass compiler will take care of the variables you’ve used in your source file, replacing the variable name with its stored value. And changing the value of the color is as quick as updating the variable content and re-compiling. Gone are the days of using “Find and Replace” in your favorite text editor to change colors in your CSS file.

A worthwhile feature that I covered previously is the “nesting” feature of SCSS. An example of that can be demonstrated here:

```html
<ul class="navbar">
  <li><a href="/">Item <span>1</span></a></li>
  <li><a href="/">Item <span>2</span></a></li>
  <li><a href="/">Item <span>3</span></a></li>
  <li><a href="/">Item <span>4</span></a></li>
  <li><a href="/">Item <span>5</span></a></li>
</ul>
```

```css
.navbar {
  font: $ubuntu-font;
  color: $blue;
  li {
    margin-left: 1rem;
    a {
      padding: 5px;
      font-size: 1.5rem;
      span {
        font-weight: 600;
      }
    }
  }
}
```
However, be aware that nesting too deeply is not good practice. The deeper you nest, the more verbose the Sass file becomes and the larger the compiled CSS will potentially be, since the nesting is flattened when compiled. So, overuse of nesting can create overly specific CSS rules that are hard to maintain. There’s a chance that the selectors can’t be reused, and there are performance issues too. Nested selectors will create a long CSS selector string that will end up generating a bigger CSS file.

## Wrapping Up
In this article, I looked at several ways of styling components in a React application. I then compared and contrasted these methods examining their advantages and disadvantages. Finally, I demonstrated how to use Sass (my preferred method of styling a React application) in a Create React App project.

Sass is a CSS preprocessor, and CSS preprocessors are here to stay. They extend the basic CSS features by providing you with a set of powerful functionalities that will raise your productivity right away. I mentioned a few benefits, but there are many more, like inheritance, functions, control directives, and expressions like if(), for() or while(), data types, interpolation, and so on.

Becoming a Sass guru may take a bit of time; all you need to do is look into the Bootstrap Sass files to see how Sass could turn into a complex thing. But learning the basics and setting it up for your project is something you could start today.




