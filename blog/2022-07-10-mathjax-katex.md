---
title: How use math equations in Docusaurus
description: Learn how to convert MathJax for Jekyll to KaTeX for Docusaurus for using math equations in text.
tags: [docusaurus, jekyll, markdown, tutorials]
---

Learn how to convert MathJax for Jekyll to KaTeX for Docusaurus for using math equations in text.

<!--truncate-->

One of the challenges I encountered when moving my website from Jekyll to Docusaurus was rendering math equations in some of my blog posts (for example, about [the apriori algorithm](blog/2021-10-17-market-basket-analysis-with-apriori-algorithm.mdx)). In Jekyll, I used [MathJax](https://docs.mathjax.org/en/latest/index.html#) with [Liquid](https://shopify.github.io/liquid/) to render them. This didn't work in Docusaurus, so instead I had to use [KaTeX](https://katex.org/).

The [Docusaurus docs](https://docusaurus.io/docs/markdown-features/math-equations) provide pretty clear instructions on how to use KaTeX in your project. This post is a more straightforward tutorial, and reflects my experience (and issues) specific to my website.


1. Install the `remark-math` and `rehype-katex` plugins (in my case, with npm):
   
    `npm install --save remark-math@3 rehype-katex@5 hast-util-is-element@1.1.0`

2. Open your project's configuration file `docusaurus.config.js`:
   
   - **At the top** (right after the lines importing the Docusaurus themes), add the two plugins:

        ```javascript
        const math = require('remark-math');
        const katex = require('rehype-katex');
        ```
    
    - **In presets**, under both the docs and blog categories, add the two plugins:

        ```javascript
        remarkPlugins: [math],
        rehypePlugins: [katex],
        ```

        Make sure to add the plugins under all page categories where you want math equations to be rendered. I initially added them only under docs, and was confused why equations were rendered on my About page, but not in blog posts, until I figured out the reason.

    - In stylesheets, add: the source of KaTeX:

        ```javascript
          stylesheets: [
            {
            href: 'https://cdn.jsdelivr.net/npm/katex@0.13.24/dist/katex.min.css',
            type: 'text/css',
            integrity:
                'sha384-odtC+0UGzzFL/6PNoE8rX/SPcQDXBJ+uRepguP4QkPCm2LBxH3FA3y+fKSiJ+AmM',
            crossorigin: 'anonymous',
            },
        ],
        ```

3. Update the formulas in existing content, considering the differences between Jekyll vs. Docusaurus, and Mathjax vs. KaTeX.
   
   - In Jekyll, formulas are wrapped in double `$$`, whereas for Docusaurus they're wrapped in single `$`. Replace all instances of `$$` with `$`.
   - If some equations are still not displayed correctly, it might be because they need a different syntax in KaTeX than in MathJax. Check this in the [KaTeX docs of suported functions](https://katex.org/docs/supported.html) and test the equations in their [online editor](https://katex.org/#demo).

