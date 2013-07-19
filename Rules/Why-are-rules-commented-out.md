There are four states that we place rules in when we create them, three of the states are assigned to policies.
- Connectivity over Security (Connectivity)
	- Either in "alert" or "drop"
- Balanced (Balanced)
	- Either in "alert" or "drop"
- Security over Connectivity (Security)
	- Either in "alert" or "drop"

The last state is "in no policies".

We have some general rules of thumb for these, as outlined below.  These are flexible in meaning as well, and are simply guidelines.

1. The first, connectivity, means "Connectivity over Security".  Meaning this is a speedy policy for people that insist on blocking only the really known bad with no false positives. 
	-  CVSS Score = 10
	-  CVE year is current - 2 (So, for example, 2013, 2012, 2011)

2. The second, balanced, means "Balanced between Connectivity and Security".  Meaning that this is a good starter policy for everyone.  It's quick, has a good base coverage level, and covers the latest threats of the day.  The policy contains everything that is in Connectivity.
	-  CVSS Score >= 9
	-  CVE year is current - 2 (For example, 2013, 2012, 2011)
	-  MALWARE-CNC rules
	-  EXPLOIT-KIT rules
	-  SQL Injection rules
	-  Blacklist rules

3. The third, security, means "Security over Connectivity".  Meaning that this is a stringent policy that everyone should strive to get to through tuning.  It's coverage is much more exhaustive, and has some policy-type rules in it.  Rules that will alert on Flash contained within an Excel file and things like that.  This policy contains everything that is in the first two.
	-  CVSS Score >= 8
	-  CVE year is current -3 (For example, 2013, 2012, 2011, 2010)
	-  MALWARE-CNC rules
	-  EXPLOIT-KIT rules
	-  SQL Injection rules
	-  Blacklist rules
	-  App-detect rules

The last state is "in no policies".  This means that we insist that you look through these by product name or CVE in order to turn them on.  These may not have a fast content match, could be false positive prone, or the vulnerability it is covering is not in a very prevalent piece of software.  

The way we make the decision about what is "on" or "off" by default when you aren't using the policies, is, if it's in balanced, it's on by default, it's it not in balanced, it's off by default.  There are a ton of exceptions to these rules, but this is the general rule of thumb for the default states.

The "alert" and "drop" determination is based upon false positive rate, alert rate and a host of other factors, it's rule independent.
