---
layout: post
title: Gulp to Azure
categories:
- Personal
tags: [javascript, azure, gulp]
published: true
---

Gulp has been in place in iVendi for about 2 months now. It's really brought down the build times, but also the complexity. Some (including me) would say this is an even bigger win.

This week I started to get to grips with Node streams in a big way so that I could write my own streaming build step, and I have to say that it was a lot easier that I had expected and definitely very powerful.

The basic premise for my task is to upload all our front end code to Azure blobs.

###First Crack
The first version of a solution came from a colleague and looked as such . . .

{% gist 9803545 %}

This solution worked but for me it was a bit too . . . Non-Streaming?

Its performing a few different tasks here

- uploading the files to azure
- prefixing a version to the filenames of JS & CSS (/static/bazinga.js --> /static/\<some-prefix\>-bazinga.js)
- insert appropriate ```<script>``` and ```<link>``` tags in the ```index.html```

So for me it was a little too mixed in its concern so i decided to break it into seperate parts, also the ```files.forEach``` seems to be going aginst what streaming is about. So i gave a crack at refactoring this and came up with two new parts.

###The versioning part

{% gist 9803617 %}

Gulp tasks work on an Object stream which will 'event' out new File objects. These can be manipulated and then passed back. So for this task I'm amending the ```chuck.path``` to insert the prefix at the right place.

###The uploading part

{% gist 9803536 %}

The azure upload is the last part in our process so for just now i have made a writeable stream that does now return any more data (a destination) but this could be changed to be correctly streaming with little or no functional difference.

Lucily the ```azure``` module provides an upload function which accepts a stream also, so after making sure the container is avaliable, i can simply pipe the chunk directly to this function **line#21**

###Amending index.html

This was just the use of ```htmlReplace()``` in a different section of the build file.

###Final task

The final thing looks something like this

```javascript
gulp.task('deploy', ['timestamp'], function(){
    'use strict';

    var container = 'dealer-' + (process.env.TRAVIS_BRANCH || 'local');

    gulp.src('dist/**')
        .pipe(version(COMMIT_SHA))
        .pipe(htmlReplace(replaceOptions))
        .pipe(azureUpload({container: container}));

});
```

If you fancy simplifying up these fuctions in forked gists or want to send any thoughts you have as gist comments or tweets, im allways up for learning & disscussing.
