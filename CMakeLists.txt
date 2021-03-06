cmake_minimum_required(VERSION 3.5 FATAL_ERROR)

# Get root folder name and set it as project name
get_filename_component(PROJECT_NAME ${CMAKE_SOURCE_DIR} NAME)
project(${PROJECT_NAME} CXX)

# Compiler Options
set(CMAKE_CXX_STANDARD 14)
set(CXX_STANDARD_REQUIRED on)

# Debugging purpose & Clang-Tidy usage
set(CMAKE_EXPORT_COMPILE_COMMANDS on)

message(STATUS "Root Directory ${CMAKE_SOURCE_DIR}")
message(STATUS "Project Name ${PROJECT_NAME}")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/out)
set(MAIN_SRC ${PROJECT_NAME})

set(SRC_FILES
            "${CMAKE_SOURCE_DIR}/src/${MAIN_SRC}.cpp"
            ) # add other source files here

include_directories(${CMAKE_SOURCE_DIR}/include)

message(STATUS "Source Files ${SRC_FILES}")

# # Clang Tidy Configuration
find_program(CLANG_TIDY_PATH NAMES clang-tidy)
if(NOT CLANG_TIDY_PATH)
    message(FATAL_ERROR "Could not find the clang-tidy")
else()
    message(STATUS "Clang Tidy ${CLANG_TIDY_PATH}")
endif()

find_program(CLANG_TIDY_PATH NAMES clang-tidy)
set(CMAKE_CXX_CLANG_TIDY 
                        ${CLANG_TIDY_PATH}
                        "-checks=-*,clang-analyzer-*,performance-*,cppcoreguidelines-*,cert-*,readability-redundant-string-cstr") 

# Boost Library
# set(Boost_USE_STATIC_LIBS ON)
# find_package(Boost COMPONENTS log program_options log_setup REQUIRED)

# message(STATUS "Boost library directories : ${Boost_LIBRARY_DIRS}")
# message(STATUS "Boost library : ${Boost_LIBRARIES}")
# message(STATUS "Boost Include directories: ${Boost_INCLUDE_DIRS}")

# # Boost
# include_directories(${Boost_INCLUDE_DIRS})
# link_libraries(${Boost_LIBRARIES})

# # curl
# find_package(curl REQUIRED)
# include_directories(${CURL_INCLUDE_DIRS})
# link_libraries(${CURL_LIBRARIES})

# # openssl
# find_package(OpenSSL REQUIRED)
# include_directories(${OPENSSL_INCLUDE_DIR})
# link_libraries(${OPENSSL_LIBRARIES})

# Print All CMake Variables
# get_cmake_property(_variableNames VARIABLES)
# foreach (_variableName ${_variableNames})
#     message(STATUS "${_variableName}=${${_variableName}}")
# endforeach()

# # Target Config
# Create Executable
add_executable(${PROJECT_NAME} ${SRC_FILES})

# Create Shared Library
# add_library(${PROJECT_NAME} SHARED ${SRC_FILES})

# Create Static Library
# add_library(${PROJECT_NAME} STATIC ${SRC_FILES})
