---
layout: post
title: How to compile opencv on linux without root
modified: {}
tags:
  - tools
  - opencv
published: true
---

##update Cmake

1. only cmake version > 2.88 can be used to compile opencv.
2. Download latest version cmake source code and cd in the folder.
3. ./bootstrap
4. make (No need to make install, just executate new cmake from built dir)

---
##Compiling OpenCV

1. Download the latest version opencv from website.
2. Mkdir build inside the unzip opencv folder.
3. cmake(execute the newly installed cmake using direct path)

The command(do not ignore **..**):

	cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=my_location -D BUILD_NEW_PYTHON_SUPPORT=ON ..


4. make
5. make install
6. Guarantee that python2.7 folder is generated in lib.
7. config the environment.
