The questions that I receive the most often via my Inbox is "What are Shared Object rules?", or "How do I use them?"

Commonly referred to as "Shared Object rules", "SO rules", "pre-compiled rules", or "Shared Objects" are detection that is written in the Shared Object rule language, which is, essentially, "C".   This allows for primarily two things for the Snort platform:

Detection that is not possible under the regular Snort rules language.  Since Shared Object rules are "C" based, they can essentially be coded to detect a much greater set of conditions than regular Snort rules can.   One of the common misconceptions about Shared Object rules are that they are closed source, and while under certain conditions ([2] below) that may be true, they are not inherently closed source.  You can, in fact write your own shared object rules, or even run your rules through the shared object generator to see how shared object rules are structured.  Check out this blog post on the VRT blog for more information on that.
It allows for obfuscation of exact detection in the rule language.  Under certain conditions (Agreements with vendors, use of Shared Object rules in 'classified' environments, Sourcefire 0-day detection, etc) it may be necessary to obfuscate how detection is performed with a particular rule.   Since Shared Object rules have to be compiled in order to use them, that's why the VRT distributes "pre-compiled" rules.  
The VRT distributes shared object rules on a variety of platforms, easy to install and use. 

However, some may be finding it difficult to use the rules, so let me point you to a couple guides.  One guide is here, on Snort.org, at the bottom of the "platform" list.  The VRT also has a blog post that can help you install the Shared Object rules.

But, by far, the easiest way to use Shared Object rules reliably is through the configuration and use of a tool called PulledPork.  After the configuration of PulledPork, the tool will generate the Shared Object rule stubs for you, and place everything in the correct directories for ease of use.  This is amongst the many features of PulledPork (including flowbit dependency resolving) which are useful.

In order to subscribe now to the VRT's newest rule detection functionality, you can subscribe for as low as $29 US dollars a year for personal users, be sure and see our business pricing as well at https://www.snort.org/products.  Make sure and stay up to date to catch the most emerging threats!
