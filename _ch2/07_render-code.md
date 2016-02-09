---
title: Render Code
---

Embed code snippets from the file system in your Jekyll site.


## Installation

### Using Bundler

Add this gem to your site's Gemfile in the `:jekyll_plugins` group:

    group :jekyll_plugins do
      gem 'octopress-render-code'
    end

Then install the gem with Bundler

    $ bundle

### Manual Installation

    $ gem install octopress-render-code

Then add the gem to your Jekyll configuration.

    gems:
      -octopress-render-code

## Usage

    {% raw %}
    {% render_code <FILE> [options] %}
    {% endraw %}

### Configuration

In your site's configuration, you can set the directory for embedded code samples.

<!-- title:"In _config.yml" -->
```
code_dir: code-examples
```

The default directory is 'downloads/code'

### Options

Note that order does not matter.

| Options      | Example                | Description                                                           |
|:-------------|:-----------------------|:----------------------------------------------------------------------|
|`lang`        | `lang:ruby`            | Defaults to guessing from file name extension. |
|`title`       | `title:"Figure 1.A"`   | Add a figcaption title to your code block. |
|`link_text`   | `link_text:"Download"` | Text for the link, default: `"Raw code"`. |
|`linenos`     | `lineos:false`         | Disable line numbering. |
|`start`       | `start:5`              | Start embedding the script from the 5th line number. |
|`end`         | `end:15`               | Stop embedding the script after 15th line number. |
|`range`       | `range:5-15`           | Embed lines 5-15 of the script. |
|`mark`        | `mark:5-7,10`          | Highlight lines of code. This example marks lines 5,6,7 and 10. |
|`class`       | `class:"solution"`     | Add CSS class name(s) to the code `<figure>` element. |

### Example

Given the existence of a file 

```
{% raw %}
{% render figure-1-a.js title:"Figure A: A Simple AJAX Request." mark:5-8
{% endraw %}
```

This will

- Embed and highlight a file at `[site_source]/downloads/code/figure-1-a.js`
- Give it a figcaption "Figure A: A Simple AJAX Request
- Visually mark lines 5,6,7, and 8.
