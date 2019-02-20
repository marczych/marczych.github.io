---
layout: post
title:  "Strategically Tactical Programming"
date:   2019-02-19 19:29:47 -0700
---

I just finished reading Ben McCormick's excellent blog post on [Strategic Coding].
It makes a lot of great points about something that is awfully hard to get right in software development: when should you take shorcuts and when should you invest the time doing it right from the beginning?
I agree with all of what Ben (and John Ousterhout for that matter) said but I have a few things to add.

The holy grail is doing _both_ strategic and tactical programming.
The trick is to find the boundaries where you need to change your mindset from one to the other.
Things that are hard to change should be done strategically because changing them can have rippling effects on other components whose changes and deployment might need to be done in lockstep.

Some examples of things to do strategically:

 - **APIs**: Changing any public API ranges from hard to impossible because many of the clients could be entirely out of your control and even unaware to you. REST API endpoints, public methods in code, network protocols, environment variables, and command line arguments come to mind.
 - **Data formats**: Data formats are a kind of public API but with some extra caveats. When changing the data format you would ideally do it in a backwards compatible way. When making backwards incompatible changes you can must choose to maintain code to deal with the old format, bite the bullet and migrate all existing data into the new format, or decide to entirely drop support for old data. Database migrations can be particularly cumbersome. Even when you control the only client using the database, you'll often have to do a staged rollout to avoid downtime or data in an inconsistent state. Database schemas and file formats are the obvious examples.

The flip side of this is all of the things that we can afford to do tactically!
Fortunately, strong APIs provide _encapsulation_ which allow us to hide implementation details behind the facade of the public interface.
We can be less thoughtful when it comes to internal choices such as data structures, algorithms, code style, and even choice of programming language and framework.
We can leverage tools like [Docker] and [OpenAPI] to encapsulate the dirty details inside.

These ideas are powerful because you can get the best of both worlds.
Spend time on the things that are hard to change and spend much less time on the things that can easily be improved in the future.
This results in a significant time savings when you never end up making those further improvements down the line or, in extreme cases, scrap the entire thing.
Depending on the project, this is a likely outcome.
However, you still need to be careful not to over-architect the public API because even those choices can take a lot of time.

I've found myself using these principles to great effect during code reviews.
I'm much more lenient when it comes to things like local variable names, algorithms, HTML structure, and command line scripts and refrain from making nitpicky comments that result in more time wasted than the theoretical benefit they would provide.
Most frontend programming falls into this category.
Other than URL structure and cookies, frontend code in general just needs to be internally consistent which is great news because Typescript, refactoring tools, and unit tests make it easy to be confident when making these types of changes.

As always, I'm still working on honing my skills in this area to be more effective.
Thanks for the interesting read, Ben!

[Strategic Coding]: https://benmccormick.org/2019/02/18/strategic-coding
[OpenAPI]: https://swagger.io/docs/specification/about/
[Docker]: https://www.docker.com/
