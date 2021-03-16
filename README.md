# README

STM32 CMake Project Template. Or as close as it gets, because STM32 code generation is tough to handle. I hope I'll be 
able to improve this repository with more flexible template. This project template should be easily easily convertible
between ***C**/**C++***.

## Where is *"int main(...)"*?

You can find it under location:

```
Core/System/Source/main.(c/cpp)
```

## Directories and description

Here I'd like to give you some understanding how I organized this project template.

+ **Core** - is directory for logic related with basic implementation of *uController* states and APIs. Initialization, 
  low level implementation, etc...
  - **Configuration** - is in general headers only (interface) library to store information about *uController* general
    and application specific configuration.
  - **Drivers** - contains API implementation for low level *uController* hardware peripherals and MCU itself. You can
    download ready packages for Arm® Cortex® from [KEIL Drivers Package](https://www.keil.com/dd2/) (*see chapter below 
    "Tips&Tricks"*).
  - **CMSIS** *KEIL* - Arm® Cortex® processors driver directory 
    + **STM32...HAL_Driver** - is hardware abstraction layer driver for *uController* internal peripherals.
  - **System** - other bare metal operations like: interrupt callbacks, basic system functions, etc...
    + **Startup** - contains start-up assembly file called before jumping to main function.
+ **Etc** - other directories/files required for project handling, like: OCD Files, etc...
+ **Scripts** - contains various scripts files, like: Bash, Linker, etc...

## Tips&Tricks

### Keil files "*.pack"

This is ordinary compressed file so you don't need any fancy KEIL software to open it. Change *\*.pack* to *\.zip* and
now you can decompress driver files and use them. Unless there is any better way to find those files this is the method.