---
title: "03 Create Hugo Site"
---

# Creating the project
```
hugo new site <HUGO_PROJECT>
cd <HUGO_PROJECT>
git init
```

# Adding a theme
Select a theme from [hugo's theme page](https://themes.gohugo.io/).
```
git submodule add <THEME_URL> themes/<THEME_NAME>
```
Example using [Notepadium](https://themes.gohugo.io/themes/hugo-notepadium/) theme
```
git submodule add https://github.com/cntrump/hugo-notepadium.git themes/hugo-notepadium
```
Add entry the following entry to config.toml
```
theme = "<THEME_NAME>"
```
Most themes will provide instructions on how to setup config.toml to use various components of the theme.
For [Notepadium](https://themes.gohugo.io/themes/hugo-notepadium/) replace the contents of config.toml with
the default values given in the description of the theme.
```
baseURL = "https://example.com"
title = "Notepadium"
theme = "hugo-notepadium"
copyright = "©2019 Notepadium."

languageCode = "zh-cn"
hasCJKLanguage = true

enableRobotsTXT = true

# Enable Disqus
#disqusShortname = "XXX"

# Google Analytics
#googleAnalytics = "UA-123-45"

[markup.highlight]
codeFences = true
noClasses = false

[markup.goldmark.renderer]
unsafe = true  # enable raw HTML in Markdown

[params]
style = "auto"  # default: auto. light: light theme, dark: dark theme, auto: based on system.
dateFormat = "Monday, January 2, 2006"  # if unset, default is "2006-01-02"
logo = ""  # if you have a logo png
slogan = "100% JavaScript-free"
license = ""  # CC License
fullRss = false # Puts entire HTML post into rss 'description' tag. If unset, default is false.

[params.comments]
enable = false  # En/Disable comments globally, default: false. You can always enable comments on per page.

[params.math]
enable = false  # optional: true, false. Enable globally, default: false. You can always enable math on per page.
use = "katex"  # option: "katex", "mathjax". default: "katex"

[params.syntax]
use = "none"  # builtin: "prismjs", "hljs". "none" means Chroma
theme = "xcode"
darkTheme = "xcode-dark"  # apply this theme in dark mode

[params.share]
enable = false
addThisId = ""
inlineToolId = ""

[params.nav]
showCategories = true       # /categories/
showTags = true             # /tags/

# custom navigation items

[[params.nav.custom]]
title = "About"
url = "/about"

[[params.nav.custom]]
title = "Hugo"
url = "https://gohugo.io/"

# for chinese
[params.beian]
  icp = ""
  gongan = ""
```

# Add a new post
Create a new post and add some content.
```
hugo new posts/<FILENAME>.md
```
The file will be located in content/posts/<FILENAME>.md

# Run the site locally
```
hugo server -D
```
**Note** '-D' flag is used to force the rendering of draft posts. Remove or make draft = false for each header of post before deploying it.


# Deploy
[Hugo docs](https://gohugo.io/hosting-and-deployment/) have extensive instruction for deployment to various platforms.
#### Deploying to github
1. Create a new repository
2. Create a file .github/workflows/gh-pages.yml with content
```
name: github pages

on:
  push:
    branches:
      - main  # Set a branch to deploy
  pull_request:

jobs:
  deploy:
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
        with:
          submodules: true  # Fetch Hugo themes (true OR recursive)
          fetch-depth: 0    # Fetch all history for .GitInfo and .Lastmod

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          # extended: true

      - name: Build
        run: hugo --minify

      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        if: github.ref == 'refs/heads/main'
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
```
3. Add/Edit the following entries in config.toml
```
baseURL = 'https://<GITHUB_USERNAME>.github.io/<GITHUB_REPO_NAME>/'
canonifyURLs = true
```
4. Commit changes and push to the repository
5. Goto repo settings -> pages. In sources expand drop down menu and select gh-pages and click save.

[Prev](/posts/02_setup) | [Next](/posts/04_whats_next)
