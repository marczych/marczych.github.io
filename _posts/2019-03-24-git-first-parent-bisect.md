---
layout: post
title:  "git-first-parent-bisect"
date:   2019-03-24 16:51:13 -0700
---

I just open sourced [`git-first-parent-bisect`][repo].
This is something that I've wanted for so long but didn't think was actually possible to do until I found this [StackOverflow answer][soa].
I clearly had a use for such a script otherwise I wouldn't have been searching for thatso I whipped up a hacky version of it and let it loose on the bug I was facing.
Sure enough, it took me straight to the offending branch and allowed me to root cause how the bug was introduced.

This script doesn't have many miles under its belt but it has worked well for me a few times so I hope it works for you too!

[repo]: https://github.com/marczych/git-first-parent-bisect
[soa]: https://stackoverflow.com/a/5650992/1135611.
