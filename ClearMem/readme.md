... here is a little experimental tool, which can free some physical RAM on your system (flushing the system cache, reducing the processes workingsets, empty the modified list and empty the standby list) ...

Use this tool, if your tbbmalloc malloc_xxxx.log shows **early fallbacks** to 'single pages' (fallback to SP).
Because i can't reproduce such fallbacks on my system (even if i reduce my phys. RAM to 6GB),
i can't really verify the success of this tool.

So this tool may or may not help you to make more 'large pages' available. Just try it out.

This tool must be started as administrator OR the user account, which you use to launch it, must have the following privileges granted:

**'Adjust memory quotas for a process'**   
**'Profile single process'** 

If this tool really help, i could integrate the functionality in 'tbbmalloc for arma'

Let me know,
Fred41