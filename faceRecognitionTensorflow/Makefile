D_SRC = src

BIN_SRCS=${D_SRC}/test.cpp ${D_SRC}/camera.cpp
COMM_SRCS+=${D_SRC}/tensorflow_mtcnn.cpp ${D_SRC}/comm_lib.cpp ${D_SRC}/utils.cpp ${D_SRC}/faceRecong.cpp

#
# opencv settings
#

OPENCV_LDFLAGS=$(shell pkg-config --libs opencv)
OPENCV_CFLAGS=$(shell pkg-config --cflags opencv)

CXXFLAGS += $(OPENCV_CFLAGS) 
LIBS += $(OPENCV_LDFLAGS)

#
# tensorflow settings
#


TF_INCS += -I./include
CXXFLAGS += $(TF_INCS) 
LIBS+=-Wl,-rpath, -L./libs -ltensorflow_cc -ltensorflow_framework


CXX := g++
CXXFLAGS+= -Wall  -ggdb -std=c++11 


COMM_OBJS=$(COMM_SRCS:.cpp=.o)
BIN_OBJS=$(BIN_SRCS:.cpp=.o)
BIN_EXES=$(BIN_SRCS:.cpp=)


default : $(BIN_EXES)

$(BIN_EXES) : $(COMM_OBJS)

$(BIN_EXES):%:%.o


%:%.o
	$(CXX) $< -o $@ $(LDFLAGS) $(COMM_OBJS) $(LIBS)

%.o : %.cpp 
	$(CXX) $(CXXFLAGS) -c $< -o $@ 

clean:
	rm -f $(BIN_EXES)  ${D_SRC}/*.o

.PHONY : all clean

