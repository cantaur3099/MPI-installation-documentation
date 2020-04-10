# MPI-installation-documentation
MPI installation doc

MPI installation documentation for mac os

Instructions:
1. Downlad the following file : https://download.open-mpi.org/release/open-mpi/v2.0/openmpi-2.0.4.tar.bz2 , I have added the file to the repository as well/

2.open terminal and navigate to the directory in which the file was intalled.

3.Once in the directory ENTER THESE INSTRUCTION ONTO THE TERMINAL PROMPT ONE AFTER ANOTHER:

  > tar xf openmpi-2.0.4.tar
  
  > cd openmpi-2.0.4/
  
  > ./configure --prefix=$HOME/opt/usr/local
  
  > make all
  
  > make install
  
  > $HOME/opt/usr/local/bin/mpirun --version
  mpirun (Open MPI) 2.0.4
  
  
 4.Open atom and paste the following code and save it as hello.c on your desktop :
 
    #include <mpi.h>
    #include <stdio.h>

    int main(int argc, char** argv) {
        MPI_Init(NULL, NULL);
        int rank;
        int world;
         MPI_Comm_rank(MPI_COMM_WORLD, &rank);
         MPI_Comm_size(MPI_COMM_WORLD, &world);
        printf("Hello: rank %d, world: %d\n",rank, world);
        MPI_Finalize();}
        
  5.navigate your terminal prompt to the desktop and enter the following commands. These commands will compile and  execute the hello.c       file.:
  
    1. for compilation:
        mpicc -o hello ./hello.c
    2. for execution:
        mpirun -np 2 ./hello
        
   6.To confirm the installation , observe if the following output is produced:
   
      Hello: rank 1, world: 2
      Hello: rank 0, world: 2
      
        
You can download Visual Studio for mac here:
https://visualstudio.microsoft.com/thank-you-downloading-visual-studio-mac/?sku=communitymac&rel=16
