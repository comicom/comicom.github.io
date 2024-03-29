---
layout: posts
title:  Introduction to Cython
date:   2022-07-20 02:31:46 +0900
categories:
  - Cython
tags:
  - language
  - C
  - C++ 11
  - Cython
  - Python
comment: true
---

version: 3.0.0a10

# Overview

Cython is a programming language that makes writing C/C++ extensions for the Python language as easy as Python itself. The source code gets translated into optimized C/C++ code and compiled as Python extension modules. This allows for both very fast program execution and tight integration with external C libraries, while keeping up the high programmer productivity for which the Python language is well known.

Type declarations can therefore be used for two purposes: for moving code sections from dynamic Python semantics into static-and-fast C semantics, but also for directly manipulating types defined in external libraries.


# Installing Cython

Unlike most Python software, Cython requires a C compiler to be present on the system. The details of getting a C compiler varies according to the system used:

  - Linux
    - The GNU C Compiler (gcc) is usually present
    - sudo apt-get install build-essential python3-dev
  - Mac OS X
    - To retrieve gcc, one option is to install Apple’s XCode
    - https://developer.apple.com/
  - Windows
    - Microsoft Visual C/C++ (MSVC)
    - https://wiki.python.org/moin/WindowsCompilers.

The simplest way of installing Cython is by using pip:
{% highlight ruby %}
pip install Cython==3.0.0a10
{% endhighlight %}

# Building Cython Code

Cython code must, unlike Python, be compiled. The general procedure for compiling Cython can now be described as follows:
  - .pyx
  - .pyd
  - setup.py
  - (optional) .c/.cpp & .h/.hpp



ref.

http://docs.cython.org/en/latest/