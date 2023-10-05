cmake_minimum_required (VERSION 3.8)

if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project ("CMakeProject1")

add_executable (CMakeProject1 "App.cpp")

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET CMakeProject1 PROPERTY CXX_STANDARD 20)
endif()

add_subdirectory(external/glfw)
add_subdirectory(external/glad/cmake)
add_subdirectory(external/glm)

target_include_directories(${PROJECT_NAME} 
	PUBLIC 
		external/glfw/include
)

target_link_directories(${PROJECT_NAME}
	PUBLIC
		external/glfw/src
) 

target_link_libraries(${PROJECT_NAME}
	glfw
	opengl32
)

