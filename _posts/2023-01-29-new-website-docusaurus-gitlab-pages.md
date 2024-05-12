---
title: Building a website with Docusaurus and GitLab Pages
description: 
tags: [docusaurus, jekyll, tutorial]
---

Just for fun, I built a new personal site: [`https://aloci.gitlab.io/lc-docusaurus`](https://aloci.gitlab.io/lc-docusaurus).

In the GitLab project, to keep organized I use different branches branches:

- `main` for everything - the branch of it all.
- `blog` for blog posts (adding new ones, updating existing ones, and fixing typos).
- `content` for website content (updating the about page and adding new projects).
- `design` for design and frontend stuff (changing fonts and colors).
- `features` for different features (adding Vale or a contact form).
- `pages` for configuring [GitLab pages for deploying the website](#deploying-docusaurus-with-gitlab-pages).

To deploy the website with GitLab pages, in the project root directory I created a new file `gitlab-ci.yml` with the following configuration:
    
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
