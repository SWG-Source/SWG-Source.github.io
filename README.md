#SWG-Source.github.io

This repository works with Jekyll and Github Pages in order to serve a website intended to provide help and information about the SWG Source project, our VM, and our codebase. It's still a work in progress.

## Would you like to contribute a guide?

The easiest way to get started is to compose a markdown file according to the Github markdown standard and add it to \_docs/. Your guide.md must begin with the following front matter in order to be seen by Jekyll:
```
---
title: Guide Title
---
```
Your markdown can begin right after including that front matter.

Once you've added your markdown file to \_docs/, Jekyll will build it into an HTML file and add a link to it to the documentation index page.

If you want to include images in your guide, please add them to assets/images/ and name them something that makes sense like {guideName}-{incrementingNumber}.png in order to keep things organized.
