cmake_minimum_required(VERSION 3.12)

set(ENGINE_PROJECT_NAME ClayEngineCore)

set(ENGINE_PUBLIC_INCLUDES

	includes/ClayEngineCore/test.h

)

set(ENGINE_PRIVATE_SOURCES

	src/ClayEngineCore/test.cpp
)

set(ENGINE_ALL_SOURCE
	${ENGINE_PUBLIC_INCLUDES}
	${ENGINE_PRIVATE_SOURCES}
)

add_library(${ENGINE_PROJECT_NAME} STATIC ${ENGINE_ALL_SOURCE})

source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${ENGINE_ALL_SOURCE})

target_include_directories(${ENGINE_PROJECT_NAME}
	PUBLIC
		includes
	PRIVATE
		src
)

target_compile_features(${ENGINE_PROJECT_NAME} PUBLIC cxx_std_17)