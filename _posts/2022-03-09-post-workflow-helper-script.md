---
layout: post
title: "Post Helper Script"
slug: post-workflow-helper-script
author: alex
categories: [bash,jekyll,blog,post]
image: assets/images/post-workflow-helper-script/imgs/img1.jpg
tags: []
---
It struck me, it might be useful to have a quick helper script to make the setup of a new post a little less hassle.  In general it's not really a big task, just copy an old post, edit the front matter and clear out the main body of the text, but I intend to extend the template I'm using to include galleries populated from a thumbnail directory linked to the post.  This and a few other workflow ideas I've had necessitate the creation of a few subdirectories under other paths and all in all I'd rather have a script do the heavy lifting.  There are probably other options out there, more fully featured and robust, but coding is fun and I'm writing this in vim - fancy isn't necessarily high on my priority list.

To that end I've went and written a little bash helper script to allow me to generate a post and the associated image directories as a one liner from the terminal. I've included some functionality to allow me to create older posts as well as I'd like to document some older projects I've done as well and give this thing some history.  It's not the most advanced script in the world, but it does the job.

If you'd like to make use of the script you can grab it from the github repo here:

Or alternatively:

wget method
add to bashrc

## How to use

To create a new post is a one-liner:

```
mkpost -s post-workflow-helper-script -a alex -t "A Handy Helper Script For Generating Posts" -i img1.jpg -c bash,jekyll,blog,post -d 2022-03-09
```

This will generate a file called `2022-03-09-post-workflow-helper-script.md` in your `./_posts/` directory,  and `.../post-workflow-helper-script/imgs/` and `.../post-workflow-helper-script/thumbs/` directories under `./assets/images`

The `2022-03-09-post-workflow-helper-script.md` will also have it's front matter populated:

```
---
layout: post
title: "A Handy Helper Script For Generating Posts"
slug: post-workflow-helper-script
author: alex
categories: [bash,jekyll,blog,post]
image: assets/images/post-workflow-helper-script/imgs/img1.jpg
tags: []
---
```


And in brief the options are:

```
-s    slug/filename/subdirectory
-a    author
-t    title
-i    title image
-c    categories
-g    tags
-d    date
```

They're all optional apart from the `-s` option, this specifies not only the slug, but the name of the file and the subdirectory that gets created in the images directory for the post in question.  While most of the options should be relatively self explanatory it's worth mentioning that catergories and tags should be separated by commas if there's more than one of them. The title image is going to assume you want to use the image directory that's created by the script, so just specify the actual image filename itself.  For the date, if the date option isn't specified, the script assumes you want to use the system date.

To ensure you don't accidently create a ton of random .md files and directories all over the place there are a few basic checks in place too.  First of it tries to ensure you're in an appropriate directory before running the script, basically you need `./_posts/` and `./assets/images/` subdirectories inside the directory from which you run the script or it's just going to complain at you.  Next it ensures you don't already have those files or directories, I don't want to overwrite anything by accident! Finally it checks if the date is a passed value that it roughly conforms to YYYY-MM-DD, although I've not gone too deep down that rabbit hole, so long as the numbers and dashes are good it doesn't necessarily ensure it's a valid date.

Other than that it should be a relatively easy script to use and modify if you so desire.
