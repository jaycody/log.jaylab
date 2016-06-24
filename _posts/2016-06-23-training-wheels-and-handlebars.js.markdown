---
layout: post
title:  "Training Wheels and Handlebars.js"
date:   2016-06-23 16:00:00 -0700
categories: dev notes 
---

### what are handlebars?

### why do I need handlebars?


### notes and exercises from various tutorials: 

#### from [Derek Banas handlebar.js tutorial on youtube](https://www.youtube.com/watch?v=4HuAnM6b2d8):

##### [01_hello_blank_generation](http://dev.jaylab.io/handlebars/01_hello_blank_generation)
- use the 'each' helper block to auto-generate html lists from an array
- use divs to separate the templates from the javascript

##### [02_hello_hunter](http://dev.jaylab.io/handlebars/02_hello_hunter)
- use **triple-stash** to render rather than escape html tags
- use the **registerHelper** method to create custom helper functions 
- create custom helper with **SafeString** to render html tags w/o triple-stash
- create custom helper with **escapeExpression** to escape a passed string, making it safe to use in the content area. 
  - Use this EVERY TIME you create a custom helper function.
- DEFINE all helpers BEFORE calling the template with all the data
- Pass in attributes to a helper function
- Generate any type of html elements with different types of stylings on the fly with helper function
- pass 'global' options that are available to all helper functions

##### [03_vandals](http://dev.jaylab.io/handlebars/03_vandals)
- **block helpers**
- script id="template-foo" type="text/x-handlebars-template"
- steps:
  1. create the helper function 