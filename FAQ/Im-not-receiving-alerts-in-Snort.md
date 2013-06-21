## I'm not receiving alerts in Snort ##

*  You running Snort on the same box as you are sending/receiving packets.
    *  This is most likely the result of a [checksum offloading issue](http://www.wireshark.org/docs/wsug_html_chunked/ChAdvChecksums.html). Try adding `-k none` to your Snort command line and see if it works. 

*  You are attempting to simply test Snort by downloading an executable file of some sort, and aren't receiving an alert
    *  Make sure you have rules that look for portable executable downloads turned on like SID 1:16425.  Also, see above and add `-k none` to your command line to see if your NIC is offloading checksums.
