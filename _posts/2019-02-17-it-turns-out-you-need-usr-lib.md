---
layout: post
title:  "It Turns Out You Need /usr/lib"
date:   2019-02-17 13:42:47 -0700
---

It was a Tuesday night at the office around 5:30 PM.
I had gotten in around 7:30 AM so I was far from operating at full capacity at this point.
The task at hand was to write an internal [Vue] quickstart guide so anyone in the company can get a quick overview of how we do front end apps and get them off the ground quickly.
I was working with the great [Vue CLI 3] which I'd had success with in the past but this time around I couldn't get the generated project to run properly.
`yarn serve` was failing because it couldn't find the `vue-cli-service` executable on the PATH.
I found several issues on the subject with various solutions ([1][vue-cli-issue-1], [2][vue-cli-issue-2]).
I tried the relevant solutions but couldn't get anything to stick.
The strangest thing is that I remember having this same issue months ago and had apparently fixed it one way or another.
In fact, I could run our other Vue apps created with a very similar template without any problems.

_What was different about these apps?_

I tried reinstalling dependencies, starting from scratch, etc. but to no avail.
Eventually I decided that it must be my node/npm/yarn install so I set out to nuke it from my system and install it from scratch.

I was a little disappointed that there didn't appear to be any equivalent to `npm uninstall -g everything`.
There were some scary looking bash commands that claimed to clean everything up but I didn't want anything to go astray so I opted to do it by hand instead.

Things were fine at first when I started running `sudo rm -rf /usr/local/lib/node` and `sudo rm -rf ~/.yarn`.
I then found `/usr/lib/npm/node_modules` and inspected its contents with `ls`.
I quickly modified the previous command by putting `sudo rm -rf` at the beginning and backspaced a little to far to leave `/usr/lib` at the end and hit Enter.

```
$ sudo rm -rf /usr/lib

```

Oops.

There was no prompt for sudo password because I had already been running commands under sudo.
As soon as I realized what I had done (about half a second), I mashed Ctrl-C a few times.
_Phew_.
It must okay, right?
I mean, how much damage could that have caused?

I ran `ls /usr/lib` and saw a few broken symlinks.
Well, maybe I can just reinstall that package and things'll be fine.

```
$ sudo apt-get update
sudo: unknown uid xxxxxxx: who are you?
```

Hmm, not a good sign.
Well, maybe I can copy the relevant files from a coworker and that'll be good enough.
Oh wait, I can't do that without root/sudo.

At this point I accepted that the machine was more or less a lost cause so I had to go into recovery mode and get it ready for imaging.
Fortunately, `/home` was on a different drive entirely so I only had to worry about system configuration.
I figured that `/etc/`, `/var/`, and `/opt/` would be a good start so I inserted a flash drive and tried to mount it but quickly realized I couldn't do that without root.
Well, let's just copy those to my home directory then.
Not so fast - you need root to be able to read most of those files.

This seemed like as good a time as any to call it a night and go home.

In the morning, I got the machine reimaged, discovered that my home directory was on a RAID1 array, reassembled said RAID array, mounted it over `/home/`, and I was off to the races!
I had the usual set backs one would expect and slowly installed the necessary packages to start working e.g. `git`, `tmux`, `vim`.

Okay, what was I doing before?
Right, trying to run a barebones Vue app.
I installed node and yarn from scratch and tried creating the app again.

```
$ yarn serve
/bin/sh: vue-cli-service: command not found
```

What?!

At this point I was baffled.
I started modifying the scripts in `package.json` to debug it.
It turns out that `yarn serve` adds some directories to `$PATH` so binaries in installed packages can be called by name e.g. `$(pwd)/node_modules/.bin`.
It just so happened that I was testing these apps in temporary directories that are made with a bash function:

```
function cd_temp {
   local name; name="${1:-default}"
   local date; date=$(date "+%Y-%m-%d.%H:%M:%S")
   local template; template="${date}_${name}_XXX"

   if [ "$(uname)" = "Darwin" ]; then
       cd "$(mktemp -d -t "$template")"
   else
       cd "$(mktemp --tmpdir --directory "$template")"
   fi
}
```

You might notice that the template for the directory has two `:` characters in it.
You might remember that `:` is the character used as the separator in `$PATH` so rather than adding the current directory to the path it ended up adding a bunch of gibberish to the path.
No wonder it couldn't find `vue-cli-service`!

Sure enough, I [changed][cd_temp_fix] the function to not use `:` in the template and everything worked.

Ultimately, this wasn't a huge set back with all things considered.
I was back up and running in a few hours and during that time I was still somewhat productive without a functional desktop by responding to emails/Slack/etc.
There are definitely some takeaways, though:

 - Tools should have an easy way to uninstall the packages that they maintain e.g. `yarn`/`npm`.
 - Be careful when running any command that starts with `sudo rm -rf /`.
 - Make sure that you backup important data in case you need to recover it or start from scratch.

[Vue]: https://vuejs.org/
[Vue CLI 3]: https://cli.vuejs.org/guide/
[vue-cli-issue-1]: https://github.com/vuejs/vue-cli/issues/2404
[vue-cli-issue-2]: https://github.com/vuejs/vue-cli/issues/1105
[cd_temp_fix]: https://github.com/marczych/dotfiles/commit/c8be0f3032e9b5a5e461b09e33f507f62ad8d4e6
