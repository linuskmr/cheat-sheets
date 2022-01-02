# C/C++

See where a `SIGSEGV` occured.

```
$ make && gdb --args ./executable
...
> r (run)
...
> bt (backtrace)
...
```

Using [strace](https://man7.org/linux/man-pages/man1/strace.1.html) to record all called system calls.

```
& make && strace ./executable
```
