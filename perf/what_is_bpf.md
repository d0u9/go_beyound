# What is BPF

References:

- [Ref 1](http://www.brendangregg.com/bpf-performance-tools-book.html)
- [Ref 2](https://lwn.net/Articles/740157/)

## Intro

Berkeley Packet Filter (BPF) is an in-kernel execution engine that processes a virtual instruction set, and has been extended recently (aka eBPF) for providing a safe way to extend kernel functionality.

In some ways, eBPF does to the kernel what JavaScript does to websites: it allows all sorts of application to be created.

The original BPF runs in a small set of RISC instructions which cannot fit the modern processors, usually 64-bits and multi-cores. So the eBPF is introduced to take advantage of advances in modern hardware. One of the most notable changes was a move to 64-bit registers and an increase in the number of registers from two to ten. Plus, a new BPF_CALL instruction made it possible to call in-kernel functions cheaply.

Originally, eBPF was only used internally by the kernel and cBPF programs were translated seamlessly under the hood. But with [commit daedfb22451d in 2014][1], the eBPF virtual machine was [exposed directly to user space][2].

[1]: https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=daedfb22451dd02b35c0549566cbb7cc06bdd53b
[2]: https://lwn.net/Articles/603983/

## What can you do with eBPF?

An eBPF program is "attached" to a designated code path in the kernel. When the code path is traversed, any attached eBPF programs are executed. Given its origin, eBPF is especially suited to writing network programs and it's possible to write programs that attach to a network socket to filter traffic, to classify traffic, and to run network classifier actions. It's even possible to modify the settings of an established network socket with an eBPF program.

Another type of filtering performed by the kernel is restricting which system calls a process can use. This is done with seccomp BPF.

eBPF is also useful for debugging the kernel and carrying out **performance analysis**; programs can be attached to tracepoints, kprobes, and perf events. Because eBPF programs can access kernel data structures, developers can write and test new debugging code without having to recompile the kernel. The implications are obvious for busy engineers debugging issues on live, running systems. It's even possible to use eBPF to debug user-space programs by using Userland Statically Defined Tracepoints.

The power of eBPF flows from two advantages: it's fast and it's safe. To fully appreciate it, you need to understand how it works.

