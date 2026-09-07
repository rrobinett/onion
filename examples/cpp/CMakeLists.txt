SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

include_directories (${PROJECT_SOURCE_DIR}/src/) 
include_directories (${PROJECT_SOURCE_DIR}/src/bindings/cpp/)

add_executable(cpp main.cpp)
target_link_libraries(cpp onion onioncpp)
