include_directories(${CPP-NETLIB_SOURCE_DIR})
find_package( Boost 1.41.0 COMPONENTS unit_test_framework system regex date_time thread filesystem )
set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_MULTITHREADED ON)

if (Boost_FOUND)
    add_executable(cpp-netlib-hello_world hello_world.cpp)
    add_executable(cpp-netlib-http_1_0_test http_1_0_test.cpp)
    add_executable(cpp-netlib-http_1_1_test http_1_1_test.cpp)
    add_executable(cpp-netlib-http_localhost_tests http_localhost_tests.cpp)
    add_executable(cpp-netlib-https_localhost_tests https_localhost_tests.cpp)
    add_executable(cpp-netlib-message_test message_test.cpp)
    add_executable(cpp-netlib-http_message_test http_message_test.cpp)
    add_executable(cpp-netlib-message_transform_test message_transform_test.cpp)
    add_executable(cpp-netlib-url_test url_test.cpp)
    target_link_libraries(cpp-netlib-hello_world ${Boost_SYSTEM_LIBRARY} ${Boost_REGEX_LIBRARY} ${Boost_DATE_TIME_LIBRARY} ${Boost_THREAD_LIBRARY} pthread)
    target_link_libraries(cpp-netlib-http_1_0_test ${Boost_LIBRARIES} pthread ssl crypto)
    target_link_libraries(cpp-netlib-http_1_1_test ${Boost_LIBRARIES} pthread ssl crypto)
    target_link_libraries(cpp-netlib-http_message_test ${Boost_LIBRARIES} pthread ssl crypto)
    target_link_libraries(cpp-netlib-message_test ${Boost_LIBRARIES} pthread ssl crypto)
    target_link_libraries(cpp-netlib-message_transform_test ${Boost_LIBRARIES} pthread ssl crypto)
    target_link_libraries(cpp-netlib-http_localhost_tests ${Boost_LIBRARIES} pthread ssl crypto)
    target_link_libraries(cpp-netlib-https_localhost_tests ${Boost_LIBRARIES} pthread ssl crypto)
    target_link_libraries(cpp-netlib-url_test ${Boost_LIBRARIES} pthread ssl crypto)
    set_target_properties(cpp-netlib-hello_world cpp-netlib-http_1_0_test cpp-netlib-http_1_1_test cpp-netlib-message_test cpp-netlib-http_message_test cpp-netlib-message_transform_test cpp-netlib-http_localhost_tests cpp-netlib-https_localhost_tests cpp-netlib-url_test PROPERTIES RUNTIME_OUTPUT_DIRECTORY ../../../build/tests)
    add_test(cpp-netlib-hello_world python httplib_acceptance.py ../../../build/tests/cpp-netlib-hello_world ../../../build/tests/cpp-netlib-hello_world.passed)
    add_test(cpp-netlib-http_1_0_test ../../../build/tests/cpp-netlib-http_1_0_test)
    add_test(cpp-netlib-http_1_1_test ../../../build/tests/cpp-netlib-http_1_1_test)
    add_test(cpp-netlib-http_localhost_tests ../../../build/tests/cpp-netlib-http_localhost_tests)
    add_test(cpp-netlib-https_localhost_tests ../../../build/tests/cpp-netlib-https_localhost_tests)
    add_test(cpp-netlib-message_test ../../../build/tests/cpp-netlib-message_test)
    add_test(cpp-netlib-http_message_test ../../../build/tests/cpp-netlib-http_message_test)
    add_test(cpp-netlib-url_test ../../../build/tests/cpp-netlib-url_test)
endif()

