# PDP-6 Emulator Design Notes

## Overview

This document describes what I had in mind for building this
system, and why I made some of the decisions that I did.

First and foremost, it should be understood that the first cut at
this is basically going to be a toy.  While it may (eventually) be
robust enough to run production workloads (what would have been considered
"production" when the machine was being manufactured and marketed, anyway),
if I can get a monitor to boot and run a few simple programs, I'll be
very happy.  Even if I can get some simple standalone (executive mode)
programs to run, I'll be somewhat happy.  I'm not aiming too high with
this first attempt.

This first attempt is not going to be built on SIMH or any other
emulation framework - it will be completely standalone.  The primary
reason for this is time - I know nothing about the internals of SIMH
or implementing a new system type within it, and don't think I have
time to learn right now - but I do know how to program in C... 
I've been kind of sitting on this project idea for a long time, waiting for
a time when I had some time...  Which I do right now (sort of...).
I know my own habits well enough to know that adding additional time
(such as learning an emulation framework first) makes it less likely
that anything is going to be done on it at all.  So, I'll forge ahead
with a design that I've had in mind since at least the early 1990's,
before SIMH and KLH10 existed...

This design will be based on a simple multi-threaded architecture, using
pthreads.  (What I originally had in mind would have used SunOS LWP's,
which would give you an idea of how long this has been cooking in my
head...)

## System Architecture

The system is based on a threading model, in which each major component of
the system runs in its own thread, and the components communicate with each
other using pthreads primitives.  Major threads/components of the system
are as follows.

### Front End (FE)

The FE thread is responsible for managing the other components of the
system, and communicating with the user about the operation and configuration
of the emulator.  When the emulator is operating, it also handles
the console terminal (CTY) I/O.  When the emulator is not operating (i.e.,
emulated processor is not running), it allows the user to perform low-level
operations in the emulated system, such as examining/modifying memory
and fast ACs, and starting the processor.  When the emulated processor
is running, even though the FE is handling CTY I/O, it should be possible
to escape back to "management mode" to poke at the state of the system.
Manages readin mode to boot from paper tape (or microtape?  Not sure if
that is even possible...).

### Arithmetic processor (APR - type 166)

Executes processor instructions, manages execution sequencing, etc.
The FE communicates with the APR to tell it when to start, and when
to stop - and the APR communicates with the FE to tell it that it's
stopped (due to a HALT operation, etc.)

### I/O processor (type 167)

Manages system I/O, communicates with the APR to get I/O requests
and provide/obtain data and conditions.

### More will go here soon

## Non-goals

I don't intend for the emulation to be fast.  The real hardware
wasn't fast, the emulation doesn't need to be fast either...

It's unlikely that I'll extend this into a PDP-10 emulator of
any kind.  There are at least two really good PDP-10 emulators
out there already (as of this writing), and a couple of others
that were built as people's personal projects.  You should look
into one of those if you're looking for a functional PDP-10
emulator.
