# Resolve Streaming Errors with DisplayLink on the macOS M1

**Author:** David Boyd<br>
**Date:** 2023-07-24

## Table of Contents

- [Introduction](#introduction)
- [Objective](#objective)
- [Prerequisites](#prerequisites)
- [Steps](#steps)
  - [Step 1: Download a downgraded Firefox](#step-1:-download-a-downgraded-firefox)
  - [Step 2: Install the Downgraded Firefox](#step-2:-install-the-downgraded-firefox)
  - [Step 3: Login and Stream](#step-3:-login-and-stream)

## Introduction

After setting up DisplayLink on the M1, I had a nice black screen overlay while
attempting to watch my Udemy videos. This may be due DisplayLink's method of
screen recording on the M1 in combination with streaming services trying to
protect their content from recorded... but that's cool; we can bypass this.

DisplayLink's [official workaround][dl-rec] is as follows:

> A workaround is to temporarily disconnect all DisplayLink screens, switch
> to another browser or disable hardware acceleration in your browser to access
> protected content.

However if I'd of wanted to disconnect DisplayLink, I wouldn't of installed it
to begin with. And both Firefox and Ungoogled-Chromium failed to resolve the
issue after I disabled hardware acceleration.

## Objective

Bypass DRM protected content to *legally* stream videos while using DisplayLink
on an M1 MacBook Pro.

## Steps

### Step 1: Download a downgraded Firefox

You can use any Firefox version up to 105.x. 
  - :warning: If using 105.x, disable auto-upgrade by pressing `⌘,` upon 
    launch, then deselect `automatic updates` (search `update` for faster
    results)

I went ahead a tested [Firefox 91.0.1][ff-9101] which can be downloaded from
the official Mozilla website.

### Step 2: Install the Downgraded Firefox

:bulb: I use Firefox as my primary browser. But using an outdated version of
anything is prone to security risks and you'll want to keep that to a minimum.
Upon installation, you'll be asked if you'll want to keep `Both` or `Replace`.
by selecting `Both`, a **Firefox 2** will be created.

### Step 3: Login and Stream

:checkered_flag: That's it! Login into the streaming site and stream your
videos!

<!-- Reference Links -->

[dl-rec]: https://support.displaylink.com/knowledgebase/articles/830301-content-protected-video-does-not-play-on-mac-while
[ff-9101]: https://ftp.mozilla.org/pub/firefox/releases/91.0.1/mac/en-US/
