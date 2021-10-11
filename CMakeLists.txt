cmake_minimum_required(VERSION 3.14)

project(clist LANGUAGES C)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(SOURCES
    clist.c
)

set(HEADERS
    clist.h
)

add_library(clist STATIC
    ${SOURCES}
    ${HEADERS}
)

set_target_properties(clist PROPERTIES
    PUBLIC_HEADER clist.h
)

target_compile_definitions(clist PRIVATE CLISTS_LIBRARY)

install(TARGETS clist
	LIBRARY DESTINATION       "${CMAKE_BUILD_TYPE}/lib"
	ARCHIVE DESTINATION       "${CMAKE_BUILD_TYPE}/lib"
        PUBLIC_HEADER DESTINATION "${CMAKE_BUILD_TYPE}/include")

set(APP_EXE test)
add_executable(${APP_EXE}
    test.c
)
target_link_libraries(${APP_EXE} clist)
add_test(Test, ${APP_EXE})
