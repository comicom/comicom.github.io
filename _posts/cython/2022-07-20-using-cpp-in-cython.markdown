---
layout: posts
title:  Using C++ in Cython
date:   2022-07-20 21:30:46 +0900
categories:
  - Cython
tags:
  - language
  - C
  - C++ 11
  - Cython
  - Python
---

version: 3.0.0a10

# Overview

  - Specify C++ language in a setup.py script or locally in a source file.
  - Create one or more .pxd files
  - cimport them in one or more extension modules (.pyx files).

# Tutorial

## Preview

  1. Write C++ API (.cpp/.h files)
  2. Declaring a C++ class interface (A.pxd file)
  3. Declare class with cdef cppclass (A.pxd file)
  4. Declare a var with the wrapped C++ class (B.pxd file)
  5. Create Cython wrapper class (B.pxd file): ** to make this accessible from external Python code **
  6. Compilation and Importing (setup.py)

example codes: https://github.com/comicom/cython_test

ref.

http://docs.cython.org/en/latest/