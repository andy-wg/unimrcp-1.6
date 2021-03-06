cmake_minimum_required (VERSION 2.8)
project (rtsptest)

# Set source files
set (RTSP_TEST_SOURCES
	src/main.c
	src/parse_gen_suite.c
)
source_group ("src" FILES ${RTSP_TEST_SOURCES})

# Application declaration
add_executable (${PROJECT_NAME} ${RTSP_TEST_SOURCES}
	$<TARGET_OBJECTS:unirtsp>
	$<TARGET_OBJECTS:aprtoolkit>
)
set_target_properties (${PROJECT_NAME} PROPERTIES FOLDER "tests")

# Input libraries
target_link_libraries(${PROJECT_NAME} 
	${APU_LIBRARIES}
	${APR_LIBRARIES}
)
# Input system libraries
if (WIN32)
	target_link_libraries(${PROJECT_NAME} ws2_32 winmm)
elseif (UNIX)
	target_link_libraries(${PROJECT_NAME} m)
endif ()

# Preprocessor definitions
add_definitions (
	${RTSP_DEFINES}
	${APR_TOOLKIT_DEFINES}
	${APR_DEFINES}
	${APU_DEFINES}
)

# Include directories
include_directories (
	${PROJECT_SOURCE_DIR}/include
	${RTSP_INCLUDE_DIRS}
	${APR_TOOLKIT_INCLUDE_DIRS}
	${APR_INCLUDE_DIRS}
	${APU_INCLUDE_DIRS}
)
