---
layout: post
title: "My FVWM2 Desktop!"
date: 2011-12-25T10:37:00+05:30
tags: software
---

After getting tired of Unity and the extra Compiz Effects fighting with each other, I decided to try some other desktop environments.
I had used fvwm2 earlier but never realized its power until now.

I had used the basic environment created by the Setup95 script.
It looked ugly and buggy.
After asking on the official freenode IRC channel I learned that the script was old and not maintained anymore.

I explored more about fvwm2 and found out the awesome screenshots of some custom fvwm2 configurations [here](https://web.archive.org/web/20120204062501/http://fvwm.org/screenshots/desktops/).
This inspired me to create my own fvwm2 configuration.
I started out with [this guide](https://web.archive.org/web/20120207192901/http://www.zensites.net:80/fvwm/guide/index.html), tweaking or skipping over some parts.

I particularly had a lot of fun messing around with the different color schemes and drawing different vectors for the buttons.
I finally settled with an orange color scheme that accented my terminals and my wallpaper.

I also had to manually scale down the images for the icons, as fvwm2 only supports .xcf .xpm and .png image formats for its icons.
I customized the FvwmButtons to respond differently to different mouse clicks, like left clicking Vim opens vim in a terminal, while middle clicking brings up Gvim and right clicking brings up the gedit text editor.
Also fun was trying to swallow different applications inside the FvwmButtons.
I ended up swallowing the digital xclock and xload load monitor.

A screenshot of my desktop:

![My Fvwm2 Desktop](/img/my-fvwm2-screenshot.png 'My Fvwm2 Desktop')

And here is my .fvwm2rc configuration file:

```
#####
## Set Environment variables
############
SetEnv fvwm_img $[FVWM_USERDIR]/images
SetEnv fvwm_icon $[FVWM_USERDIR]/icons
#SetEnv fvwm_script $[FVWM_USERDIR]./scripts
SetEnv fvwm_wallpapers $[FVWM_USERDIR]/wallpaper

## Default programs
SetEnv fvwm_webbrowser /usr/bin/firefox
SetEnv fvwm_term /usr/bin/xterm
SetEnv fvwm_mail /usr/bin/thunderbird
SetEnv fvwm_media_player /usr/bin/banshee
SetEnv fvwm_video_player /usr/bin/vlc

#####
## Virtual Desktops
############
DesktopSize 2x2
DesktopName 0 Spaces
#DesktopName 1 Work
#DesktopName 2 Games
EdgeScroll 0 0
EdgeResistance 450  450
EdgeThickness 1

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

#####
##
## DestroyFunc FuncName
## AddToFunc   FuncName
## + I (Action to happen immediately)
## + C (Action to happen on a mouse 'click)
## + D (Action to happen on a mouse 'double click')
## + H (Action to happen on a mouse 'hold')
## + M (Action to happen on a mouse 'motion')
##
############

#####
## Startup Functions
############
DestroyFunc StartFunction
AddToFunc   StartFunction
#+ I Module FvwmTaskBar
+ I Module FvwmPager
+ I Module FvwmButtons BarButtons
+ I Module FvwmButtons PagerButton
+ I Exec exec feh --bg-fill $[fvwm_wallpapers]/ws_Black_and_White_City_1280x1024.jpg
#+ I Exec exec xcompmgr
+ I Exec exec synapse --startup

DestroyFunc InitFunction
AddToFunc   InitFunction
#+ I Exec exec xscreensaver
#+ I Exec exec fvwm-root -r $[fvwm_wallpapers]/background.png
+ I Exec exec feh --bg-fill $[fvwm_wallpapers]/ws_Black_and_White_City_1280x1024.jpg
#+ I FvwmXmms
#+ I FvwmATerm

DestroyFunc RestartFunction
AddToFunc   RestartFunction
+ I Nop

#####
## Basic Functions
############
DestroyFunc FvwmDeleteOrDestroy
AddToFunc   FvwmDeleteOrDestroy
+ H Nop
+ M Nop
+ C Delete
+ D Destroy

DestroyFunc FvwmIconifyOrShade
AddToFunc   FvwmIconifyOrShade
+ C Iconify
+ D WindowShade

DestroyFunc FvwmMaximize
AddToFunc   FvwmMaximize
+ H Nop
+ M Nop
+ C Maximize $0 $1

DestroyFunc FvwmMoveOrIconify
AddToFunc   FvwmMoveOrIconify
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
#when the viewport is moved beyond the border of the desktop.
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

#####
## Basic Bindings
############
Key F1 A M Menu MenuFvwmRoot
Key Tab A M WindowList Root c c NoDeskSort, SelectOnRelease Meta_L
Key Super_L A A FvwmATerm
#Mouse 1 R A Menu FvwmRootMenu
#Mouse 3 R A Menu FvwmWindowOpsMenu
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
##Custom Functions!
Mouse 5 R A FvwmScrollNextPage
Mouse 4 R A FvwmScrollPrevPage
Key Right A CM FvwmRightPage
Key Left A CM FvwmLeftPage
Key Up A CM FvwmUpPage
Key Down A CM FvwmDownPage
Mouse 3 A M FvwmMouseResize

#
#Bindings are set up as follows, you can either bind a key to an
#action by 'Key X Context Modifier Action' or bind the mouse to an
#action 'Mouse X Context Modifier Action'.
#Context is where the mouse is currently located (as shown above)
#and the Modifier is any combination of the following;
#(A)ny, (C)ontrol, (S)hift, (M)eta, (N)othing, or 1-5,
#representing the X Modifiers mod1-mod5 (man xmodmap).
#Examples of bindings are as follows:
#

#####
## Window Colorsets
############
Colorset 1 fg Green, bg Black
Colorset 2 fg Red, bg Black
Colorset 3 fg White, bg Black
Colorset 4 fg Gray, bg Black
Colorset 5 fg Black, bg #FF9500
Colorset 6 fg Gray, bg #C24E00
Colorset 7 fg #FF9500, bg Black
#Colorset 7 fg #006AFF, bg #FF9500
#Colorset 8 fg #0074C2, bg #C24E00

#####
## Window Decor MyDecor
############
DestroyDecor MyDecor
AddToDecor   MyDecor
+ TitleStyle Centered Height 18
+ ButtonStyle 1 ActiveUp Vector 4 30x30@3 60x60@3 60x30@4 30x60@3
+ ButtonStyle 1 ActiveDown Vector 4 30x30@3 60x60@3 60x30@4 30x60@3
+ ButtonStyle 1 Inactive Vector 4 30x30@3 60x60@3 60x30@4 30x60@3
+ ButtonStyle 3 ActiveUp Vector 5 30x60@3 60x60@3 60x50@3 30x50@3 30x60@3
+ ButtonStyle 3 ActiveDown Vector 5 30x60@3 60x60@3 60x50@3 30x50@3 30x60@3
+ ButtonStyle 3 Inactive Vector 5 30x60@3 60x60@3 60x50@3 30x50@3 30x60@3
+ ButtonStyle 5 ActiveUp Vector 7 30x30@3 30x60@3 60x60@3 60x30@3 30x30@3 30x35@3 60x35@3
+ ButtonStyle 5 ActiveDown Vector 7 30x30@3 30x60@3 60x60@3 60x30@3 30x30@3 30x35@3 60x35@3
+ ButtonStyle 5 Inactive Vector 7 30x30@3 30x60@3 60x60@3 60x30@3 30x30@3 30x35@3 60x35@3
+ ButtonStyle 2 ActiveUp Vector 4 25x25@3 75x25@3 50x75@3 25x25@3
+ ButtonStyle 2 ActiveDown Vector 4 25x25@3 75x25@3 50x75@3 25x25@3
+ ButtonStyle 2 Inactive Vector 4 25x25@3 75x25@3 50x75@3 25x25@3
+ ButtonStyle 4 ActiveUp Vector 4 75x75@3 25x75@3 50x25@3 75x75@3
+ ButtonStyle 4 ActiveDown Vector 4 75x75@3 25x75@3 50x25@3 75x75@3 -- Flat
+ ButtonStyle 4 Inactive Vector 4 75x75@3 25x75@3 50x25@3 75x75@3 -- Flat

+ TitleStyle -- Flat
+ BorderStyle Simple -- NoInset Flat
+ ButtonStyle All -- UseTitleStyle
+ ButtonStyle All -- Flat

#Vectors are just simple line drawings. Each vector is set up
#on a 100x100 grid and can have any number of points all
#connected by lines. The syntax is
#'Vector [number of points] [[point1] [point2] ...]'.
#The points are defined by 'XxY@Z' where Z is any number 0-4
#representing the color to be used for the line.
#0 - Shadow(sh), 1 - Hilight(hi), 2 - Background(bg),
#3 - Foreground(fg), 4 - Invisible.

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
## PagerButton
############
Style "PagerButton" NoTitle,NoHandles, Sticky, WindowListSkip, \
!Borders, CirculateSkip, !Iconifiable, FixedSize, StaysOnBottom

DestroyModuleConfig PagerButton: *
*PagerButton: Geometry 15x180-0+0
*PagerButton: Back black
*PagerButton: Fore #FF9500
*PagerButton: Rows 1
#*PagerButton: Frame 3
*PagerButton: Columns 1
*PagerButton: (Title "&lt;",Action(Mouse 1) 'Next (FvwmPager, CirculateHit) Iconify')

#####
## FvwmPager
############
Style "FvwmPager" !Icon, NoTitle, !Handles, !Borders, Sticky, WindowListSkip, \
CirculateSkip, StaysOnTop, FixedPosition, FixedSize
# !Iconifiable

DestroyModuleConfig FvwmPager: *
*FvwmPager: Geometry 320x180-15+0
#*FvwmPager: Colorset * 9
#*FvwmPager: HilightColorset * 10
#*FvwmPager: BalloonColorset * 9
*FvwmPager: Back black
*FvwmPager: Fore grey60
#*FvwmPager: WindowColorsets 9 10
*FvwmPager: Font "none"
#"xft:Sans:Bold:pixelsize=12:minspace=True:antialias=True"
*FvwmPager: Balloons All
*FvwmPager: BalloonFore black
*Fvwmpager: BalloonBack bisque
*FvwmPager: BalloonFont "xft:Sans:Bold:pixelsize=12:minspace=True:antialias=True"
*FvwmPager: BallonYOffset +2
*FvwmPager: Window3dBorders
*FvwmPager: MiniIcons
*FvwmPager: UseSkipList
#*FvwmPager: Columns 3
*FvwmPager: Rows 1

#####
## BarButtons
#############
Style "BarButtons" !Title, !Handles, !Borders, Sticky, WindowListSkip, \
CirculateSkip, StaysOnTop, FixedPosition,  FixedSize, !Iconifiable

DestroyModuleConfig BarButtons: *
*BarButtons: Fore #FF9500
*BarButtons: Back Black
*BarButtons: Frame 1
*BarButtons: Font "xft:sans-serif:Bold:pixelsize=10;-*-helvetica-bold-r-*-*-10-*-*-*-*-*-*-*"
*BarButtons: Geometry 55x400-0-0
*BarButtons: Rows 8
*BarButtons: (1x1, Icon $[fvwm_icon]/orange_folder_32x32.png, Action(Mouse 1) 'Exec exec pcmanfm')
*BarButtons: (1x1, Icon $[fvwm_icon]/utilities-terminal.png, Action(Mouse 1) 'Exec exec gnome-terminal', \
Action(Mouse 3) 'Exec exec xterm -fg orange -bg black')
*BarButtons: (1x1, Icon $[fvwm_icon]/vim-32.xpm, Action(Mouse 1) 'Exec exec gnome-terminal -e vim', \
Action(Mouse 2) 'Exec exec gvim', \
Action(Mouse 3) 'Exec exec gedit')
*BarButtons: (1x1, Icon $[fvwm_icon]/firefox_32x32.png, Action(Mouse 1) 'Exec exec firefox')
*BarButtons: (1x1, Icon $[fvwm_icon]/thunderbird_32x32.png, Action(Mouse 1) 'Exec exec thunderbird')
*BarButtons: (1x1, Icon $[fvwm_icon]/openarena32.xpm, Action(Mouse 1) 'Exec exec openarena')
*BarButtons: (1x1, Swallow "xload" "Exec exec xload -label CPU -update 2 -background Black -foreground Orange")
*BarButtons: (1x1, Swallow "xclock" "Exec \
exec xclock -hands orange -highlight orange -foreground orange -background black -digital -brief -padding 4")
```
