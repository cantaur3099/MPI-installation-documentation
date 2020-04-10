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
      
 Note:
 I have noticed that during execution pmix offers an unnecesary exception of the form:
 
        PMIX ERROR: ERROR in file gds_ds12_lock_pthread.c at line 206
        
  To prevent this, before the execution of main file always :
        
        export PMIX_MCA_gds=hash
        
 This helps subside the pmix noice and has to be repeated every session.
 
 
Note:
The maximum number of slots that pmi allows is by default 2 in macs. A "slot" is the Open MPI term for an allocatable unit where we can
launch a process. This determines how many time we can run an instruction in a code.
To extend the number of slots carry out the following steps:

1.Create a hostfile with anyname 
2.within the write:

          localhost slots = <#>
          
where #=no. of slots needed.

3. while compiling write the  following on the terminal prompt:
        
        mpicc  -hostfile -<filename>
        
 4. While running wite the following on the terminal prompt:
            
            
            mpirun -hostfile <filename> -np <#> <codefilename>
            
            
  
          
 
