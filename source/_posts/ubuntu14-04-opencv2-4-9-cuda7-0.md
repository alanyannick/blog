---
title: caffe:ubuntu14.04+opencv2.4.9+cuda7.0
date: 2016-04-09 17:20:15
tags: caffe
categories: caffe

---


 
### *Step1* install opencv2.4.9 on ubuntu 


- (*recommand*)Opencv 2.4.9 according to 

Total reference :
http://www.cnblogs.com/platero/p/3993877.html
http://blog.csdn.net/wingfox117/article/details/46278001
http://blog.csdn.net/xyy19920105/article/details/50815660

>reference link:
http://stackoverflow.com/questions/28010399/build-opencv-with-cuda-support
When meet the question of `NCVPixelOperations.hpp`
>Download link:
>NCVPixelOperations.hpp_ 
http://download.csdn.net/download/znculee/9294885
to revise.
#### Steps:
download opencv2.4.9
`
unzip opencv-2.4.9
cd opencv-2.4.9
mkdir release
cd release
cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D CUDA_ARCH_BIN=3.2 ..
make
`
success snapshot:
![opencv](http://img.blog.csdn.net/20160408131143436)
after that,input command:


`sudo make install`
![这里写图片描述](http://img.blog.csdn.net/20160408131946392)


Then how to import on the python
`cp the cv2.so file which in the ~/opencv-2.4.9/build/lib` 
to
![这里写图片描述](http://img.blog.csdn.net/20160408153241537)
and get the successful results:
![这里写图片描述](http://img.blog.csdn.net/20160408153345459)

- (normally)Opencv 2.4.9 according to  
http://blog.csdn.net/xiaojidan2011/article/details/40153933
> if you meet the following question like:
``Building NVCC (Device) object modules/core/CMakeFiles/cuda_compile.dir/src/cuda/Debug/cuda_compile_generated_gpu_mat.cu.obj
nvcc fatal : Unsupported gpu architecture 'compute_11'``
>revise the command as:
``cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local -D CUDA_GENERATION=Kepler ..``


- Other reference:
Opencv 3.0 according to `*(recommand)*`
https://github.com/jayrambhia/Install-OpenCV
>just need to run the following code:
  ``$ cd Ubuntu
 $ chmod +x * 
$ ./opencv_latest.sh``

- Time consumption: about 30 minutes

### *Step2* install cuda7.0
>sudo dpkg -i cuda-repo-<distro>_<version>_<architecture>.deb
sudo apt-get update
sudo apt-get install cuda
export PATH=/usr/local/cuda-7.0/bin:$PATH

>export LD_LIBRARY_PATH=/usr/local/cuda-7.0/lib64:$LD_LIBRARY_PATH
cd /etc/ld.so.conf.d
vim cuda.conf
(then adding) 
usr/local/cuda-7.0/lib64

### Step3 Boost
>sudo apt-get install mpi-default-dev　　#安装mpi库
sudo apt-get install libicu-dev　　　　　#支持正则表达式UNICODE字符集
sudo apt-get install python-dev　　　　　#需要python的话
sudo apt-get install libbz2-dev

>sudo apt-get install libatlas-base-dev 


### Step4 Caffe installing
>make all -j8 
make test -j8
make run test -j8 

when meet the error about:
>.build_release/tools/caffe
.build_release/tools/caffe: error while loading shared libraries: libcudart.so.7.0: cannot open shared object file: No such file or directory

`need to do`:

>export PATH=/usr/local/cuda-7.0/bin:$PATH 

>export LD_LIBRARY_PATH=/usr/local/cuda-7.0/lib64:$LD_LIBRARY_PATH

`success:`
![这里写图片描述](http://img.blog.csdn.net/20160408142424526)

## Step5 Python & Matlab wrapper
### Matlab Wrapper
then compile the `python wrapper` & `matlab wrapper`
 if meet the error:
 >In file included from ./include/caffe/util/device_alternate.hpp:40:0,
                 from ./include/caffe/common.hpp:19,
                 from ./include/caffe/blob.hpp:8,
                 from ./include/caffe/caffe.hpp:7,
                 from /home/ym/caffe-master/matlab/+caffe/private/caffe_.cpp:18:
./include/caffe/util/cudnn.hpp:5:19: fatal error: cudnn.h: No such file or directory

then means that you should link the cuDNN
http://www.cnblogs.com/platero/p/4118139.html
>tar -xzvf cudnn-6.5-linux-R1.tgz
cd cudnn-6.5-linux-R1
sudo cp lib* /usr/local/cuda/lib64/
sudo cp cudnn.h /usr/local/cuda/include/

then you will see the success results:
![这里写图片描述](http://img.blog.csdn.net/20160408144221642)

![这里写图片描述](http://img.blog.csdn.net/20160408144309502)

When run matlab demo, i get the following error:
>Invalid MEX-file '/home/ym/caffe-master/matlab/+caffe/private/caffe_.mexa64': libcudart.so.7.0: cannot open shared object file:
>No such file or directory

Solved link:
http://www.cnblogs.com/smartvessel/archive/2011/01/21/1940868.html
Methods:
>cd /etc/ld.so.conf.d
sudo vi cuda.conf
(adding)
/usr/local/cuda/lib64
(:wq)
sudo ldconfig

---

>总结下来主要有3种方法：
1. 用ln将需要的so文件链接到/usr/lib或者/lib这两个默认的目录下边
ln -s /where/you/install/lib/*.so /usr/lib
sudo ldconfig


>2.修改LD_LIBRARY_PATH
export LD_LIBRARY_PATH=/where/you/install/lib:$LD_LIBRARY_PATH
sudo ldconfig


>3.修改/etc/ld.so.conf，然后刷新
vim /etc/ld.so.conf
add /where/you/install/lib
sudo ldconfig

---

### python wrapper
>1.revise the Makefile.configure
>`make pycaffe`
>2.after compile, export the PATH into the /etc/profile 
and execute 
>`source ~/.bashrc or /etc/profile`
>3.cannot find google.protobuf.internal:
![这里写图片描述](http://img.blog.csdn.net/20160408155501092)

solve:

>`conda install -c https://conda.anaconda.org/anaconda protobuf `


![这里写图片描述](http://img.blog.csdn.net/20160408155734009)

success!

---
matlab configure:

```
## Refer to http://caffe.berkeleyvision.org/installation.html
# Contributions simplifying and improving our build system are welcome!

# cuDNN acceleration switch (uncomment to build with cuDNN).
USE_CUDNN := 1

# CPU-only switch (uncomment to build without GPU support).
# CPU_ONLY := 1

# uncomment to disable IO dependencies and corresponding data layers
# USE_OPENCV := 0
# USE_LEVELDB := 0
# USE_LMDB := 0

# uncomment to allow MDB_NOLOCK when reading LMDB files (only if necessary)
#	You should not set this flag if you will be reading LMDBs with any
#	possibility of simultaneous read and write
# ALLOW_LMDB_NOLOCK := 1

# Uncomment if you're using OpenCV 3
# OPENCV_VERSION := 3

# To customize your choice of compiler, uncomment and set the following.
# N.B. the default for Linux is g++ and the default for OSX is clang++
# CUSTOM_CXX := g++

# CUDA directory contains bin/ and lib/ directories that we need.
CUDA_DIR := /usr/local/cuda
# On Ubuntu 14.04, if cuda tools are installed via
# "sudo apt-get install nvidia-cuda-toolkit" then use this instead:
# CUDA_DIR := /usr

# CUDA architecture setting: going with all of them.
# For CUDA < 6.0, comment the *_50 lines for compatibility.
CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \
		-gencode arch=compute_20,code=sm_21 \
		-gencode arch=compute_30,code=sm_30 \
		-gencode arch=compute_35,code=sm_35 \
		-gencode arch=compute_50,code=sm_50 \
		-gencode arch=compute_50,code=compute_50

# BLAS choice:
# atlas for ATLAS (default)
# mkl for MKL
# open for OpenBlas
BLAS := atlas
# Custom (MKL/ATLAS/OpenBLAS) include and lib directories.
# Leave commented to accept the defaults for your choice of BLAS
# (which should work)!
# BLAS_INCLUDE := /path/to/your/blas
# BLAS_LIB := /path/to/your/blas

# Homebrew puts openblas in a directory that is not on the standard search path
# BLAS_INCLUDE := $(shell brew --prefix openblas)/include
# BLAS_LIB := $(shell brew --prefix openblas)/lib

# This is required only if you will compile the matlab interface.
# MATLAB directory should contain the mex binary in /bin.
# MATLAB_DIR := /usr/local
# MATLAB_DIR := /Applications/MATLAB_R2012b.app
MATLAB_DIR := /usr/local/MATLAB/R2015a

# NOTE: this is required only if you will compile the python interface.
# We need to be able to find Python.h and numpy/arrayobject.h.
PYTHON_INCLUDE := /usr/include/python2.7 \
		/usr/lib/python2.7/dist-packages/numpy/core/include
# Anaconda Python distribution is quite popular. Include path:
# Verify anaconda location, sometimes it's in root.
# ANACONDA_HOME := $(HOME)/anaconda
# PYTHON_INCLUDE := $(ANACONDA_HOME)/include \
		# $(ANACONDA_HOME)/include/python2.7 \
		# $(ANACONDA_HOME)/lib/python2.7/site-packages/numpy/core/include \

# Uncomment to use Python 3 (default is Python 2)
# PYTHON_LIBRARIES := boost_python3 python3.5m
# PYTHON_INCLUDE := /usr/include/python3.5m \
#                 /usr/lib/python3.5/dist-packages/numpy/core/include

# We need to be able to find libpythonX.X.so or .dylib.
PYTHON_LIB := /usr/lib
# PYTHON_LIB := $(ANACONDA_HOME)/lib

# Homebrew installs numpy in a non standard path (keg only)
# PYTHON_INCLUDE += $(dir $(shell python -c 'import numpy.core; print(numpy.core.__file__)'))/include
# PYTHON_LIB += $(shell brew --prefix numpy)/lib

# Uncomment to support layers written in Python (will link against Python libs)
# WITH_PYTHON_LAYER := 1

# Whatever else you find you need goes here.
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib

# If Homebrew is installed at a non standard location (for example your home directory) and you use it for general dependencies
# INCLUDE_DIRS += $(shell brew --prefix)/include
# LIBRARY_DIRS += $(shell brew --prefix)/lib

# Uncomment to use `pkg-config` to specify OpenCV library paths.
# (Usually not necessary -- OpenCV libraries are normally installed in one of the above $LIBRARY_DIRS.)
# USE_PKG_CONFIG := 1

BUILD_DIR := build
DISTRIBUTE_DIR := distribute

# Uncomment for debugging. Does not work on OSX due to https://github.com/BVLC/caffe/issues/171
# DEBUG := 1

# The ID of the GPU that 'make runtest' will use to run unit tests.
TEST_GPUID := 0

# enable pretty build (comment to see full commands)
Q ?= @

```

python configure:

```
## Refer to http://caffe.berkeleyvision.org/installation.html
# Contributions simplifying and improving our build system are welcome!

# cuDNN acceleration switch (uncomment to build with cuDNN).
USE_CUDNN := 1

# CPU-only switch (uncomment to build without GPU support).
# CPU_ONLY := 1

# uncomment to disable IO dependencies and corresponding data layers
# USE_OPENCV := 0
# USE_LEVELDB := 0
# USE_LMDB := 0

# uncomment to allow MDB_NOLOCK when reading LMDB files (only if necessary)
#	You should not set this flag if you will be reading LMDBs with any
#	possibility of simultaneous read and write
# ALLOW_LMDB_NOLOCK := 1

# Uncomment if you're using OpenCV 3
# OPENCV_VERSION := 3

# To customize your choice of compiler, uncomment and set the following.
# N.B. the default for Linux is g++ and the default for OSX is clang++
# CUSTOM_CXX := g++

# CUDA directory contains bin/ and lib/ directories that we need.
CUDA_DIR := /usr/local/cuda
# On Ubuntu 14.04, if cuda tools are installed via
# "sudo apt-get install nvidia-cuda-toolkit" then use this instead:
# CUDA_DIR := /usr

# CUDA architecture setting: going with all of them.
# For CUDA < 6.0, comment the *_50 lines for compatibility.
CUDA_ARCH := -gencode arch=compute_20,code=sm_20 \
		-gencode arch=compute_20,code=sm_21 \
		-gencode arch=compute_30,code=sm_30 \
		-gencode arch=compute_35,code=sm_35 \
		-gencode arch=compute_50,code=sm_50 \
		-gencode arch=compute_50,code=compute_50

# BLAS choice:
# atlas for ATLAS (default)
# mkl for MKL
# open for OpenBlas
BLAS := atlas
# Custom (MKL/ATLAS/OpenBLAS) include and lib directories.
# Leave commented to accept the defaults for your choice of BLAS
# (which should work)!
# BLAS_INCLUDE := /path/to/your/blas
# BLAS_LIB := /path/to/your/blas

# Homebrew puts openblas in a directory that is not on the standard search path
# BLAS_INCLUDE := $(shell brew --prefix openblas)/include
# BLAS_LIB := $(shell brew --prefix openblas)/lib

# This is required only if you will compile the matlab interface.
# MATLAB directory should contain the mex binary in /bin.
# MATLAB_DIR := /usr/local
# MATLAB_DIR := /Applications/MATLAB_R2012b.app
MATLAB_DIR := /usr/local/MATLAB/R2015a

# NOTE: this is required only if you will compile the python interface.
# We need to be able to find Python.h and numpy/arrayobject.h.
PYTHON_INCLUDE := /usr/include/python2.7 \
		/usr/lib/python2.7/dist-packages/numpy/core/include
# Anaconda Python distribution is quite popular. Include path:
# Verify anaconda location, sometimes it's in root.
# ANACONDA_HOME := $(HOME)/anaconda
# PYTHON_INCLUDE := $(ANACONDA_HOME)/include \
		# $(ANACONDA_HOME)/include/python2.7 \
		# $(ANACONDA_HOME)/lib/python2.7/site-packages/numpy/core/include \

# Uncomment to use Python 3 (default is Python 2)
# PYTHON_LIBRARIES := boost_python3 python3.5m
# PYTHON_INCLUDE := /usr/include/python3.5m \
#                 /usr/lib/python3.5/dist-packages/numpy/core/include

# We need to be able to find libpythonX.X.so or .dylib.
PYTHON_LIB := /usr/lib
# PYTHON_LIB := $(ANACONDA_HOME)/lib

# Homebrew installs numpy in a non standard path (keg only)
# PYTHON_INCLUDE += $(dir $(shell python -c 'import numpy.core; print(numpy.core.__file__)'))/include
# PYTHON_LIB += $(shell brew --prefix numpy)/lib

# Uncomment to support layers written in Python (will link against Python libs)
# WITH_PYTHON_LAYER := 1

# Whatever else you find you need goes here.
INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include
LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib

# If Homebrew is installed at a non standard location (for example your home directory) and you use it for general dependencies
# INCLUDE_DIRS += $(shell brew --prefix)/include
# LIBRARY_DIRS += $(shell brew --prefix)/lib

# Uncomment to use `pkg-config` to specify OpenCV library paths.
# (Usually not necessary -- OpenCV libraries are normally installed in one of the above $LIBRARY_DIRS.)
# USE_PKG_CONFIG := 1

BUILD_DIR := build
DISTRIBUTE_DIR := distribute

# Uncomment for debugging. Does not work on OSX due to https://github.com/BVLC/caffe/issues/171
# DEBUG := 1

# The ID of the GPU that 'make runtest' will use to run unit tests.
TEST_GPUID := 0

# enable pretty build (comment to see full commands)
Q ?= @

```