# SSU-351
A great class from a funny professor (Computer Architecture)
* Project 1


# Data Charts
* Optimization difference, at NUM_BLOCKS 1000000 (Time average of 10 trials in seconds)

| OPT | alloca | list | malloc | new |
| --- | --- | --- | --- | --- |
| -O2 | 0.194000 | 0.293000 | 0.221000 | 0.288000 |
| -O1 | 0.255000 | 0.295000 | 0.222000 | 0.292000 |
| -g | 0.579000 | 1.909000 |0.473000|1.749000|

* NUM_BLOCK difference, at OPT -O2 (Time average of 10 trials in seconds)

| NUM_BLOCKS | alloca | list | malloc | new |
| --- | --- | --- | --- | --- |
| 10000 | 0.000000 | 0.002000 | 0.000000 | 0.003000 |
| 1000000 | 0.194000 | 0.293000 | 0.221000 | 0.288000 |
| 50000000 | 9.640000 | 14.438000 | 10.717000 |14.152000 |

* DATA per NODE test, max and min set to the same number, NUM_BLOCKS 100000, OPT -O2 (Time average of 10 trials in seconds)

| MIN/MAX SIZE | alloca | list | malloc | new |
| --- | --- | --- | --- | --- |
| 10 | 0.095000 | 0.192000 | 0.123000 | 0.193000 |
| 100 | 0.435000 | 0.541000 | 0.487000 | 0.517000 |
| 1000 | 3.883000 | 3.919000 | 3.740000 | 3.907000 |
| 10000 | 36.233000 | 38.081000 | 35.434000 | 36.310000 |

* Number of BREAKS, OPT -O2 (Time average of 10 trials in seconds)

| NUM_BLOCKS | alloca | list | malloc | new |
| --- | --- | --- | --- | --- |
| 10000 | 69 | 156 | 137 | 156 |
| 100000 | 69 | 933 | 751 | 933 |
| 1000000 | 69 | 8711 | 6888 | 8711 |
| 10000000 | 69 | 86480 | 68251 | 86480 |

# Questions
1. # Which program is fastest? Is it always the fastest?
   
   The fastest of the programs is alloca, which finished first in the majority of situations by a noticible margin. It outperformed both list and new every single time, while falling behind malloc only when the size of data per node began to get large, (finsing in 36.233000 seconds compared to malloc's 35.434000 seconds).

2. # Which program is slowest? Is it always the slowest?

   The over all slowest of the programs is list, although it is faster compared to new on several occasions, typically during the faster trials. For example during the data size trial it is faster at 0.192000 seconds compared to the 0.193000 of new.

3. # Was there a trend in program execution time based on the size of data in each Node? If so, what, and why?

   There is a trend that the larger the size of the data, the longer the execution takes. Larger data requires more memory and therefor takes additional time to allocate and hash, drastically increasing time once data size gets bigger. At a data size of 10000 each trial was taking an average of far above 30 seconds to complete. (Took so long I had time to watch an episode of a show)

4. # Was there a trend in program execution time based on the length of the block chain?

   There was also a trend where the length of the block chain increased execution time. This makes sense because with more nodes there is more data to hash and allocate memory for. This trend is slower growing than that of data size though.

5. # Consider heap breaks, what's noticeable? Does increasing the stack size affect the heap? Speculate on any similarities and differences in programs?

  Increasing the stack size by adding more data effects heap breaks for all programs except for alloca, which remains the same between each amount. This is likely due to the fact that is allocates to the stack dynamically, meaning that the amount it allocates to the heap is unafffected. Malloc allocates more data to the stack then new and list, but all three of them take full advantage of the heap and therefor have more heap breaks, which also takes longer.

6. # Considering either the malloc.cpp or alloca.cpp versions of the program, generate a diagram showing two Nodes. Include in the diagram:
* the relationship of the head, tail, and Node next pointers.
* show the size (in bytes) and structure of a Node that allocated six bytes of data
* include the bytes pointer, and indicate using an arrow which byte in the allocated memory it points to.


| HEAD        | NumBytes 6 |
|-------------|------ |
| *NEXT  | *bytes |
    |         |
    |          -------------V
    V          &NumBytes |  0  |  1  |  2  |  3  |  4  |  5  |
| TAIL        | NumBytes n |
|-------------|------ |
| *NEXT  | *bytes |

This is a standard linked list with a next pointer and pointers for head and tail. The difference is that each one has a bytes pointer, which points the size of Size type past the numBytes location in memory.

7. # There's an overhead to allocating memory, initializing it, and eventually processing (in our case, hashing it). For each program, were any of these tasks the same? Which one(s) were different?

  List and new both do things in very much the same way. The only difference is that list uses more of what is built into c++, while new is a much more familiar implementation of a linked list. They often have times that are identical, and share in ther number of heap breaks. Alloca and Malloc are similar in some ways, such as their node structure, but differ greatly in where their memory is allocated and when. They all share their hashing process, or at least they looked identical to me between each of their files.

8. # As the size of data in a Node increases, does the significance of allocating the node increase or decrease?

   The signifigance increases, as time is greatly affected by data size, regardless of which program. In fact the size of the data appeared to have the greatest impact of each of the tested catagories. This is likely due to the need to allocate more memory for bigger data points.
