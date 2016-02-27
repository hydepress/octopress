---
title: Content For
---

Add content_for and yield tags to Jekyll with conditional rendering and in-line filters.


## Installation

If you're using bundler add this gem to your site's Gemfile in the `:jekyll_plugins` group:

    group :jekyll_plugins do
      gem 'octopress-content-for'
    end

Then install the gem with Bundler

    $ bundle

To install manually without bundler:

    $ gem install octopress-content-for

Then add the gem to your Jekyll configuration.

    gems:
      -octopress-content-for

## Usage

Use it like a typical `content_for` tag.

```
{% raw %}
{% content_for awesome_content %}
some content
{% endcontent_for %}

{% yield awesome_content %}  //=> some content
{% endraw %}
```

Use in-line filters.

```
{% raw %}
{% yield awesome_content | upcase %}  //=> SOME CONTENT
{% endraw %}
```

Use conditional rendering in both `content_for` and `yield` tags.

```
{% raw %}
{% content_for footer unless page.footer == false %}
Footer!
{% endcontent_for %}

{% yield footer if page.footer %}
{% endraw %}
```

