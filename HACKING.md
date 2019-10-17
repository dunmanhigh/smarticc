# How this site works

The blog is made with Jekyll, a blogging framework that builds _everything_ into static files, which are served with Github Pages.

**N.B.** If you see a placeholder in a code snippet with (round) brackets around them, replace the whole placeholder, including the brackets. 

Also, **N.B.** If you're making changes on your own machine, please set your editor to use **Unix-style line endings**. If you're using Sublime Text, Notepad++, Atom, VSCode or any other competent text editor, this shouldn't be an issue; just don't use Notepad if you're on Windows (looking at you @zehata)

## Setup
This is not necessary.

Alternatively, you can set it up on your own machine. You'll need to install Ruby as well as rubygems, which usually come together. You'll also need bundler, which you can get with 

```shell
gem install bundler
```

Fork and clone the repository, then run

```shell
bundle install
```

You should now be able to serve the site from your machine with 

```shell
bundle exec jekyll serve
```

...and head to localhost:4000, or whatever the command shows. As a bonus, all pages will rebuild whenever you save a file, EXCEPT `_config.yml`. The built site is placed in `_site` and served from there; you don't need to push this folder, but it's useful if you want to see build output.

## Adding posts
To add a new post, just place a new `.md` file in the `_posts` directory with the following **front matter** in front of the file, including the dashes:

```yaml
---
title: (title of your post)
categories: (article | tutorial)
tags: (any number of lowercase tags separated by spaces)
---
```

Please check the tags page on the site to look for any existing tags suitable for your post. If there aren't any, you can add your own, but try to do this as a last resort; a tag that's only used by one article kinda defeats the purpose of the tag, right? idk

## Messing with headers, footers and stylesheets
You can look at `_layouts/default.html` to get a general sense of how pages on the site are laid out. In essense, for every page using the `default` layout:

* `_includes/head.html` includes stylesheet links and the `<title>` 
* `_includes/header.html` provides the nav bar on top of every page, and 
* `_includes/footer.html` provides the footer on every page;
* `_layouts/default.html` then injects content into the main section of the page for any page using `layout: default` in its front matter.

Pretty much every page on the site uses `layout: default` to get the stylesheets, headers and footers they need; **if you want to make changes to the main structure that affect most pages on the site, mess around with the `.html` files in `_includes/`.**

### Stylesheets
If you have some `f r e s h` new `.css` files to include in the site, add the `.css` file in the `assets/style` directory, and include them in `_includes/head.html`, in a similar fashion to the other styles there.

Remember that the CSS there affects everything on a page, including headers and footers, so remember to test and see if your style selectors accidentally conflict with headers or footers.

## Post layouts and page variables
The post template is in `_layouts/post.html`. While you can just dump normal HTML in there, you can also include **templates** with variables that change dynamically **per post**, including:

* `page.title`, the title of the post bieng rendered
* `page.content`, the contents of the post being rendered
* `page.date`, the date specified in the post
* `page.tags`, a list of tags specified for the post
* `page.(WHATEVER)`; you can also access any `key: value` pair defined in a post's front matter (the list of values declared at the top of a post, between three dashes `---`).

A full list is [here, on the Jekyll docs](https://jekyllrb.com/docs/variables/#page-variables).

**Include variables with** `{{ (variable) }}`.

Jekyll uses the [Liquid engine](https://shopify.github.io/liquid/) for templating, and can do things like [conditional flow](https://shopify.github.io/liquid/tags/control-flow/) and [iteration](https://shopify.github.io/liquid/tags/iteration/), useful for lists like `page.tags`. Read their docs for more info.

## The home page, and site variables
The home page lives in `_layouts/home.html`. Same deal as with `post.html`, except that `home.html` uses **static** site variables instead of page variables that changes per post.

* `site.posts` contains a list of every single post; each `post` object is the exact same type of object as mentioned earlier
* `site.title` is the name of the _entire_ site
* `site.(WHATEVER)` contains any custom variable defined in `_config.yml`, like "twitter_username"

## Category index pages
This site uses categories to classify types of pages (articles & tutorials, as of 23 Jul '18). While Jekyll provides built-in support to _label_ pages with categories, as of 2018-07-13 it unfortunately doesn't support generating pages indexing all pages in a particular category.

A hack involving a [collection](https://jekyllrb.com/docs/collections/) of "category index" pages is currently being used to show category indexes. However, this requires that there be a <category>.md file in `_category` for every category on the site.

If you're making a new type of page, just add a file `(category).md` in `_category/` with the content:

```yaml
layout: category_index
arg: (name of category)
```

If you want to change the structure of the category index page, edit `_layouts/category_index.html`. Just be sure to keep the iteration tags around whatever element to duplicate for each article.

## Tag index page
This site uses tags to classify topics, such as `ruby`, `machine-learning` and so on. Instead of a page for every tag on the site, `/tags.html` lists every single tag, and every article in each tag. 

The details for the iteration used on the index page can be found in `/tag.html`. 

## One last thing
This probably isn't the best structure ever for a Jekyll site; feel free to make changes to how the site works, but be sure to update this document if anything here becomes out-of-date with your changes.

If you run into issues, the [Jekyll docs](https://jekyllrb.com/docs) is a good place to start. Be sure to check out the [Liquid docs](https://shopify.github.io/liquid/) if you're doing templating.
