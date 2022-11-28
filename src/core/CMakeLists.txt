SLIB_INIT(
    LNAME Core
    SRCS core_riscv.c
    PUB_REQ Interrupt Rcc Sysinit
)

add_subdirectory(interrupt)
add_subdirectory(sysinit)
add_subdirectory(rcc)