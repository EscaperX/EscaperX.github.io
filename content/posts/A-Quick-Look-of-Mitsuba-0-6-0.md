---
title: A Quick Look of Mitsuba 0.6.0
date: 2022-09-16 21:53:29
draft: false
tags: [Mitsuba, Software]
categories: [Graphics]
---

## Installation
In fact, it's quite easy to compile and run mitsuba 0.6.0 on your morden operating system, although it is a 7 years-old software.

All tools you need are:
1. Visual Studio 2017. Someone says there will be confusing problem using morden visual studio like version 2019 or 2022, so it's better to follow the requirement. You can get this old version from this [link](https://visualstudio.microsoft.com/thank-you-downloading-visual-studio/?sku=Community&rel=17).
2. Scons. A construction tool used by mitsuba to organize those files. Scons 3 is used in a branch of mitsuba 0.5.0 so you may install scons simply by `pip install scons==3.1.2`.
3. Qt 5.9.1. Qt 5.9.1 is used in the dependencies of mitsuba. If there's no Qt 5.9.1 on your computer you may not be able to run the GUI version after compiling. If there's no furture needs of development, choose 'mvsc x64 2017' is enough for mitsuba.


It will be much more convenient to use branch `mitsuba-renderer/scons-python3`, for which python 2.x is rarely installed in the morden computer.
You can start by
```shell
git clone https://github.com/mitsuba-renderer/mitsuba.git -b scons-python3
```

And then download dependencies from https://github.com/mitsuba-renderer/mitsuba.git and copy them to `mitsuba/denpendencies/`.

Mitsuba 0.6.0 requires MVSC 2017 to compile the source code. Git Bash usually doesn't provide a directly access to `cl.exe` and other libraries. You can use 'x64 Command Prompt for VS 2017' which intergrates all the necessary libraries. Run `scons` on this command prompt.

After compiling all the source code, the executable files will be generated at `mitsuba/dist/`.

You can now start your journey of Mitsuba 0.5.0.
