---
layout: post
title:  "jayWiki Gollum Fail"
date:   2014-12-17 16:00:00 -0700
categories: dev notes 
---

# Notes from a failed wiki
This post is similar to the 2016_06_21 entry, Things I Did to Install Jekyll, except this post ends in failure.  And thankfully so, else I'd have been stuck with a [gollum wiki](1) these past 18months.  Heh. Maybe it wouldn't have been so bad.  As it happened, I kept my posts in nvAlt instead and waited for the sting and consequences to fade away.  As you'll see, the gollum install went south and as a final hail-marry I updated to Yosemite.  Nothing else happened after that, nothing here anyway.  Yosemite went right on ahead and jacked up my apache config and then proceeded to render useless the SimpleOpenNI Kinect libraries I used in the Processing programming language.  Of course, I didn't realize the extent to which SimpleOpenNI was broken until the night of that gig, Portal, held the Chabot Space and Science Center in March of 2015.  I was to build the Portal Controller, an interactive exploration of computational feedback blah blah blah.  One would think that I'd have tested the Kinect PRIOR to the event. Well, does earlier-in-the-day count as PRIOR-to-the-event?  Shoot, I thought the Kinect component of the project was in the bag, as I'd used the Kinect reliably in 4 previous gigs leading up to the Portal project. Unfortunately, those previous gigs all happened PRIOR to my failed gollum-wiki setup and the reluctant hail-marry install of Yosemite.

BTW, this post was actually published to my log.jaylab Jekyll blog in june of 2016, but in honor of failed attempts everywhere, I've used the attempted publish date instead.

And one last thing before the end begins, a quote from Marijin Haverbeke's Eloquent Javascript (that I just started reading today):

>
What hostility to the richness of programming--to try to reduce it to something straightforwar and predictable adn to place a taboo on all the weird and beautiful programs! The landscape of programming techniques is enormous, fascinating in it diversity, and still largely unexplored.  It is certainly littered with traps and snares, luring the inexpereienced programmer into allkinds of horrrible mistakes, but that only means you should proceed with caustion and keep your wits about you.  As you learn, there will alwasys be new challenges and new territory to explore.  Programmers who refuse to keep exporing will surely stagnate, forget their joy, and lost the will to program (and become managers).

 
## jaywiki
> initial page
______________________________

### overview
This wiki contains jaynotes for jaylabs and jaypops

_______
### Projects
- jayPop blog desribing kids software
- immersive computing (aka virtual reality eg. oculus vr)

### History
- 2014-12-17 
    - created jaywiki in dropbox/sites.
    - install gollum attempt failed.  requires brew install icu4c
    - installing [[homebrew]]
        - run brew doctor before installing anything
    - uninstall homebrew
    - [ ] need gollum-site a static site gneraotor for gollum
        - generates statics site from a gollum wiki
    - running into some issue with icu4c dependency.  Installed with MacPorts but nothing but trouble.  The following came close to working
    ```sudo gem install gollum -- --with-icu-dir=/opt/local/lib --with-icu-include=/opt/local/include```
        - supposedly homebrew handles this library.  but then MacPorts?  I guess I'll have to run homebrew on the chaote machine from now on.  rumor has it that crossing the macports homebrew streams would be bad.
    - reinstalled homebrew
    - this is serious pit
    - unistalled nokgiri
    - worked around charlock_holmes by setting --with-icu-dir=path
    - possibly some of the developer tools are missing, soooo
    ```xcode-select --install```
    - but guess what, looks like mac store no longer offers dev tools for those of us still on Mavericks.  Yup 10.10 forced upon me.  not that I mind; both minitron and newtron are running 10.10.  but chaote the work computer.  I was hestitant due to rumored macports issues and considering I was trying to run mediaWiki locally from apache....decided to stick with 10.9.  but alas....the times they are a changing.
        + the answer is likelikely in here somewhere
        + http://www.nokogiri.org/tutorials/installing_nokogiri.html
        + but I have not the time currently....
        + just gonna update to yosemite. dang it all to hell.

[1](https://github.com/gollum/gollum)