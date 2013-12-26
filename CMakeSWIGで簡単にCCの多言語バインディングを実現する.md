今ではすっかり有名になったCMakeとSWIGですが、この二つを組み合わせると簡単にC/C++のグルーコードを生成できます。

Advent Calendar2013を締めくくるにしてはショボい内容ですいません...

#PythonからC++のコードを使用する

##ディレクトリ構成

 * CMakeLists.txt
 * example.h
 * example.i
 * **build**

##テストプログラム

```cmake:CMakeList.txt
find_package(PythonLibs REQUIRED)
find_package(SWIG REQUIRED)
include(${SWIG_USE_FILE})
include(GenerateExportHeader)

include_directories(
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${PROJECT_BINARY_DIR}
    ${PYTHON_INCLUDE_PATH}
)

set(EXAM_SRCS
    example.h
)

set(INTERFACE_FILES
    example.i
)

set_source_files_properties(${INTERFACE_FILES} PROPERTIES CPLUSPLUS   ON)
swig_add_module(example python ${INTERFACE_FILES}
    ${EXAM_SRCS}
)

swig_link_libraries(example
    ${PYTHON_LIBRARIES}
)
```

```cpp:example.h
#pragma once
#include <string>
class ExampleClass{
    std::string m_msg;
public:
    ExampleClass() : m_msg("Hello World") { }
    const std::string& get_msg(){ return m_msg; }
    void set_msg(const std::string &msg){ m_msg = msg; }
};
```

```cpp:example.i
%module example
%include "std_string.i"

%{
#define SWIG_FILE_WITH_INIT
%}
%{
#include "example.h"
%}

%include "example.h"

```

##ビルド

    $cd build && cmake .. && make

##実行
    $python
    >>> import example
    >>> e = example.ExampleClass()
    >>> e.get_msg()
    'Hello World'
    >>> e.set_msg("FizzBuzz")
    >>> e.get_msg()
    'FizzBuzz'

#他の言語では

CMakeLists.txtで他言語を指定すれば使えます。





