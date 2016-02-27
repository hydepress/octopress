---
title: Multilingual
---

Add multiple language features to your Jekyll site. This plugin makes it easy to:

- Add language-specific post indexes, archives, and RSS feeds.
- Link between translated posts and pages.
- Use language in your permalinks. 
- Cross-post a single post to all languages.
- Add translation dictionaries to simplify site templates.
- Tag and category indexes are automatically filtered by language.


## Installation

If you're using bundler add this gem to your site's Gemfile in the `:jekyll_plugins` group:

    group :jekyll_plugins do
      gem 'octopress-multilingual'
    end

Then install the gem with Bundler

    $ bundle

To install manually without bundler:

    $ gem install octopress-multilingual

Then add the gem to your Jekyll configuration.

    gems:
      - octopress-multilingual

## An important note

**There is no Jekyll standard for multilingual sites** and many plugins will not work properly with this setup. Octopress and it's
plugins are being designed to support multilingual features, but without a standard, some use-cases may be overlooked. If you have a
problem with an Octopress plugin supporting your multilingual site, please file an issue and we'll do our best to address it.

Note: First-party Octopress plugins are designed to support multilingual sites but other plugins may not work how you'd expect on multilingual sites. Modifying plugins is beyond the scope of this guide.

Also, if you are using flags to represent languages on your site, you might like to read, [Why flags do not represent language](http://flagsarenotlanguages.com/blog/why-flags-do-not-represent-language/).

## Helpful Plugins

These plugins automatically add multilingual features to your site when used with Octopress Multilingual.

- [Octopress Linkblog](https://github.com/octopress/linkblog) adds link-blogging indexes (articles-only, links-only) and feeds for each language.
- [Octopress Feeds](https://github.com/octopress/feeds) adds RSS feeds for each language.

## Setup

When adding this plugin to your site, you will need to:

1. Configure your site's main language, e.g. `lang: en`.
2. Add a language to the YAML front-matter of your posts, e.g. `lang: de`.
3. Add post indexes and RSS feeds for secondary languages.

First, be sure to configure your Jekyll site's main language. An site written primarily in English would add this to its Jekyll configuration:

```yaml
lang: en
```

Here we are setting the default language to English. Posts without a defined language will be treated as English posts.
For a list of standard language codes, refer to [ISO 639-1](http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). You can also use
the [language]-[region] method of setting your site's language, like `en-us` for American English or `de-at` for Austrian German.

### Setting a language for pages or posts

Specify a page or post's language in the YAML front matter.

```yaml
title: "Ein nachdenklicher Beitrag"
lang: de
```

You can, refer to a page or post language by `page.lang` or `post.lang`. This plugin adds the filter `language_name` which can convert the language short-name into the native language name. For example:

```
{% raw %}
{{ en | language_name }} # English
{{ de | language_name }} # Deutsch
{{ es | language_name }} # Español
{% endraw %}
```

Many common language codes are supported, but you can add to or override these in Jekyll's site configuration:

```
language_names:
  es: Spanish
  omg: WTFBBQ
```

## Indexes, RSS feeds and Archives.

If you are writing English and German posts, you'll want an English-only and a German-only post index. To do that, just set the
language in the YAML front-matter of your post-index. 

For example, this will loop through only German posts:

```
{% raw %}
---
lang: de
---
{% for post in site.posts %} ... {% endfor %}
{% endraw %}
```

And this will loop through only English posts:

```
{% raw %}
---
lang: en
---
{% for post in site.posts %} ... {% endfor %}
{% endraw %}
```

If your default post index is at `/index.html` you should create additional indexes for each secondary language. If you also write in German, you can create a posts index at `/de/index.html`. This approach will work for post archives and RSS feeds, though if you are using [octopress-feeds](https://github.com/octopress/feeds), RSS feeds for each language will be generated automatically.

How does it work? First this plugin groups all of your posts by language. Then at build time, any page with a language defined will
have its posts filtered to display only matching languages. This also works for `site.categories` and `site.tags`.
If your site uses [octopress-linkblog](https://github.com/octopress/linkblog) to publish link-posts, your `site.articles` and `site.linkposts` will be filtered as well.

## Site template language dictionaries

It's annoying to have to write multiple site layouts and includes when the only differences are translated words. Octopress Multilingual
adds language dictionaries to make this much easier. In your site's `_data` directory you can add language dictionaries with the file
naming pattern `lang_[language_code].yml`. For example:

```
_data
  lang_en.yml
  lang_de.yml
```

Your files might look like this:

```
# lang_en.yml
title: English title

# lang_de.yml
title: Deutsch titel
```

Now in your layouts or includes you can reference these dictionaries under the global variable `lang`. The configured page or post
language will determine which language dictionary is used. For example:

```
{% raw %}
# On a page or post where lang: en
{{ lang.title }} => English title

# On a page or post where lang: de
{{ lang.title }} => Deutsch titel
{% endraw %}
```

If no language is configured for a page or post, it will default to the site's default language.

```
{% raw %}
# No page lang, site is configured lang: en
{{ lang.title }} =>  English title
{% endraw %}
```

Since these are Jekyll data sources, these dictionaries can also be accessed at `site.data.lang_en` and `site.data.lang_de`. This
plugin merely adds the global `lang` variable and swaps out context based on configured language.

## Link between translated posts or pages

URLs can change and manually linking to translated posts or pages isn't the best idea. This plugin helps you link posts together using a shared translation ID. With [octopress](https://github.com/octopress/octopress), you'll be able to automatically add translation IDs to pages and posts. Then you can reference the array of translations with `post.tranlsations` or `page.translations`. Here's the syntax:

```
$ octopress id path [path path...]
```

This will create a unique key and automatically write it to the YAML front-matter each of the pages or posts you pass in. Here's an
example:

```
$ octopress id _posts/2015-02-02-english-post.md _posts/2015-02-02-deutsch-post.md _posts/2015-02-02-espanol-post.md
```

This will add `translation_id: fcdbc7e82b45346d67cced3523a2f236` to the YAML front-matter of each of these posts. There's nothing special about this key except that it is unique. If you want to write your own you can, it'll work just fine.

When you have posts or pages with a `translation_id` you can use the `translations` or `translation_list` tags to list links to translated posts or pages. For example:

```
{% raw %}
{% translations page %} # On a page/post layout
{% translations post %} # In a post loop

# Which outputs:
<a class='translation-link lang-de' href='/de/2015/02/02/deutsch-post'>Deutsch</a>, <a class='translation-link lang-es' href='/es/2015/02/02/espanol-post'>Español</a>

# If you prefer a list:
{% translation_list post %}

# Which ouputs:
<ul class='translation-list'>
  <li class='translation-item lang-de'>
    <a class='translation-link lang-de' href='/de/2015/02/02/deutsch-post'>Deutsch</a>
  </li>
  <li class='translation-item lang-es'>
    <a class='translation-link lang-es' href='/es/2015/02/02/espanol-post'>Español</a>
  </li>
</ul>
{% endraw %}
```

If you'd rather access translated posts manually, you can loop through the translations like this:

```
{% raw %}
{% if page.translated %}
  Translations: {% for t in page.translations %}
    <a href="{{ t.url }}">{{ t.lang | language_name }}</a>
  {% endfor %}
{% endif %}
{% endraw %}
```

## Reference posts by language

All posts are grouped by language and can be accessed directly with `site.posts_by_language`. For example:

```
{% raw %}
{% for post in site.posts_by_language.de %}  # German posts
{% for post in site.posts_by_language.en %}  # English posts
{% endraw %}
```

If you have [octopress-linkblog](https://github.com/octopress/linkblog) installed, you can access groups of link-posts and articles too.

```
{% raw %}
{% for post in site.linkposts_by_language.de %}  # German linkposts
{% for post in site.articles_by_language.de %}   # German articles
{% endraw %}
```

### Cross-posting languages

If you would like to write a post which shows up in indexes and feeds for every language, set `lang_crosspost: true` in your post's YAML front-matter.

```
title: "Ein nachdenklicher Beitrag"
lang: de
lang_crosspost: true
```

This post will show up with every language. However, it will be treated exactly like a post written in German
and will have one canonical URL.

### Language in permalinks

This plugin does not use categories to add language to URLs. Instead it adds the `:lang` key to Jekyll's permalink template.
Any post **with a defined language** will have its language in the URL. If this changes URLs for your site, you probably should [set up redirects](https://github.com/jekyll/jekyll-redirect-from).

If you define your own permalink style, you may use the `:lang` key like this:

```yaml
permalink: /posts/:lang/:title/
```

If you have not specified a permalink style, or if you are using one of Jekyll's default templates, your post URLs will change to include their language.
When using Jekyll's `pretty` url template, URLs will look like this:

```
/site_updates/en/2015/01/17/moving-to-a-multilingual-site/index.html
/site_updates/de/2015/01/17/umzug-in-eine-mehrsprachige-website/index.html
```

This plugin updates each of Jekyll's default permalink templates to include `:lang`.

```ruby
pretty  => /:lang/:categories/:year/:month/:day/:title/
none    => /:lang/:categories/:title.html
date    => /:lang/:categories/:year/:month/:day/:title.html
ordinal => /:lang/:categories/:year/:y_day/:title.html
```

If you don't want language to appear in your URLs, you must configure your own permalinks without `:lang`.

## Temporary language scoping

Using the `set_lang` liquid block, you can temporarily switch languages while rendering a portion of your site. For example:

```
{% raw %}
{{ page.lang }}    # => 'en'
{{ site.posts }}   # => All posts

{% set_lang de %}
  {{ page.lang }}  # => 'de'
  {{ site.posts }} # => German posts
{% endset_lang %}

{{ page.lang }}    # => 'en'
{{ site.posts }}   # => All posts
{% endraw %}
```

The `set_lang` tag will also accept variables, for example:

```
{% raw %}
{% assign lang = 'de' %}
{% set_lang lang %}   # equivilent to {% set_lang de %}

# On some page
{% include some_partial.html lang='de' %}

# In _includes/some_partial.html
{% set_lang include.lang %}    # equivilent to {% set_lang de %} 
{% endraw %}
```

If you have the [octopress-linkblog](https://github.com/octopress/linkblog) plugin installed, this will also change languages for your
`site.articles` and `site.linkposts` loops.

