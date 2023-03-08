# cmake-helper-modules
Custom helper modules for CMake projects


## Usage

To use this package, either place it on your default `CMAKE_MODULE_PATH` (or add custom path to it) and include the desired module:

```
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "<path>/cmake")
include(CMakeFetchHelpers)
```


Alternatively, the [FetchContent](https://cmake.org/cmake/help/latest/module/FetchContent.html) module can be used to ensure this package is available at configure time without having to configure it locally:

```
## Get custom helper modules from remote repository
include(CMakeFetchHelpers OPTIONAL RESULT_VARIABLE CMakeFetchHelpers_FOUND)
if(CMakeFetchHelpers_FOUND)
    message(WARNING "Found CMakeFetchHelpers!")
else()
    include(FetchContent)
    FetchContent_Declare(cmake-helper-modules
        GIT_REPOSITORY  https://github.com/joaocandre/CMakeHelpers
        GIT_TAG main
    )
    FetchContent_MakeAvailable(cmake-helper-modules)
    set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${cmake-helper-modules_SOURCE_DIR}/cmake")
    include(CMakeFetchHelpers)
endif()
```
