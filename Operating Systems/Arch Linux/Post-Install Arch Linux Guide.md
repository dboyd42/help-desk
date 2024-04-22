# Post-Installation To Do Guide for Arch Linux

**Author:** David Boyd<br>
**Date:** 2024-04-22

## Table of Contents

## Necessary Programs

### Audio

``` bash
pacman -S pipe-wire
```

### Power Settings

``` bash
# ACPI Power Mgmt -> Used for hibernation
pacman -S acpid
```

## Programming Languages

### Rust

[Official Rust link.][rust]

``` bash
# Rust
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

## Desktop Programs

### Browsers

``` bash
pacman -S qutebrowser
# pipewire-jack, noto-sans
```

<!-- References -->
[Official Rust link.]: https://www.rust-lang.org/learn/get-started
