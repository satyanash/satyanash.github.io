---
layout: post
title: "Designing a UI for the Elderly"
date: 2012-12-05T01:54:00+05:30
tags: software
---

My grandfather is an 83 year old fellow.
He has no computer experience whatsoever, but wanted to learn computers for day to day tasks such as Email and Facebook.
I decided that I wanted to keep the interface simple and hassle free.
Fvwm seemed to be the best option to design a UI that would be easy to learn and use and without any clutter.
All of the UI contains operations that can be carried out with a single mouse button to reduce complexity.

### Set Environment

Only the place where icons are stored is required.

```
#####
## Set Environment variables
############
SetEnv fvwm_icon /home/other/Pictures/FvwmIcons/
```

### Virtual Desktops

Use only a single desktop. We do not need more than one.

```
#####
## Virtual Desktops
############
DesktopSize 1x1
DesktopName 0 Spaces
EdgeScroll 0 0 
EdgeResistance 450  450
EdgeThickness 1
```

### Window Focus Policy

Use the popular default ClickToFocus mouse focus policy. ClickToFocus allows for the buttons to work on the currently active window.
I do not use SloppyFocus as it prevents the central control buttons from working. This is because other windows may get activated as you glide your mouse over them in order to reach the ButtonBar.

```
#####
## Mouse and Focus Behavior
############
ClickTime 350
MoveThreshold 3
Style * ClickToFocus, MouseFocusClickRaises
```

### Other Settings

Make sure maximized windows are padded by 100px on the right. Define the startup function.

```
##Ignore Num Lock Modifier
IgnoreModifiers L25
##Maximize Threshold
EwmhBaseStruts 0 100 0 0

#####
## Startup Functions
############
DestroyFunc StartFunction
AddToFunc   StartFunction
+ I Module FvwmButtons BarButtons
+ I Exec exec xsetroot -mod 2 2 -bg \#000000
```

### Colorsets

Define a high contrast colorset. In this case, Black and White.

```
Colorset 0 fg White, bg Black
Colorset 1 fg Black, bg White
```

### Mouse Behaviour

Disable clicks on the desktop.
Make sure clicking on icons automatically de-iconifies windows.
Also have a backdoor to start the Fvwm default menu, so that we can start xterm and other goodies.

```
#####
## Basic Bindings
############
Key F1 A M Menu MenuFvwmRoot
Mouse 1 R A Menu NoneFunction
Mouse 3 R A Menu NoneFunction
Mouse 1 I A Iconify off
```

### Buttons

I started out with designing buttons.
These would act as startup places for application that would be used.
I made them as big as possible with large text and a high contrast.
It consisted of only the swallowed Xclock, Firefox, Thunderbird and some window controls.

### Session Control

I also kept Session Control options like logging out and shutting down the computer on the buttons itself.
This streamlines the concept of a central bar.

### Buttons

Specifically:

* ‘STOP’ button closes Fvwm, and drops back to the login manager.
* ‘CLOSE’ button closes the active window.
* ‘BIG’ will maximize the current window.
* ‘MINIMIZE’ will Iconify the current window, giving a way to have multiple things open.
* ‘TYPING’ will open the Text Editor gedit.
* ‘FACEBOOK’ opens Facebook in Chromium in the app mode, i.e. without tabs.
* ‘EMAIL’ opens Gmail in Chromium in the app mode, i.e. without tabs.
* ‘INTERNET’ opens Firefox with Google as the homepage.
* The last button is a swallowed Xclock.

The Geometry height must be changed according to your monitor.

```
#####
## BarButtons
#############
Style "BarButtons" !Title, !Handles, !Borders, Sticky, WindowListSkip, CirculateSkip, FixedPosition,  FixedSize, !Iconifiable, NeverFocus

DestroyModuleConfig BarButtons: *
*BarButtons: Fore White
*BarButtons: Back Black
*BarButtons: Frame 1
*BarButtons: ActiveColorset 1
*BarButtons: Font "xft:sans-serif:Bold:pixelsize=15;-*-helvetica-bold-r-*-*-10-*-*-*-*-*-*-*"
*BarButtons: Geometry 100x900-0-0
*BarButtons: Rows 9
*BarButtons: (1x1,Title "STOP", Icon $[fvwm_icon]/poweroff_64x64.png, Action(Mouse 1) 'Quit')
*BarButtons: (1x1,Title "CLOSE", Icon $[fvwm_icon]/close_64x64.png, Action(Mouse 1) 'Current Delete')
*BarButtons: (1x1,Title "BIG", Icon $[fvwm_icon]/maximize_3.png, Action(Mouse 1) 'Current Maximize')
*BarButtons: (1x1,Title "ICON", Icon $[fvwm_icon]/maximize_3.png, Action(Mouse 1) 'Current Iconify toggle')
*BarButtons: (1x1,Title "TYPING", Icon $[fvwm_icon]/textedit_64x64.png, Action(Mouse 1) 'Exec exec gedit')
*BarButtons: (1x1,Title "FACEBOOK", Icon $[fvwm_icon]/facebook.png, Action(Mouse 1) 'Exec exec chromium-browser --app=http://www.facebook.com')
*BarButtons: (1x1,Title "EMAIL" ,Icon $[fvwm_icon]/email_64x64.png, Action(Mouse 1) 'Exec exec chromium-browser --app=http://www.gmail.com')
*BarButtons: (1x1,Title "INTERNET" ,Icon $[fvwm_icon]/firefox_64x64.png, Action(Mouse 1) 'Exec exec firefox')
*BarButtons: (1x1, Swallow "xclock" "Exec exec xclock -hands white -highlight white -foreground white -background black -padding 4 -norender")
```

### Window Decoration

I wanted to keep the window decoration as simple as possible.
I decided to go without any title bars and made sure that all the applications automatically occupied the complete desktop.
To close and minimize the windows, I used buttons that were placed in the Buttons bar itself.
These buttons perform the operations on the active window itself and do not need any kind of selection.
Effectively you cannot move or resize windows at all.
You may only use the buttons provided in the bar to the right which affect only the active window.

### No border, no Handles, no title bar

```
Style * !Borders, NoHandles, NoTitle
DestroyModuleConfig Chromium-browser: *
```

To make the computer automatically log in to Fvwm, you can configure the “Automatic Login” option in GDM. If you do not use gdm, you might want to start xinit with Fvwm as the window manager command, automatically on startup. This can be put into a script, so that as soon as Fvwm is Stopped, xinit ends and the next command is triggered, which can be the shutdown command.

