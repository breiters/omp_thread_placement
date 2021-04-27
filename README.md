# omp_thread_placement

A little tool to explore the thread placement and pinning of the OpenMP runtime.

# Where did my OMP threads go?

I found it hard to understand, how OMP threads are assigned to the sockets and physical/logical cores, depending on the different OMP environment variables (`OMP_PROC_BIND`, `OMP_PLACES`, `OMP_NUM_THREADS`), so I wrote this [little tool](./omp_threads.c) that prints the initial assignments and also if threads are allowed to move during the execution.

Maybe it helps someone (link with OMP when compiling). Feel free to edit / distribute.

---

It also lead to the following observation:

If you do not set `OMP_PROC_BIND`, but set `OMP_PLACES=sockets`, threads can move between different logical cores during the execution, but only on their initial socket -- they are pinned to a socket.

If you do not set `OMP_PROC_BIND`, but set `OMP_PLACES=cores`, threads can move between different logical cores during the execution, but only on their initial physical core -- they are pinned to a physical core.

If you do not set `OMP_PROC_BIND`, but set `OMP_PLACES=threads`, threads are pinned to logical cores and can not move at all -- they are pinned to a logical core (hw-thread).
