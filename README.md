# Make Libraries with CMake

Creating a shared or static library using CMake

## Phase 1: Traditional Method (without CMake)

### Create an object file for `hello.c`

```console
cd src
gcc -c -Wall -Werror -fpic hello.c
```

The command above should generate this file:

```
hello.o
```
### Create a shared library for `hello.c`

```console
gcc -shared -o libhello.so hello.o
```

The command above should generate this file:

```
libhello.so
```
To understand the purpose of these commands read this article:

[Shared libraries with GCC on Linux](https://www.cprogramming.com/tutorial/shared-libraries-linux-gcc.html)

### Create a static library for `hello.c`

Having file `hello.o` we can create a static library for it using the following command.

```console
ar -rc libhello.a hello.o 
```

The command above should generate this file:

```
libhello.a
```

Fore more information read this article:

[How to Create and Use a C Static Library](https://medium.com/@eightlimbed/how-to-create-and-use-a-c-static-library-eec33d502aeb)

### Compile `main.c` program 

The `main.c` program uses the `Hello` function from `libhello` library. So we must use the `libhello.so` shared library or `libhello.a` static library to compile `main.c` program

```console
gcc -L. -Wall -o main main.c -lhello
```

The command above by default uses `libhello.so` shared library if it doesn't exist GCC looks for `libhello.a` static library.

If you want to make it use only `libhello.a` static library you should use this command:

```console
gcc -L. -Wall -o main main.c -l:libhello.a
```

Now run the `main` generated executable:

```console
./main
```

**The difference between shared and static libraries can be seen here.**

If you use `libhello.a` static library, `main` executable embeds `Hello()` function in itself and does not need the `libhello.a` file anymore.

But if you use `libhello.so` shared library, you will get an error message after execution of `./main`. Because the `main` executable needs the `libhello.so` file to call `Hello()` function.

To solve this problem for shared libraries there are many solutions which two of them is mentioned here:

- [GOOD SOLUTION] Open terminal in the directory where `libhello.so` exists and execute this command to tell the Linux that where the `libhello.so` is located.

```console
export LD_LIBRARY_PATH=$PWD:$LD_LIBRARY_PATH
```
- [BAD SOLUTION] Embed the "path" to the `libhello.so` in the `main` executable using GCC.
This is not a good solution because if you move `libhello.so` to other location this solution becomes useless!

```console
gcc -L. -Wall -Wl,-rpath=$PWD -o main main.c -lhello
```

[RPATH and RUNPATH](http://blog.tremily.us/posts/rpath/)

### Use `readelf` command

To see the list of shared libraries which the `main` executable needs, use this command:

```console
readelf -d main
```


