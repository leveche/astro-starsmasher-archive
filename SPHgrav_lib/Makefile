.SUFFIXES: .cu 

CXX  := g++
CC   := gcc
AR   := ar ruv
RANLIB := ranlib

# path to your CUDA installation
#CUDAPATH       := $(shell dirname $(shell dirname $(shell which nvcc)))
CUDAINCLUDE    := -I$(CUDAPATH)/include
NVCC           := $(CUDAPATH)/bin/nvcc

#use this for Fermi cards
NVCCFLAGS := -arch=sm_20
#use this for GTX280/290/295, or any GT200 architecture with DP support
# NVCCFLAGS := -arch=sm_13
NVCCFLAGS += -O4 -g  $(CUDAINCLUDE)  -I./ -Xptxas -v,-abi=no 

# NVCCFLAGS += -maxrregcount=32
NVCCFLAGS += -Xcompiler="-Wall"
CUDA_LIBS = -L$(CUDAPATH)/lib64 -lcudart

CXXFLAGS  +=  -Wall -g -O4
# LDFLAGS   +=  -fopenmp
LDGPUGLAGS := $(LDFLAGS) $(CUDA_LIBS)

OBJS = grav_force_direct.cu_o
GRAVLIB = libSPHgrav.a

all: $(GRAVLIB)

$(GRAVLIB): $(OBJS)
	/bin/rm -f $@
	$(AR) $@ $(OBJS)

.cpp.o: 
	$(CXX) $(CXXFLAGS) -c $< -o $@

%.cu_o:  %.cu
	$(NVCC) $(NVCCFLAGS) -c $< -o $@

clean:
	/bin/rm -rf *.cu_o $(GRAVLIB)

$(GRAVLIB): cutil.h cuVec3.h cuVector.h

