---
layout: post
title:  "Actually Writing Code"
date:   2018-08-23 21:37:09 -0700
---

I just read an article that chronicled the development of a small programming project by a relatively inexperienced developer.
It's not very important which one but a few times it said something along the lines of "I've only spent 5% of my time actually writing code."
I've heard that phrase a lot over the years.
Hell, I've said it myself from time to time.
It should probably be included in [Shit Programmers Say].

Programmers like to write code and view anything other than writing code as unproductive time.
"I only _actually write code_ 20 hours a week."
"That project took 10 hours but I only spent a few hours _actually writing code_."

It's understandable because that's what we're trained to do and shipping code is generally the "useful output" that is valuable to the company and customers.

However, technical challenges surrounding programming tasks are often necessary evils.
The article that prompted this one in particular described the battle between JavaScript libraries and clashing CSS.
Sure - spending a few hours getting that sorted out is unfortunate but it likely far outweighs the cost of implementation without leveraging those libraries.
Docker giving you problems?
You have to learn its idiosyncrasies and play along if you want the isolation and reproducibility that it offers.
What about wanting hermetic builds from Bazel but struggling to shoehorn your project into its prescriptive worldview?
It's up to you to decide if the benefits outweigh the downsides.

As for a professional software engineer, there are plenty of important things to do that are _not_ actually writing code: documentation, code review, design docs, project planning/scheduling, and performance reviews to name a few.
With any luck, these tasks will be an efficient and worthwhile use of time.

[No Silver Bullet] discusses how there won't be single breakthrough in computing that results in an order of magnitude increase in productivity, performance, efficiency, etc.
Libraries, languages, frameworks, and the like yield modest yet significant results in some of those categories.
However, they sometimes result in *less* time actually writing code because more of the work has been shifted into installing, configuring, and generally understanding how to use these tools.
And that's okay.
The end goal isn't to write more code - the code is merely a means to an end.
Shipping a product and solving a customer's problem is the end goal.
I haven't been in the game very long but it appears that over time programming has moved to more of a plumbing job in that you need to find compatible parts and put them together in a particular way to solve the problem at hand.
Even visual programming removes the need to actually write any code because it's just clicking and dragging boxes and lines around yet you can still solve some real problems.

I don't mean to imply that struggling with tools is a necessary evil and we shouldn't try to fix it - quite the opposite in fact.
Better tools, development environments, and libraries are accelerating the rate of development like never before and result in better products so we should continue to make them better.
Productivity should be measured more on how much of a problem is solved in a given amount of time _not_ how much of it is spent actually writing code or how many lines of code were written.
It's often much much easier to solve a problem by coming up with a better and more pragmatic solution rather than immediately jumping into the code when the first solution presents itself.

So stop being so concerned about not actually writing code - it's sometimes a better use of your time.

[Shit Programmers Say]: https://hackernoon.com/shit-programmers-say-translated-946849c2fbd4
[No Silver Bullet]: http://www.cs.nott.ac.uk/~pszcah/G51ISS/Documents/NoSilverBullet.html
