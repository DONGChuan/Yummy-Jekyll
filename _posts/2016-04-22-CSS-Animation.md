---
title: WordPress Snippets and Hacks
date: '2016-04-22 00:00:00'
layout: post
tags:
- css
categories: CSS
---
Post revisions are super useful sometimes, but from time to time you might want to clean your database. Here’s a super easy way to delete all posts revisions.

Open you functions.php file and paste the following code:

    $wpdb->query( "DELETE FROM $wpdb->posts WHERE post_type = 'revision'" );

Save the file and open your blog homepage to run the code. Once done, there’s no need to keep the code snippet in your functions.php file, as it will always delete all post revisions. So simply remove it.

## Automatically link Twitter usernames in WordPress

Are you using Twitter a lot? Today’s recipe is a cool piece of code to automatically link Twitter usernames on your posts, pages, and comments.

Paste the code below into your functions.php file:

```
function twtreplace($content) { $twtreplace = preg_replace('/([^a-zA-Z0-9-_&])@([0-9a-zA-Z_]+)/',"$1<a href=\"http://twitter.com/$2\" target=\"_blank\" rel=\"nofollow\">@$2</a>",$content); return $twtreplace; }

add_filter('the_content', 'twtreplace'); 
add_filter('comment_text', 'twtreplace’);
```

Once you saved the file all twitter usernames in posts and comments will automatically be linked to their Twitter profiles. Usernames have to be written under the form @username.