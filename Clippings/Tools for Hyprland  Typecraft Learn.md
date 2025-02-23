---
title: "Tools for Hyprland | Typecraft Learn"
source: "https://typecraft.dev/hyprland-for-newbs/tools-for-hyprland"
author:
published:
created: 2025-02-23
description: "In this episode of Hyprland for Newbs, we take your setup from basic to next-level, guiding you through essential tweaks that enhance both functionality and usability. These simple yet powerful changes will significantly improve your daily workflow."
tags:
  - "clippings"
---
This page is a tutorial for enhancing a Hyprland setup, focusing on essential tools and configurations to improve functionality and usability. It covers configuring Hyprland with tools like Hyprshot for screenshots, Swaync for notifications, Hyprlock for screen locking, and Hypridle for power management. The tutorial includes installation instructions using Arch Linux's `yay` package manager and provides configuration snippets for each tool. The page emphasizes customization and personalizing the Hyprland environment, with a promise of future content on aesthetic enhancements.

<iframe src="https://player.vimeo.com/video/1019015363?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write" title="Hyprland for Newbs - Episode 2"></iframe>

## Hyprland is great, but...

Hyprland is a great piece of technology, but a base install of hyprland lacks a lot of essential tooling for day-to-day workflows.

But you see, that is kind of the point of Linux, and Hyprland in general. This is not the walled garden of Apple. This is not a Neovim configuration that is fully-baked like NvChad. The point is to give you a tiling WM and you can figure it *however* you want.

**That's Hyprland.**

Just like [Neovim for Newbs](https://typecraft.dev/neovim-for-newbs/), I'm *not* going to give you something to copy and paste. We're going to show you the *how* of configuration so you can make Hyprland sing ***your*** tune.

So buckle up, I'm going to show you the programs that I think are **essential** in any Hyprland installation. And spoiler alert, I use all of these myself.

### BUT FIRST

Before we go installing some of the extras, let's update the Hyprland config. These updates make it feel a *lot* better to me. So let's dig in and modify the config.

You can easily go to the config by opening kitty with `$mainMod + R` and searching for `kitty`. After opening kitty, we can use neovim to open our config.

Edit that config

### Changing our file manager.

Let's do a little house cleaning, shall we? The first thing I want to do is change my `$fileManager` to something that is actually installed on my system. You see, I started with gnome as a base, and I have `nautilus` installed as my file manager. So let's change that.

Make our terminal open with `$mainmod + return`

By default, our terminal shortcut is a little... how should I say, non-ergonomic? So let's change that. We can improve it with a simple configuration change.

`bind = $mainMod, return, exec, $terminal`

### Change our launcher to something more ergonomic

I like the mac OS days of using `$mainMod + space` to open my launcher. So let's update that as well.

`bind = $mainMod, space, exec, $menu`

### Last but not least, vim keys for navigation

We can't be vim nerds and use our arrows to navigate between active windows in this setup.

ahhhh, that's better

## Let's make this config Shine

We need some programs that Hyprland doesn't come installed with. These tools will allow us to make this config a daily driver. Let's start with something that might sound weird at first, but we'll build on it. Let's start with a screenshot tool.

### [hyprshot](https://github.com/Gustash/hyprshot)

`hyprshot` is an amazing screenshot tool that provides us with a lot of functionality at little cost. Under the hood, hyprshot uses `grim` to take images and `slurp` for selecting the thing to take a screenshot of.

**Together, this makes for a great tool.**

First, we'll need to install it. If you remember, I use Arch (btw), so I'll use `yay` to add it.

Next, we can test hyprshot with a simple command.

When you run this command, you'll see the mouse has a newfound ability to select a window. And when this window is selected, you'll have a screenshot saved! This is fantastic. Before we move on, we'll add a keybinding to our config.

Keybinding for Hyprshot

💡

**The second line will allow us to select a region by dragging our mouse!**

This is great and all, but you know what? I don’t see any notification that a screenshot was taken. Which brings me to my next program on the list.

### [swaync](https://github.com/ErikReider/SwayNotificationCenter)

`swaync` is a notification daemon for wayland. The way swaync works with hyprland is amazing. It also looks pretty great out of the box.

To use swaync, we'll need a companion program. You see, swaynv is really just a daemon that waits for notification events, and displays these notifications in wayland systems. We need the program that actually sends the notifications.

Thankfully, `libnotify` is pretty ubiquitous on all linux systems. In fact, `libnotify` should be installed on your system already. If it isn't, check your base system's notification program.

#### Installation of Swaync

Once installed, we can run swaync in our terminal by just typing `swaync`. Next, open up another terminal, and test that swaync is running correctly. We can send a notification to swaync using libnotify by running the `notify-send` command, like so:

Test your notifications!

![](https://cms.typecraft.dev/content/images/2024/10/2024-10-13-235245_hyprshot.png)

there it is, notifications!

Next, we are going to want to make sure our notification daemon is running whenever we load hyprland. To do so, we'll add this to our config.

Adding swaync on startup

### [hyprlock](https://github.com/hyprwm/hyprlock)

`hyprlock` is part of the hypr ecosystem. This is a group of tools that work very well with hyprland and add a lot of functionality on top of the base install. For example, it adds the ability to have a `lockscreen`. Like everything else here, it's highly configurable. First, let's check out the basic usage.

#### Installation of Hyprlock

You can install hyprlock just like all other packages in this tutorial.

Installation

For hyprlock to run, you'll need a configuration. Create it easily with a touch command.

Just like with `hyprland`, you need to configure it to make it really useful. The good news is, there is a solid base configuration that enables `hyprlock` to show a basic login form. Once it's locked, you'll see it. You should definitely read the docs for `hyprlock` but in the meanwhile, here is a basic config for showing the login screen.

The above ☝️code will show a basic input form when your screen is locked. Try it out by running `hyprlock`. It is cool, albeit barebones.

We'll add a keybinding to our config now so it's easy to lock our machine whenever we go outside to touch grass.

### hypridle

Another basic thing that any system really needs is some power-saving and auto-sleep features. Another tool in the `hypr` ecosystem is `hypridle`. It gives us all that we need VERY easily.

### Install Hypridle

Installation

Hypridle has a very interesting and powerful convention for its configuration. Just like with `hyprlock`, we'll create our config first.

`hypridle` relies on "listener" blocks to control how and when it runs certain things. You can test this out with a basic configuration

Basic config

To test it, just run `hypridle` in your terminal.

☝️will send a notification (to `swaync` I hope) in 5 seconds that you are about to time out! When you move your mouse, it will tell you that you've resumed. Now you have tested that hypridle is working! Here is a better example of a config you can use moving forward:

You know what's coming next. It's adding a line to the configuration of `hyprland` so this launches on load.

### Conclusion

We’ve covered a ton of ground in this episode of Hyprland for Newbs, and our configuration is now well on its way to being more ergonomic, more functional, and ready for day-to-day use. But we’re just getting started. Hyprland’s minimalism allows for some incredible customization, and we’ve only scratched the surface with tools like Hyprshot, Swaync, and Hyprlock.

What’s next? We’ll be diving into the aesthetics that transform Hyprland from a simple tiling window manager into an environment that not only works the way you want but looks incredible while doing it. We’re talking sleek bar setups, dynamic wallpapers, and personalized themes that make your desktop sing. Your Hyprland install is about to look as good as it feels.

So, stay tuned. If you thought this episode added essential functionality, Episode 3 is going to blow your mind. You won’t want to miss it—Hyprland is about to become your dream setup.