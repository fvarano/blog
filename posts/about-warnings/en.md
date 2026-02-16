---
title: "About Warnings"
date: "2026-02-16"
language: "en"
---

Warnings in code are different from errors: they don't block the workflow, and it's possible to reach "working" code even while ignoring them. This characteristic makes them easy to overlook, but can lead to serious consequences over time.

## Why ignoring warnings is dangerous

When we systematically ignore warnings, three things happen:

1. **We lose understanding**: we skip the opportunity to understand a potential problem in our code
2. **We generate distrust**: the warning system loses credibility and usefulness
3. **We create noise**: a wall of warnings makes it impossible to notice when a new one appears or when one gets resolved

## How to handle warnings correctly

### Understand before acting

The first step is to understand what the tool is telling us. What's the reason behind that warning? Why is that practice discouraged? What problems can it lead to? Only after understanding the context does it make sense to decide how to proceed.

In most cases, the best solution is to follow the guidance from the documentation of the tool that issued the warning.

### If it's a false positive

First of all: **are we really sure?**

If after careful analysis we confirm it's a false positive:

1. Disable the warning **locally** on the specific portion of code (never at the project level)
2. Document with a comment the reason why it's considered a false positive in that specific case
3. If the same situation repeats in many places in the code with the same reason (symptom of a systemic project issue), consider creating a centralized atomic component or function that encapsulates the code with the warning disabled and the related documentation

### If it's a systemic issue

When a warning or error is systemic to the project and not solvable at the application code level, once again: **are we really sure?**

If the answer is yes:

1. Consider a suppression at the build level, but **only for strictly necessary warnings**
2. Schedule a periodic re-evaluation of this decision because:
   - It's likely that the suppression is no longer necessary after an update of the affected dependencies
   - The dependencies might be obsolete and replaceable with modern alternatives (e.g., Babel → [Oxc](https://oxc.rs), [esbuild](https://esbuild.github.io/)) or no longer necessary (e.g., Sass → [native CSS](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Nesting_selector) ([baseline](https://caniuse.com/css-nesting)))

## Conclusion

A clean build is a sign of a project under control. Warnings, if listened to, can help us catch problems before they become critical and keep the code more understandable over time.
