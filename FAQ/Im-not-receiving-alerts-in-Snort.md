## I'm not receiving alerts in Snort ##

*  You running Snort on the same box as you are sending/receiving packets.
    *  This is most likely the result of a [checksum offloading issue](http://www.wireshark.org/docs/wsug_html_chunked/ChAdvChecksums.html). Try adding `-k none` to your Snort command line and see if it works. 