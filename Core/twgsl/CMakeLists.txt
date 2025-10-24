set(SOURCES
    "Source/main.cpp")

add_executable(twgsl ${SOURCES})
target_link_libraries(twgsl PRIVATE tint_api)
target_link_options(twgsl
    PRIVATE
    -sEXPORTED_FUNCTIONS=["_test","_spirv_to_wgsl","_free","_malloc"]
    -sEXPORTED_RUNTIME_METHODS=["HEAPU8","HEAPU32"]
    --js-library=${CMAKE_CURRENT_SOURCE_DIR}/Source/callbacks.js
    --extern-pre-js=${CMAKE_CURRENT_SOURCE_DIR}/head.js
    --extern-post-js=${CMAKE_CURRENT_SOURCE_DIR}/tail.js
    PUBLIC
    -sSTACK_SIZE=1MB
    -sALLOW_MEMORY_GROWTH=1
)

set_target_properties(twgsl PROPERTIES
    INTERPROCEDURAL_OPTIMIZATION_RELEASE ON
)
