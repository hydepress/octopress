---
title: Codeblock
---

Write beautiful code snippets within any template.


## Installation

### Using Bundler

Add this gem to your site's Gemfile in the `:jekyll_plugins` group:

    group :jekyll_plugins do
      gem 'octopress-codeblock'
    end

Then install the gem with Bundler

    $ bundle

### Manual Installation

    $ gem install octopress-codeblock

Then add the gem to your Jekyll configuration.

    gems:
      - octopress-codeblock

## Usage

    {% raw %}
    {% codeblock [options] %}
    [lines of code code]
    {% endcodeblock %}
    {% endraw %}

### Options

Note that order does not matter.

| Options      | Example                | Description                                                           |
|:-------------|:-----------------------|:----------------------------------------------------------------------|
|`lang`        | `lang:ruby`                 | Used by the syntax highlighter. Passing 'plain' disables highlighting.|
|`title`       | `title:"Figure 1.A"`   | Add a figcaption title to your code block. |
|`link_text`   | `link_text:"Download"` | Text for the link, default: `"link"`. |
|`linenos`     | `linenos:false`        | Disable line numbering. |
|`start`       | `start:5`              | Start the line numbering at the given value. |
|`mark`        | `mark:1-4,8`           | Highlight lines of code. This example marks lines 1,2,3,4 and 8 |
|`class`       | `class:"css example"`  | Add CSS class names to the code `<figure>` element |


### Example

```
{% raw %}
{% codeblock lang:ruby title:"Check if a number is prime" mark:3 %}
class Fixnum
  def prime?
    ('1' * self) !~ /^1?$|^(11+?)\1+$/
  end
end
{% endcodeblock %}
{% endraw %}
```

Demo

<!-- title:"Check if a number is prime" mark:3 -->
```ruby
class Fixnum
  def prime?
    ('1' * self) !~ /^1?$|^(11+?)\1+$/
  end
end
```

