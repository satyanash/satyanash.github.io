---
layout: post
title: "Fvwm Explained"
date: 2012-12-05T02:11:00+05:30
tags: software
---
The earlier post about my Fvwm Desktop was a fairly short one.
In this second part I try to explain some parts of that configuration file.
I have also made some changes to my desktop to make it more usable.

Most of the following code segments can be written in any order and will work without any errors.
As mentioned earlier, the [online manual pages](https://web.archive.org/web/20130119073110/http://www.fvwm.org/documentation/manpages/stable/) are a wealth of information and should be referred to whenever possible.
You can also use [this beginner’s guide](https://web.archive.org/web/20121226191849/http://www.zensites.net:80/fvwm/guide/index.html) for reference.
And if all else fails, the `#fvwm` channel on irc.freenode.net can be helpful.

A lot or most of my configuration and the explanation text below is based on or has been directly sourced from the beginner’s guide mentioned above.
I am by no means an expert on the usage of this Window Manager.
I just wanted to explain the general configurations, in an easy to understand way for myself and others.

### Setting Variables

Variables in the file can be used to set values which may change.
The following code segment sets some default directories which may be accessed later on.
Essentially, variables here are used to store a string to avoid repetition.
You can also use variables to indicate default programs.

```
#####
## Set Environment variables
############
SetEnv fvwm_img $[FVWM_USERDIR]/images
SetEnv fvwm_icon $[FVWM_USERDIR]/icons
SetEnv fvwm_script $[FVWM_USERDIR]/scripts
SetEnv fvwm_wallpapers $[FVWM_USERDIR]/wallpaper

## Default programs
SetEnv fvwm_webbrowser /usr/bin/firefox
SetEnv fvwm_term /usr/bin/xterm
SetEnv fvwm_mail /usr/bin/thunderbird
SetEnv fvwm_media_player /usr/bin/banshee
SetEnv fvwm_video_player /usr/bin/vlc
```

Here, `$FVWM_USERDIR` is the location where your configuration files are stored. You can find out its value from the shell using:

```
echo $FVWM_USERDIR
```

All the other variables set above are also accessible from the shell in the same way, once Fvwm has loaded the configuration file.

### Mouse Focus and Window Margins

Use these values to set your mouse focus scheme.
I prefer to use the `SloppyFocus` and `MouseFocusClickRaises` scheme.
The margins decide the portion of the screen that will be left empty when a window maximizes and are set using the `EwmhBaseStruts` command.
We also ignore the Num-Lock key as a modifier.

```
#####
## Mouse and Focus Behavior
############
ClickTime 350
MoveThreshold 3
Style * SloppyFocus, MouseFocusClickRaises

##Ignore Num Lock Modifier
IgnoreModifiers L25
##Maximize Threshold
EwmhBaseStruts 0 55 0 0
```

### Functions

Functions in Fvwm are functions in like any other languages.
You can call them to perform a set of actions again and again.
However, every line/command within an Fvwm function has an event associated with it.
That line will execute only when that event occurs.
So a specific object can be interacted with in the following ways:

* `+ I` – Immediately
* `+ C` – Single Click
* `+ D` – Double Click
* `+ H` – Hover
* `+ M` – Motion AKA Click and Drag

The following is the general syntax of a function:

```
#####
## Sample Function, Will not work
#############
DestroyFunc FuncName
AddToFunc   FuncName
+ I (Action to happen immediately)
+ C (Action to happen on a mouse 'click)
+ D (Action to happen on a mouse 'double click')
+ H (Action to happen on a mouse 'hover')
+ M (Action to happen on a mouse 'motion')
```

Your function can assign one or more commands to these events; which will get called whenever that object is interacted with using that specific type of event.

The start-up functions are functions with predefined names, which are automatically called during the start, restart events of the Fvwm Window Manager.
These are mainly used to start the Fvwm modules that you will be defining later in your configuration.
You can also play sounds, start the xscreensaver daemon, set the wallpaper, start conky and other things.
The `+ I` is used for immediate execution.

```
#####
## Startup Functions
############
DestroyFunc StartFunction
AddToFunc   StartFunction
#+ I Module FvwmTaskBar
+ I Module FvwmPager FvwmMiniPager
#+ I Module FvwmPager FvwmMegaPager
+ I Next (FvwmMiniPager, CirculateHit) Iconify
+ I Next (FvwmMegaPager, CirculateHit) Iconify
+ I Module FvwmButtons BarButtons
+ I Module FvwmButtons PagerButton
#+ I Module FvwmButtons FvwmTrayer

DestroyFunc InitFunction
AddToFunc   InitFunction
+ I Exec exec xscreensaver
+ I Exec exec aplay /home/me/sounds/curve.wav
+ I Exec exec nitrogen --restore
+ I Exec exec guake
+ I Exec exec synapse --startup
+ I Exec exec conky

DestroyFunc RestartFunction
AddToFunc   RestartFunction
+ I Exec exec aplay /home/me/sounds/apert.wav
```

These are some of my user defined functions and can be called from other locations in the configuration file:

```
######
## Basic Functions
############
DestroyFunc FvwmDeleteOrDestroy
AddToFunc   FvwmDeleteOrDestroy
## This function will delete/destroy your window.
## Equivalent to pressing the X button on other popular GUIs.
+ H Nop
+ M Nop
+ C Delete
+ D Delete
+ C Exec exec aplay /home/me/sound/lboom.wav
+ D Exec exec aplay /home/me/sound/lboom.wav

DestroyFunc FvwmIconifyOrShade
AddToFunc   FvwmIconifyOrShade
## Will Iconfify (Minimize) Or Shade (RollUp)
## Depending on the type of click
+ C Iconify
+ D WindowShade

DestroyFunc FvwmMaximize
AddToFunc   FvwmMaximize
## Will maxinmize the window
+ H Nop
+ M Nop
+ C Maximize $0 $1

DestroyFunc FvwmMoveOrIconify
AddToFunc   FvwmMoveOrIconify
## Will move or Iconify(Minimize)
## Depending on type of click
+ M Move
+ D Iconify

DestroyFunc FvwmWindowShade
AddToFunc   FvwmWindowShade
+ C WindowShade $0
#+ D WindowShade $0

#Syntax of GotoPage
#GotoPage prev | [options] x[p] y[p]
#Possible options are wrapx and wrapy
#to wrap around the x or y coordinate 
#when the viewport is moved beyond
#the border of the desktop.

DestroyFunc FvwmScrollNextPage
AddToFunc FvwmScrollNextPage
+ C GotoPage wrapx wrapy +1p +1p

DestroyFunc FvwmScrollPrevPage
AddToFunc FvwmScrollPrevPage
+ C GotoPage wrapx wrapy -1p -1p

DestroyFunc FvwmRightPage
AddToFunc FvwmRightPage
+ I GotoPage wrapx wrapy +1p +0p

DestroyFunc FvwmLeftPage
AddToFunc FvwmLeftPage
+ I GotoPage wrapx wrapy -1p -0p

DestroyFunc FvwmUpPage
AddToFunc FvwmUpPage
+ I GotoPage wrapx wrapy +0p +1p

DestroyFunc FvwmDownPage
AddToFunc FvwmDownPage
+ I GotoPage wrapx wrapy -0p -1p

DestroyFunc FvwmMouseResize
AddToFunc FvwmMouseResize
+ M Resize
```

### Mouse and Keyboard Bindings AKA Shortcuts

You can also set the different shortcuts for the Window Manager, such as Alt+F4. These can be configured for both the mouse and the keyboard.

```
## Binding syntax for Keyboard
Key X Context Modifier Action
## Binding syntax for Mouse
Mouse X Context Modifier Action
```

X key or the main Key is used to separate multiple commands using the same modifiers. For a keyboard, this can be any number, letter, special character or a Function key. On a mouse, it can be the Left, Right or Middle button.

Context is where the mouse is currently located as shown in the diagram below. It can be any one of the following:

* R – Root Window
* I – Iconified Windows
* F – Frame Corners (Draggable corners used for resizing)
* S – Frame Sides (Draggable sides for vertical/horizontal resizing)
* W – Application Window
* T – Title Bar
* 0-9 – Ten Buttons on the title bar, each of which can be assigned a function.

### Context Layout Diagram

The Modifier is one or more modifier keys used along with the main Key. You can club multiple modifiers together, such as CM for Ctrl+Alt and CSM for Ctrl+Shift+Alt. The order in which you write them does not matter. Possible modifiers are:

* A – Any – Any Key
* C – Control – Control Key
* S – Shift – Shift Key
* M – Meta – Meta, also known as Alt key
* N – Nothing – No modifier key required
* 1-5 – representing the X Modifiers mod1-mod5 (man xmodmap).

Action can be any Fvwm built-in command, a user defined function or a third party application. To execute third party applications, use `Exec exec <command>` like so:

```
Key t A CM Exec exec xterm
```

Now, suppose I want to emulate the `Alt+Tab` feature popularly found in all other desktop environments.
We know that Fvwm already provides a `WindowList` function that displays a selectable list of current windows.
So we just need to figure out a way to bind this function to a shortcut.
I would use the following string to create the bind:

```
## Binding syntax for Keyboard
## Key X Context Modifier Action
Key Tab A M WindowList
```

Here,

* **Keyword**: is Key since this is a keyboard shortcut
* **Actual Key**: Tab
* **Context**: Anywhere – A
* **Modifier**: Meta/Alt – M
* **Action**: Run built in command WindowList.

You must assign a command to each button 1-9 on the title bar of every window.
Suppose we want to assign the custom function `FvwmDeleteOrDestroy` defined earlier to the rightmost button which is 2, we would do the following:

```
## Binding syntax for Mouse
## Mouse X Context Modifier Action
Mouse 1 2 A FvwmDeleteOrDestroy
```

Here,

* **Keyword**: is Mouse, since this is a mouse binding
* **Actual Key**: is 1 to indicate a Left Click press. 2 for Middle Click and 3 for a Right Click.
* **Context**: Where the click is actually done, in this case ’2′ for button no. 2 on the title bar.
* **Modifier**: Any or none modifier keys required to perform this action.
* **Action**: Call custom function FvwmDeleteOrDestroy

Examples of bindings are as follows:

```
#####
## Basic Bindings
############
Key F1 A M Menu MenuFvwmRoot
Key Tab A M WindowList Root c c NoDeskSort, SelectOnRelease Meta_L
Mouse 2 R A WindowList Root c c NoDeskSort, SelectOnRelease Meta_L
Key Super_L A A FvwmATerm
Mouse 1 R A Menu RootMenu
Mouse 3 R A Menu MenuFvwmRoot
Mouse 1 1 A FvwmDeleteOrDestroy
Mouse 1 3 A FvwmIconifyOrShade
Mouse 1 5 A FvwmMaximize 100 100
Mouse 2 5 A FvwmMaximize 0 100
Mouse 3 5 A FvwmMaximize 100 0
Mouse 1 W M FvwmMoveOrIconify
Mouse 1 I A FvwmMoveOrIconify
Mouse 4 T A FvwmWindowShade True
Mouse 5 T A FvwmWindowShade False
Mouse 1 2 A FvwmWindowShade False
Mouse 1 4 A FvwmWindowShade True
##My Custom Functions!
Mouse 5 R A FvwmScrollNextPage
Mouse 4 R A FvwmScrollPrevPage
Key Right A CM FvwmRightPage
Key Left A CM FvwmLeftPage
Key Up A CM FvwmUpPage
Key Down A CM FvwmDownPage
Key t A CM Exec exec gnome-terminal
Mouse 3 A M FvwmMouseResize
Key s A CM Exec exec /usr/local/bin/switchscreen
Key F12 A C Next (FvwmMegaPager, CirculateHit) Iconify
```

### Colorsets

Colorsets are essentially color schemes that you will be using to color your windows, buttons and all other objects.
These can be created using the colorset command.
You can specify the background, foreground, highlight background and foreground etc.

Fvwm uses plain integer numbers to distinguish the colorsets.
By default the following numbers will be used if any colorset is not specified for a specific object:

    * 0 = Default colors
    * 1 = Inactive windows
    * 2 = Active windows
    * 3 = Inactive menu entry and menu background
    * 4 = Active menu entry
    * 5 = greyed out menu entry (only bg used)
    * 6 = module foreground and background
    * 7 = hilight colors

Colors can be specified using their conventional names such as Black, Orange, Gray, Green, Yellow etc.
You may also use RGB hexadecimal codes such as `#ABCDEF` or `#FF95F0`.
Here are some colorsets that I like to use:

```
#####
## Colorsets
############
Colorset 1 fg Green, bg Black
Colorset 2 fg Red, bg Black
Colorset 3 fg White, bg Black
Colorset 4 fg Gray, bg Black
Colorset 5 fg Black, bg #FF9500
Colorset 6 fg Gray, bg #C24E00
Colorset 7 fg #FF9500, bg Black
Colorset 8 fg Orange, bg Gray
Colorset 20 fg #dedede, bg #2d2d2d, sh #0d0d0d, hi #4d4d4d
Colorset 21 fg #dedede, bg #3d3d3d, sh #0d0d0d, hi #4d4d4d
Colorset 22 fg #dedede, bg #0d0d0d, sh #0d0d0d, hi #4d4d4d
```

### Window Decorations

Fvwm also supports styling of windows which are often called themes.
You can configure almost all elements of a window, even those attributes which are seldom found in other window managers.
The `Style` command is used to set attributes of a window to values other than the default or to set the window manager default styles.

Sample styles that you can apply to all or specific windows:

```
#####
## Window Styles
############
Style "*" UseDecor MyDecor
Style "*" Font "xft:Sans:Bold:size=8:minspace=False:antialias=True"
Style "*" BorderWidth 2, HandleWidth 4
Style "*" Colorset 6
Style "*" HilightColorset 5
Style "*" BorderColorset 6
Style "*" HilightBorderColorset 5

#####
## Synapse No Border Config
##############
Style "Synapse" !Borders, NoHandles, NoTitle, StaysOnTop
DestroyModuleConfig Synapse: *

#####
## Chromium No Border Config
##############
Style "Chromium-browser" !Borders, NoHandles, NoTitle
DestroyModuleConfig Chromium-browser: *

#####
## Guake No Border Config
##############
Style "Guake.py" !Borders, NoHandles, NoTitle, StaysOnTop
DestroyModuleConfig Guake.py: *

#####
## Wine ShowTitle Configuration
##############
Style "Wine" Borders, Handles, Title
DestroyModuleConfig Wine: *
```

Window Decors are styles that define how a window actually looks.
You can configure everything from the title bar button positions to the border width.
Follow that link for examples on how to configure pixmaps or vector drawings for buttons and other options.

### Configuring The Virtual Desktops

Virtual Desktops is a feature which is omnipresent on any Linux Distribution.
These are generally handled by the window manager itself.
I use the following properties to get a virtual desktop with 4 pages in a 2×2 arrangement.
This Virtual Desktop is given the Title “Spaces”.

```
#####
## Virtual Desktops
############
DesktopSize 2x2
DesktopName 0 Spaces
EdgeScroll 0 0
EdgeResistance 450  450
EdgeThickness 1
```

Gives the following arrangement:

```
 __________________________________
|                |                 |
|                |                 |
|                |                 |
|________________|_________________|
|                |                 |
|                |                 |
|                |                 |
|________________|_________________|
```

