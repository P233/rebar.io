---
layout: page
title: Guide
---

## Guide

### Box-sizing

Rebar use `padding` for gutter (same as Bootstrap 3 grids). In order to get a better control of grid width, `box-sizing: border-box` is required. (see [* { Box-sizing: Border-box } FTW](http://www.paulirish.com/2012/box-sizing-border-box-ftw/))

{% highlight css %}
html {
  box-sizing: border-box;
}
*, *:before, *:after {
  box-sizing: inherit;
}
{% endhighlight %}

### Mobile first or Desktop first

Rebar supports both mobile first and desktop first `@media query` types. Each type affects how you setup the containers and grids. If mobile first, media feature is `min-width`, the other way round, media feature is `max-width`. By default, mobile first is enabled. If you'd like to enable desktop first, create a variable and set it to false: `$mobile-first: false`.

### Responsive Slices

The core part of Rebar is responsive slices. In the `$breakpoints` variable you can set a list of breakpoints (`n` breakpoints), and it will represent `n + 1` responsive slices. For example, when mobile first enabled, `$breakpoints: 481px 769px 993px` represents four slices: slice 0 for any width, slice 1 for `min-width: 481px`, slice 2 for `min-width: 769px`, and slice 3 for `min-width: 993px`. When setting `width: 1 1/2 null 1/3` to a container or grid, the first value `1` is for slice 0, the second value `1/2` is for slice 1, the third value `null` is for slice 2, and the fourth value `1/3` is for the last slice 3.

Based on the `$mobile-first` setting, there are two circumstances: 

{% highlight text %}
$mobile-first:  true
---------------------------------------------------------------------------
 $breakpoints:                481px         769px         993px
      slice 0:  0 ------------------------------------------------------- ∞
      slice 1:                |-----------------------------------------> ∞
      slice 2:                              |---------------------------> ∞
      slice 3:                                            |-------------> ∞
---------------------------------------------------------------------------
     $gutters:  20px          20px          26px          30px
        width:  100%          50%           null          33.3%
{% endhighlight %}

{% highlight text %}
$mobile-first:  false
---------------------------------------------------------------------------
 $breakpoints:                992px         768px         480px
      slice 0:  ∞ ------------------------------------------------------- 0
      slice 1:                |-----------------------------------------> 0
      slice 2:                              |---------------------------> 0
      slice 3:                                            |-------------> 0
---------------------------------------------------------------------------
     $gutters:  30px          26px          20px          20px
        width:  33.3%         50%           null          100%
{% endhighlight %}


#### null

The `null` means do not output this setting at the corresponding slice. In the above example, Rebar won't output the `width` setting at slice 2, so the width is still the last set width. You can consider `null` as inherit, but in `gutter-left` and `gutter-right` settings, `null` means reset to the default gutter width. `null` can not be used in `$gutters` as well.

Trailing `null` can be omitted, for example, `width: 1/3 null null null` can be write as `width: 1/3`.


### Setup container and grid

All settings for container and grid are saved in `$container` and `$grid` Sass maps or Stylus hashes. To create a new container or gird class, nest a second level map/hash, quote selector(s) as name, and then add settings inside. For example: 

**Sass map**

{% highlight scss %}
$container: (
  ".container": (
    width: 100px 300px 600px 900px
  )
);
$grid: (
  ".third": (
    width: 1 null 50% 1/3
  )
);
{% endhighlight %}

**Stylus hash**

{% highlight js %}
$container = {
  ".container": {
    width: 100px 300px 600px 900px
  }
};
$grid = {
  ".third": {
    width: 1 null 50% 1/3
  }
};
{% endhighlight %}

Read [settings](/settings.html) to check out all available settings of Rebar.


### Columns

Rebar doesn't have a fixed amount of columns. To set a 6 columns grid of 12 columns, you can set the width to `1/2`, `50%`, `.5`, or `6/12`. It's also possible to set up untypical width grids, like one grid with width `64.136%` and another grid with width `(1 - 64.136%)`.

When setting `width` `max-width` `min-width` `offset` `gutter` and `$gutters` in Rebar, you can use fraction `1/2`, decimal `.5`, percentage `50%` or number with unit like `600px` `40em`.


### @import rebar

Rebar need to be `@import` after the `$container` and `$grid` maps/hashes, therefore it can read settings from them. It is recommended to organise the settings code in the following order:

{% highlight scss %}
// Default Settings (optional)
// $mobile-first: true
// $max-width:    1170px
// $breakpoints:  481px 769px 993px
// $gutters:      20px 20px 26px 30px

// Containers
$container: ();

// Grids
$grid: ();

// Import Rebar
@import "rebar";
{% endhighlight %}

### Generate CSS

When compiling, Rebar generates CSS code based on all your settings. It will output clean code as possible as it can. All elements with default gutter will be outputted in one CSS rule. All 100% width grids will be outputted in one CSS rule as well.


---

## slicer() Mixin

The `slicer()` mixin helps Rebar to target responsive slices and generate `@media query` code, but it can also be used independently. It accepts one or two arguments. Passing slice index to it will get the corresponding `@media query` code. Passing negative slice index to it will get the opposite corresponding `@media query` code. Passing two slice indexs will get a responsive range. For example: 

{% highlight scss %}
// $mobile-first: true
// $breakpoints:  481px 769px 993px
@include slicer(2) {}
@include slicer(-2) {}
@include slicer(2, -3) {}
{% endhighlight %}

is compiled to:

{% highlight scss %}
@media screen and (min-width: 769px) {}
@media screen and (max-width: 768px) {}
@media screen and (min-width: 769px) and (max-width: 992px) {}
{% endhighlight %}

All valid `slicer()` results:

{% highlight text %}
$mobile-first:  true
---------------------------------------------------------------------------
 $breakpoints:                481px         769px         993px
---------------------------------------------------------------------------
   slicer(-1):  0 <----------|
    slicer(1):                |-----------------------------------------> ∞
   slicer(-2):  0 <------------------------|
    slicer(2):                              |---------------------------> ∞
   slicer(-3):  0 <--------------------------------------|
    slicer(3):                                            |-------------> ∞
---------------------------------------------------------------------------
slicer(1, -2):                |<---------->|
slicer(2, -3):                              |<---------->|
slicer(1, -3):                |<------------------------>|
{% endhighlight %}

{% highlight text %}
$mobile-first:  false
---------------------------------------------------------------------------
 $breakpoints:                992px         768px         480px
---------------------------------------------------------------------------
   slicer(-1):  ∞ <----------|
    slicer(1):                |-----------------------------------------> 0
   slicer(-2):  ∞ <------------------------|
    slicer(2):                              |---------------------------> 0
   slicer(-3):  ∞ <--------------------------------------|
    slicer(3):                                            |-------------> 0
---------------------------------------------------------------------------
slicer(1, -2):                |<---------->|
slicer(2, -3):                              |<---------->|
slicer(1, -3):                |<------------------------>|
{% endhighlight %}

Please note there is no `slicer(0)`.

The `slicer()` mixin can only be `@include` after `@import "rebar"`. It is recommended to setup the grid system earlier in your project, such as after the CSS reset.

### query-breakpoint() Function

Because the `slicer()` mixin can only output `min-width` and `max-width` media features. The `query-breakpoint()` function will help you to get the breakpoint width if other media features are needed. Passing a negative slice index will return the queried breakpoint width with `-1` (if mobile first) or `+1` (if desktop first). For example:


{% highlight scss %}
/* $mobile-first: true */
/* $breakpoints:  481px 769px 993px */
@media screen and (min-device-width: query-breakpoint(1))
              and (max-device-width: query-breakpoint(-3)) {}

/* $mobile-first: false */
/* $breakpoints:  992px 768px 480px */
@media screen and (max-device-width: query-breakpoint(1))
              and (min-device-width: query-breakpoint(-3)) {}
{% endhighlight %}

is compiled to:

{% highlight css %}
/* $mobile-first: true */
/* $breakpoints:  481px 769px 993px */
@media screen and (min-device-width: 481px) and (max-device-width: 992px) {}

/* $mobile-first: false */
/* $breakpoints:  992px 768px 480px */
@media screen and (max-device-width: 992px) and (min-device-width: 481px) {}
{% endhighlight %}
