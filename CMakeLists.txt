cmake_minimum_required(VERSION 2.8.3)
project(h4r_libsersyncproto)

find_package(catkin REQUIRED COMPONENTS
  roscpp
)


find_package(Boost REQUIRED COMPONENTS system)

catkin_package(
   INCLUDE_DIRS src/SerSyncProto/include
   LIBRARIES h4r_libsersyncproto
   CFG_EXTRAS h4r_libsersyncproto-extras.cmake
)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
# include_directories(include)
include_directories(
  src/SerSyncProto/include
  ${catkin_INCLUDE_DIRS}
)

## Declare library
set_source_files_properties(src/SerSyncProto/src/sersyncproto.c PROPERTIES LANGUAGE CXX )
add_library(h4r_libsersyncproto
   src/SerSyncProto/src/sersyncproto.c
)


#############
## Install ##
#############

# Mark executables and/or libraries for installation
install(TARGETS h4r_libsersyncproto
   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
 )

## Mark header files for installation
install(DIRECTORY src/SerSyncProto/include
   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
   FILES_MATCHING PATTERN "*.h"
   PATTERN ".svn" EXCLUDE
)

## Mark source file for installation
install(FILES
   src/SerSyncProto/src/sersyncproto.c
   DESTINATION ${CATKIN_PACKAGE_SHARE_DESTINATION}/src/SerSyncProto/src/
)