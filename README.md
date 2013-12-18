... this is an **experimental** replacement for armas default **custom memory allocator** ...

This custom memory allocator is based on the latest **intel tbb malloc 4.2, updt. 2** and should work with arma server and client.

You can find the source code of intels tbb 4.2, updt. 2 here:

[https://www.threadingbuildingblocks.org/sites/default/files/software_releases/source/tbb42_20131118oss_src.tgz](https://www.threadingbuildingblocks.org/sites/default/files/software_releases/source/tbb42_20131118oss_src.tgz)

and some general infos about custom memory allocator for arma and the BIS interface description can be found here:

[http://community.bistudio.com/wiki/ArmA_2:_Custom_Memory_Allocator](http://community.bistudio.com/wiki/ArmA_2:_Custom_Memory_Allocator)

This project is covered by the same license as provided with the source code from intel (GPL 2.0).

Some small optimizations in the interface, a little workaround, adaption of some internal parameters and the fact, that this allocator allocates memory regions in **large pages** (2048kB), instead of **small pages** (4kB) results in better performance, compared with the default allocator tbb4malloc_bi.dll. 

This allocator works best/only on 64 bit OS, with at least 8GB RAM.


HOW TO USE:

Copy **tbbmalloc.dll** in your arma3/dll directory.
append **-malloc=tbbmalloc** to your arma 3 start line.

**tbbmalloc** is prefer to use RAM in **large pages** (2048kB instead of 4kB).

The use of large pages requires the **lock pages in memory privilege** for the arma user.

Make sure your arma user account has this privilege set in your **local security policies** settings (secpol.msc, restart required). If your useraccount, which you use to start arma, is member of the **administrator group**, you have to start arma **as administrator**!

On client, i measured between 6-9% higher framerates with "Helos A3-bench". Especially in  multiplayer games,
i noticed significant smoother gameplay (higher and more stable framerates), for longer running sessions. On server i have no benchmark, but it should accelerate here too, dependend on mission and server load.   

This test version logs some timing data to **malloc_PIDX.log** and it would be helpful, if you could post me your logfile results in BIS forum (server&administration), together with some info about your system (OS, RAM, CPU) and test conditions, like arma build, server or client, mission running.

The tbbmallocs logfile looks like in this example:

    SeLockMemoryPrivilege: granted, huge pages enabled

	0.000s: 0.117ms  2048k at:0xffc00000 Alloc LP
	0.000s: 0.001ms   128k at:0x01ec0000 Alloc SP
	0.015s: 0.362ms  8192k at:0xff400000 Alloc LP
	0.593s: 0.199ms  4096k at:0xff000000 Alloc LP
	0.593s: 0.174ms  4096k at:0xfec00000 Alloc LP
	0.593s: 0.174ms  4096k at:0xfe800000 Alloc LP
	.....

The first line for example tells you, that the required privileg is set correctly.     
(LP means large pages, SP means small pages)



IMPORTANT:   
The goal of this little research project, is to verify the performance gain by using large pages for memory allocations and some other optimizations.
   
So this project will not provide a permanent replacement for the default memory allocator. 
Instead the results will be provided to BIS and hopefully help to improve the default memory allocator as part of the arma distribution.



Greets and let me know your results,
Fred41
