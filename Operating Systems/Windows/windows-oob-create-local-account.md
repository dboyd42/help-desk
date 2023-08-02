# How to Create a Local Account on Windows OOB OS Setup

**Author:** David Boyd<br>
**Date:** 2023-06-08
>> **Updated:** 2023-08-02

## Introduction

The point is to not have to always use or register a OneDrive, Outlook,
or any other Microsoft account when installing Windows OS.

## Prerequisites

This assumes your Windows experience is OOB (Out-of-the-Box) or a similar fresh
install.

## Steps

### Step 1: Get Command Prompt

``` bash
<Shift-F10>
```

### Step 2: Open Task Manager

``` cmdprompt
\> taskmanager
```

:bulb: For Windows 11 ARM64, `taskmanager` has been moved to `Taskmgr.exe`

### Step 3: Kill Network COnnection Flow

1. Click on `Background Process`
2. Select `NetworkConnectionFlow`
3. Click EndTask

