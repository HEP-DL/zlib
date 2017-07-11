cmake_minimum_required (VERSION 2.8)

project(zlib)

# cetbuildtools contains our cmake modules
SET ( CETBUILDTOOLS_VERSION $ENV{CETBUILDTOOLS_VERSION} )
IF (NOT CETBUILDTOOLS_VERSION)
    MESSAGE (FATAL_ERROR "ERROR: setup cetbuildtools to get the cmake modules")
ENDIF()

set(CMAKE_MODULE_PATH $ENV{ART_DIR}/Modules
		      $ENV{CETBUILDTOOLS_DIR}/Modules
		      ${CMAKE_MODULE_PATH})

include(CetCMakeEnv)
cet_cmake_env()

cet_set_compiler_flags(DIAGS CAUTIOUS
  WERROR
  NO_UNDEFINED
  EXTRA_FLAGS -pedantic
  EXTRA_CXX_FLAGS -std=c++11 )

cet_report_compiler_flags()

find_ups_product( cetbuildtools v4_14_01 )

#set (ZLIB_EXPORTED_TARGETS "zlib-targets")
add_subdirectory(zlib)
cet_add_to_library_list( zlib )
cet_add_to_library_list( zlibstatic )

#install(EXPORT zlib zlibstatic DESTINATION lib/zlib)
# tests
add_subdirectory(test)

# ups - table and config files
add_subdirectory(ups)



# packaging utility
include(UseCPack)

