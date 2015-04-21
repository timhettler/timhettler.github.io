---
layout: post
title:  "CSS-Only Placeholder Images"
date:   2015-04-21 12:00:00
categories: css sass
---
Often times, I'm ready to get started on the basic structure of a website before the final visual assets are complete. I don't like using "in progress" images because they can be distracting during client reviews – the client may focus on the incomplete visuals, distracting them from giving feedback on other parts of the project. Likewise, placeholder image services like Placekitten or Fill Murray are not only distracting, but also very unprofessional-looking. As a final point, using placeholder image services requires you to rely on a 3rd-party service, which I like to avoid whenever possible.

My answer to this problem is building CSS-only placeholder images. A naive solution is to simply set the width & height of an empty div:

{% highlight css %}
.placeholder {
  background-color: LightCoral;
  height: 200px;
  width: 200px;
}
{% endhighlight %}

The problem with this code is that the element will not maintain its intrinsic ratio when resized. For responsive sites (read: all sites now), this is a deal-breaker. To maintain the proper aspect ratio, we can use the so-called **padding-bottom hack**. This technique first came to my attention in Nicolas Gallagher's [Flexible CSS Cover Images][1] article, but has been around in some form at least since it was described in Thierry Koblentz's 2009 A List Apart article, [Creating Intrinsic Ratios for Video][2]. The gist of this technique is that the padding property is always based on an element's width, so leaving the height of an element undefined and setting the padding-bottom to a percentage makes the element maintain a consistent ratio when resized.

Anyway, if we update our example to use the padding-bottom hack:

{% highlight css %}
.placeholder {
  background-color: LightCoral;
  width: 200px;
}

.placeholder:before {
  padding-bottom: 100%;
}
{% endhighlight %}

...the element wil always maintain a 1:1 ratio. If we set the padding-bottom to 50%, then it would create a 2:1 ratio.

I've taken this solution one step further and wrapped it into a Sass extension called [Sass-FPO][3]. FPO stands for "For Placement Only"; "placeholders" are already a reserved keyword in Sass, so I chose FPO to reduce confusion.

<p class="sassmeister" data-gist-id="14af5a6c73d723ad4715" data-height="480" data-theme="tomorrow"><a href="http://sassmeister.com/gist/14af5a6c73d723ad4715">Play with this gist on SassMeister.</a></p><script src="http://cdn.sassmeister.com/js/embed.js" async></script>


Using this Sass mixin, we can start coding faster, and have our placeholder images blend seamlessly into the design. If you find this helpful, please star the project on Github, or mention it on Twitter!

[1]: http://nicolasgallagher.com/flexible-css-cover-images/
[2]: http://alistapart.com/article/creating-intrinsic-ratios-for-video
[3]: https://github.com/timhettler/sass-fpo