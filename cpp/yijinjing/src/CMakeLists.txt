AUX_SOURCE_DIRECTORY(journal SOURCE_FILES_JOURNAL)
AUX_SOURCE_DIRECTORY(nanomsg SOURCE_FILES_NANOMSG)
AUX_SOURCE_DIRECTORY(service SOURCE_FILES_SERVICE)
AUX_SOURCE_DIRECTORY(time SOURCE_FILES_TIME)

ADD_LIBRARY(${PROJECT_NAME} SHARED
        ${SOURCE_FILES_JOURNAL}
        ${SOURCE_FILES_NANOMSG}
        ${SOURCE_FILES_SERVICE}
        ${SOURCE_FILES_TIME}
        )
SET_TARGET_PROPERTIES(${PROJECT_NAME} PROPERTIES LINKER_LANGUAGE CXX)

IF(WIN32)
    TARGET_LINK_LIBRARIES(${PROJECT_NAME} nanomsg SQLiteCpp fmt ${Boost_LIBRARIES})
ENDIF()
IF(UNIX)
    TARGET_LINK_LIBRARIES(${PROJECT_NAME} nanomsg SQLiteCpp fmt iconv ${Boost_LIBRARIES})
ENDIF()
