set(INCROOT ${PROJECT_SOURCE_DIR}/include/Galileo/Framework)
set(SRCROOT ${PROJECT_SOURCE_DIR}/src/Galileo/Framework)

# all source files
file(GLOB INCS "${INCROOT}/*.h")
file(GLOB SRCS "${SRCROOT}/*.cpp")

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "${Galileo_SOURCE_DIR}/bin")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${Galileo_SOURCE_DIR}/bin")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "${Galileo_SOURCE_DIR}/bin")

set(Qt6WidgetsTools_DIR "${Qt6_DIR}WidgetsTools")
set(Qt6CoreTools_DIR "${Qt6_DIR}CoreTools")
set(Qt6GuiTools_DIR "${Qt6_DIR}GuiTools")

# Find the QtWidgets library
find_package(Qt6 COMPONENTS Core Widgets REQUIRED)

# Tell CMake to run moc when necessary:
set(CMAKE_AUTOMOC ON)


# As moc files are generated in the binary dir, tell CMake
# to always look for includes there:
include_directories("${Galileo_SOURCE_DIR}/bin")

# We need add -DQT_WIDGETS_LIB when using QtWidgets in Qt 5.
#add_definitions(${Qt5Widgets_DEFINITIONS})

add_library(Framework SHARED ${SRCS} ${INCS})

target_link_libraries(Framework Qt6::Widgets Qt6::Core)