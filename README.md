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
$ ./configure --prefix=/Users/aarunishsinha/mpi/           (replace aarunishsinha by your user name on your Mac)
```
This may take a while to complete. When it is done,
```
$ make all install
```
This will also take a while to complete

### Alternate Install
If you have Homebrew installed,
```shell
$ brew install open-mpi
```
### Testing
```C
#include <stdio.h>
#include <string.h>
#include <mpi.h>

const int MAX_STRING = 100;

int main(void){
  char greeting[MAX_STRING];
  int comm_sz;
  int my_rank;

  MPI_Init(NULL,NULL);
  MPI_Comm_size(MPI_COMM_WORLD,&comm_sz);
  MPI_Comm_rank(MPI_COMM_WORLD,&my_rank);

  if(my_rank!=0){
    sprintf(greeting, "Greetings from the process %d of %d!", my_rank,comm_sz);
    MPI_Send(greeting, strlen(greeting)+1, MPI_CHAR, 0,0,MPI_COMM_WORLD);
  }
  else{
    printf("Greetings from the process %d of %d!\n", my_rank,comm_sz);
    for(int q=1;q<comm_sz;q++){
      MPI_Recv(greeting, MAX_STRING, MPI_CHAR,q,0,MPI_COMM_WORLD,MPI_STATUS_IGNORE);
      printf("%s\n", greeting);
    }
  }
  MPI_Finalize();
  return 0;
}
```
Try running the above code block
```shell
mpicc -o mpi_hello mpi_hello.c
mpirun -np 2 ./mpi_hello
```

Output:
```
Greetings from the process 0 of 2!
Greetings from the process 1 of 2!
```
