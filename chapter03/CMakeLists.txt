cmake_minimum_required(VERSION 3.18)

set(TO-BUILD
    enum_gpu
    hello_world
    set_gpu
    simple_device_call
    simple_kernel
    simple_kernel_params
    )

foreach(exec IN LISTS TO-BUILD)
    project(${exec} LANGUAGES C CUDA)
    add_executable(${exec} ${exec}.cu)
    target_compile_options(${exec} PRIVATE $<$<COMPILE_LANGUAGE:CUDA>:--expt-relaxed-constexpr>)
    set_property(TARGET ${exec} PROPERTY CUDA_ARCHITECTURES OFF)
endforeach()
