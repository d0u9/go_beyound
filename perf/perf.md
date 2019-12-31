# perf

Reference:

- [perf Examples](http://www.brendangregg.com/perf.html)
- [perf Tutorial](https://perf.wiki.kernel.org/index.php/Tutorial)

# Introduction

**perf** is a Linux system command which utilizes the power of varies Linux trace mechanisms to profile the Linux OS on the fly. **perf** is based on the **perf_events** interface exportd by recent versions of the Linux kernel.

It provides a unity tool to trace different activities the Kernel is behaving from the bottom CPU to upper layer of applications running in usersapce, written in advanced programming language such as JS or JAVA.

Perf can answer questions such as:

- Why is the kernel on-CPU so much? What code-paths?
- Which code-paths are causing CPU level 2 cache misses?
- Are the CPUs stalled on memory I/O?
- Which code-paths are allocating memory, and how much?
- What is triggering TCP retransmits?
- Is a certain kernel function being called, and how often?
- What reasons are threads leaving the CPU?


