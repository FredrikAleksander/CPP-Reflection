# C++ Reflection

[![Join the chat at https://gitter.im/CPP-Reflection/Lobby](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/CPP-Reflection/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

## Preface
I worked on a complete reflection pipeline starting in the summer of 2015 for a game project / editor. My intent by creating this repository was to share my experience and how I came about developing it. The response from the community motivated me to make it a tad bit more official by allowing others to consume and build it easily, rather than just giving you code and saying "fill in the pieces".

I created a blog where I talk more in detail about the process and try to share my experiences as best as possible. You can find the blog here -

https://austinbrunkhorst.com/cpp-reflection-part-1/

## Building
There are three buildable sections in this repository - [Runtime](https://github.com/AustinBrunkhorst/CPP-Reflection/tree/master/Source/Runtime), [Parser](https://github.com/AustinBrunkhorst/CPP-Reflection/tree/master/Source/Parser) and [Examples](https://github.com/AustinBrunkhorst/CPP-Reflection/tree/master/Examples). I setup an environment for building using CMake - yes it's insane but it's also awesome so let's just go with it. All examples are assuming you're working from the root of this repository.

### Requirements
 - [LLVM 3.8.0](http://llvm.org/releases/download.html)+ (for libClang)
 - A C++17 compliant compiler

#### Runtime
There are no dependencies in the runtime so building is pretty straightforward.



*Create a build directory.*

    mkdir Build && cd Build
    
*Generate a build system using any [desired generator](https://cmake.org/cmake/help/v3.0/manual/cmake-generators.7.html) in CMake.*

    cmake -G "<Desired Generator>" ../Source/Runtime
    
*Build - you can use any IDE if applicable to the generator, but you can also just build straight from CMake.*

    cmake --build . --target MetaRuntime
    
#### Parser
There are more moving parts in this because the parser actually has dependencies and builds to an executable. Don't worry though! I'm here to walk you through this.

##### Install LLVM 3.8 for LibClang
**Windows** - download the [32 bit](http://llvm.org/releases/3.8.0/LLVM-3.8.0-win32.exe) or [64 bit](http://llvm.org/releases/3.8.0/LLVM-3.8.0-win64.exe) pre-built binaries.

**Unix based systems** - find the appropriate package. On Linux Mint I just did the following.

    sudo apt-get install libclang-3.8-dev

The installation should be located in `/usr/lib/llvm-3.8`

Once installed, set an environment variable `LLVM_ROOT` to the root of the installation directory. You can skip this step, but an environment variable makes the CMake command simpler.


*Create a build directory.*

    mkdir Build && cd Build
    
*Generate a build system using any [desired generator](https://cmake.org/cmake/help/v3.0/manual/cmake-generators.7.html) in CMake.*

    cmake -G "<Desired Generator>" ../Source/Parser

*If you skipped creating environment variables, you'll have to define variables for resolution in CMake directly - just add these two switches in the command above.*

    -DLLVM_ROOT=<PATH>
    
*Build - you can use any IDE if applicable to the generator, but you can also just build straight from CMake.*

    cmake --build . --target MetaParser

#### Examples
You will need to follow the same steps for setting up the dependencies explained in the **Parser** build instructions.

Just like the other two targets you'll do the following -

*Create a build directory.*

    mkdir Build && cd Build
    
*Generate a build system using any [desired generator](https://cmake.org/cmake/help/v3.0/manual/cmake-generators.7.html) in CMake.*

    cmake -G "<Desired Generator>" ../Examples
    
*Build - you can use any IDE if applicable to the generator, but you can also just build straight from CMake.*

    cmake --build .

Remember to add the extra switches for defining `LLVM_ROOT` if you skipped adding them as an environment variable.

All of the examples build to a simple executable that demonstrates the specific features/functionality in use.

I don't have immediate intentions of documenting the interfaces and such with the runtime library, but hopefully the examples cover all parts of the runtime and people can get the whole picture there. My blog posts cover the development process and the reason I made the decisions I did. 

Feel free to contact me with any questions or concerns! Also, pull requests are very welcome!

