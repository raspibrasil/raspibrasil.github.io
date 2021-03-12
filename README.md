# Source and tools for the Raspberry Pi Brasil website

Live here: https://www.raspberrypibrasil.com

This repo contains the contents and the site-generation tools to make the content available, including:

 - Page publisher with template engine: `sitegen`
 - Tag builder for posts: `maketags`
 - Atom RSS feed generator (blog only): `genfeed`
 - Full-site sitemap generator: `makesitemap`

These tools require Python 3.7 or above to work, plus the `python-markdown` module, usually installable via `pip3 install markdown`.

## Publishing procedures

### Publishing a single page

 1. Edit `template.html` to taste (structure, styling, etc). Make sure to leave exactly two "holes" with `%s` within it, as per the example. These will be filled by the page's title and contents, respectively.
 2. Write your page's content in [Markdown](https://en.wikipedia.org/wiki/Markdown), save it to a `.md` file.
 3. Run `./sitegen FILE.md` to publish a page named `FILE.html`

### Publishing a blog post

 1. Create a directory for your blog, for example: `blog/`
 2. Create a subdirectory for your blog post, for example `blog/my_first_post/`
 3. Write your post's contents as the `index.md` file under your subdirectory.
 4. Write your publishing date as the `pubdate` file under your subdirectory. Use the format `YYYY-MM-DD`, i.e. 2021-03-01
 5. From the site's root, run `./sitegen blog/my_first_post/index.md`

### Publishing a Directory Index

 1. Create a directory `blog/` where all the pages in `.md` will be posted.
 2. Run `./sitegen -i -d blog blog/*.md` to make an index of all files under `blog/`
 3. The index of `blog` will be available as `blog/index.html`

### Generating blog tags

 1. Create a file `categories` under your post's directory as `blog/my_first_post/categories`
 2. Write every category of your blog post in a separate line of the `categories` file. UTF-8 and spaces are supported. Example:

    welcome
    announcement
    news
    my blog

 3. From the site's root, run `./maketags`
 4. All your blog's tags are now indexed under `blog/tags/`

### Generating the blog feed

 1. From the site's root, run `./genfeed`
 2. Your site's feed is available at `atom.xml`

### Generating a sitemap

 1. Run `./makesitemap` from the site's root
 2. Your sitemap is available at `sitemap.xml` (you can change this in the settings)
