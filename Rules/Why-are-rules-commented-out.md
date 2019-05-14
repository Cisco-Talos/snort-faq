There are five states that we place rules in when created, four of the states are assigned to policies.

- Connectivity over Security (Connectivity)
	- Either in "alert" or "drop"
- Balanced (Balanced)
	- Either in "alert" or "drop"
- Security over Connectivity (Security)
	- Either in "alert" or "drop"
- Maximum Detection (max-detect)
	- Either in "alert" or "drop"

The last state is "No policy".

These policies are maintained by the metadata keyword in the Snort rules language. Each of the default policies is defined below and the requirements for adding a rule to a particular category are outlined and explained.

The criteria and rule category is logically an "OR" condition.

For example for **Balanced**, if the CVSS score is 9 and the vulnerability year is within the last 3 years. It should be in that policy. 
OR if the category of the rule is MALWARE-CNC, BLACKLIST, SQL-INJECTION, or EXPLOIT-KIT it should be in that policy. 

1. **Connectivity over Security**
	1. This policy is specifically designed to favor device performance over the security controls in the policy. It should allow a customer to deploy one of our devices with minimal false positives and full rated performance of the box in most network deployments. In addition, this policy should detect the most common and most prevalent threats our customers will experience. 
	2. *Criteria*:
		1. CVSS Score = 10
		2. CVE year is current - 2 (So, for example, 2019, 2018, 2017)
2. **Balanced**
	1. This policy is the default policy that is recommended for initial deployments. This policy attempts to balance security needs and performance characteristics. Customers should be able to start with this policy and get a very good block rate with public evaluation tools, and relatively high performance rate with evaluation and testing tools. *It is the default shipping state of the Snort Subscriber Ruleset for Open-Source Snort.*
	2. *Criteria*:
		1. CVSS Score >= 9
		2. CVE year is current - 2 (For example, 2019, 2018, 2017)
		3. MALWARE-CNC rules
		4. EXPLOIT-KIT rules
		5. SQL Injection rules
		6. Blacklist rules
		7. Includes the rules in the **Connectivity over Security** policy.
3. **Security over Connectivity**
	1. This policy is designed for the small segment of our customer base that is exceptionally concerned about organizational security. Customers deploy this policy in protected networks, that have a lower bandwidth requirements, but much higher security requirements. Additionally, customers care less about false positives and noisy signatures. Application control, and locked down network usage are also concerns to customers deploying this policy. It should provide maximum protection, and application control, but should not bring the network down.
	2. *Criteria:*
		1. CVSS Score >= 8
		2. CVE year is current -3 (For example, 2019, 2018, 2017, 2016)
		3. MALWARE-CNC rules
		4. EXPLOIT-KIT rules
		5. SQL Injection rules
		6. Blacklist rules
		7. App-detect rules
		8. Includes the rules in the **Connectivity over Security** and **Balanced** policies.
4. **Maximum Detection**
	1. This ruleset is meant to be used in testing environments and as such is not optimized for performance. False Positives for many of the rules in this policy are tolerated and/or expected and FP investigations will normally not be undertaken. 
	2. *Criteria:*
		1. The coverage is required for in field testing
		2. Includes rules in the Security, Balanced, and Connectivity rule sets.
		3. Includes all active rules above Sid:10000, unless otherwise specified.

Tlast state is "in no policies".  This means that we insist that you look through these by product name or CVE in order to turn them on.  These may not have a fast content match, could be false positive prone, or the vulnerability it is covering is not in a very prevalent piece of software.  

**Miscellaneous Policy Information**

Rules in the listed policies are evaluated on a rule by rule basis. There will be some rules that are older and not in the criteria above that will be in the default policies. The above is the selection criteria for default rules, and is always subject to change based upon the threat landscape