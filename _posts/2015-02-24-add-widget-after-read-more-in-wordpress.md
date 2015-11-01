---
layout: post
title: Add a Dynamic Widget After the Read More Link in WordPress
permalink: /blog/add-widget-after-read-more-in-wordpress/
---

While I was tinkering with my WordPress blog
[Self-Learner](http://www.self-learner.com), I realized that it would be
convenient if I could automatically include a Google ad inside every post,
right after the "read more" link in single post views.

Turns out, there is no plugin or built-in hook for latching onto that
specific part of a post (please correct me if I'm wrong), so your only option
is to hack it.

Since WordPress allows you to preprocess posts, you can crawl through the
content and look for the "more link" placeholder and place a custom sidebar
there which can then accommodate widgets. By doing so you'll be able to
dynamically drag and drop content right into that spot from the Widgets panel.
If no widget is present, it will simply do nothing.

First, let's create a sidebar by copying and pasting the following code into
your theme's *functions.php* file:

{% highlight php startinline=true %}
add_action('widgets_init', 'YOUR_THEME_widgets_init');

function YOUR_THEME_widgets_init()
{
  register_sidebar(array(
    'name'          => 'After More Link',
    'id'            => 'after_more_link',
    'before_widget' => '',
    'after_widget'  => '',
    'before_title'  => '',
    'after_title'   => '',
  ));
}
{% endhighlight %}

Then bind the sidebar to the more link placeholder:

{% highlight php startinline=true %}
add_filter('the_content', 'widget_added_after_more_link');

function widget_added_after_more_link($text)
{
  $sidebar_id = 'after_more_link';

  if (is_single() && is_active_sidebar($sidebar_id)) {
    $pos1 = strpos($text, '<span id="more-');
    $pos2 = strpos($text, '</span>', $pos1);

    if ($pos1 && $pos2) {
      ob_start();
      dynamic_sidebar($sidebar_id);
      $widget_content = ob_get_contents();
      ob_end_clean();

      $text1 = substr($text, 0, $pos2);
      $text2 = substr($text, $pos2);
      $text = $text1 . $widget_content . $text2;
    }
  }

  return $text;
}
{% endhighlight %}

Now go to your dashboard and place any widget inside the sidebar entitled
*After More Link*.
