---
layout: post
title: CSS Animation
category: CSS
tags: [css]
---

Quick note about CSS animation. 

## CSS Animation

CSS3 animation lets an element gradually change from one style to another.

Two steps:

1. Use `@keyframes` to define an animation.
2. Set this animation on an element with animation properties

We could set properties one-by-one or with following shorthand:

{% highlight css %}
animation: [animation-name] [animation-duration] [animation-timing-function] [animation-delay] [animation-iteration-count] [animation-direction] [animation-fill-mode] [animation-play-state];
{% endhighlight %}

## @keyframes

It defines what the animation looks like at each stage of the animation timeline. It is composed of:

* Name of the animation. For example, changeColor.
* Stages: From 0% to 100% to represent the whole process of animation
* CSS Properties: The CSS properties defined for each stage of the animation timeline.

Following example creates an animation called `changeColor` and assign it to `div:hover`:

{% highlight css %}
@keyframes changeColor {
  0% {
    background: red;
  }
  60% {
    background: blue;
  }
  100%{
    background: green;
  }
}

div:hover{
  animation: changeColor 5s ease .1s;
}
{% endhighlight %}

> In above example, we could also use `from` to represent `0%` and `to` to represent `100%`

## Animation Properties

It has following properties: 

1. animation-name
2. animation-duration
3. animation-timing-function
4. animation-delay
5. animation-iteration-count
6. animation-direction
7. animation-fill-mode
8. animation-play-state

### animation-name

The name of the animation, defined in the @keyframes.

### animation-duration

The duration of the animation, in seconds (e.g., 5s) or milliseconds (e.g., 200ms).

### animation-timing-function

The speed curve or pace of the animation:

| Timing Function | Description |
|---|---|
| linear | The animation has the same speed from start to end |
| ease | **Default value**. The animation has a slow start, then fast, before it ends slowly. |
| ease-in | Start slowly and end fast.  |
| ease-out | Start more quickly than linear ones and end slowly. The opposite of ease-in. |
| ease-in-out | Both a slow start and a slow end |
| initial | Sets this property to its default value. So `ease`. |
| inherit | Inherits this property from its parent element. |

> Check [The basics of easing](https://developers.google.com/web/fundamentals/design-and-ui/animations/the-basics-of-easing?hl=en) for details.

### animation-delay 

It specifies when the animation will start. The value is defined in seconds (s) or milliseconds (mil).

### animation-iteration-count

It specifies the number of times that the animation will play. The possible values are:

* a specific number of iterations (default is 1)
* `infinite` - repeats forever
* `initial`
* `inherit`

### animation-direction

It specifies whether the animation should play forward, reverse, or in alternate cycles.

* `normal` - Default. On each cycle the animation resets to the beginning state (0%) and plays forward again (to 100%).

* `reverse` - On each cycle the animation resets to the end state (100%) and plays backwards (to 0%).

* `alternate` - On each odd cycle, the animation plays forward (0% to 100%). On each even cycle, the animation plays backwards (100% to 0%).

* `alternate-reverse` - On each odd cycle, the animation plays in reverse (100% to 0%). On each even cycle, the animation plays forward (0% or 100%).

### animation-fill-mode

It specifies if the animation styles are visible before or after the animation plays. 

* `normal` - Default. The animation does not apply any styles to the element, before or after the animation.

* `forwards` - After the animation is finished, the styles defined in the final keyframe (100%) are retained by the element.

* `backwards` - Before the animation (during the animation delay), the styles of the initial keyframe (0%) are applied to the element.

* `both` - `forwards` with `backwards`.

### animation-play-state

Two values: `running` and `paused`.

It specifies whether the animation is `playing` or `paused`. **Resuming a paused animation starts the animation where it was left off. But if pause an animation, the element style will return back to its origin.**

Example:

{% highlight css %}
div:hover {
  animation-play-state: paused;
}
{% endhighlight %}

## Multiple Animations

Add multiple animations to a selector with comma:

{% highlight css %}
div {
  animation: animationA 2s, animationB 2s;
}
{% endhighlight %}

## Refs

* [Imooc 十天精通CSS3](http://www.imooc.com/learn/33)
* [CSS Animation for Beginners](https://robots.thoughtbot.com/css-animation-for-beginners#animation-iteration-count)
* [CSS3 animation-timing-function Property](http://www.w3schools.com/cssref/css3_pr_animation-timing-function.asp)