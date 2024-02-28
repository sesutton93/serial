cmake_minimum_required(VERSION 3.8)
project(serial)

# Find catkin
find_package(ament_cmake REQUIRED)


## Sources
add_library(${PROJECT_NAME}
    src/serial.cpp
    include/serial/serial.hpp
    include/serial/v8stdint.hpp
)

target_sources(${PROJECT_NAME} PRIVATE
    src/impl/unix.cpp
    src/impl/list_ports/list_ports_linux.cpp
)
target_link_libraries(${PROJECT_NAME} rt pthread)



## Include headers
target_include_directories(${PROJECT_NAME} PRIVATE include)

## Install executable
install(TARGETS ${PROJECT_NAME}
	ARCHIVE DESTINATION lib
	LIBRARY DESTINATION lib
)

## Install headers
install(FILES include/serial/serial.hpp include/serial/v8stdint.hpp
	DESTINATION include/serial)

## Tests
#if(BUILD_TESTING)
#    find_package(ament_lint_auto REQUIRED)
#    ament_lint_auto_find_test_dependencies()
#    add_subdirectory(tests)
#endif()

#set(rt_LIBRARIES rt)
#set(pthread_LIBRARIES pthread)
ament_export_libraries(${PROJECT_NAME})
ament_export_include_directories(include)
#ament_export_dependencies(rt pthread)
ament_package()
