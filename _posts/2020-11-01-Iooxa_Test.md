---
title: "Iooxa Test"
description: "Testing Iooxa Graphing Interaction in Fastpages"
layout: post
toc: false
comments: true
image:
date: 2020-11-01 11:39:52
hide: false
search_exclude: false
---
We're going to try interactive function-plotting via a little javascript from [iooxa.dev](https://iooxa.dev/).
Here's the code we're about to add, escaped so you can see it.

```html
<script async="" src="https://unpkg.com/@iooxa/article"></script>
<article>
    <r-svg-chart width="400", height="250" xlim="[-3, 3]" ylim="[-0.01,3]" xlabel="x" ylabel="ReLU(x)">
        <r-svg-eqn eqn="Math.max(0, x)" stroke="blue" stroke-width="3"></r-svg-eqn>
    </r-svg-chart>
</article>
```
If you put the above few lines into a raw HTML file and open it in a browser, you get a nice plot of a ReLU activation.

And now we'll add below raw, and see if it the plot appears:

<script async="" src="https://unpkg.com/@iooxa/article"></script>
<article>
    <r-svg-chart width="400", height="250" xlim="[-3, 3]" ylim="[-0.01,3]" xlabel="x" ylabel="ReLU(x)">
        <r-svg-eqn eqn="Math.max(0, x)" stroke="blue" stroke-width="3"> </r-svg-eqn>
    </r-svg-chart>
</article>

How did we do?  Did we get a plot?  

No, for some reason Fastpages is escaping a few of the angle-brackets for line defining the `r-svg-eqn` object.  Don't do that, Fastpages! Leave my HTML alone!
