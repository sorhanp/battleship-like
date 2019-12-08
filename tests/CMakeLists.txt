# See if Check is installed
find_package(Check REQUIRED)
if(CHECK_FOUND)
    message(STATUS "CHECK_INCLUDE_DIR: ${CHECK_INCLUDE_DIR}")

    add_executable(battleships-like-tests 
        main_tests.c)

    target_link_libraries(battleships-like-tests
    PUBLIC ${CHECK_LIBRARIES})

    include_directories(${CHECK_INCLUDE_DIR})

    target_compile_options(battleships-like-tests
    PUBLIC "-pthread")

endif()