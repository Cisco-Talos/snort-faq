If a log in your Snort-log directory is an empty file like this:

`-rw-------. 1 root  root     0 Sep 20 11:30 merged.log.1411187404`
`-rw-------. 1 root  root     0 Sep 20 11:30 tcpdump.log.1411187404`


One of the causes of this problem may be the "$NO_PACKET_LOG" option (-N)  in Snort's startup script at /etc/init.d/snort.
Please delete it from this line:

------------------
 `daemon --pidfile=$PID_FILE $SNORTD $ALERTMODE $LINK_LAYER $DUMP_APP -e -D $PRINT_INTERFACE $INTERFACE -u $USER 
` -g $GROUP $CONF -l $LOGDIR $PASS_FIRST $BPFFILE $BPF && success || failure
------------------


and restart snort again.
