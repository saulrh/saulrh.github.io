---
layout: page
title: Projects
permalink: /projects/
---

This is a short list of things I've built or contributed to that I'm
sufficiently proud of to want to show off. None of them are
groundbreaking, but each of them made me happy in some way.

# XBindJoy

[XBindJoy](https://github.com/saulrh/XBindJoy) is my take on a
macro-binding program for gamepads and joysticks. The twist is that
it's actually implemented as a tightly-focused API for reading input
devices and sending synthetic X events in [GNU
Guile](https://en.wikipedia.org/wiki/GNU_Guile), giving the user
dramatically more power than they have in other macro-binding tools.

I built XBindJoy because I wanted a better way to use my [Microsoft
Sidewinder Strategic
Commander](https://en.wikipedia.org/wiki/Microsoft_SideWinder#Strategic_Commander),
which is kind of like the illegitimate offspring of a throttle lever
and a gaming keypad. Its original drivers used the three thumb buttons
and the three-position slider as layering toggles, giving the device a
fantastic number of bindings. It was much less useful with
gamepad-keybinding programs of the time, which generally didn't handle
arbitrary layering. XBindJoy let me do basically whatever I wanted.

As a secondary goal, I used XBindJoy to teach myself a bit about C,
X11, the Linux joystick and event APIs, and embedded
interpreters.

# Tridactyl

[Tridactyl](https://github.com/tridactyl/tridactyl) is a Vim-like
interface for Firefox, inspired by Vimperator/Pentadactyl. I can't
claim credit for starting the project, or even doing much of the work,
but I am responsible for a couple notable code cleanups, features,
bugfixes, and bugs:

#### Vimperator-style hint filtering

[This feature](https://github.com/tridactyl/tridactyl/pull/258) allows
you to select a link by typing a fragment of its link text. No more
having to locate and precisely type out a hint's randomly-selected
identifier - you've already read and comprehended the link you want to
follow, just type it in!

#### Autocontainer Extension Coexistence

Several popular Firefox extensions use Firefox's Containers feature to
isolate particular sites, ensuring they're only ever opened in
specific containers by closing tabs that try to open links in the
wrong container and reopening them with the right one. Configuring two
or more extensions to contain the same site in different containers
can lead to them fighting over the site and opening infinite
tabs. Some extensions thankfully implement APIs that allow other
extensions to cooperate with them, and [this
feature](https://github.com/tridactyl/tridactyl/pull/953) teaches
Tridactyl to use these APIs to coordinate with several of the more
popular container-management extensions.

#### Excmds in Content Script

The WebExtension model provides several contexts for extension
code. Some code runs in a per-firefox-instance "background"
context. Some code runs in a per-tab "content" context. Some code runs
inside the page itself via injected script elements. Tridactyl
originally did nearly everything in the background process; keystrokes
would be caught by page code, messages would be sent to the background
context, the background context would make a decision, and a message
would be sent back to the focused tab telling the injected script what
to do. This caused some major problems, such as commands happening on
the wrong tab. [I
did](https://github.com/tridactyl/tridactyl/pull/962) some
[refactoring](https://github.com/tridactyl/tridactyl/pull/1489) to
move a bunch of state that should have been per-tab into the per-tab
scripts, dramatically improving stability and performance. Sadly, in
that refactor I also introduced a major security bug, so go me. :tada:



