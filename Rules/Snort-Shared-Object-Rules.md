# Snort Shared Object Rules #

Commonly referred to as "Shared Object rules", "SO rules", "pre-compiled rules", or "Shared Objects" are detection that is written in the Shared Object rule language, which is, [essentially, "C"](https://en.wikipedia.org/wiki/C_(programming_language)).   This allows for primarily two things for the Snort platform:

1. Detection that is not possible under the regular Snort rules language.  Since Shared Object rules are "C" based, they can essentially be coded to detect a much greater set of conditions than regular Snort rules can.   One of the common misconceptions about Shared Object rules are that they are closed source, and while under certain conditions that may be true, they are not inherently closed source.  You can, in fact write your own shared object rules
2. It allows for obfuscation of exact detection in the rule language.  Under certain conditions (Agreements with vendors, use of Shared Object rules in 'classified' environments, Sourcefire 0-day detection, etc) it may be necessary to obfuscate how detection is performed with a particular rule.   Since Shared Object rules have to be compiled in order to use them, that's why Talos distributes "pre-compiled" rules.  

Talos distributes shared object rules on a variety of platforms, easy to install and use. 

However, some may be finding it difficult to use the rules, so let me point you to a couple guides. Talos has a [blog post](http://blog.talosintel.com/2009/01/using-vrt-certified-shared-object-rules.html) that can help you install the Shared Object rules.

But, by far, the easiest way to use Shared Object rules reliably is through the configuration and use of a tool called [PulledPork](https://github.com/shirkdog/pulledpork).  After the configuration of PulledPork, the tool will generate the Shared Object rule stubs for you, and place everything in the correct directories for ease of use.  This is amongst the many features of PulledPork (including flowbit dependency resolving) which are useful.
