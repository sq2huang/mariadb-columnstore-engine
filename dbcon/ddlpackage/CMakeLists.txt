INCLUDE_DIRECTORIES( ${ENGINE_COMMON_INCLUDES} )

#TODO: put generated files in the binary directory
ADD_CUSTOM_COMMAND(
    OUTPUT ${CMAKE_CURRENT_SOURCE_DIR}/ddl-gram.cpp ${CMAKE_CURRENT_SOURCE_DIR}/ddl-scan.cpp
    COMMAND /bin/sh ./ddl-gram.sh ${BISON_EXECUTABLE}
    COMMAND /bin/sh ./ddl-scan.sh ${LEX_EXECUTABLE}
    WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}
    DEPENDS ddl.y ddl.l
)

set_source_files_properties(ddl-scan.cpp PROPERTIES COMPILE_FLAGS -Wno-sign-compare)

########### next target ###############

ADD_LIBRARY(ddlpackage SHARED
    serialize.cpp
    ddl-scan.cpp
    ddl-gram.cpp
    ddlpkg.cpp
    columndef.cpp
    createtable.cpp
    tabledef.cpp
    sqlstatement.cpp
    sqlstatementlist.cpp
    altertable.cpp
    createindex.cpp
    dropindex.cpp
    droptable.cpp
    sqlparser.cpp
    markpartition.cpp
    restorepartition.cpp
    droppartition.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/ddl-gram.cpp 
    ${CMAKE_CURRENT_SOURCE_DIR}/ddl-scan.cpp
    )

INSTALL(TARGETS ddlpackage DESTINATION ${ENGINE_LIBDIR} COMPONENT columnstore-libs)

