# IT Support / KBS

**Author:** David Boyd<br>
**Updated:** 2023-06-21

## Table of Contents

- [Introduction](#introduction)
- [Getting Started](#getting-started)
  - [Command Line Interface](#command-line-interface)
    - [Example 1: Perform a basic operation](#example-1-perform-a-basic-operation)
    - [Example 2: Configure advanced settings](#example-2-configure-advanced-settings)
    - [Example 3: Render MD file](#exmaple-3-render-md-file)
- [Troubleshooting](#troubleshooting)

## Introduction

This repo acts as a knowledge base system (KBS) for various IT issues and their
*hopeful* resolutions that I have worked tirelessly though. The repo has been
updated to fit a more IT KBS structure. Note, there is a current work in
progress to update all RST files to MD.

## Getting Started

The fastest method to search for an issue would be to use `grep -ri` from the
root directory. But to each their own!

### Command Line Interface

### Examples

- [Example 1: Perform a basic search](#example-1-perform-a-basic-search)
- [Example 2: Perform a filename search](#example-1-perform-a-filename-search)
- [Example 3: Render MD file](#exmaple-3-render-md-file)

#### Example 1: Perform a basic search

``` bash
# Search for all files with matching occurences of insensitive case "arch"
PATTERN='arch'
grep -ri $PATTERN
```

Using `r` to search `r`ecursively through the repo and `i` to search regardless
of upper/lowercase.

#### Example 2: Perform a filename search

``` bash
# Search for all filenames with matching occurences of insenitive case "arch"
PATTERN='*arch*'
find ./ -type f -iname $PATTERN
```

Use the `*` to implement a wildcard search with flags `-type f` for filenames
and `-iname` for `i`nsensitive case searching.

#### Example 3: Render MD file

##### Method 1: GitHub

As these files are public, you can navigate to the desired file and have GitHub
render markdown file from there.

##### Method 2: NeoVim Plugin - MardownPreview

This requires  Neo(vim)'s plugin [MarkdownPreview][mdp]. You can also refer to
my [Arch dotfiles][dotties] or [macOS dotfiles][mac-nvim] for setup.

``` bash
# Open the markdown file in vim and run the plugin
nvim +MarkdownPreview README.md
```

## Troubleshooting

:warning: Not all documents have been verified.  Additionally, some of the 
solutions may have "worked" by a random combination of attempts. So not all 
documents are guaranteed to work. "Here's looking at you, kid."

<!-- Reference Links -->

[mdp]: https://github.com/iamcco/markdown-preview.nvim
[dotties]: https://github.com/dboyd42/dotfiles/tree/master/home/.config/nvim
[mac-nvim]: https://github.com/dboyd42/dotfiles/blob/master/macos-setup.md
