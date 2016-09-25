---
title: Broadcasting on Twitch with OBS
layout: "post"
date: "2016-09-25 10:30:00 -0900"
description: "Step by step guide on configuring OBS with twitch.tv, with pictures."
keywords: "open broadcasting system, OBS, twitch, broadcasting, streaming, setup, installation, configuration"
---

## Setup
1. Navigate to https://obsproject.com/download, and click the appropriate OBS Studio
link for your operating system. This guide will continue with MAC OSX.
2. Double click on OBS.dmg (or .exe for Windows) file downloaded, and continue through the installer.
You'll need to run root privileges to complete the installation.
(INSTALLATION PIC HERE)
3. Launch OBS. I used Spotlight to find OBS and launch.
4. Your initial launch will require you to accept the license agreement.
(LICENSE PIC HERE)
(INITIAL LAUNCH HERE)

## Associate your Twitch.tv account with OBS.
1. Click the "Settings" button **OR** Click OBS menu, then Preferences.
2. Click "Stream"
3. Open browser and navigate to your Twitch.tv dashboard's Stream Key section:
https://www.twitch.tv/{USERNAME}/dashboard/streamkey, replacing {USERNAME} with
your Twitch user name.
(TWITCH STREAM PAGE)
4. Click "Show Key", then click "I Understand" to warning dialog.
(TWITCH WARNING)
5. Copy key displayed and paste into OBS "Stream Key" input opened in step 2.
6. You are now configured to stream to Twitch.

## Create Scenes and Sources
 - Scenes are groupings of sources. Think layers like photoshop.
 - Sources are things to display. Think the circle you drew on the layer in
photoshop.

Lots of broadcasters have at least two scenes. One that shows some kind of
message indicating they are about to start. A second one that shows their camera
and video game simultaneously.

You'll start out with Scene named Default that has no Sources. This is a good
starting point to add your initial game to stream.

## Add Source
1. Click the + icon in the Sources area
(Add source)
2. Launch your game of choice
3. Select Window Capture. This lets you output an entire window. For browsers
with multiple tabs, this means the tab displayed will be what is shown.
4. Create new, I named mine "Game", and leave "Make source visible". The latter options displays the
new source immediately. Unchecking this, you will need to click the eye icon
next to the source in order to see your game being played.
5. Select the game you launched in step 2 and click "OK"
(Select game)
6. Resize the game appropriately to fit your screen or desired height/width
(Resize game)
