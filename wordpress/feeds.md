# WordPress Feeds

## WordPress Built-in Feeds {#wordpress-built-in-feeds}

By default, WordPress comes with various feeds. They are generated by template tag for [bloginfo()](https://developer.wordpress.org/reference/functions/bloginfo/) for each type of feed and are typically listed in the sidebar and/or footer of most WordPress Themes. They look like this:

URL for [RDF/RSS 1.0 feed](https://web.resource.org/rss/1.0/) 

```
<?php bloginfo('rdf_url'); ?>
```

URL for [RSS 0.92 feed](https://www.rssboard.org/rss-0-9-2)

```
<?php bloginfo('rss_url'); ?>
```

URL for [RSS 2.0 feed](https://www.rssboard.org/rss-specification) 

```
<?php bloginfo('rss2_url'); ?>
```

URL for [Atom feed](http://www.atomenabled.org/) 

```
<?php bloginfo('atom_url'); ?>
```

URL for comments RSS 2.0 feed 

```
<?php bloginfo('comments_rss2_url'); ?>
```

The first four feeds display recent updates and changes to your site's content for the different feedreaders. Of these, the RSS feeds are the most well known. The last feed example is used by RSS 2.0 feedreaders and does not show your site's content. It only shows the comments made on your site.

To track the comments on a specific post, the [post_comments_feed_link()](https://developer.wordpress.org/reference/functions/post_comments_feed_link/) template tag is used on single post pages like this:

```
<?php post_comments_feed_link('RSS 2.0'); ?>
```

There are ways to modify these feeds, and these are covered in the article on [Customizing Feeds](https://codex.wordpress.org/Customizing_Feeds).

## Adding Feeds {#adding-feeds}

Not all WordPress Themes feature all of the RSS Feed types that are available through WordPress. To add a feed to your site, find the location of where the other feeds are, typically in your sidebar.php or footer.php template files of your Theme. Then add one of the tags listed above to the list, like this example:

```
<ul class="feeds">
  <li><a href="<?php bloginfo('rss2_url'); ?>" title="<?php _e('Syndicate this site using RSS'); ?>"><?php _e('<abbr title="Really Simple Syndication">RSS</abbr>'); ?></a></li>
  <li><a href="<?php bloginfo('atom_url'); ?>" title="<?php _e('Syndicate this site using Atom'); ?>"><?php _e('Atom'); ?></a></li>
  <li><a href="<?php bloginfo('comments_rss2_url'); ?>" title="<?php _e('The latest comments to all posts in RSS'); ?>"><?php _e('Comments <abbr title="Really Simple Syndication">RSS</abbr>'); ?></a></li>
</ul>
```

### Adding Graphics to Feed Links {#adding-graphics-to-feed-links}

Many people like to have a graphic representing the feed instead of words. There are now [standards](http://www.feedicons.com/) for these graphics or "buttons", but you can [make your own](https://kalsey.com/tools/buttonmaker/) to match the look and colors on your site. ![](https://wordpress.org/documentation/files/2019/03/rssfeed.gif)

To add a graphic to your feed link, simply wrap the link around the graphic such as:

```
<a href="<?php bloginfo('rss2_url'); ?>" title="<?php _e('Syndicate this site using RSS'); ?>"><img src="https://example.com/images/feed-icon-14x14.png" alt="RSS Feed" title="RSS Feed"></a>
```

### Changing Addresses {#changing-addresses}

If you are currently using other webblog software and are changing to WordPress, or are moving your weblog to a new location, you can "forward" RSS readers to your new RSS feeds using file rewrites and redirects in your .htaccess file.

Edit the `.htaccess` file in your root folder; if no file exists, create one.

Here is an example for a b2 feed:

```
RewriteRule ^b2rss2.php(.*)? /wordpress/?feed=rss2 [QSA]
```

Here is an example for MovableType Users:

```
RewriteRule ^index.xml(.*)? /wordpress/?feed=rss2 [QSA]
```

