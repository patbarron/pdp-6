# PDP-6 Emulator

This is (or, more accurately, may eventually become...) a standalone PDP-6 emulator.  The ultimate goal is to
be able to run the PDP-6 monitors found here:

http://pdp-6.trailing-edge.com

This may require building some tools to actually build the monitor from source (like maybe an assembler, to start
with...), and get it on to a disk image to boot from.

My goal is to emulate the instruction set and some I/O (enough to get the monitor running) - I have no
intention of trying to simulate the PDP-6 at the circuit level, like https://github.com/aap/pdp6
does.

I refer to this as a "standalone" emulator, meaning that it is not built on SIMH or some other emulation
framework.  Even though it probably could be - the SIMH PDP-10 (KA10) emulator probably has most of the code that
would be required to do this, but some small differences in APR behavior between the PDP-6 and PDP-10 most
likely mean that one could not run the PDP-6 monitor directly on a PDP-10, even though just about everything
else is the same.  I may revisit this at some point in the future, if I learn more about the SIMH framework,
and am able to copy/paste code from the SIMH KA10 emulator to make it function like a PDP-6.

At this moment, there's basically nothing here except this README.md file, to act as a placeholder to get
the repository on GitHub.  Feel free to contribute code if you are so inclined.  ;-)
