---
layout: post
title:  "How I set up this Jekyll site"
date:   2021-06-20 21:10:00
categories: blog
---

There are tons and tons of Jekyll tutorials, most of them way better than this, but this is how I built this personal site. Somehow, I come back to it every few months and have no idea of what's going on, so hopefully this helps me next time I want to change stuff, or helps you if it's your first time around.

# Installing prerequisites
This part is pretty straightforward, you have to install Ruby and Jekyll. I'm on macOS so I used Homebrew for this. The Jekyll website has good guides for these steps [here](https://jekyllrb.com/docs/installation/macos/) and [here](https://jekyllrb.com/docs/).

# Starting a new site
Once that's installed, if everything is working well, you should be able to initialize a new site like this:
{% highlight bash %}
jekyll new mysite
{% endhighlight %}
This will create a folder with all the basic stuff. Inside this folder you should be able to serve the site:
{% highlight bash %}
cd mysite
jekyll serve
{% endhighlight %}
> I am running `Ruby 3.0.1`, and apparently [it is not supported yet](https://github.com/github/pages-gem/issues/752), so you'll get an error that requires you to manually add `webrick` like this:  `bundle add webrick`, before `jekyll serve`

This creates the following directory structure:
{% highlight bash %}
   mysite
   ├── 404.html
   ├── Gemfile
   ├── Gemfile.lock
*  ├── _config.yml
*  ├── _posts
   │   └── 2021-06-20-welcome-to-jekyll.markdown
   ├── _site
   │   ├── ...
*  ├── about.markdown
*  └── index.markdown
{% endhighlight %}

The most important things to understand are:
  - **`_config.yml`:** This is basically a document with general variables of the site. Jekyll uses the Liquid language to make templates, it's very simple and useful, you can read more about it [here](https://jekyllrb.com/docs/liquid/). Any variable defined in this document can be called like  ``site.whatever`` for example: {% raw %}``{{ site.email }}``{% endraw %}.
  - **`_posts/`:** These are... posts. It's an easy way to add stuff like blog posts or project pages that follow a template. Using this is the real benefit of using Jekyll, because there's a bunch of tricks with the Liquid syntax so that it will format everything automatically and generate indexes or menus on its own, so once you set it up you don't have to update everything manually.
  - **`about.markdown`** and **`index.markdown`:** These are the main pages. They will appear in the top navigation bar.


# Editing the theme
You'll notice that the directory is missing a bunch of important folders, like all the `css` and page structure stuff. That's because it reading everything from whatever *theme* is defined in `_config.yml`, for example. `theme: minima`. To edit it, we first need to find it. We can do it like this:
{% highlight bash %}
bundle info minima

* minima (2.5.1)
  Summary: A beautiful, minimal theme for Jekyll.
  Homepage: https://github.com/jekyll/minima
  Path: /usr/local/lib/ruby/gems/3.0.0/gems/minima-2.5.1
{% endhighlight %}

and we can copy all of that to our project to have our own copy:
{% highlight bash %}
cd mysite/
cp -r /usr/local/lib/ruby/gems/3.0.0/gems/minima-2.5.1/* .
{% endhighlight %}

Now we'll have all these things:

{% highlight bash %}
  ├── LICENSE.txt
  ├── README.md
  ├── _includes
  │   ├── disqus_comments.html
  │   ├── footer.html
  │   ├── google-analytics.html
  │   ├── head.html
* │   ├── header.html
  │   ├── icon-github.html
  │   ├── icon-github.svg
  │   ├── icon-twitter.html
  │   ├── icon-twitter.svg
  │   └── social.html
  ├── _layouts
  │   ├── default.html
  │   ├── home.html
* │   ├── page.html
  │   └── post.html
* ├── _sass
  │   ├── minima
  │   │   ├── _base.scss
  │   │   ├── _layout.scss
  │   │   └── _syntax-highlighting.scss
  │   └── minima.scss
  └── assets
      ├── main.scss
      └── minima-social-icons.svg
{% endhighlight %}

### Understanding the theme:
- **`layouts`:** These define how the all the markdown files (both in the top directory, like `index.markdown` and things inside `_posts/` will be interpreted.) Markdown files have a *front matter*, which is basically a `yaml`:
{% highlight markdown %}
---
layout: page
title: About
permalink: /about/
---

Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua...
{% endhighlight %}

So, in this case, `layout: page`, means that the {% raw %} `{{ contents }}` {% endraw %}of the markdown file will be "embeded" however specified in `_layouts/page.html`:
{% highlight html %}
{% raw %}
---
layout: default
---
<article class="post">

  <header class="post-header">
    <h1 class="post-title">{{ page.title | escape }}</h1>
  </header>

  <div class="post-content">
    {{ content }}
  </div>

</article>
{% endraw %}
{% endhighlight %}

As you can see, `_layouts/page.html` itself has a *front matter* that specifies `layout: default`. So it will be nested-embeded inside whatever is specified in `_layouts/default.html`:

{% highlight html %}
{% raw %}
<!DOCTYPE html>
<html lang="{{ page.lang | default: site.lang | default: "en" }}">

  {%- include head.html -%}

  <body>

    {%- include header.html -%}

    <main class="page-content" aria-label="Content">
      <div class="wrapper">
        {{ content }}
      </div>
    </main>

    {%- include footer.html -%}

  </body>

</html>

{% endraw %}
{% endhighlight %}

This layout has a few lines that specify `include`.

- **`_includes`:** These are pieces of `html` code that you can *include* in the layouts. It is useful for things like the header and footer of the website, which are constant across layouts.
- **`_sass/minima/`:** All of the `*.scss` have the what you can change to modify look.

# What I changed
So this website is only a few steps away from *minima*. But the main things I changed are the following:

### 1. A bunch of the CSS
There are a lot of small changes that you can find in `_sass/`, to change the navigation menu, colors, font, spacing, etc. (If you add any new `.scss` files, remember to add the import statement in `minima.scss`.)

### 2. Added a few simple pages
I made the about page the main page, and added one for `publications.md` and `blog.md` that are pretty simple.

### 3. Projects
The landing project pages have to do two things: 1. Generate a *sub menu*, that highlights the *current* page, and 2. List the projects included under `projects/science/_posts` or `projects/other/_posts`, including a logo, author and github link.


That's about it. It took me a bit to get a hang of Liquid and the Jekyll structure, it might seem as overkill for something as simple as this website where directly editing the html is much easier, but I do see the appeal of auto-generating pages from markdown. Fun stuff to try.