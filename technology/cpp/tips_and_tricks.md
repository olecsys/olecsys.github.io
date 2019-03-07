GCC Environment variables:
* C_INCLUDE_PATH - add include path to C compiler
* CPLUS_INCLUDE_PATH - add include path to C++ compiler
* LIBRARY_PATH - add libraries path to C, C++ linker

So, to remove unused functions, you need:

* Compile with “-fdata-sections” to keep the data in separate data sections and “-ffunction-sections” to keep functions in separate sections, so they (data and functions) can be discarded if unused.
* Link with “--gc-sections” to remove unused sections.

cmake verbose mode:
-DCMAKE_VERBOSE_MAKEFILE:BOOL=ON