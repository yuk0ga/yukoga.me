+++
title = "Introducing Koga (Hugo Theme)"
date = 2018-04-26T21:33:53+10:00
Description = ""
image = "hugo-logo.png"
tags = ["hugo", "koga-theme"]
categories = ["Development", "English"]
archives = ["2018/04"]

+++

"Koga" is a **Hugo theme** that I, Yu Koga created from scratch (Don't judge me for naming it after myself).

So this article is not an introduction about myself, but instead it is a **basic tutorial** on how to use the Koga theme.

# Prerequisites
- Basic knowledge on how to use the command line

# Initial Steps
## Install Hugo
If you have not installed Hugo yet, do that now by running the following commands:
```bash
brew install hugo
```
To check that you have successfully installed it, run
```bash
hugo version
```
and it should return the version of hugo you have installed.

## Create New Site
```bash
hugo new site example
```
Replace "example" with whatever directory name you like.

## Add Theme
```bash
cd example
git init
git submodule add https://github.com/yuk0ga/koga.git themes/koga
```
Again, replace "example" with the directory name you decided to use.

# Configurations
## Edit config.toml
Replace the content of config.toml with the following:
```toml
theme = "koga"
baseURL = "https://example.com"
languageCode = "en-us"
title = ""
MetaDataFormat = "toml"
pygmentsCodeFences = true
pygmentsUseClasses = true

[taxonomies]
    tag = "tags"
    category = "categories"
    archive = "archives"

[params]
    emailHash = "enter your email hash for gravatar"
    fullName = "your full name here"

    [params.social]
      Github = "your github username"
      Facebook = "your facebook username"
      Twitter = "your twitter username"
      Instagram = "your instagram username"

[menu]

  [[menu.main]]
    name = "Home"
    url = "/"
    weight = 1

  [[menu.main]]
    identifier = "post"
    name = "Posts"
    url = "/post/"
    weight = 2

  [[menu.main]]
    identifier = "categories"
    name = "Categories"
    url = "/categories/"
    weight = 3

  [[menu.main]]
    identifier = "tags"
    name = "Tags"
    url = "/tags/"
    weight = 4

  [[menu.main]]
    identifier = "archives"
    name = "Archives"
    url = "/archives/"
    weight = 5
```
Set your baseURL, title, email hash for your Gravatar icon, full name, and social media usernames.

## Delete `_default.md` in archetypes
Run the following command:
```bash
rm -rf archetypes/_default.md
```

## Create Directory "static/images"
```bash
mkdir static/images
```
Put any image you use inside static/images, and refer to any of them using the url: "static/images/image.png"

## Add CNAME file (For custom domains)
```bash
vi static/CNAME
*I*
custom-domain.com
*esc*
:wq
```

# Creating Contents
## Add your bio
```bash
hugo new about.md
```
In about.md, set the archetype title to whatever catchcopy you wish to use, and add a short bio of yourself as the content.

## Add a Project
```bash
hugo new project/whatever.md
```
In the project markdown file, set the following:

- Name of project
- Description
- Source of Image (URL) A placeholder URL is set as default.
- Github repository name
- Weight (0 = not important. 1 = important. 2 = less important.. so on)

All fields are predefined as a frontmatter, so all you have to do is fill in the blanks.

## Create an Article
```bash
hugo new post/whatever.md
```
### Table of Contents
If you wish to enable table of contents for your post, be sure to delete
```bash
toc = false
```
from the frontmatter.

### Images
Use the figure shortcode to add images to your Article.
For example:
```bash
# surround this code with another set of curly braces {}
{< figure class="img-80" src="https://media-cdn.mag2.com/p/news/wp-content/uploads/2017/11/20171103_katsudon-650x401.jpg" title="美味しそうなカツ丼" >}
```
Will result into:
{{< figure class="img-80" src="https://media-cdn.mag2.com/p/news/wp-content/uploads/2017/11/20171103_katsudon-650x401.jpg" title="美味しそうなカツ丼" >}}

### Code
To include some code snippets, simply surround the code with triple backticks like this:
~~~bash
```bash
cat config.toml
```
~~~
This will be rendered as:
```bash
cat config.toml
```
