---
title: Building a website with Docusaurus and GitLab Pages
description: 
tags: [docusaurus, jekyll, tutorial]
---

I [created the website](https://github.com/lorenanda/lorenanda.github.io) you're seeing now over two years ago, using [Jekyll](https://jekyllrb.com/) and [GitHub Pages](https://pages.github.com/). For a start, I used the [Beautiful Jekyll theme](https://beautifuljekyll.com/), but in time I edited it to match my personal style. 

## Creating a GitLab project

To keep organized, I use different branches branches:

- `main` for everything - the branch of it all.
- `blog` for blog posts (adding new ones, updating existing ones, and fixing typos).
- `content` for website content (updating the about page and adding new projects).
- `design` for design and frontend stuff (changing fonts and colors).
- `features` for different features (adding Vale or a contact form).
- `pages` for configuring [GitLab pages for deploying the website](#deploying-docusaurus-with-gitlab-pages).

## Deploying Docusaurus with GitLab Pages

1. In the project root directory, I created a new file `gitlab-ci.yml`.
2. In the `gitlab-ci.yml` file, I used the following configuration:
    
    ```yaml
    image: node:15.12-alpine3.13

    stages:
        - deploy

    pages:
        stage: deploy
        script:
            - npm install
            - npm run build
            - mv ./build ./public
        artifacts:
            paths:
                - public
            only:
                - main
    ```
    
    - `only: main` means that the script will run only for changes made in the main branch. If I wanted to run the pipeline for other branches, I'd add the names of the respective branches.
3. In the `docusaurus.config` file, 
4. Access the page: [`https://aloci.gitlab.io/lc-docusaurus`](https://aloci.gitlab.io/lc-docusaurus).
    
