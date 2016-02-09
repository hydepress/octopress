---
title: Date Format
---

Put nicely formatted dates on any post or page.


## Installation

Add this line to your application's Gemfile:

    gem 'octopress-date-format'

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install octopress-date-format

Next add it to your gems list in Jekyll's `_config.yml`

    gems:
      - octopress-date-format
    
## Usage

Any post (or page with a date) will automatically have some new date attributes. 

- `date` - The date, `2014-07-03 14:08:00 +0000`
- `date_text` - The formatted date, Jul 3rd, 2014
- `time_text` - The formatted time, 2:08 pm
- `date_xml` - The XML schema formatted date, 2014-07-03T14:08:00+00:00
- `date_html` - The formatted date in a `<time>` tag.
- `date_time_html` - The formatted date and time in a `<time>` tag.

Here's an example of what would be rendered with `{{ post.date_time_html }}`.

```html
<time class='entry-date' datetime='2014-07-03T14:08:00+00:00'>
  <span class='date'>
    <span class='date-month'>Jul</span>
    <span class='date-day'>3</span><span class='date-suffix'>rd</span>,
    <span class='date-year'>2014</span>
  </span>
  <span class='time'>2:08 pm</span>
</time>
```

If you update a post or page and want to display this in a template, add this to YAML
front-matter, `date_updated: 2014-07-03 15:03:15` and your post will have updated date
attributes as well.

- `updated` - The date, `2014-07-03 15:03:15 +0000`
- `date_updated_text` - The formatted date, Jul 3rd, 2014
- `time_updated_text` - The formatted time, 3:03 pm
- `date_updated_xml` - The XML schema formatted date, 2014-07-03T15:03:15+00:00
- `date_updated_html` - The formatted date in a `<time>` tag.
- `date_time_updated_html` - The formatted date and time in a `<time>` tag.

Of course you can use Liquid conditionals when outputting an updated date.

```
{% raw %}
{% if post.updated %}Updated: {{ post.date_time_updated_html }}{% endif %}
{% endraw %}
```

## Configuration

You may change the formatting of the dates and times in
Jekyll's configuration file. Here are the defaults:

```
date_format: 'ordinal'     # July 3rd, 2014
time_format: '%-I:%M %P'   # 2:08 pm
```

To choose a different format, use a [Ruby strftime](http://apidock.com/ruby/DateTime/strftime)
compatible string. For example:

```
date_format: "%Y-%m-%d"  # e.g. 2014-07-03
time_format: "%H:%M"     # 24 hour time
```

