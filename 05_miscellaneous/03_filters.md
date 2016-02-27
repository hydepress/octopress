---
title: Filters
---

A set of handy liquid filters used by Octopress.

- full_urls - Replace relative URLs with absolute URLs (searches for `href` and `src` properties).
- full_url - Replace a relative URL with an absolute URL.
- canonical_url - Convert a URL to the proper canonical version.
- titlecase - Properly capitalize titles with John Gruber’s [Title Case](http://daringfireball.net/2008/05/title_case).
- smartquotes - Smartly curl your quotation marks with John Gruber’s [Smarty Pants](http://daringfireball.net/projects/smartypants/).
- unorphan - Insert a non-breaking space between the last two words in a title.
- sluggify - Replaces all non-word characters in a string with dashes.
- classify - An alias for sluggify (seems appropriate when working with CSS class names).
- compact_newlines - Compact groups of empty lines into one, because Liquid templates have lots of whitespace.
- join_lines - Remove all new lines, joining each line with a separator. (defaults to a space).
- strip_url_protocol - Remove the protocol before a URL, e.g. `http://` or `https://`.

Also, not a filter, but this adds `excerpted` (true/false) to post's data. Meaning you can use `{% raw %}{% if post.excerpted %}{% endraw %}` in a post loop.

## Installation

If you're using bundler add this gem to your site's Gemfile in the `:jekyll_plugins` group:

    group :jekyll_plugins do
      gem 'octopress-filters'
    end

Then install the gem with Bundler

    $ bundle

To install manually without bundler:

    $ gem install octopress-filters

Then add the gem to your Jekyll configuration.

    gems:
      -octopress-filters

## Examples

### Full URLs

Any relative links in your site will be expanded with the `url` configuration in Jekyll's `_config.yml`. This filter only affects URLs
beginning with `/` inside of `href` or `src` attributes.

```
{% raw %}
{{ post.content | full_urls }}
{% endraw %}
```

You might use this if you're working on an RSS feed, you'll need to be sure all relative URLs in your content are expanded to full URLs.

### Full URL

This filter prepends input with the `url` configuration in Jekyll's `_config.yml`.

```
{% raw %}
{{ post.url | full_url }}
{% endraw %}
```

### Canonical URL

This filter expands the URL to be a full URL, then removes "index.html" if it is present. Here are some examples.

```
{% raw %}
{{ "about/index.html" | canonical_url }}  //=> http://example.com/about/
{{ "about.html" | canonical_url }}        //=> http://example.com/about.html
{{ "/" | canonical_url }}                 //=> http://example.com/
{% endraw %}
```

### Titlecase

```
{% raw %}
{{ post.title | titlecase }}  //=> This Is a Properly Capitalized Title
{% endraw %}
```

### Smartquote

```
{% raw %}
{{ post.content | smartquotes }}
{% endraw %}
```

### Unorphan

```
{% raw %}
{{ post.title | unorphan }}  //=> This Is a Properly Capitalized&nbsp;Title
{% endraw %}
```

### Sluggify/Classify

```
<article class="{{ post.class | classify }}">
```

### Compact newlines

```
{% raw %}
{{ content | compact_newlines }}
{% endraw %}
```

### Join lines

```
{% raw %}
{% capture page_title %}
{{ page.title }}
{{ site.header.title }}
{% endcapture %}

<head>
  <title>{{ page_title | join_lines: " - " }}</title>
  …
{% endraw %}  
```

### Strip URL protocol

```
{% raw %}
{{ site.url }}                        # https://some-site.com/
{{ site.url | strip_url_protocol }}   # some-site.com/
{% endraw %}
```

### Excerpted posts

In your templates, you may want to show different content if a post is excerpted. This plugin automatically searches each post for the
excerpt separator and adds the `excerpted` state to the post data. So you can do something like this.

```
{% raw %}
{% if post.excerpted %}
  {{ post.excerpt }}
  <a href="{{ post.url }}"Continue reading →</a>
{% else %}
  {{ post.content }}
{% endif %}
{% endraw %}
```

Jekyll has an `excerpt_separator` configuration which lets you define how Jekyll selects your post excerpts. By default this config is
set to `"\n\n"`, but redefining the config to something like `excerpt_separator: <!--more-->` makes it easy to decide
which content is excerpted, or even whether posts have excerpts at all.
