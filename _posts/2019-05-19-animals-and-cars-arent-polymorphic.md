---
layout: post
title:  "Animals and Cars Aren't Polymorphic"
date:   2019-05-19 17:05:52 -0700
---

I've grown tired of the common polymorphism example classes and think that they do polymorphism a disservice because they don't demonstrate the real power of virtual dispatch.
For example:

```python
class Animal():
    def sound(self):
        raise NotImplementedError()


class Dog(Animal):
    def sound(self):
        return 'woof'


class Cat(Animal):
    def sound(self):
        return 'meow'


class Fox(Animal):
    def sound(self):
        return 'ring-ding-ding-ding-dingeringeding'


for animal in [Dog(), Cat(), Fox()]:
    print(animal.sound())
```

I'll spare you the example implementation but also remember the classic `Car` base class with abstract `wheelCount()` and `doorCount()` methods for derived classes to implement.

A programmer might understand how these classes behave and reason through code using them but still not understand when polymorphism should be used.
In fact, this is a bad use of polymorphism.
A better implementation would merely have a single class with member variables to capture the relevant information along with factory functions to create common instances of them:

```python
class Animal():
    def __init__(self, sound):
        self.sound = sound

    def sound(self):
        return self.sound


def Dog():
    return Animal('woof')


def Cat():
    return Animal('meow')


def Fox():
    return Animal('ring-ding-ding-ding-dingeringeding')


for animal in [Dog(), Cat(), Fox()]:
    print(animal.sound())
```

An `enum` with singletons for the necessary instances would also be a good choice but you get the idea.

So what _is_ a good example of polymorphism?
Something that actually requires different code to run rather than only different data:

```python
class ChatChannel():
    def send_message(self, message):
        raise NotImplementedError()


import slack


class SlackChannel(ChatChannel):
    def __init__(self, channel):
        self.channel = channel

    def send_message(self, message):
        slack.send_message(self.channel, message)


import hipchat


class HipChatChannel(ChatChannel):
    def __init__(self, channel):
        if channel.startswith('@'):
            self.is_user = True
            self.channel = channel.lstrip('@')
        else:
            self.is_user = False
            self.channel = channel.lstrip('#')

    def send_message(self, message):
        if self.is_user:
            hipchat.send_user_message(self.channel, message)
        else:
            hipchat.send_channel_message(self.channel, message)


channels = [
    SlackChannel('#general'),
    SlackChannel('@alice'),
    HipChatChannel('#random'),
    HipChatChannel('@bob'),
]

for channel in channels:
    channel.send_message('Hello World!')
```

This example has a `ChatChannel` class which is implemented by `SlackChannel` and `HipChatChannel`.
`SlackChannel` uses the `slack` library to send a message while `HipChatChannel` uses the `hipchat` library and has some special handling for users and channels.
The different library dependencies and logic is something that you can't do with pure data like in the revised `Animal` example.
You _could_ do it by passing in a lambda, storing it as a member variable, and calling that to send the message.
However, that's just hand rolled virtual dispatch at which point you're better off using proper inheritance for it.

All of this is _not_ to say that the `Animal` example shouldn't be used at all!
It can be useful to demonstrate the concept in a very basic way but the conversation should quickly move to more motivational examples to help explain when polymorphism should and should not be used.
