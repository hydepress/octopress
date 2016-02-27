---
title: Markdown
---

Why? Because you should be able to:

- Write markdown anywhere.
- Process `{% raw %}{% include %}{% endraw %}` tags with markdown.

## Installation

If you're using bundler add this gem to your site's Gemfile in the `:jekyll_plugins` group:

    group :jekyll_plugins do
      gem 'octopress-markdown-tag'
    end

Then install the gem with Bundler

    $ bundle

Or install it manually:

    $ gem install octopress-markdown-tag

Then add the gem to your Jekyll configuration.

    gems:
      - octopress-markdown-tag

## Usage

### Embed Markdown in HTML

Drop some markdown in your html, and it will render nicely

```html
{% raw %}
<!-- Some random HTML file-->
<div>
{% markdown %}

## That's right folks!

Markdown in your `HTML`!

- Any template
- Any time

{% endmarkdown %}
</div>
{% endraw %}
```

### Convert included partials with markdown 

Correctly render markdown files which are included in an HTML page.

```html
{% raw %}
<!-- Another random HTML file-->

<div>
{% markdown %}{% include coolcat.md %}{% endmarkdown %}
</div>
{% endraw %}
```

That's pretty much it. Have fun!
