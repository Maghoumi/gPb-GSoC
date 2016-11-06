project(gPb)
cmake_minimum_required(VERSION 2.8)
#add_compile_options(-std=c++11)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake-modules/")

set(CMAKE_BUILD_TYPE Release)

# To avoid OpenCV linking problems
option(CUDA_USE_STATIC_CUDA_RUNTIME OFF)

#########################################################
# FIND OpenCV
#########################################################
find_package(Arpack REQUIRED)
find_package(OpenCV REQUIRED)

add_compile_options(-std=c++11)

#########################################################
# Add sources and files
########################################################
include_directories (include/gPb include/sPb include/seg ${ARPACK_INCLUDE_DIR})

set(SOURCE_FILES
    src/main.cpp
	src/gPb/globalPb.cpp
	src/gPb/filters.cpp
	src/sPb/buildW.cpp
	src/sPb/ic.cpp
	src/sPb/affinity.cpp
	src/sPb/smatrix.cpp
	src/sPb/normCut.cpp
	src/seg/watershed.cpp
	src/seg/VisWatershed.cpp
	src/seg/contour2ucm.cpp
	src/seg/ucm_mean_pb.cpp
	src/seg/uvt.cpp 
)

add_executable(${PROJECT_NAME} ${SOURCE_FILES})
target_link_libraries( ${PROJECT_NAME} ${LIBS} ${OpenCV_LIBS} ${ARPACK_LIB} -L/opt/local/lib -larpack -lparpack -L/opt/local/lib/gcc47 -lgfortran)
