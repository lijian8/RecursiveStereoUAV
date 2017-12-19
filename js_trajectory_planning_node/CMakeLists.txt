cmake_minimum_required(VERSION 2.8.3)
project(js_trajectory_planning_node)

add_compile_options(
    $<$<CXX_COMPILER_ID:GNU>:-std=c++14>
)

find_package(catkin REQUIRED COMPONENTS
    roscpp
    roslaunch
    js_messages
)

roslaunch_add_file_check(launch USE_TEST_DEPENDENCIES)

find_package(js_messages REQUIRED)

###################################
## catkin specific configuration ##
###################################

catkin_package(
    INCLUDE_DIRS
    LIBRARIES trajectory_planning_node
    CATKIN_DEPENDS roscpp js_messages
)

###########
## Build ##
###########

include_directories(
    include
    ${js_messages_INCLUDE_DIRS}/includes
    ${js_messages_INCLUDE_DIRS}
    ${catkin_INCLUDE_DIRS}
)

add_executable(trajectory_planning_node
    src/trajectory_planning_node.cpp
)

target_link_libraries(trajectory_planning_node
    ${catkin_LIBRARIES}
)

add_dependencies(trajectory_planning_node
    js_messages_generate_messages_cpp
)

#############
## Install ##
#############

install(TARGETS trajectory_planning_node
     RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
)

#############
## Testing ##
#############

