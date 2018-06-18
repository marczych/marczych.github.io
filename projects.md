---
layout: default
title: Projects - Marc Zych
name: projects
---

A complete list of open source repositories that I've contributed to can be found on [GitHub].
Here are the most interesting ones:

# Matryoshka

[Matryoshka] is a configurable caching library for PHP that allows you to build custom caching behavior on the fly.
This is accomplished by wrapping existing backends with reusable components.
For example, given an existing backend you can easily change its functionality by wrapping it with another backend to prefix all keys, change expiration times, gather metrics, disable gets, etc.
More information can be found in the [introductory blog post][Matryoshka post] and the [README][Matryoshka README] on GitHub.
Developing this library was a great experience as it gave me the chance to practice test-driven development which resulted in 98% code coverage.

# iFixit Android App

The [iFixit Android App] is an [open source][iFixitAndroid repo] app that provides repair information for everything and has community features such as guide editing, favoriting, and commenting.
Users can also download repair guides to their device to view them while offline.
The app was started as a final class project with [Tim Asp] and iterated upon in a subsequent class.
Since then, we've added more features, improved its stability, and maintained it through several Android system updates.

# Ray Tracer

I wrote a [ray tracer] in my intro to graphics class which featured spheres, phong shading, depth of field, and reflections.
I then built upon it in my graduate graphics course and added refaction, procedural textures, and normal mapping.
It's written entirely in C++ and uses OpenMP to parallelize the work.
Check out the [README][ray tracer README] to see renders and runtime stats.

# Global Game Jam

[Global Game Jam] is an event where teams from all over the globe create games according to a theme from start to finish in 48 hours.
It is a lot of fun to take a weekend and work with different people on a very unique project.
I also got the chance to do nearly all of the music for these games which was a blast.
Here are the four games that I've developed at Global Game Jams over the last few years:

_[Planes on a Snake]_ is a game whose plot is a play on the movie Snakes on a Plane.
The player controls Jamuel L. Sackson by firing at enemy plans before they crash into the snake-covered earth.

In _[Heart Healer Extreme]_, the player controls an enthusiastic man tasked with keeping everybody in the city happy.
As the game progresses, new heart healing weapons become available which have various cooldowns, effectivenesses, and ranges.

[Peggle Damacy] is a mashup of [Peggle] and [Katamari Damacy].
The goal is to collect all of the pegs on the board but only the ones in the player's available spectrum can be collected.
Collecting pegs expands the available spectrum and increases the size of the fired ball.

[Business Team] came to life when [Business Time] and [SpaceTeam] came together.
This is a web based cooperative game that involves telling your teammates to complete certain tasks before the time runs out.
This was written using [Node.js] and [socket.io].
The playable game can be found at [businessteamgame.com].


[GitHub]: https://github.com/marczych
[Planes on a Snake]: http://archive.globalgamejam.org/2012/planes-snake
[Heart Healer Extreme]: http://2013.globalgamejam.org/2013/heart-healer-extreme
[Peggle Damacy]: http://globalgamejam.org/2014/games/peggle-damacy
[Business Team]: http://globalgamejam.org/2015/games/business-team
[businessteamgame.com]: http://businessteamgame.com
[LOVE]: https://love2d.org/
[Global Game Jam]: http://globalgamejam.org/
[Peggle]: http://www.popcap.com/peggle-1
[Katamari Damacy]: https://en.wikipedia.org/wiki/Katamari_Damacy
[Business Time]: https://www.youtube.com/watch?v=AqZcYPEszN8
[SpaceTeam]: http://www.sleepingbeastgames.com/spaceteam/
[socket.io]: http://socket.io/
[Node.js]: https://nodejs.org/
[Matryoshka]: https://github.com/iFixit/Matryoshka
[Matryoshka post]: http://itbrokeand.ifixit.com/2015/01/20/matryoshka-configurable-caching-library-for-php.html
[Matryoshka README]: https://github.com/iFixit/Matryoshka#readme
[iFixit Android App]: https://play.google.com/store/apps/details?id=com.dozuki.ifixit
[iFixitAndroid repo]: https://github.com/iFixit/iFixitAndroid
[Tim Asp]: https://github.com/timothyasp
[ray tracer]: https://github.com/marczych/RayTracer
[ray tracer README]: https://github.com/marczych/RayTracer#readme
