# cmake-cortex-m

Template files for integrating CMake on CLion with ARM microcontrollers

## CLion Project settings

### Toolchains

Change your compiler to compile with `arm-none-eabi-gcc` and debug with `arm-none-eabi-gdb`

### CMake

Add `-DCMAKE_TOOLCHAIN_FILE=util/arm-gcc-toolchain.cmake` as CMake options.