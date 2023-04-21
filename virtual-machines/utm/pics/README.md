# Emulation on macOS via UTM

## Summary

This is really a proof of concept, that Apple's M1's AArch64 can emulate the x86-64 architeture.  This has been tested with the SANs SIFT VM and Kioptrix.  However, due to limited HW specs on my testing machine, the emulation suffers in terms of speed.  Large GUI applications can take more than 10 minutes to load... IF they even load at all.

Nonetheless, feel free to reach out to me if you've tested this on higher specs (especially with an M1 Pro/Max/Ultra) and how the emulation ran.  It'd be nice if this could be resolved; but until then, c'est la vie!

![M1 chip emulating x86-64](./pics/proof-of-concept.png "Proof of Concept")
