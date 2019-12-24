# First contact with eBPF

References:

- [Ref 1](http://www.brendangregg.com/ebpf.html)


## Basic to eBPF

A BPF bytecode can be accepted and attached to 4 diefferent event sources:

- **kprobes**: kernel dynamic tracing.
- **uprobes**: user level dynamic tracing.
- **tracepoints**: kernel static tracing.
- **perf_events**: timed sampling and PMCs.

A BPF program has **two** ways to pass measured data back to userspace:

- **per-event details**
- **BPF map**

## Front End

### bcc

Abbreviation of BPF Compiler Collection.
GITHUB; https://github.com/iovisor/bcc

For old kernels, you maybe need to check `tools/old` for a legacy version.

Example tracing code can be found in the `examples/tracing` and `tools/` directories.

Usually bcc is located `/usr/share/bcc`, you need to manually add `toos/` directories to your PATH environment.

### bpftrace

Is a high-level front-end for BPF tracing, which uses libraries from bcc.

## BCC examples

For a quick view, we copy-paste examples from [brendangregg's blog][1].

