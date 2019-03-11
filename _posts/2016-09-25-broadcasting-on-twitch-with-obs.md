---
title: Broadcasting on Twitch with OBS
layout: "post"
date: "2016-09-25 10:30:00 -0900"
description: "Step by step guide on configuring OBS with twitch.tv, with pictures."
keywords: "open broadcasting system, OBS, twitch, broadcasting, streaming, setup, installation, configuration"
---

## Setup
1. Navigate to <a href="https://obsproject.com/download" aria-label="OBS download" target="_blank">https://obsproject.com/download</a>, and click the appropriate OBS Studio
link for your operating system. This guide will continue with MAC OSX.
2. Double click on OBS.dmg (or .exe for Windows) file downloaded, and continue through the installer.
You'll need to run root privileges to complete the installation.
<a href="/assets/img/2016/09/25/obs_install.png" target="_blank" aria-label="Link to full image of OBS installation"><amp-img src="/assets/img/2016/09/25/thmb_obs_install.png" alt="OBS installation" height="284" width="404"></amp-img></a>
3. Launch OBS. I used Spotlight to find OBS and launch.
<!--excerpt-->
4. Your initial launch will require you to accept the license agreement.
<a href="/assets/img/2016/09/25/obs_license.png" target="_blank" aria-label="Link to full image of OBS license acceptance"><amp-img src="/assets/img/2016/09/25/thmb_obs_license.png" alt="OBS license acceptance" height="295" width="298"></amp-img></a>
<a href="/assets/img/2016/09/25/obs_initial_open.png" target="_blank" aria-label="Full image of initial OBS opening"><amp-img src="/assets/img/2016/09/25/thmb_obs_initial_open.png" alt="initial OBS opening" height="470" width="622"></amp-img></a>

## Associate your Twitch.tv account with OBS.
1. Click the "Settings" button **OR** Click OBS menu, then Preferences.
2. Click "Stream"
3. Open browser and navigate to your Twitch.tv dashboard's Stream Key section:
<a href="https://www.twitch.tv/USERNAME/dashboard/streamkey" aria-label="Twitch dashboard" target="_blank">https://www.twitch.tv/USERNAME/dashboard/streamkey</a>, replacing USERNAME with
your Twitch user name.
<a href="/assets/img/2016/09/25/twitch_streamkey_page.png" target="_blank" aria-label="Full image of Twitch stream key page"><amp-img src="/assets/img/2016/09/25/thmb_twitch_streamkey_page.png" alt="Twitch stream key page" height="134" width="434"></amp-img></a>
4. Click "Show Key", then click "I Understand" to warning dialog.
<a href="/assets/img/2016/09/25/twitch_streamkey_warning.png" target="_blank" aria-label="Full image of Twitch stream key warning"><amp-img src="/assets/img/2016/09/25/thmb_twitch_streamkey_warning.png" alt="Twitch stream key warning" height="207" width="287"></amp-img></a>
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
<a href="/assets/img/2016/09/25/obs_add_source.png" target="_blank" aria-label="Full image of adding an OBS Source"><amp-img src="/assets/img/2016/09/25/thmb_obs_add_source.png" alt="Adding an OBS Source" height="185" width="222"></amp-img></a>
2. Launch your game of choice
3. Select Window Capture*. This lets you output an entire window. For browsers
with multiple tabs, this means the tab displayed will be what is shown.
4. Create new, I named mine "Game", and leave "Make source visible". The latter options displays the
new source immediately. Unchecking this, you will need to click the eye icon
next to the source in order to see your game being played.
5. Select the game you launched in step 2 and click "OK"
<a href="/assets/img/2016/09/25/obs_select_game.png" target="_blank" aria-label="Full image of game selection"><amp-img src="/assets/img/2016/09/25/thmb_obs_select_game.png" alt="Game selection" height="259" width="314"></amp-img></a>
6. Resize the game appropriately to fit your screen or desired height/width
<a href="/assets/img/2016/09/25/obs_resize.png" target="_blank" aria-label="Link to full image resizing game window"><amp-img src="/assets/img/2016/09/25/thmb_obs_resize.png" alt="Resizing game window" height="236" width="391"></amp-img></a>

<small>*A better option is to use Game Capture (Syphon), but requires a tad more details to setup. See Source: Game Capture on <a href="https://help.twitch.tv/customer/portal/articles/1262922-open-broadcaster-software#Scenes & Sources" target="_blank" aria-label="Scenes & Sources in OBS">Scenes & Sources</a></small>

## Stream time
At this point you should have OBS setup sufficiently to get you on air. You should be able to click "Start Streaming" and in your Twitch dashboard <a href="https://www.twitch.tv/USERNAME/dashboard" aria-label="Twitch dashboard" target="_blank">https://www.twitch.tv/USERNAME/dashboard</a> and see the same as your actual game.

Happy broadcasting.
