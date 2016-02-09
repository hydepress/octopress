---
title: Quote
---

Easy HTML5 blockquotes for Jekyll sites.


## Installation

### Using Bundler

Add this gem to your site's Gemfile in the `:jekyll_plugins` group:

    group :jekyll_plugins do
      gem 'octopress-quote-tag'
    end

Then install the gem with Bundler

    $ bundle

### Manual Installation

    $ gem install octopress-quote-tag

Then add the gem to your Jekyll configuration.

    gems:
      -octopress-quote-tag

## Usage

```
{% raw %}
{% quote [options] %}
Some great quote
{% endquote %}
{% endraw %}
```

Options:

| option | default | description |
|:-------|:--------|:------------|
| author | nil     | String: Quote author |
| title  | nil     | String: Title of work cited |
| url    | nil     | String: Link to work |


### Example

```
{% raw %}
{% quote author:"Bob McAwesome" url:http://example.com title:"Great Wisdom" %} 
Never pet a burning dog.
{% endquote %}
{% endraw %}
```

```
<figure class='quote'>
  <blockquote>
    <p>Some great quote</p>
  </blockquote>
  <figcaption class='quote-source'>
    <span class='quote-author'>Bob McAwesome</span>
    <cite class='quote-title'><a href='http://example.com'>Great Wisdom</a></cite>
  </figcaption>
</figure>
```

## Why?

In Markdown Blockquotes are simple but attribution isn't. Also,
writing the semantic HTML is tricky and easy to forget.

```
> Some cool quote

# becomes:

<blockquote>
  <p>Some cool quote</p>
</blockquote>
```

But what if you want to cite an author or a source?

```
> Some cool quote
> - Bob McAwesome

# becomes:

<blockquote>
  <p>Some cool quote
- Bob McAwesome</p>
</blockquote>
```

Which doesn't work at all since a browser will see it as:

```
Some cool quote - Bob McAwesome
```

And now you know.
