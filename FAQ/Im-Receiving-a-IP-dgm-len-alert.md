## I'm receiving an error regarding IP Datagram length, what is the problem? ##

If you are receiving an error message that looks like:

`(snort_decoder) WARNING: IP dgm len > captured len`

This is an indication that the packets being passed to Snort from whatever device is on the other end (Switch, router, etc) are bigger than the standard Ethernet length of 1514.

The way to fix this is to pass a specific `snaplen` or Snap Length to Snort on the command line, try `-P 65535`.
