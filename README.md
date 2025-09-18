# Final Workshop Alejandro

## Flags used for the compilation 

- `-fopenmp` -> This flag enables the compilation of the code that uses OpenMP directives.
- `-Ofast` -> This flag enables aggressive optimizations, including flags like `-O3` `-ffast-math` `-fallow-store-data-races`. The important thing about this flag is that, unlike `-O3`, this flag sacrifices some precision in math operations for faster execution.

**Complete compilation line**

`gcc -o bin/mmm mmm_implementation.c -fopenmp -Ofast`

## Difficulties and how I approached them
The main difficulty was knowing what I could do to optimize the execution time and where I could find that information. It was my first time exploring OpenMP tools and compiler flags.

These difficulties were primarily solved by reading various resources that seemed to offer solutions to my problems. Also, when I reached a dead end, I asked for tips and tricks that some of my friends already knew. This way, I was able to investigate specific topics and discover more information in general.

Terminal usage, C language, and compilation of the program were not a problem at all. 

## Some support references on the research
**OpenMP**
- [Mastering OpenMP Performance](https://www.openmp.org/wp-content/uploads/openmp-webinar-vanderPas-20210318.pdf)
- [Introduction to OpenMP](https://carleton.ca/rcs/rcdc/introduction-to-openmp/)
- [OpenMP Application Programming Interface Examples](https://www.openmp.org/wp-content/uploads/openmp-examples-6.0.pdf)

**Flags for compilation**
- [Beware of fast-math](https://simonbyrne.github.io/notes/fastmath/#title)
- [Options That Control Optimization](https://gcc.gnu.org/onlinedocs/gcc/Optimize-Options.html)

## Results on Apolo
