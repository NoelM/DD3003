## Report for lab on OpenMP

1. I simply modified the two existing print statements in the
source file so that they read `printf("Starting on %i threads\n", omp_get_max_threads());`
and `printf("Hello World from thread %i!\n", omp_get_thread_num());`, respectively.

2. I predict it will print 8 copies of "a= 110 b= 10"... It did not, it printed
8 copies of "a= 10 b= 10. Ok, I see, the variable set as private is not _really_
the one which got assigned to 100 before we set it private; it got cleared
when it was set as private.

When using `firstprivate` the results seem more sensible.
The `lastprivate` command will set the original `a` to the
last value it is set to in a thread after they have all finished.
It might be useful for example when performing some local sumation
and one want the last pertial sum to have been applied.

3. When doubling the threads, starting from 1, one notices that
the runtime decreases (from 8.8 seconds) up until one reaches
128 threads (1.10 seconds), after which the execution time
starts increasing again.

I found `guided` with chunk size `1` to be quickest
at 1.126866 (for 8 threads).

4. 