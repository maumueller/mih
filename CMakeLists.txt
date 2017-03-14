cmake_minimum_required(VERSION 2.6)
project (mih)

find_package(HDF5 REQUIRED)

set (CMAKE_CXX_FLAGS "-DSINGLE_CORE -O2 -fopenmp -DNDEBUG")
# -Wall -march=native -mtune=native")

include_directories ("${PROJECT_SOURCE_DIR}/include" "${HDF5_INCLUDE_DIRS}")

add_library(mihlib src/array32.cpp src/mihasher.cpp src/sparse_hashtable.cpp src/bucket_group.cpp src/reorder.cpp)

add_executable (mih interface/mih_interface.cpp interface/loadVar.cpp interface/saveRes.cpp)
target_link_libraries (mih ${HDF5_LIBRARIES} mihlib)

project (linscan)
add_executable (linscan interface/linscan_interface.cpp src/linscan.cpp interface/loadVar.cpp interface/saveRes.cpp)
target_link_libraries (linscan ${HDF5_LIBRARIES})
