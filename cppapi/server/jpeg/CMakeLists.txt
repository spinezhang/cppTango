set(SOURCES jpeg_bitstream.cpp
            jpeg_color.cpp
            jpeg_dct.cpp
            jpeg_decoder.cpp
            jpeg_encoder.cpp
            jpeg_memory.cpp)
if(WIN32)
    add_library(jpeg_objects_dyn OBJECT ${SOURCES})
    add_library(jpeg_objects_sta OBJECT ${SOURCES})
    target_compile_definitions(jpeg_objects_dyn PRIVATE "${dyn_defs}")
    target_compile_definitions(jpeg_objects_sta PRIVATE "${static_defs}")

    if(CMAKE_BUILD_TYPE STREQUAL "Debug")
        target_compile_options(jpeg_objects_sta PRIVATE "/MTd")
    else()
        target_compile_options(jpeg_objects_sta PRIVATE "/MT")
    endif()
else(WIN32)
    add_library(jpeg_objects OBJECT ${SOURCES})
    target_compile_options(jpeg_objects PRIVATE -fPIC)
endif(WIN32)
