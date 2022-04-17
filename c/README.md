# C/C++

## See where a `SIGSEGV` occured.

```
$ make && gdb --args ./executable
...
> r (run)
...
> bt (backtrace)
...
```

## Using [strace](https://man7.org/linux/man-pages/man1/strace.1.html) to record all called system calls

`-f`: Follow child processes

```
& make && strace -f ./executable
```

## Load core dump

```
$ gdb program core
```

## Examine process's mapped files

Show files that are mapped into a process and their rights (read, write, executable).

```
$ gdb
> starti
> info proc
process <ID>
...
(gdb has to keep running)
$ cat /proc/<ID>/maps
```

## Show symbols from object file

```
$ nm --demangle BINARY
```

## Show strings in object file

```
$ strings BINARY
```
