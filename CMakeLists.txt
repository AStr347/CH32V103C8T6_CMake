cmake_minimum_required(VERSION 3.20.0)

# include compiler and linker options
include(CHCompilers.cmake)
# include func for fast static lib creating
include(libbuilder.cmake)

project(CH32V103 C ASM)

include_directories(src/arch)

add_executable(${PROJECT_NAME}.elf src/main.c)


add_subdirectory(src)
add_subdirectory(Startup)
target_link_libraries(${PROJECT_NAME}.elf Startup Core Debug Misc)

add_custom_target(${PROJECT_NAME}.hex ALL
    COMMAND ${CMAKE_OBJCOPY_COMPILER} -O ihex ${PROJECT_NAME}.elf ${PROJECT_NAME}.hex
    COMMAND ${CMAKE_SIZE_COMPILER} --format=berkeley ${PROJECT_NAME}.elf
    COMMAND ${CMAKE_OBJDUMP_COMPILER} --source --all-headers --demangle --line-numbers --wide ${PROJECT_NAME}.elf > ${PROJECT_NAME}.lst
    COMMAND ${CMAKE_NM_COMPILER} -n -l -C ${PROJECT_NAME}.elf > symbol.txt
    COMMAND ${CMAKE_READELF_COMPILER} -a ${PROJECT_NAME}.elf > readelf.txt
    DEPENDS ${PROJECT_NAME}.elf
)