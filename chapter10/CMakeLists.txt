cmake_minimum_required(VERSION 3.18)

set(TO-BUILD
    basic_single_stream
    basic_double_stream
    basic_double_stream_correct
    copy_timed
    )

foreach(exec IN LISTS TO-BUILD)
    project(${exec} LANGUAGES C CUDA)
    add_executable(${exec} ${exec}.cu)
    target_link_libraries(${exec} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}/../lib/glut64.lib)
    target_compile_options(${exec} PRIVATE $<$<COMPILE_LANGUAGE:CUDA>:--expt-relaxed-constexpr>)
    set_property(TARGET ${exec} PROPERTY CUDA_ARCHITECTURES OFF)
endforeach()
