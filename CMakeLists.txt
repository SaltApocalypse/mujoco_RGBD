cmake_minimum_required(VERSION 3.10)

project(mujoco_camera)

# Compiler settings
SET (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -pthread")

# finding modules
find_package(OpenCV REQUIRED) 
find_package(PCL REQUIRED)
find_package(glfw3 REQUIRED)


# Specify directories
set(MUJOCO_INCLUDE_DIR /home/salta/.conda/envs/mujoco/lib/python3.10/site-packages/mujoco/include)
set(MUJOCO_LINK_DIR /home/salta/.conda/envs/mujoco/lib/python3.10/site-packages/mujoco)
set(GLFW_INCLUDE_DIR /usr/include/GLFW)

set(MUJOCO_LIBS
    ${MUJOCO_LINK_DIR}/libmujoco.so.3.2.6 
    glfw
    GL
    GLEW
    m
    dl
)

include_directories(${MUJOCO_INCLUDE_DIR}
                    include
                    ${OpenCV_INCLUDE_DIRS}
                    ${PCL_INCLUDE_DIRS}
                    ${GLFW_INCLUDE_DIR})

                    
link_directories(${MUJOCO_LINK_DIR}
                ${PCL_LIBRARY_DIRS})

add_executable(multi_win_test
                src/two_window.cpp
                src/mujoco_rgbd_camera.cpp)

target_link_libraries(multi_win_test
            ${MUJOCO_LIBS}
            ${OpenCV_LIBS}
            ${PCL_LIBRARIES})