---
title: "04 Templates"
---

# Templates
Some of the most used templates are:-
- [Base Template](https://gohugo.io/templates/base/)
- [List Template](https://gohugo.io/templates/lists/)
- [Single Template](https://gohugo.io/templates/single-page-templates/)

These templates are basic HTML files that has access to variables and contents from your post.
These files are stored in ./layouts director.

Default templates can be placed in ./layouts/_default

For templates specific to a folder in ./contents say ./content/dir1, the corresponding templates should be in ./layouts/dir1

Base template is created as baseof.html. This contains outer shell of all other templates.

List template (list.html) is for the page that lists out pages (in a particular directory or all the pages of your site). [The homepage](/) is an example of a list page.

The primary view of content in Hugo is the single view. Hugo will render every Markdown file provided with a corresponding single template (single.html). This page is an example of single page.

[Prev](/posts/03_new_project) | [Next](/posts/05_whats_next)
