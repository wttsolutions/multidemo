# Project documenting

****TL;DR****; write documentation to markdown files, store them in the project repository and view them in the browser (see `package.json -> scripts -> docs:build`)

## Motivation

Project documentation is a place where the developer/manager/customer can see WHY something was implemented on the project and WHICH WAY. Good documentation lets anyone get answers to the questions like: "why this feature was implemented?", "What is this feature related to?", "Do we still need it?", "Hot to test it?" while a project is developing and changing.

Assumed that project documentation is created __mainly__ by the developer alongside the code changes but __sometimes__ can be improved by QA, manager or customer (anyone else who can edit markdowns & commit to git)

## Quick start

``` 
yarn 
yarn docs:build
yarn docs:preview
```
and see the demo docs at the `http://localhost:3000`

## Technical details

1. Write documentation to markdown files and keep them in the project repository.

2. Validate markdowns by remark & plugins (formatting, styling, template substitution, link check, etc)

3. View markdowns in a browser (using docsify js lib)

```
MARKDOWN --(remark)--> MARKOWN --(docsify)--> BROWSER
```

### Why in this way?

Why document plain markdowns instead of some cool online wiki WYSIWYG?

Proc:
  - easy to modify (any plain text editor OR VSCode md editor)

  - easy to read (directly OR in browser+markdown plugin OR in simply in the browser after markdown->html convertion (see p.3)

  - documentation is always synchronized with functionality and it's possible to see documentation **changes** (for example to QA)

  - QA can easily see DIFF changes in documentation => can pay attention to the correspondent parts of the system that were changed

Cons:
  - the necessity to create a git commit on documentation changes.



### Markdown editing


#### Preview markdown

1. By "Markdown Preview Enhanced" VSCode extension

(alt: docsify preview https://marketplace.visualstudio.com/items?itemName=dzylikecode.docsify-preview )

2. By [Markdown Viewer](https://chrome.google.com/webstore/detail/markdown-viewer/ckkdlimhmcjmikdlpkmbgfkaikojcbjk) chrome extenstion or a similar ones


#### Add images to md

Either:

* VSCode > Markdown Paste extenstion & Ctrl+Alt+v hotkey
* VSCode > drag&drop & manual fix path
* VSCode > Ctrl+Shift+p > "markdown insert an image from the workspace" (can set the custom key for this)
* By any text editor manually ![my image](myimage.jpg)


#### Add a link to markdown

Either:

* by any text editor manually
* `VSCode >  Ctrl+Shift+p > "markdown insert an image from the workspace"` (can set the custom hotkey for this)
* VSCode > type `[]()` and press `Ctrl+space` inside `()` and in the dropdown select a desired location like "file.md#chapter"

* Manually by any text editor `[user](glossary.md#user)`

Also consider using markdown **definition links** as a recommended way of using links that are repeated on a page


#### Possible Docsify -> Rehype replacement in future


In case of problems with docsify it's possible to use rehype to convert md to html:

    MARKDOWN --(remark)--> MARKOWN --(docsify)--> BROWSER

#### Which to choose: remark plugin or docsify plugin

Use remark plugins when need to process the PRIMARY markdown data (check links, validate syntax, etc) and use docsify plugins when need PRESENT markdown data (like show TOC, search on site, styling, etc)



#### See also


remark/plugins.md at main · remarkjs/remark https://github.com/remarkjs/remark/blob/main/doc/plugins.md#list-of-plugins

remark-plugin · GitHub Topics https://github.com/topics/remark-plugin

rehype/plugins.md at main · rehypejs/rehype https://github.com/rehypejs/rehype/blob/main/doc/plugins.md#list-of-plugins

Transforming Markdown with Remark & Rehype | ryanfiller.com https://www.ryanfiller.com/blog/remark-and-rehype-plugins#basic-plugin-structure

Explore - unified https://unifiedjs.com/explore/

Quick start https://docsify.js.org/#/quickstart


Tools to convert items like "JIRA-123" to links:
 - autolink items like JIRA-123 to links using one of the:
   - https://gitlab.com/staltz/remark-linkify-regex
   - https://unifiedjs.com/explore/package/remark-autolink-references/
   - https://github.com/remarkjs/remark-gfm
   - https://github.com/remarkjs/remark-github


#### TODO
 - link prevew

## How to create a cool documentation

Focus on the question WHY everywhere and skip obvious details

Imagine we have a Login form:

```
   login    [      ]
   password [      ]
   promo    [      ]

   OK
```

Good documentation shouldn't say things like "when the user needs to log in the login page is displayed. Input your login, password and promo to the correspondent field and press OK".

Instead, consider the aspects like following:

* How did we get to this form?
* Who is the user?
* Why user need to log in to a site? Which benefits it gives to him?
* Where user should get the data required by the form?
* What if user data are lost/incorrect?
* What are the detailed aspects of the desired data (login allowed chars, password length, promo case)
