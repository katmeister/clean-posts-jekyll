---
layout: post
title:  "Demo: This is clean AF"
date:   2016-01-12 22:08:33 -0800
snippet: "Want full-bleed backgrounds and images that templates can't fulfill? But hate mixing Markdown/Liquid with HTML? Here's a simple method!"
---
{% include styles.md %}

{{ wrapper_white }}
{{ writing }}
Want full-bleed backgrounds and images that templates can't fulfill? But hate mixing Markdown/Liquid with HTML? Here's a simple method!

## Create styles.md
In order to remove clunky HTML from your Markdown file, we need to put them in a separate file that we can include using Liquid.

Create a **styles.md** file in your includes folder (or whatever you want to name it). This is where you'll put your HTML blocks. Create a corresponding **_styles.scss**.

## Use capture
Liquid has a nifty feature called **capture** that, as the name suggests, captures a string into a variable. Here, I'm capturing my div tags into 'writing' and 'end_block.'

{% highlight html %}
{% raw %}
{% capture writing %}
<div class="wrapper" markdown="1">
{% endcapture %}

{% capture end_block %}
</div>
{% endcapture %}
{% endraw %}
{% endhighlight %}

Be sure to include **markdown="1"** in your tags. This retains Markdown rendering within the HTML blocks, and you'll see the correct syntax highlighting in your text editor.

{% highlight css %}
{% raw %}
.wrapper {
  max-width: 800px;
  margin: 0 auto;
  padding: 0 30px;
}
{% endraw %}
{% endhighlight %}

Style your HTML accordingly in your SCSS or CSS file and capture as many HTML blocks as you want in styles.md. Don't forget to capture closing tags!

## Include in your posts
At the beginning of your .markdown posts, include styles.md:

{% highlight html %}
{% raw %}
{% include styles.md %}
{% endraw %}
{% endhighlight %}

Now, you're ready to use the HTML blocks throughout your post! Use Liquid output to start and end the block, like this:
{% highlight html %}
{% raw %}
{{ writing }}
Yay content!
{{ end-block }}
{% endraw %}
{% endhighlight %}

{{ end_block }}
{{ end_block }}

{{ wrapper_beige }}
{{ writing }}
# Full-bleed backgrounds
You can easily insert full-bleed color backgrounds into your posts. Define .color-wrapper and .beige classes in your CSS:

{% highlight css %}
{% raw %}
.color-wrapper {
  width: 100%;
  padding: 60px 0;
}

.beige {
  background: #f1e5c2;
}
{% endraw %}
{% endhighlight %}

{% highlight html %}
{% raw %}
{% capture wrapper_beige %}
<div class="color-wrapper beige" markdown="1">
{% endcapture %}
{% endraw %}
{% endhighlight %}

{% highlight html %}
{% raw %}
{{ wrapper_beige }}
{{ writing }}
Your writing is now in full-bleed bg! Nice and clean!
{{ end_block }}
{{ end_block }}
{% endraw %}
{% endhighlight %}

{{ end_block }}
{{ end_block }}

{{ full_image }}
![img](http://placehold.it/1600x800)
{{ end_block }}

{{ wrapper_orange }}
{{ writing }}
# Image assets
Mix it up with full-bleed images and fitted images.
{{ end_block }}

{{ midsize_image }}
![img](http://placehold.it/1600x800)
{{ end_block }}

{{ writing }}
Fitted images are great for vertical designs so it's easier to see all the details with minimal scrolling.
{{ end_block }}
{{ end_block }}
