You must have the `git` package installed to do anything.

To build ROOT, you must also have some other packages.

For Scientific Linux:

First, run:

```
yum install -y epel-release
```

then

```
yum install -y git make cmake3 gcc-c++ gcc binutils libX11-devel libXpm-devel libXft-devel libXext-devel
```

For Ubuntu:

```
sudo apt install git dpkg-dev cmake g++ gcc binutils libx11-dev libxpm-dev libxft-dev libxext-dev libpng libjpeg
```

Download these two files:

https://repo.continuum.io/archive/Anaconda3-4.2.0-Linux-x86_64.sh

https://root.cern.ch/download/root_v6.08.02.source.tar.gz

and then run the script:

```
bash Anaconda3-4.2.0-Linux-x86_64.sh
```

Install anaconda to the default location and don't add the path to your .bashrc

Now run:

```
export PATH=~/anaconda3/bin:$PATH
conda install virtualenv
```

Now we move on to installing ROOT:

```
tar xzf root_v6.08.02.source.tar.gz
cd root-6.08.02/
mkdir builddir
cd builddir
cmake3 -DCMAKE_INSTALL_PREFIX=~/root-6.08.02-pythonAnaconda3 -DPYTHON3=ON -DPYTHON_EXECUTABLE=~/anaconda3/bin/python3.5 -DPYTHON_INCLUDE_DIR=~/anaconda3/include/python3.5m -DPYTHON_LIBRARY=~/anaconda3/lib/libpython3.5m.so .. >& logConfigure
cmake3 --build . >& logBuild
cmake3 --build . --target install >& logInstall
```

You may have to replace cmake3 with cmake on Ubuntu and other OS's or run the configure step twice.

Now, on to the femb_python package. In whatever directory you want to work in, run:

```
conda create -n myenv
```

then activate the conda environment with:

```
source activate myenv
```

Now get the package:

```
git clone https://github.com/jhugon/femb_python.git
cd femb_python
```

and setup the package:

```
./setup.sh
pip install -e .
```
