---
title: '[JavaScript] JavaScript tools'
created: '2022-11-23T18:24:01.490Z'
modified: '2022-12-23T19:58:23.775Z'
---

# [JavaScript] JavaScript tools

## IntersectionObserver object : 

You can create a new IntersectionObserver object, and set a threshold.
**Threshold is a number between 0 and 1, that represents the viewable area of the target element in the screen**.
For example, 0 represents no area of element is visible. A value of 0.10 represents about 10% area is viewable in screen. Value of 1 means element is fully viewable in screen.
You can even specify multiple thresholds.

## Cuando un elemento se hace visible en la pantalla (**threshold [0]**) : 
In the current case where we just want to know when element becomes viewable in screen, the Javascript code will be :
```js
var observer = new IntersectionObserver(function(entries) {
	// isIntersecting is true when element and viewport are overlapping
	// isIntersecting is false when element and viewport don't overlap
	if(entries[0].isIntersecting === true)
		console.log('Element has just become visible in screen');
}, { threshold: [0] });

observer.observe(document.querySelector("#main-container"));
```

## Cuando un elemento es totalmente visible en la pantalla (**threshold [1]**):
If we want to know when element becomes fully visible in screen :
```js
var observer = new IntersectionObserver(function(entries) {
	if(entries[0].isIntersecting === true)
		console.log('Element is fully visible in screen');
}, { threshold: [1] });

observer.observe(document.querySelector("#main-container"));
```

## Detectar current mediaQuerie :

```js
window.matchMedia("(max-width: 500px)").matches;
// returns true || false
```
