project(android)

include_directories(
  system/core/include/arch/${OS_FAMILY}-${ARCH}
  system/core/include
  libnativehelper/include/nativehelper
)

if( WINDOWS )
	include_directories(
	  libcore/luni/src/main/native
	)
  add_definitions(-DMINGW_HAS_SECURE_API=1)

endif() 

add_definitions(-DICU_DATA_DIR="/usr/share/icu")
if(IOS AND X86)
  add_definitions(-DICU_DATA_DIR_PREFIX_ENV_VAR="IPHONE_SIMULATOR_ROOT")
endif()
add_definitions(-DHAVE_ANDROID_OS=1)

# CARL set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -include AndroidConfig.h")
# CARL set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -include AndroidConfig.h")

# CARL add_subdirectory(dalvik)
# TMP add_subdirectory(libcore)
add_subdirectory(libnativehelper)
add_subdirectory(external/expat)
add_subdirectory(external/fdlibm)
# TMP add_subdirectory(external/icu4c)
# CARL add_subdirectory(external/javasqlite)
# TMP add_subdirectory(external/openssl)
if(NOT DARWIN)
  # Mac OS X and iOS ships with sqlite so we'll just use that
  add_subdirectory(external/sqlite)
endif()
add_subdirectory(external/zlib)
set(ANDROID_OBJECTS
# CARL  ${DALVIK_OBJECTS} 
# TMP  ${LIBCORE_OBJECTS} 
  ${LIBNATIVEHELPER_OBJECTS} 
  ${EXTERNAL_EXPAT_OBJECTS} 
  ${EXTERNAL_FDLIBM_OBJECTS}
# TMP  ${EXTERNAL_ICU4C_OBJECTS}
# CARL  ${EXTERNAL_JAVASQLITE_OBJECTS}
# TMP  ${EXTERNAL_OPENSSL_OBJECTS}
  ${EXTERNAL_SQLITE_OBJECTS}
  ${EXTERNAL_ZLIB_OBJECTS}
  PARENT_SCOPE
)
