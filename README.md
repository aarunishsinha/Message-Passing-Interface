# Message-Passing-Interface
Getting started with Open-MPI in C

## Installing MPI in MacOS
version = 11.2.3
gcc version = 10.2.0_4
### Download
You can download version 4.1.0 from [here](https://www.open-mpi.org/software/ompi/v4.1/) (or find the current latest version)

### Extract and Install
- Assuming that the downloaded file is in your ~/Downloads directory.
- The installation on **my** machine assumes that the user is **aarunishsinha**, change the username according to you device
- Open a **Terminal** window and type the following commands
```shell
$ cd
$ mkdir mpi
$ mkdir mpi/download
$ cd mpi/download
$ mv ../../Downloads/openmpi-4.1.0.tar.bz2
$ tar -xzvf openmpi-4.1.0.tar.bz2
$ cd openmpi-4.1.0
$ ./configure --prefix=/Users/aarunishsinha/mpi/    _(replace aarunishsinha by your user name on your Mac)_
```
This may take a while to complete. When it is done,
```
$ make all install
```
This will also take a while to complete
