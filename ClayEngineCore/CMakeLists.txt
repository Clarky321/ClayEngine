cmake_minimum_required(VERSION 3.12)

include(FetchContent)

set(ENGINE_PROJECT_NAME ClayEngineCore)

# Fetch SDL2
FetchContent_Declare(
    sdl2
    GIT_REPOSITORY https://github.com/libsdl-org/SDL.git
    GIT_TAG release-2.0.22
)

FetchContent_MakeAvailable(sdl2)  # Эта команда автоматически настраивает SDL2

# Fetch ImGui
FetchContent_Declare(
    imgui
    GIT_REPOSITORY https://github.com/ocornut/imgui.git
    GIT_TAG docking
)

FetchContent_GetProperties(imgui)
if(NOT imgui_POPULATED)
    FetchContent_Populate(imgui)
    file(GLOB IMGUI_SOURCES ${imgui_SOURCE_DIR}/*.cpp ${imgui_SOURCE_DIR}/backends/imgui_impl_sdl2.cpp ${imgui_SOURCE_DIR}/backends/imgui_impl_sdlrenderer2.cpp)
    file(GLOB IMGUI_HEADERS ${imgui_SOURCE_DIR}/*.h ${imgui_SOURCE_DIR}/backends/imgui_impl_sdl2.h ${imgui_SOURCE_DIR}/backends/imgui_impl_sdlrenderer2.h)
    add_library(ImGui STATIC ${IMGUI_SOURCES} ${IMGUI_HEADERS})
    target_include_directories(ImGui PUBLIC ${imgui_SOURCE_DIR} ${imgui_SOURCE_DIR}/backends)
endif()

target_include_directories(ImGui PUBLIC ${sdl2_SOURCE_DIR}/include)  # Добавляем пути к SDL2 для ImGui

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

target_include_directories(${ENGINE_PROJECT_NAME} PUBLIC includes ${sdl2_SOURCE_DIR}/include)

target_compile_features(${ENGINE_PROJECT_NAME} PUBLIC cxx_std_17)

target_link_libraries(${ENGINE_PROJECT_NAME} SDL2-static SDL2main ImGui)
