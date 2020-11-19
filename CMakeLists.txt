cmake_minimum_required(VERSION 2.8.12 FATAL_ERROR)
project(NoLifeNx CXX)
if("${CMAKE_CXX_COMPILER_ID}" MATCHES "Clang" OR "${CMAKE_CXX_COMPILER_ID}" MATCHES "GNU")
    add_compile_options(-std=c++11)
endif()
aux_source_directory(. NOLIFENX_SOURCES)
add_library(NoLifeNx ${NOLIFENX_SOURCES})
if(${BUILD_SHARED_LIBS})
    install(TARGETS NoLifeNx LIBRARY DESTINATION lib)
else()
    install(TARGETS NoLifeNx LIBRARY ARCHIVE DESTINATION lib)
endif()
file(GLOB NOLIFENX_HEADERS . *.hpp)
install(FILES 
audio.hpp
bitmap.hpp
file.hpp
node.hpp
nxfwd.hpp
nx.hpp
DESTINATION include/nx)

IF (APPLE)
    include_directories(/usr/local/Cellar/lz4/1.9.2/include)
    target_link_libraries(NoLifeNx /usr/local/Cellar/lz4/1.9.2/lib/liblz4.a)
ELSEIF (UNIX AND NOT APPLE)
    include_directories(/usr/lz4/1.9.2/include)
    target_link_libraries(NoLifeNx /usr/lz4/1.9.2/lib/liblz4.a)
ELSEIF (WIN32)
    include_directories(${PROJECT_SOURCE_DIR}/../lz4/include)
    target_link_libraries(NoLifeNx ${PROJECT_SOURCE_DIR}/../lz4/dll/liblz4.lib)
ENDIF()
