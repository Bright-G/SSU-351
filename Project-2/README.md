## This Graph demonstrates how additional threads speed up the mean function, in terms of:
<img width="313" height="42" alt="image" src="https://github.com/user-attachments/assets/f6b527ba-1c2c-450d-9fe4-aa3acce453de" />

![This graph shows the relationship between the number of threads and the speedup the program sees compared to using 1 thread](Project-2/Graph.png)
This graph follows a log curve, where each  set of addtional threads increase the speed up less and less,and eventually start to become innefective almost entirely
### Around a speed up around 18 times, the function fails to make more progress with more threads
This means that progress with adding more threads is not linear, and depreciates in effectiveness with this task rather quickly.

## Determining the p-value:

While my understanding of p-values is shaky at best, from the description provided on canvas, when you have more threads to total time taken to compute will only decrease so far.
This is because there is an unavoidable non-parallelized part of the code. So my estimation of p considers that while using the most threads the time taken is:
### 1.87 seconds
and the time with one thread is
### 34.01 seconds
<img width="252" height="558" alt="image" src="https://github.com/user-attachments/assets/7df94c1f-b0d8-49f5-9f61-5d4ffaf18250" />
this means that ~0.0549 of the program cannot be removed through parallelization, or ~0.9451 of the program can be parallelized out of the final time.
Then the p-value would be 0.09451

## As for the data used per iteration?
I beliebve that each read from data is 4 bytes, each read from sums is 8 bytes, and each write to sums is another 8. So in total it takes 20 bytes per iteration.
### Kernel bandwidth:
I'm guessing this can be found by seeing how much data can be processed by each thread in a given amount of time. For the single threaded program it takes 34 seconds to process 1 billion elements, giving an effective bandwidth of 0.12 GB/s
For the multithreaded program it takes 9.5 seconds (about) to process the same number of values. This implies a total bandwidth of 0.42 GB/s, meaning per kernel it is approximately 0.21 GB/s.
That means that the effieciency per kernel is actually greated in the multithreaded approach (seemingly)

# Computing volume:

<img width="668" height="405" alt="image" src="https://github.com/user-attachments/assets/2c0729e0-867a-4ff9-8d33-32bf50e12003" />

While computing volume it is obvious that the speed up from adding more threads is much more linear. This differs from the log curve of the mean code.
