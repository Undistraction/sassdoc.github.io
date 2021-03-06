---
layout: default
title: "Theme context"
group: "Custom theme"
---

If you want to create your own theme, you'll have to mess with the
`ctx` object that will be passed to you.

This object contains the current project informations, the user's
configuration, and the parsed documentation data.

I'll describe here the general context structure, but the documentation
data is defined in [its own page](/data-interface/).

## Overview

{% highlight js %}
{
  view: {
    // Raw data from `view.json` or any JSON file passed to
    // SassDoc's `--config` option (or API equivalent).
  },

  package: {
    // Raw data from the project's `package.json`, or a JSON file
    // whose path was given in `view.package`, or an object directly
    // defined in `view.package`.
  },

  theme: function (dest, ctx) {
    // The theme function, probably a reference to **your** theme
    // function if you're writing a theme. You can ignore it unless you
    // want some kind of recursivity.
  },

  data: {
    // Parsed documentation object like described in Sassdoc Data
    // Interface wiki page.
  },
}
{% endhighlight %}

View
----

Don't assume the view object will contain anything. If the user
haven't got a `view.json` and didn't set a `--config`, it will be
an empty object.

The view has no strict interface. The users can put whatever they
want in this object. You can use it to let the user configure your
theme (the main purpose of the view object is indeed configuration).

<p class="note  note--info"><strong>Note:</strong> if you use <a href="https://github.com/SassDoc/sassdoc-filter">SassDoc Filters</a>, they also can be configured with the view object. Watch the filters documentation.</p>

An example view object, assuming you use some filters:

{% highlight js %}
{
  display: {
    access: ['public', 'private'],
    alias: false,
  },

  groups: {
    slug: 'Title',
    helpers: 'Helpers',
    hacks: 'Dirty Hacks & Fixes',
    'undefined': 'Ungrouped',
  }
}
{% endhighlight %}

## Package

[Ahem](https://www.npmjs.org/doc/files/package.json.html).

<p class="note  note--info"><strong>Note:</strong> with the <a href="https://github.com/SassDoc/sassdoc-filter#markdown">Markdown filter</a>, <code>package.description</code> will be parsed as Markdown.</p>

## Data

Everything is in [Data Interface](/data-interface/).
