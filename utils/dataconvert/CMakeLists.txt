
include_directories( ${ENGINE_COMMON_INCLUDES} )


########### next target ###############

set(dataconvert_LIB_SRCS dataconvert.cpp)

add_library(dataconvert SHARED ${dataconvert_LIB_SRCS})

install(TARGETS dataconvert DESTINATION ${ENGINE_LIBDIR} COMPONENT columnstore-libs)
