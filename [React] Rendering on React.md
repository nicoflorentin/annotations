---
tags: [React]
title: '[React] Rendering on React'
created: '2022-09-23T19:52:28.535Z'
modified: '2022-10-20T03:14:21.349Z'
---

# [React] Rendering on React

Source : https://www.developerway.com/posts/react-re-renders-guide#part1

When React component re-renders itself?
There are four reasons why a component would re-render itself: **state changes, parent (or children) re-renders, context changes, and hooks changes**. There is also a big myth: that re-renders happen when the component’s props change. By itself, it’s not true (see the explanation below).

🧐 Re-renders reason: state changes
When a component’s state changes, it will re-render itself. Usually, it happens either in a callback or in useEffect hook.

State changes are the “root” source of all re-renders.



🧐 Re-renders reason: parent re-renders
A component will re-render itself if its parent re-renders. Or, if we look at this from the opposite direction: when a component re-renders, it also re-renders all its children.

It always goes “down” the tree: the re-render of a child doesn’t trigger the re-render of a parent. (There are a few caveats and edge cases here, see the full guide for more details: The mystery of React Element, children, parents and re-renders).



🧐 Re-renders reason: context changes
When the value in Context Provider changes, all components that use this Context will re-render, even if they don’t use the changed portion of the data directly. Those re-renders can not be prevented with memoization directly, but there are a few workarounds that can simulate it (see Part 7: preventing re-renders caused by Context).



🧐 Re-renders reason: hooks changes

Everything that is happening inside a hook “belongs” to the component that uses it. The same rules regarding Context and State changes apply here:

state change inside the hook will trigger an unpreventable re-rerender of the “host” component
if the hook uses Context and Context’s value changes, it will trigger an unpreventable re-rerender of the “host” component
Hooks can be chained. Every single hook inside the chain still “belongs” to the “host” component, and the same rules apply to any of them.



⛔️ Re-renders reason: props changes (the big myth)
It doesn’t matter whether the component’s props change or not when talking about re-renders of not memoized components.

In order for props to change, they need to be updated by the parent component. This means the parent would have to re-render, which will trigger re-render of the child component regardless of its props.

Only when memoization techniques are used (React.memo, useMemo), then props change becomes important.
