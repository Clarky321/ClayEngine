cmake_minimum_required(VERSION 3.12)

set(PROJECT_NAME ClayEngine)
project(${PROJECT_NAME})

add_subdirectory(ClayEngineCore)

add_subdirectory(ClayEngineEditor)

set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ClayEngineEditor)