# Final Workshop Alejandro

## OpenMP directives

```C
#pragma omp parallel default(none) shared (size,A,B,C) private (i,j) // Ideal way of initializing variables with NUMA nodes
        {

            #pragma omp for schedule(static)

            for(i = 0; i < size; i++){
                for(j = 0; j < size; j++){
                    A[j][i] = 1 + ((double)rand() / RAND_MAX) * MAX_NUM;
                    B[j][i] = 1 + ((double)rand() / RAND_MAX) * MAX_NUM; 
                    C[j][i] = 0;
                }
            }

        }
```
According to some documentation, `Mastering OpenMP Performance`, using this structure is a more NUMA friendly data initialization.

```C
#pragma omp parallel for collapse (3)
        //#pragma omp simd

            for(j = 0; j < size; j++){
                for(int k = 0; k < size; k++){
                    for(i = 0; i < size; i++){
                        C[i][j] += A[i][k] * B[k][j];
                    }
                }
            }

```

Using these directives, we convert those three for loops into one, making us have a higher number of data points but only one loop. Also, this enables SIMD operations, so we can vectorize the operations done on the matrices.

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
| JobID   | JobName     | Partition | State      | Elapsed | TotalCPU | MaxRSS   |
|---------|-------------|-----------|------------|---------|----------|----------|
| 100458  | MMM-SCAR-+  | learning  | COMPLETED  | 00:03:23| 01:43:06 |          |
| 100458.batch | batch  |           | COMPLETED  | 00:03:23| 01:43:06 | 134768K  |

***From the .out file***

Size of matrices: 2349

Running time: 123.730780

