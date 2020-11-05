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
<r-svg-chart width="400", height="250" xlim="[-3, 3]" ylim="[-0.01,3]" xlabel="x" ylabel="ReLU(x)">
   <r-svg-eqn eqn="Math.max(0, x)" stroke="blue" stroke-width="3"></r-svg-eqn>
</r-svg-chart>
```
If you put the above few lines into a raw HTML file and open it in a browser, you get a nice plot
of a ReLU activation
([click for example](https://hedges.belmont.edu/~shawley/iooxa_try.html)).

Now we'll add that code as raw HTML and see if the plot appears here:

<script async="" src="https://unpkg.com/@iooxa/article"></script>
<r-svg-chart width="400", height="250" xlim="[-3, 3]" ylim="[-0.01,3]" xlabel="x" ylabel="ReLU(x)">
   <r-svg-eqn eqn="Math.max(0, x)" stroke="blue" stroke-width="3"> </r-svg-eqn>
</r-svg-chart>

How did we do?  Did we get a plot?  

No, for some reason Fastpages is escaping a few of the angle-brackets for line defining the `r-svg-eqn` object.  Don't do that, Fastpages! Leave my HTML alone!

## A Hack That Works

Your `images/` folder is *theoretically* just for images.  But if you take the HTML code that you want to sneak past nbdev and put it in a file in the `images/` directory, then you can load it via an iframe. So let's put the above three lines in a file called `iooxa_graph.html` and save it in the `images/` directory. Then we put the following
in this post:

```html
<iframe src="../../../images/iooxa_graph.html" width="700px" height="280px" frameBorder="0"></iframe>
```

And here we go:

<iframe src="../../../images/iooxa_graph.html" width="700px" height="280px" frameBorder="0"></iframe>

Yea? :-) Now, why do that?  

Well, because now we can have some more interactivity, like this LeakyReLU graph and some half-wave rectifiers:
<iframe src="../../../images/iooxa_rect.html" width="800px" height="1000px" frameBorder="0"></iframe>

Nice. :-)
