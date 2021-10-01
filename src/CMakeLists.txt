cmake_minimum_required(VERSION 3.4)

# Project Name
project(HelloLibrary)

# Generate shared / static librarry for hello.c
# STATIC generates `libhello.a`
# SHARED geneartes `libhello.so`
add_library(hello SHARED hello.c)

# Genarete `main` executable from `main.c`
add_executable(main main.c)

# Link `main` program with `hello` library
target_link_libraries (main hello)

# Note: Order of CMake commands is important!