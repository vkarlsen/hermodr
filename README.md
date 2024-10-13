# HERMODR

## About
Hermodr is a simple system alert thingie. It runs a number of checks, called
`scouts`, that send a notification if a non-acceptable condition is detected.

It is intended to run periodically, and will only generate output if a problem
has been found (unless `VERBOSE` and/or `MOREVERBOSE` is set).

Its main alerting channel is ntfy.sh. Set `ntfy_enable="YES"` to enable it,
and remember to change `ntfy_topic` to your own topic. It can also alert to
`stdio` by setting `stdio_enable="YES"`.

All files in the `scouts/` directory need to have the executable bit set.

Currently, it only checks for:
- High load avg
- Low disk space
- Non-running processes (specific ones)
- High CPU usage
- High CPU temperature
- zpool health

New checks are welcome!

## Principles
- Simple: Easy to set up, easy to use, easy to modify
- Portable: Keep dependencies to a minimum

## Dependencies
- bourne-compatible shell
- curl
- Base components like bc, grep, awk, top

## Installation
It can be run from its own directory, or it can be installed system-wide
under a `PREFIX` like `/usr/local`.
The main script is in `./bin`, the common functions and scouts live in
`./libexec/hermodr/`.
There's a sample `hermodr.conf.sample` in `./etc` that needs to be copied
to `hermodr.conf`.

## Running
Run it in a crontab as often as you wish, e.g.
`0 * * * * /bin/hermodr`
It does not need root privileges to run.

## Portability
It is supposed to work on:
- All BSDs
- SunOS
- Linux

