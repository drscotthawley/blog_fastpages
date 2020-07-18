---
title: "Citations in Fastpages via BibTeX and jekyll-scholar"
description: Supporting scholarly blogging by drawing references from your database.
layout: post
toc: true
comments: true
image:
hide: false
search_exclude: false
---

*(N.B.: The following was created as a Markdown file in `_posts/`. For Jupyter notebooks, the same things apply; one simply enters the Liquid codes into Markdown cells.  [Quick Jupyter example.](https://drscotthawley.github.io/devblog4/jupyter/2020/07/01/BibTeX-Check-For-Jupyter.html)*)



## How to Cite 

For demonstration purposes, I'll take the liberty of citing a couple of my recent papers, namely the first SignalTrain paper{% cite signaltrain %} and the new one by Billy Mitchell{% cite billy_signaltrain2 %}.  Instead of using the LaTeX code {% raw %}\cite{ \<whatever> }{% endraw %}, I use the Liquid code {% raw  %}{% cite \<whatever> %}{% endraw %}.  For example, the first citation above is written as "{% raw  %}{% cite signaltrain %}{% endraw %}" in the Markdown file that generates this HTML page. 


The two citation markings above point to the References section at the end of this post where the full references are printed out in the bibliography style of my choice.


## Drawing from the Bibliography 

In the main blog directory, create a new directory called `_bibliography/`, and place your BibTeX file there as [references.bib](../_bibliography/references.bib).  In the case of this demo, the references file looks like this:

```bibtex
@conference{signaltrain,
  title = {Profiling Audio Compressors with Deep Neural Networks},
  author = {Hawley, Scott H. and Colburn, Benjamin and Mimilakis, Stylianos Ioannis},
  booktitle = {Audio Engineering Society Convention 147},
  month = {Oct},
  year = {2019},
  url = {http://www.aes.org/e-lib/browse.cfm?elib=20595}
}               

@article{billy_signaltrain2, 
  title={Exploring Quality and Generalizability in Parameterized Neural Audio Effects},
  author={William Mitchell and Scott H. Hawley},
  journal={ArXiv},  
  year={2020},
  volume={abs/2006.05584} 
  url = {https://arxiv.org/abs/2006.05584}
} 
```

Note that this  (single) references file is for your entire blog. The great thing about this is that all your Jupyter notebooks and Markdown posts will draw from this same file, which could be hundreds of references long, and jekyll-scholar will only include the ones you need for each post.

Finally, at the end of your post, you signal the creation of the list of references by using the Liquid tag

```liquid
{% raw %}{% bibliography --cited %}{% endraw %}
```

...so I'll put that at the very bottom of this file.  (Currently that'll generate an error, because we haven't enabled jekyll-scholar yet, but we'll do that next.)   The optional argument `--cited` means it'll only list the references cited in your post.


## Enabling Jekyll-Scholar


To enable jekyll-scholar, all we need to do is make the following two changes, and perhaps a third.  

1. In `_config.yml`, add "` - jekyll-scholar`" to the list of `plugins:`.

2. Edit the `Gemfile` to include `gem 'jekyll-scholar'` where the other plugins are listed. 

3. Optional: The default citation format is "apa".  If you want to change that, you can add the following to your `_config.yml` file: 

   ```yaml
   scholar:
       style: <name>
   ```

   ...naming one of the styles in the [CSL style repository](https://github.com/citation-style-language/styles) (but leaving off the `.csl` ending).  Tip from the CSL maintainers:

   > To quickly search the styles in the GitHub [CSL style repository](https://github.com/citation-style-language/styles) by file name, press “t” to activate GitHub’s [File Finder](https://github.com/blog/793-introducing-the-file-finder) and start typing.

   Note however that the `csl-styles` Gem package used by jekyll-scholar **lags behind the official CSL style repository**, so some names you choose may not work.  In that case, you can supply a CSL file yourself.  For this demo, I found the file `physical-review-d.csl`, added it to my main blog directory, and then specified the style name `physical-review-d` in `_config.yml`.  This produced the bracketed-number citation markers above, and the reference format you see below in the References section.

The convenience of this BibTeX/jekyll-scholar approach is that instead of having to manually edit references on each individual page -- say, if you wanted to change citation formats (or alternatively, update information about a paper  cited in multiple posts) -- now you only change **one line** in `_config.yml` (or update one spot in `references.bib`) and the system "builds out" the change "everywhere."

Happy blogging! 


# References

{% bibliography --cited %}

