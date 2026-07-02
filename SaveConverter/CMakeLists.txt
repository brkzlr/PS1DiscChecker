add_executable(save_converter src/main.c src/aes.c src/sha1.c)
include_directories(include)
set_target_properties(save_converter PROPERTIES
	C_STANDARD 11
	C_STANDARD_REQUIRED ON
	C_EXTENSIONS OFF
	EXPORT_COMPILE_COMMANDS ON
	RUNTIME_OUTPUT_DIRECTORY "${CMAKE_SOURCE_DIR}/bin"
)
target_compile_options(save_converter PRIVATE -pedantic-errors)
# Disable unused AES modes for all translation units so struct AES_ctx has one layout everywhere
target_compile_definitions(save_converter PRIVATE CTR=0 CBC=0)

install(TARGETS save_converter RUNTIME DESTINATION bin)
