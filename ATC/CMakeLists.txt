aux_source_directory(. SRC_LIST)

file(GLOB HEADERS "*.h")

add_executable(ATC ${SRC_LIST} ${HEADERS})
 
 
find_package(ATC)
find_package(Web3)

target_include_directories(ATC PRIVATE ..)
target_link_libraries(ATC ${ATC_EVM_LIBRARIES})
target_link_libraries(ATC ${Web3_WEB3JSONRPC_LIBRARIES})
target_link_libraries(ATC ${Web3_WEBTHREE_LIBRARIES})

if (EVMJIT)
	# Do we need include paths here?
	target_link_libraries(ATC ${ATC_EVMJIT_LIBRARIES})
	ATC_copy_dlls(EVMJIT_DLLS)
endif()

if (UNIX AND NOT APPLE)
	target_link_libraries(ATC pthread)
endif()

install(TARGETS DESTINATION bin)


