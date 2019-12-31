# kProbes

Reference:

- [Kprobes](https://www.kernel.org/doc/Documentation/kprobes.txt)
- [Kprobes internals](https://lse.epita.fr/lse-summer-week-2017/slides/lse-summer-week-2017-03-kprobes-internals.pdf)

# Introduction

According to the documentation of Linux kernel, Kprobes enables you to dynamically break into any kernel routine and collect debugging and performance non-disruptively. You Can trap at almost any kernel code address, specifying a handler routine to be invoked when the breakpoint is hit.

Two types of Kprobes currenty available: Kprobes, and Kretprobes.

A Kprobe can be inserted on virtually any instruction in the kernel. However, Kretprobes can only be fired when a specific function returns.

# How does a Kprobe work?

Kprobe firstly copies the insructions that will be probed, and replace the first byte(s) of the probed instruction with a breakpoint instruction (e.g., int3 on i386 and x86_64).

During the execution time, when the probe point is hit, a trap occurs, CPU's context is saved along with stack information. Then the control passed to Kprobe via notifier_call_chain mechanism. Kprobes executes the "pre_handler" associated with the Kprobe, passing the handler the address of the Kprobe struct and the saved registers.

Next, Kprobe single-steps its copied instructions which is made when Kprobe is registered. And finally, after each instruction is triggered, Kprobe executes the "post_handler", if we registered it before. After the process all above, Kprobe releases the control and continue to execute instruction following the breakpoint.

