cmake_minimum_required(VERSION 3.0.0)
project(lucygl VERSION 0.1.0)

include(CTest)
enable_testing()

set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS 1)

set(CMAKE_CXX_STANDARD 20)

add_library(lucygl SHARED
	src/OpenGL/DrawCall.cpp
	src/OpenGL/FrameBuffer.cpp
	src/OpenGL/Functions.cpp
	src/OpenGL/IndexBuffer.cpp
	src/OpenGL/Make.cpp
	src/OpenGL/Shader.cpp
	src/OpenGL/Status.cpp
	src/OpenGL/Texture.cpp
	src/OpenGL/Types.cpp
	src/OpenGL/UniformBuffer.cpp
	src/OpenGL/VertexArray.cpp
	src/OpenGL/VertexBuffer.cpp
)

find_package(SDL2 CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE SDL2::SDL2 SDL2::SDL2main)

find_package(implot CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE implot::implot)

find_package(imgui CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE imgui::imgui)

find_package(imguizmo CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE imguizmo::imguizmo)

find_package(nlohmann_json CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE nlohmann_json nlohmann_json::nlohmann_json)

find_package(assimp CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE assimp::assimp)

find_package(yaml-cpp CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE yaml-cpp)

find_path(STB_INCLUDE_DIRS "stb_c_lexer.h")
target_include_directories(lucygl PRIVATE ${STB_INCLUDE_DIRS})

find_package(EnTT CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE EnTT::EnTT)

find_package(glm CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE glm::glm)

find_package(glad CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE glad::glad)

find_package(stduuid CONFIG REQUIRED)
target_link_libraries(lucygl PRIVATE stduuid)

# target_link_libraries(lucygl PRIVATE)

set_target_properties(lucygl PROPERTIES VERSION ${PROJECT_VERSION})
set_target_properties(lucygl PROPERTIES SOVERSION 1)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/DrawCall.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/FrameBuffer.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/Functions.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/IndexBuffer.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/LucyGL.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/Make.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/Shader.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/Status.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/Texture.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/Types.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/UniformBuffer.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/VertexArray.h)
# set_target_properties(lucygl PROPERTIES PUBLIC_HEADER include/LucyGL/VertexBuffer.h)
target_include_directories(lucygl PUBLIC include/LucyGL)
target_include_directories(lucygl PUBLIC src)
include(GNUInstallDirs)
install(TARGETS lucygl
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR})

configure_file(lucygl.pc.in lucygl.pc @ONLY)
install(FILES ${CMAKE_BINARY_DIR}/lucygl.pc DESTINATION ${CMAKE_INSTALL_DATAROOTDIR}/pkgconfig)

include(C:/Users/krishnadev/vcpkg/scripts/buildsystems/vcpkg.cmake)
include_directories("./include/" "./dependencies/include/" src C:/Users/krishnadev/vcpkg/installed/x64-windows/include "C:/Program Files/Microsoft Visual Studio/2022/Community/VC/Tools/MSVC/14.32.31326/include/")

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)