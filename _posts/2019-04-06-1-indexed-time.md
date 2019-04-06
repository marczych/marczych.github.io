---
layout: post
title:  "1-indexed time?"
date:   2019-04-06 12:51:28 -0700
---

The clock in my car has an interesting quirk: it often resets to 1:00 shortly after starting the engine.
Electrical issues aside, it made me think about how we represent time in terms of hours in a day.
In particular, I've always been perplexed by 11PM to 12AM being the boundary of the day.
Not only does the number increase but there is also a transition from post meridiem to ante meridiem.
This, of course, results in confusion when declaring deadlines and specifying times on exactly 12AM and often 11:59PM is used instead to clarify.

Oddly enough, this weird system lines up nicely with 24-hour time (military time).
Other than 00:00 and 12AM, the times match if you subtract 12 hours from the PM times.
This is awfully convenient for programmers when looking at log files because the conversion is very straightforward.
Although, there is often a time zone offset to account for which gums up the works.

So in some sense, our hours are 0-indexed because 01:00 is the _second_ hour rather than the first.
And now returning to the clock in my car, they most likely decided to 1-index it to make the spec as simple as "count from 1 to 12 and loop around."

Anyway, [time is hard][holman] and I should probably buy a new car.

[24-hour clock]: https://en.wikipedia.org/wiki/24-hour_clock
[holman]: https://zachholman.com/talk/utc-is-enough-for-everyone-right
