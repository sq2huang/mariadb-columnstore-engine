
include_directories( ${ENGINE_COMMON_INCLUDES} )


########### next target ###############

set(rowgroup_LIB_SRCS rowaggregation.cpp rowgroup.cpp)

#librowgroup_la_CXXFLAGS = $(march_flags) $(AM_CXXFLAGS)

add_library(rowgroup SHARED ${rowgroup_LIB_SRCS})

target_link_libraries(rowgroup ${NETSNMP_LIBRARIES} funcexp)

install(TARGETS rowgroup DESTINATION ${ENGINE_LIBDIR} COMPONENT columnstore-libs)

