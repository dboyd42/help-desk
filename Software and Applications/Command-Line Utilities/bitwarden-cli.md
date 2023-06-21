# How to Install BitWarden CLI on Linux

**Author:** David Boyd<br>
**Date:** 2023-06-13

## Table of Contents

- [Introduction](#introduction)
- [Objectives](#objectives)
- [Prerequisites](#prerequisites)
- [Steps](#steps)
  - [Step 1: Download and Install](#step-1-download-and-install)
  - [Step 2: Title](#step-2-title) #TODO
  - [Step 3: Title](#step-3-title) #TODO
- [Conclusion](#conclusion)
- [Tips and Best Practices](#tips-and-best-practices)
- [Additional Resources](#additional-resources)

## Introduction

- [Official BitWarden Guide][bw-doc-cli]
- [Official Bitwarden Video Guide][bw-youtube]

## Objectives

1. To get the BitWarden CLI setup in a Linux environment
2. TO integrate API key security using BitWarden

## Prerequisites

*[List any prerequisites or requirements that readers need to fulfill before
following the guide.]*

## Steps

### Step 1: Download and Install

``` bash
# 1. Download the file (refer to the official docs if link doesn't work)
wget https://vault.bitwarden.com/download/?app=cli&platform=linux

# 2. Unzip the file
unzip bw-linux-2023.5.0.zip

# 3. Change the permissions to make it executable
chmod u+x bw

# 4. Move binary to /usr dir for global execution (assuming /usr in $PATH)
sudo mv bw /usr/local/bin/

# 5. Test installation
bw --version

# 6. Install dependencies
pacman -S jq
```

### Step 2: *Title*

*[Explain the second step, breaking it down into smaller sub-steps if
applicable.]*

### Step 3: *Title*

*[Continue with the subsequent steps, ensuring clarity and logical flow.]*

## Tips and Best Practices

*[Share any additional tips, best practices, or common pitfalls to help readers
achieve better results.]*

## Conclusion

*[Summarize the guide and reiterate the key points. Optionally, suggest next
steps or provide additional resources for readers to explore.]*

## Additional Resources

*[Include any relevant links or resources that can further assist readers in
their journey.]*

<!-- Reference Links -->

[bw-doc-cli]: https://bitwarden.com/help/cli/
[bw-youtube]: https://www.youtube.com/watch?v=Qe4oGJREV8Q&ab_channel=Bitwarden
