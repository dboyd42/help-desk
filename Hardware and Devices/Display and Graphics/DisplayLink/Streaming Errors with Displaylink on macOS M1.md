# Resolve Streaming Errors with DisplayLink on the macOS M1

**Author:** David Boyd<br>
**Date:** 2023-07-24
> Updated: 2023-07-26

## Table of Contents

- [Introduction](#introduction)
- [Objective](#objective)
- [Steps](#steps)
  - [Step 1: Download an Outdated Firefox](#step-1-download-an-outdated-firefox)
  - [Step 2: Install the Outdated Firefox](#step-2-install-the-outdated-firefox)
  - [Step 3: Set No Autoupdate](#step-3-set-no-autoupdate) 
  - [Step 4: Login and Stream](#step-4-login-and-stream)

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

### Step 1: Download an Outdated Firefox

You can use any Firefox version up to 105.x. 

I went ahead a tested [Firefox 91.0.1][ff-9101] which can be downloaded from
the official Mozilla website.

### Step 2: Install the Outdated Firefox

:bulb: I use Firefox as my primary browser. But using an outdated version of
anything is prone to security risks and you'll want to keep that to a minimum.
Upon installation, you'll be asked if you'll want to keep `Both` or `Replace`.
by selecting `Both`, a **Firefox 2** will be created.

:warning: Do NOT open the application!!!

### Step 3: Set No Autoupdate 

This is important as I learned the hardway... We need to disable auto update
and upon initial launch, it will do just that. There are two methods for this
madness, but the first method is a more permanent means as the second was only
a temporary solution--this may have also been caused by click on :x: "Create 
new profile" :x: which I don't recommend doing.

#### Method 1: Create Policies File

```bash
# 1. Change dir into the downloaded old Firefox.app 
cd /Applications/Firefox\ 2.app

# 2. Create a distributions directory and create a policies JSON file
mkdir distributions && cd $_
vim policies.json
```

Copy and paste the following into your `policies.json` file:

``` json
{
"policies":
   {
     "DisableAppUpdate": true
    }
}
```

#### Method 2: Disable Auto Updates in Firefox Settings

1. Disconnect from the internet
2. Open Firefox > `Settings`
3. Scroll down or search for `Firefox Updates`
4. Select `Check for updates but let you choose to install them`
5. Recconect your internet connection

:warning: This method ultimately does the same as above, but I've come across instances
where it still auto update upon relaunching the app.

### Step 4: Login and Stream

:warning: You'll have a pesky `New Update... Available Now!` alert each time
you run the initial Firefox version, but this is a small inconvienance compared
to having no video displayed while playing DRM content. Aaaaand....

:checkered_flag: That's it! Login into the streaming site and stream your
videos!

<!-- Reference Links -->

[dl-rec]: https://support.displaylink.com/knowledgebase/articles/830301-content-protected-video-does-not-play-on-mac-while
[ff-9101]: https://ftp.mozilla.org/pub/firefox/releases/91.0.1/mac/en-US/
