## su2 sovler ##
#to compile this solver, go to the folder containing SU2, make a new directory su2install, this will be used to store SU2 installation. 

# run the following in terminal
git clone https://github.com/shanjierenyidp/SU2wpc.git
cd SU2wpc

# assuming your in the current path = your-own-path
apt-get update -y && apt-get install -y openmpi-bin libopenmpi-dev swig m4
env MPICC=/usr/bin/mpicc pip install mpi4py
export PATH=/usr/local/cuda/bin:$PATH
export CPATH=/usr/local/cuda/include:$CPATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
export CXXFLAGS="-O3"
git clone --branch feature_pytorch_communicator  https://github.com/su2code/SU2 
mkdir su2/install
cd SU2 
./preconfigure.py --enable-mpi --with-cc=/usr/bin/mpicc --with-cxx=/usr/bin/mpicxx --prefix=your-own-path/su2install/SU2 --enable-autodiff --enable-PY_WRAPPER --disable-tecio --update
        # && make -j 8 install
sudo make -j 16 Install
# add this to ~/.bashrc
export PATH=$PATH:your-own-path/su2install/SU2/bin
export PYTHONPATH=$PYTHONPATH:your-own-path/su2install/SU2/bin
export SU2_RUN=your-own-path/su2install/SU2/bin
export SU2_HOME=your-own-path/SU2
