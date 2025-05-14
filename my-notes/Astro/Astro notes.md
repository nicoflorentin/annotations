
#### Import local scripts

**When to use this:** when your script lives inside of `src/`.

Astro will build, optimize, and add these scripts to the page for you, following its [script processing rules](https://docs.astro.build/en/guides/client-side-scripts/#script-processing).

src/components/LocalScripts.astro

```html
<!-- relative path to script at `src/scripts/local.js` -->
<script src="../scripts/local.js"></script>

<!-- also works for local TypeScript files -->
<script src="./script-with-types.ts"></script>
```

#### Load external scripts