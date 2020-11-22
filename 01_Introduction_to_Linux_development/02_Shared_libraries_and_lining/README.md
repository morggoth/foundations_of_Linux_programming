Here we created Hello World, which is splitted to separate modules.

## Step by step building of the program

```bash
# Just compile a separate modules
gcc -o hello.o -c hello.c
gcc -o main.o -c main.c

# Link oblect files into single executing bunary
gcc -o hello hello.o main.o
```

## Compile a shared library

```bash
gcc -o libHello.sh -shared -fPIC hello.c
# the -fPIC flag is required on x64 hosts
```

To find name of the our function in .so we can use _nm_ command. It lists symbols from object files.

```bash
nm libHello.so
```

## Compile the binary with shared library

```bash
gcc main.c -L. -lHello -o hello_shared
```

Where:

- -L flag contains a path where our .so is storred
- -l flsg contains _main_ name of required .so (withoit 'lib' prefix and '.so' postfix)

Order of arguments is very important here.

But builded in this way programm will failed, because system don't know about our .so file. We have to register .so in system ld service and we have multiple options here:

- put a .so in knows directory for shared libreries like _/lib_ and _/usr/lib_
- set env vars:
  - LD_PRELOAD
  - LD_LIBRARY_PATH

```bash
LD_LIBRARY_PATH=. ./hello 	# this must work
```

One more usefull utility is _ldd_, which is print shared object dependencies.
