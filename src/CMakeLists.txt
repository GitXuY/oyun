
##########
# Add a few things for some CMake parameters
##########
add_definitions (-DOYUN_VERSION=${OYUN_VERSION})
add_definitions (-DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX})
if (CMAKE_BUILD_TYPE STREQUAL "")
  # Don't let things build without a build type (default to Release)
  set (CMAKE_BUILD_TYPE "Release")
endif()


##########
# Get the source lists
##########
file (GLOB_RECURSE OYUN_SOURCE *.cpp)
if (MSVC OR WIN32)
  list (APPEND OYUN_SOURCE "${CMAKE_SOURCE_DIR}/build/oyun.rc")
endif()
file (GLOB_RECURSE OYUN_HEADERS *.h)

file (GLOB_RECURSE TEST_SOURCE common/*.cpp game/*.cpp tourney/*.cpp)
file (GLOB_RECURSE TEST_HEADERS common/*.h game/*.h tourney/*.h)


##########
# Add CppUnitLite directories
##########
include_directories (${CMAKE_SOURCE_DIR}/lib/CppUnitLite)
link_directories (${CMAKE_BINARY_DIR}/lib/CppUnitLite)


##########
# Link wxWidgets
##########
find_package (wxWidgets REQUIRED base core adv html)
include (${wxWidgets_USE_FILE})


##########
# Link the executable
##########
if (APPLE)
  set (OYUN_TARGET "Oyun")
else ()
  set (OYUN_TARGET "oyun")
endif ()

add_executable (${OYUN_TARGET} ${OYUN_SOURCE} ${OYUN_HEADERS})
target_link_libraries (${OYUN_TARGET} ${wxWidgets_LIBRARIES})

add_executable (oyun_test ${TEST_SOURCE} ${TEST_HEADERS})
target_link_libraries (oyun_test cppunitlite ${wxWidgets_LIBRARIES})


##########
# Set executable properties
##########
if (MSVC OR WIN32)
  set_target_properties (${OYUN_TARGET} PROPERTIES WIN32_EXECUTABLE TRUE)
elseif (APPLE)
  set_target_properties (${OYUN_TARGET} PROPERTIES MACOSX_BUNDLE TRUE)
  
  set_target_properties (${OYUN_TARGET} PROPERTIES MACOSX_BUNDLE_INFO_STRING "${OYUN_VERSION}")
  set_target_properties (${OYUN_TARGET} PROPERTIES MACOSX_BUNDLE_ICON_FILE "${CMAKE_SOURCE_DIR}/build/oyun.icns")
  set_target_properties (${OYUN_TARGET} PROPERTIES MACOSX_BUNDLE_GUI_IDENTIFIER "net.charlespence.oyun")
  set_target_properties (${OYUN_TARGET} PROPERTIES MACOSX_BUNDLE_LONG_VERSION_STRING "${OYUN_VERSION}")
  set_target_properties (${OYUN_TARGET} PROPERTIES MACOSX_BUNDLE_BUNDLE_NAME "Oyun")
  set_target_properties (${OYUN_TARGET} PROPERTIES MACOSX_BUNDLE_SHORT_VERSION_STRING "${OYUN_VERSION}")
  set_target_properties (${OYUN_TARGET} PROPERTIES MACOSX_BUNDLE_COPYRIGHT "Copyright (C) 2004-2011 Charles Pence")
endif ()

set_target_properties (oyun_test PROPERTIES COMPILE_DEFINITIONS "BUILD_TESTS")


##########
# Install the executable
##########
install (TARGETS ${OYUN_TARGET} 
  RUNTIME DESTINATION bin
  BUNDLE DESTINATION .)
