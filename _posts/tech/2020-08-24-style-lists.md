---
layout: post
title:  "Display list item number on a different element"
description: "Using a custom CSS counter to display list number on an element that is not a list item <li>"
categories: tech
tags: css
---

![screenshot](/assets/img/posts/style-lists/list-style.png)

A quick post about how I style elements in lists (that are not the `<li>` itself) with the corresponding item number using a custom [CSS counter](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters).

I regularly use custom list styling like this for work on [mozilla.org](https://www.mozilla.org). Here is a simplified real-world example: 

## html
```html
<ol>
    <li>
        <h3>Click on the Firefox installer.</h3>
        <div>
            <img src="..." alt="...">
        </div>
        <div>
            <p><strong>Look down, look left.</strong> Click on the Firefox installer in the lower bottom left-hand corner.</p>
        </div>
    </li>

    <li>
        <h3>Select ‘Yes.’</h3>
        <div>
            <img src="..." alt="...">
        </div>
        <div>
            <p>Click YES for Firefox. <strong>Select YES</strong> on the pop-up window to finish the install.</p>
        </div>
    </li>
</ol>
```

The native styling for these list items isn't positioned where we would like. A better spot would be alongside the titles `<h3>`.

## CSS

```css
ol {
    counter-reset: list-counter;
    list-style: none;
}
```
Targeting the parent ordered list element `<ol>`, we set our custom [CSS counter](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Lists_and_Counters/Using_CSS_counters) named `list-counter` to 0 via `counter-reset`

**PRO-TIP:** You can name this counter whatever you would like **except** `list-item`. It is a special keyword value for counters that _will absolutely_ cause cross-browser counting issues. I learned this the hard way and discovered this "bug" via [stackoverflow](https://stackoverflow.com/a/53423535/11167751).

`list-style: none` is also included here to remove the default number display, which we will soon be replacing with our own custom version.

```css
ol>li {
    counter-increment: list-counter;
}
```
Targeting all direct `li` children of the `ol` element to increment `list-counter` by 1.

```css
h3::before {
    background: #4a4a55;
    border-radius: 50%;
    color: #ffffff;
    content: counter(list-counter);
    font-size: 1rem;
    line-height: 2.5rem;
    text-align: center;
    margin: 0 16px 16px 0;
    /*- any desired styles -*/
}
```
_Now the fun part!_ 😎

We can use our dynamic variable of `list-counter` inside a `counter()` function to display the correct number value. I chose to do this by selecting the `::before` [pseudo-element](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-elements) which is the perfect vessel for inserting our list numbers via `content: counter(list-counter)`.
