# Make Libraries with CMake

Creating a shared or static library using CMake

## Phase 1: Traditional Method (without CMake)

```console
cd src
gcc -c -Wall -Werror -fpic hello.c
gcc -shared -o libhello.so hello.o
gcc -L/home/mp/coding/desktop/c-libs -Wall -o main main.c -lhello
export LD_LIBRARY_PATH=$PWD:$LD_LIBRARY_PATH
./main
```
The above commands should generate these three files:

```
hello.o
libhello.so
main
```

To understand the exact meaning of the commands read this article:

[Shared libraries with GCC on Linux](https://www.cprogramming.com/tutorial/shared-libraries-linux-gcc.html#fn:pic)
