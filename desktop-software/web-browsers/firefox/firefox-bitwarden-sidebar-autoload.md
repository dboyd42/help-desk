# How to Disable the BitWarden Sidebar from Auto-Loading

**Author:** David Boyd<br>
**Date:** 2023-05-11

> Reference URL: [BitWarden Issue #1991][gh-solution]

## Issue

Upon resetting Firefox's SSL settings due to a
[WiFi connection error][pr-eof-err], the BitWarden extension started
auto-loading the sidebar in every new window.

## Solution

To resolve the **Firefox specific error**:

1. Click the **BitWarden drop-down menu** in the far upper left side
2. Choose either `History` or `Bookmarks`
3. Close the sidebar

Henceforth, the sidebar should not auto-load upon spawning a new window or
new session.

<!-- Reference Links -->

[pr-eof-err]: ./../../../wifi/pr_end_of_file_error-firefox.md
[gh-solution]: https://github.com/bitwarden/clients/issues/1991
