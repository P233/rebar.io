---
layout: page
title: Settings
---

## Settings

### Default settings

There are four default settings of Rebar: `$mobile-first`, `$max-width`, `$breakpoints` and `$gutters`. To change a default value, create the variable before `@import "rebar"` and assign it a new value.

#### $mobile-first

Set media feature type, set to `true` will use `min-width`, and set to `false` will use `max-width`. It's set to `true` by default.

#### $max-width

Set default `max-width` for all containers. The default value is `1170px`.

#### $breakpoints

Set a breakpoints list. If mobile first the default list is `481px 769px 992px`. and if desktop first the default list is `992px 769px 481px`. You can set as many breakpoints as you need.

#### $gutters

Set default gutter width at each responsive slice. If mobile first the default list is `20px 20px 26px 30px`, and if desktop first the default list is `30px 26px 20px 20px`. This list should always have one more value than `$breakpoints`.


---


### Container settings

There are five settings for container. None of them are required, so a very basic container can be created like this: 

{% highlight scss %}
$container: (
  ".container": ()
);
{% endhighlight %}

{% include container.html %}

#### gutter

Container doesn't have gutter by default, set this to `true` to enable gutter. Gutter width is from the `$gutters` variable. In other words, this setting will turn a container to a full width grid but without nesting structure.

{% highlight text %}
Type:     boolean
Default:  false
Length:   single value
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container-gutter": (
    gutter: true
  )
);
{% endhighlight %}

{% include container-gutter.html %}

#### nested

Set a nested container. It works like the `.row` class of Bootstrap. If this set to `true` the other settings won't be affected, so use this setting independently.

{% highlight text %}
Type:     boolean
Default:  false
Length:   single value
{% endhighlight %}

example: 

{% highlight scss %}
$container: (
  ".container-gutter": (
    gutter: true
  ),
  ".container-nested": (
    nested: true
  )
);
{% endhighlight %}

{% include container-nested.html %}

#### width

Set fixed width at each responsive slice.

{% highlight text %}
Type:     number (1/2 | .5 | 50% | 600px | 40em) | null
Default:  null
Length:   space separated multiple values
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container-width": (
    width: 100px 300px 600px 900px
  )
);
{% endhighlight %}

{% include container-width.html %}

#### max-width

Adjust max width for container, this setting will override the default `$max-width`.

{% highlight text %}
Type:     number (1/2 | .5 | 50% | 600px | 40em)
Default:  $max-width
Length:   single value
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container-max-width": (
    max-width: 1280px
  )
);
{% endhighlight %}

{% include container-max-width.html %}

#### min-width

Set min width for container.

{% highlight text %}
Type:     number (1/2 | .5 | 50% | 600px | 40em)
Default:  null
Length:   single value
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container-min-width": (
    min-width: 600px
  )
);
{% endhighlight %}

{% include container-min-width.html %}


---


### Grid settings

There are eight settings for grid. None of them are required, but blank setting will create a grid with auto width.

#### float

Adjust float direction at each responsive slice.

{% highlight text %}
Type:     string (left | right | none) | null
Default:  left
Length:   space separated multiple values
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container": ()
);

$grid: (
  ".grid-float": (
    width: 1/3,
    float: right left null right
  )
);
{% endhighlight %}

{% include grid-float.html %}

#### offset-left

Set left offset (`margin-left`) at each responsive slice. If a grid only has `offset-left` or `offset-right` setting, the default `float` and `padding` properties won't be outputted, so this setting can be also used to create an offset class and use it independently.

{% highlight text %}
Type:     number (1/2 | .5 | 50% | 600px | 40em) | null
Default:  null
Length:   space separated multiple values
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container": ()
);

$grid: (
  ".grid-offset-left": (
    width: 1/2,
    offset-left: 0 null 30px 1/4
  )
);
{% endhighlight %}

{% include grid-offset-left.html %}

#### offset-right

Set right offset (`margin-right`) at each responsive slice. If a grid only has `offset-right` or `offset-left` setting, the default `float` and `padding` properties won't be outputted, so this setting can be also used to create an offset class and use it independently.

{% highlight text %}
Type:     number (1/2 | .5 | 50% | 600px | 40em) | null
Default:  null
Length:   space separated multiple values
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container": ()
);

$grid: (
  ".grid-offset-right": (
    width: 1/2,
    float: right,
    offset-right: 0 null 30px 1/4
  )
);
{% endhighlight %}

{% include grid-offset-right.html %}

#### gutter-left

Adjust left gutter width (`padding-left`) at each responsive slice, each value should not be omitted. For example, clear the left gutter have to set `gutter-left: 0 0 0 0`. In this setting, `null` means reset to the default gutter width not inherit form the previous value.

{% highlight text %}
Type:     number (1/2 | .5 | 50% | 600px | 40em) | null
Default:  $gutters/2
Length:   space separated multiple values
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container": ()
);

$grid: (
  ".grid-gutter-left": (
    width: 1/2,
    gutter-left: 0 null 5% 30px
  )
);
{% endhighlight %}

{% include grid-gutter-left.html %}

#### gutter-right

Adjust right gutter width (`padding-right`) at each responsive slice, each value should not be omitted. For example, clear the right gutter have to set `gutter-right: 0 0 0 0`. In this setting, `null` means reset to the default gutter width not inherit form the previous value.

{% highlight text %}
Type:     number (1/2 | .5 | 50% | 600px | 40em) | null
Default:  $gutters/2
Length:   space separated multiple values
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container": ()
);

$grid: (
  ".grid-gutter-right": (
    width: 1/2,
    gutter-right: 0 null .05 30px
  )
);
{% endhighlight %}

{% include grid-gutter-right.html %}

#### width

Set fixed grid width at each responsive slice.

{% highlight text %}
Type:     number (1/2 | .5 | 50% | 600px | 40em) | null
Default:  null
Length:   space separated multiple values
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container": ()
);

$grid: (
  ".grid-width": (
    width: 1 null .5 1/4
  )
);
{% endhighlight %}

{% include grid-width.html %}

#### max-width

Set max width for grid.

{% highlight text %}
Type:     number (1/2 | .5 | 50% | 600px | 40em)
Default:  null
Length:   single value
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container": ()
);

$grid: (
  ".grid-max-width": (
    max-width: 800px
  )
);
{% endhighlight %}

{% include grid-max-width.html %}

#### container

Set grid as a container. If this set to `true`, gutter won't be outputted.

{% highlight text %}
Type:     boolean
Default:  false
Length:   single value
{% endhighlight %}

example:

{% highlight scss %}
$container: (
  ".container": ()
);

$grid: (
  ".grid-container": (
    width: 2/3,
    container: true
  )
);
{% endhighlight %}

{% include grid-container.html %}
