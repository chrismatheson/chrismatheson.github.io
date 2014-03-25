---
layout: post
title: Gulp to Azure
categories:
- Personal
tags: [javascript, azure, gulp]
published: true
---

```javascript
function azureUpload(opts) {

    var blobService = azure.createBlobService(),
        containerName = opts.container;

    console.log('setting container: ' + containerName);
    blobService.createContainerIfNotExists(containerName, {publicAccessLevel : 'blob'}, function(error){
    });

    //create a writeable stream
    var az = require('stream').Writable({objectMode: true});

    az._write = function (chunk, enc, next) {

        var filename = chunk.relative;

        //Need better way of estalblishing if this is a file or dir
        if(filename === '') {
            next();
        } else {
            console.log('Uploading: ' + filename);
            chunk.pipe(blobService.createBlob(containerName, filename, azure.Constants.BlobConstants.BlobTypes.BLOCK));
            next();
        }
    };

    return az;
}

gulp.task('deploy', ['timestamp'], function(){
    'use strict';

    var container = 'dealer-' + (process.env.TRAVIS_BRANCH || 'local');

    gulp.src('dist/**')
        .pipe(azureUpload({container: container}));

});

```
