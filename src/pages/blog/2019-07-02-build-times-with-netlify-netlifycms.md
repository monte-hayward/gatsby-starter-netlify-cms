---
templateKey: blog-post
title: Build Times with Netlify & NetlifyCMS
date: 2019-07-02T20:32:55.566Z
description: Describes time used by the Netlify Build system
featuredpost: true
featuredimage: /img/ram-dass-separateness.jpg
tags:
  - scaling
  - build
  - cms
---
This example site builds in about 2 minutes.
If you include an image and do not kill the image deploy, 4+ minutes.
Use of `editorial_workflow` could cut down on builds activated.
When there are > 5 builds concurrently running, Netlify kills the middle ones and keeps the first and last, docs report.

The next step clearly would be incremental builds, which are not without complications. They are described for React Static sites in [How to Scale Massive React Static sites with Incremental Builds](https://www.netlify.com/blog/2019/01/17/how-to-scale-massive-react-static-sites-with-incremental-builds/). 

What about Gatbsy incremental builds, though? `Searching...` 
In late May, an [alpha version](https://github.com/gatsbyjs/gatsby/issues/5002#issuecomment-496689016) had incremental builds. It appears the solution went live in [2.9.0](https://github.com/gatsbyjs/gatsby/pull/14359#issuecomment-500707616) June 11.

```shell
3:28:12 PM: Build ready to start
3:28:15 PM: build-image version: 9e0f207a27642d0115b1ca97cd5e8cebbe492f63
3:28:15 PM: build-image tag: v3.3.2
3:28:15 PM: buildbot version: ef8d0929ed0baabafd8bbb7d0b021e1fc24180c0
3:28:15 PM: Fetching cached dependencies
3:28:15 PM: Starting to download cache of 183.7MB
3:28:17 PM: Finished downloading cache in 1.428551105s
3:28:17 PM: Starting to extract cache
...
3:28:34 PM: Executing user command: npm run build
...
3:28:41 PM: info bootstrap finished - 4.805 s
3:28:41 PM: success run static queries — 0.238 s — 2/2 8.45 queries/second
3:29:40 PM: gatsby-plugin-purgecss: Only processing  /opt/build/repo/src/components/all.sass
3:29:48 PM: success Building production JavaScript and CSS bundles — 66.134 s
3:29:48 PM: success Rewriting compilation hashes — 0.001 s
3:29:49 PM: success run page queries — 0.772 s — 22/22 28.54 queries/second
3:29:51 PM: 
3:29:51 PM: gatsby-plugin-purgecss:
3:29:51 PM:  Previous CSS Size: 235.50 KB
3:29:51 PM:  New CSS Size: 24.94 KB (-89.41%)
3:29:51 PM:  Removed ~210.56 KB of CSS
3:29:51 PM: 
3:29:52 PM: success Building static HTML for pages — 0.902 s — 22/22 52.95 pages/second
3:29:52 PM: info Done building in 75.484 sec
3:29:52 PM: Function Dir: /opt/build/repo/lambda
3:29:52 PM: TempDir: /tmp/zisi-221263800
3:29:53 PM: Prepping functions with zip-it-and-ship-it 0.3.1
3:29:53 PM: [ { path: '/tmp/zisi-221263800/hello.zip', runtime: 'js' } ]
3:29:53 PM: Prepping functions complete
3:29:53 PM: Caching artifacts
3:29:53 PM: Started saving node modules
3:29:53 PM: Finished saving node modules
3:29:53 PM: Started saving yarn cache
3:29:53 PM: Finished saving yarn cache
3:29:53 PM: Started saving pip cache
3:29:54 PM: Finished saving pip cache
3:29:54 PM: Started saving emacs cask dependencies
3:29:54 PM: Finished saving emacs cask dependencies
3:29:54 PM: Started saving maven dependencies
3:29:54 PM: Finished saving maven dependencies
3:29:54 PM: Started saving boot dependencies
3:29:54 PM: Finished saving boot dependencies
3:29:54 PM: Started saving go dependencies
3:29:54 PM: Finished saving go dependencies
3:29:54 PM: Build script success
3:29:54 PM: Starting to deploy site from 'public'
3:29:54 PM: Creating deploy tree 
3:29:54 PM: 56 new files to upload
3:29:54 PM: 0 new functions to upload
3:29:58 PM: Starting post processing
3:30:02 PM: Post processing done
3:30:02 PM: Site is live
3:30:27 PM: Finished processing build request in 2m12.117979123s
```
## Uploading an Image Requires its own build

Image is a required field on blog posts. A Netlify build launches when the image is committed, which is before the page is committed.

### Image upload

```
3:37:24 PM: Build ready to start
...
3:39:38 PM: Finished processing build request in 2m9.883058191s
```

### blog post save

```shell
3:38:04 PM: Waiting to build. Currently running 1 concurrent builds on your account
...
3:41:14 PM: Finished processing build request in 2m0.668940422s
```

The page commit build reports number of files changed.

```
69 new files uploaded

26 generated pages and 43 assets changed.

New pages include:

index.html
404/index.html
about/index.html
blog/index.html
contact/index.html
products/index.html
404.html
blog/2016-12-17-making-sense-of-the-scaas-new-flavor-wheel/index.html
blog/2019-07-02-build-times-with-netlify-netlifycms/index.html
blog/2019-07-02-quick-add-blog/index.html

No redirect rules processed

This deploy did not include any redirect rules. Learn more about redirects.

info
49 header rules processed

All header rules deployed without errors.

info
All linked resources are secure

Congratulations! No insecure mixed content found in your files.
```
