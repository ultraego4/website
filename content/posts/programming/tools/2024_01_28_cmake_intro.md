+++
title = 'How i grasped the basics of CMake aka CMAKE NIGHTMARE'
date = 2024-01-28T15:30:32+01:00
draft = false
tags=["cmake","c++"]
summary="Now systems could have multiple build systems installed, and also lets say your developing on linux and you would want your application to be cross platform, you would have to specify rules for your build process for the specific build system on the windows platform. Now CMake comes in and lets you do exactly that in a high-level config file and also in a managable format, hence the name cross-platform build system generator. It generates the build system specific build files for the given build systems."
+++

Well cmamke is an interesting thing, and it took me some time to grasp the fundamentals when i first started leraning about it, i didnt find the offical learn documentation very helpful, and couldnt really find any decent videos either. Doing my c++ uni course i was using Visual Studio I KNOW I KNOW... but the unit tests specifically had to be written in vs studios native c++ test framework so my teacher could run it through hes unit tests as well.

Back in summer when i started learning c++ first on my own before the uni course i used the gnu compiler but really only knew how to generate an exectuable nothing other then that.

While researching and learning how cmake works, i was able to also deepen my knowledge about compilers and build systems.

Ok first of all to understand why cmake is useful lets talk about build systems. A build system is a set of tools used for compiling and linking. It controls the generation of executables. For example the GNU Make on linux.

Now systems could have multiple build systems installed, and also lets say your developing on linux and you would want your application to be cross platform, you would have to specify rules for your build process for the specific build system on the windows platform. Now CMake comes in and lets you do exactly that in a high-level config file and also in a managable format, hence the name cross-platform build system generator. It generates the build system specific build files for the given build systems.

And heres my CMakeLists.txt for the space shooter game, with lots of explanation and useful things to remember when using cmake.

## Example CmakeLists.txt

**General tips for CMakeLists.txt for cross-platform builds**
 - cross platform paths / instead of \
 - if(WIN(32???)) or if(UNIX) find and link these dependencies
 - CMake variables for  compiler and linking flags
 - mindful file naming conventions


**Compiler flags (all compilers usually have this with the same syntaxs)**
 - -00, -01, -02, -03 | optimization levels
 - -Wall | enable warnings
 - -g | add debugging info

**Set compiler flags in CMakeLists.txt**
 - if you dont explicitly define the flags and build with release type 
 - CMake uses default flags!!!
 - set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O2 -Wall") | for a general setup without build types
 - CMAKE_CXX_FLAGS | is related to a general setting
 - CMAKE_CXX_FLAGS_DEBUG or CMAKE_CXX_FLAGS_RELEASE | for different build types (do set for both of them if needed)
 - if(CMAKE_CXX_COMPILER_ID STREQUAL "compiler(GNU for g++)") | to use different flags for different compilers


**Cmake commands**
 1. cmake | run it where CMakeLists.txt is!!!, generates the build files
 2. cmake --build | run it in the corresponding build directory!!!, builds based on the generated build files
example
 - CMakeLists.txt in prject root, cwd=project/build/Release(build-type) then cmake -G "Ninja" -DCMAKE_BUILD_TYPE=Release ../..
 - cmake --build .

**Cmake flags**
 - -B folder | specify build folder
 - -G "build system" | specify the generator (GNU make, Ninja, Visual Studio etc.), use it with cmake
 - -DCMAKE_BUILD_TYPE=build type(DEBUG) | specify the build type, use it with cmake
 - -DCMAKE_EXPORT_COMPILE_COMMANDS=1 | generates compile_commands.json (can specify this in CMakeLists.txt as well), use it with cmake


**Compile_commands.json**
 - SHOULDNT BE MAINTANED BY HAND!!!!
 - set(CMAKE_EXPORT_COMPILE_COMMANDS ON) or cmake flag | generates the file
 - if you use RELEASE and DEBUG build type cmake flags its generated based on that
 - this helps the IDEs to analyze and understand your sources (go to definiton, find references etc.)
 - build system independence, describes build commands and flags generally (useful when using different build systems or multi-build system environments)
 - should be regenerated every time you add or remove source files, change compiler flags, or other adjustments


**Fetch libraries and dependencies**
 - allows you to automatically download and integrate external projects into cmake
 - it checks if the fetched  content is already download locally or not
 
 - 1. include allows to fetch
 - 2. you can decleare the content with FetchContent_Declare (name, repo, branch)
 - 3. make the fetched content available in this current project
Commands:
```
include(FetchContent)
FetchContent_Declare(
   sfml
   GIT_REPOSITORY https://github.com/SFML/SFML.git
   GIT_TAG        2.5.x
)
FetchContent_MakeAvailable(sfml)
```


**The CMakesLits.txt for the spaceshooter game:**
```
#must start with this
cmake_minimum_required(VERSION 3.10) 
project name and programing language
project(SpaceShooter LANGUAGES CXX)

#set c++ standard
set(CMAKE_CXX_STANDARD 17)

#generate compile_commands.json
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

#set SOURCES variable for source files
set(SOURCES 
    src/main.cpp
    src/game.cpp
) 

#set include(headers) directory
include_directories(${CMAKE_SOURCE_DIR}/include)

#copy resource to the executable folder (TEMP SOLUTION CURRENTLY)
file(COPY ${CMAKE_SOURCE_DIR}/resources DESTINATION ${CMAKE_BINARY_DIR})

#find the SFML libraries on your machine (if installed) (faster builds)
find_package(SFML 2.5 COMPONENTS system window graphics audio network REQUIRED)

#executable
add_executable(spaceshooter ${SOURCES})

#link SFML to the executable
#PRIVATE means it will only link to this app
target_link_libraries(spaceshooter PRIVATE sfml-system sfml-window sfml-graphics sfml-audio sfml-network)

```


## References

CMake: https://cmake.org/cmake/help/latest/

