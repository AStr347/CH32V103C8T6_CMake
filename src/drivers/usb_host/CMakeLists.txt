SLIB_INIT(
    LNAME UsbHost
    SRCS ch32v10x_usb_host.c
    INCLUDE include
    PRIV_REQ Core Debug
    PUB_REQ Usb
)