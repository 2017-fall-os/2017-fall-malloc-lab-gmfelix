# os-malloc
This directory contains:

myAllocator.c: a first-fit allocator
myAllocator.h: its header file

myAllocatorTest1.c: a test program for my allocator 

malloc.c: a replacement for malloc that uses my allocator
test1.c: a test program that uses this replacement malloc

There are two different testers as some implementations of printf
call malloc to allocate buffer space. This causes test1 to behave
improperly as it uses myAllocator as a malloc replacement. In this
case myAllocatorTest1 will function correctly. The only difference
between the programs is that test1 uses myAllocator as a malloc
replacement and myAllocatorTest1 uses myAllocator directly.

Makefile: a fairly portable "makefile", targets "all" and "clean"

To compile: 
 $ make 
To clean:
 $ make clean

The cygwin runtime uses malloc() and brk() extensively.  It is
interesting to compare the output of test1 & myAllocatorTest1.  All
those extra allocated regions are being used by cygwin's libraries!

<h3> Work done </h3>

The method findBestFit is used to find the block that best fits the amount of memory required.
First, findBestFit finds the first fit using the method provided: "findFirstFit".
Once a match has been found, the method tries to find a better fit than the one provided, if so, it returns that one. Otherwise, just return the first fit.
BestFitAllocRegion allocates a block that satisfies the space needs, makes it free by adding the prefix and suffix, and then allocates it before returning the pointer to the beginning of the usable space.

resizeRegion was modified in order to coalesce the next region, if enough space is available, to the current region in order to expand the memory space.

During this lab I worked with Jose Cabrera in order to exchange ideas on how to solve the resize region problem

