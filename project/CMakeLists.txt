set(PROJECT_NAME project_name)

# Sources files of the project
set(SRC_FILES
    main.c
    ...
    gcc_startup.S)

# Include folders
set(INC_FOLDERS 
    include
    ...)

# C flags
set(CFLAGS
    -Wall
    -Werror
    ...)

# Some more CFLAGS depending on build type if you have several defined
if (CMAKE_BUILD_TYPE MATCHES Debug)
    add_definitions(-DDEBUG=1 -O0 -g3)
elseif(CMAKE_BUILD_TYPE MATCHES Release)
    add_definitions(-O3)
endif()

# C++ flags
set(CXXFLAGS )

# Path to directories used when linking (object files and libs)
link_directories(./ ./lib/)

# Property to add for assembler files
set_source_files_properties(../../../../../components/toolchain/gcc/gcc_startup_nrf52.s PROPERTIES COMPILE_FLAGS "-x assembler-with-cpp")

# Lib to link
set(LIB_FILES any_lib.a m)

# Linker flags
set(CMAKE_EXE_LINKER_FLAGS "-Tlinker_script.ld -Map=${PROJECT_NAME}.map ...")

set(BUILD_SHARED_LIBS OFF)
include(${SDK_ROOT}/util/utils.cmake)

project(${PROJECT_NAME} C ASM)
string(REPLACE ";" " " CFLAGS "${CFLAGS}")
set(CMAKE_C_FLAGS ${CFLAGS})
include_directories(${INC_FOLDERS})
add_executable(${PROJECT_NAME} ${SRC_FILES})

# Link with libraries
target_link_libraries (${PROJECT_NAME} ${LIB_FILES})

# Display some more info (using utils.cmake)
firmware_size(${PROJECT_NAME})

# Also generate hex file 
generate_object(${PROJECT_NAME} .hex ihex)

