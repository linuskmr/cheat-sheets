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

Demangle rust symbol names by pipeing this into [rustfilt](https://crates.io/crates/rustfilt).

## Show strings in object file

```
$ strings BINARY
```

## Dump sections of a binary

```
$ readelf -x .rodata BINARY
```

## Display table of contents of an .a archive

![](https://fasterthanli.me/content/articles/why-is-my-rust-build-so-slow/assets/c-build-pipeline.5ce1780d188652a1.svg)
> From https://fasterthanli.me/articles/why-is-my-rust-build-so-slow

Many object files (`.o`) can be combined into an `.a` archive file.
You can show the contents via:

```
$ ar t blabla.a
```

## Dynamic linker

Set the environmental variable `LD_DEBUG=all` to see what the linker does at runtime.


### ldd

`ldd` prints shared object dependencies.

Attention: ldd is a bash script, which invokes the executable with the environmental variable `LD_TRACE_LOADED_OBJECTS=1`,
so the executable has to run on the computer executing ldd. If this is not possible,
consider (using readelf to get shared library depenedencies)[#get-shared-library-dependencies-with-readelf].

### Get shared library dependencies with readelf

```
readelf --dynamic BINARY
```

> If you set LD_PRELOAD to the path of a shared object, that file will be loaded before
> any other library (including the C runtime, libc.so). So to run ls with your special
> malloc() implementation, do this:
> 
> `$ LD_PRELOAD=/path/to/my/malloc.so /bin/ls`
>
> — https://stackoverflow.com/a/426260

## printf with string length

`printf("%.*s\n", str_len, str);`

## kill by name

```
$ killall -SIGINT processname
```
