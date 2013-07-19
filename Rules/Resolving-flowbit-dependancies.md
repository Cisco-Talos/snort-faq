You'll notice one of two conditions:
`Warning: flowbits key 'http.rtf' is set but not ever checked.`
or
`Warning: flowbits key 'http.rtf' is checked but not ever set.`

I'll break these warnings down and explain them, but first allow me to explain what a flowbit is for those that may not know.

The manual states the following:
	"The flowbits keyword is used in conjunction with conversation tracking from the Stream preprocessor. It allows rules to track states during a transport protocol session. The flowbits option is most useful for TCP sessions, as it allows rules to generically track the state of an application protocol.
	There are eight keywords associated with flowbits. Most of the options need a user-defined name for the specific state that is being checked. This string should be limited to any alphanumeric string including periods, dashes, and underscores. The keywords set and toggle take an optional argument which specifies the group to which the keywords will belong. When no group name is specified the flowbits will belong to a default group. All the flowbits in a particular group (with an exception of default group) are mutually exclusive. A particular flow cannot belong to more than one group."
In other words, flowbits allow you to set and track the state of a flow in between one or more rules. 

Let me explain the two "warning" messages above.

First, the group name of the flowbit that has the "problem" is "`http.rtf`".  In the VRT, we have a naming convention that we use for flowbits, and this name above tells me that this is an "RTF" document being downloaded over HTTP.  In other words, the way the rules are going to be written means that someone on your network has requested an "rtf" document.

`Warning: flowbits key 'http.rtf' is set but not ever checked.`
The above warning means that there is one rule that uses the syntax: "`flowbits:set,http.rtf`", but the rule that "checks" the flowbit isn't turned on.  We are using the condition of the first rule that "sets" the flowbit to use later in other rules.  Let me give you an example rule:

`alert tcp $HOME_NET any -> $EXTERNAL_NET $HTTP_PORTS (msg:"WEB-MISC rtf download attempt"; flow:to_server,established; content:".rtf"; http_uri; flowbits:set,http.rtf;)`

Someone on your network, connecting to "$EXTERNAL_NET" on an HTTP port, making a web request for a .rtf file.  Finally, we set the flowbit tracking the state. 

We can then use an additional rule to check for a vulnerability inside of the ".rtf" file by using the "`isset`" keyword.

`alert tcp $EXTERNAL_NET $HTTP_PORTS -> $HOME_NET any (msg:"EXPLOIT .rtf file is bad!"; flowbits:isset,http.rtf; flow:from_server,established; content:"bad stuff";)`

The above rule checks to see that the flowbit "`isset`" before checking the rest of the rule.  Essentially, in order for the second rule to fire, the first one has to have already fired.

The other warning above is the opposite.

`Warning: flowbits key 'http.rtf' is checked but not ever set.`


This indicates that the rule that reads "`isset,http.rtf`" is turned on, but the rule that reads "`set,http.rtf`" is not.

The above "Warnings" aren't fatal.   Meaning Snort will still start, even if you have these errors.  However, if you don't have one or the other "`set`" or "`isset`" rules turned on and you are receiving these errors, this indicates that effectively you aren't using that set of rules, or multiple rules.

The advantage of flowbits is that rule writers can write several different rules that check for vulnerabilities inside the rtf document file format, all checking to see if the "`http.rtf`" flowbit has been set first.  This will cause entire rule chains to not fire if an "rtf" file isn't downloaded first (for example).

There are two ways to fix this problem.  You can either:
Go through the rules files individually to turn on the rules that will fix the flowbits.
Use a tool that automates this process for you.
The tool that I most often recommend is PulledPork.  PulledPork, aside from managing your rules for you, even resolving and using Shared Object rules correctly, it also auto-resolves flowbit dependancies.  Turning on rules that should be on in order for all of your flowbits to work correctly.

You can read more about flowbits in section 3.6.10 of the [Snort Manual](http://manual.snort.org)
