---
layout: post
title: "My Scoutmob Setup"
date: 2011-08-24 23:42
comments: true
categories: 
---

When I got my Scoutmob laptop (a quad-core 15' MBP) a couple of months ago, I wrote down everything I needed for making it ready for development.  Here's my minimum viable development setup.

**Chrome (Dev Channel).** At one point I was dabbling with writing Chrome Extensions, but there's not really a good reason to continue using the dev channel - 'cept that it's been pretty stable for me.

**iTerm2.** I was a tmux user, and screen before that.  Based on a recommendation from [Amro](http://amro.co), I've been using [iTerm2](http://iterm2.com) for a few weeks now. Not totally sold on it, but it's a narrow win over tmux because of its ease of set up. I recommend downloading the [Solarized theme](http://ethanschoonover.com/solarized) for it.

**Divvy.** Great app for organizing windows.  Use it all the time.

**Dropbox.** Easy filesharing. More importantly, I need it for my next app, which is...

**1Password.** I use this a lot already, but I need to use this more. You're only as safe as your weakest password.

**Homebrew.** Best package manager for OSX.  No reason to use anything else.

**XCode 4.** Requirement for Homebrew, but starting some serious iOS development as well.

**TextMate.** I vi occasionally, but TextMate is my editor of choice, especially for Ruby/Rails development.  I recommend the Solarized theme for it as well.

**Twitter.** I don't tweet enough to need anything more.

**Notational Velocity.** Synchronized to Simplenote, I've built up enough notes over time to where this is tool is now an essential part of how I work. I've tried Evernote, but it wants to be more than I really need.

**iStat Menu.** I tried to go without installing this initially - until my machine started getting sluggish. Essential for finding misbehaving processes.

**JumpCut.** Clipboard history.  Nice not having to worry about overwriting your current clipboard contents.

**Git (via Homebrew).** I would use this even if I didn't need to push to a remote repository. It's the safety net for software developers.

**RVM.** Nice that it makes upgrading Ruby a breeze, but Gemsets is the killer feature.

**MySQL (via Homebrew).** It's what we use at Scoutmob.

**POW.** Always available Rails apps. Install the powder gem to make managing applications a snap.

**Ack (via Homebrew).** Super fast searches on the command line. Also, I recommend install the [Ackmate](https://github.com/protocool/ackmate) plugin for TextMate.

My [dotfiles](http://github.com/cyu/dotfiles) and [dotvim](http://github.com/cyu/dotvim) Projects. Gets my terminal environment how I like it quickly.

In addition, there are two settings I do every time I setup a new machine:

* _Turn off Dashboard._ Never use it. and it hijacks a very useful function key. Speaking of function keys...
* _Use F1, F2, ... Keys._ Instead of the feature keys. Developers pretty much live in those function keys.

