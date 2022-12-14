cmake_minimum_required(VERSION 3.16.3)

project(rnx2rtkp)

set (RTKLIB_SRC ${CMAKE_CURRENT_SOURCE_DIR}/src)

include_directories(RTKLIB_SRC)

set (SRC
    ${RTKLIB_SRC}/rnx2rtkp.c
    ${RTKLIB_SRC}/rtkcmn.c
    ${RTKLIB_SRC}/rinex.c
    ${RTKLIB_SRC}/rtkpos.c
    ${RTKLIB_SRC}/postpos.c
    ${RTKLIB_SRC}/solution.c
    ${RTKLIB_SRC}/lambda.c
    ${RTKLIB_SRC}/geoid.c
    ${RTKLIB_SRC}/sbas.c
    ${RTKLIB_SRC}/preceph.c
    ${RTKLIB_SRC}/pntpos.c
    ${RTKLIB_SRC}/ephemeris.c
    ${RTKLIB_SRC}/options.c
    ${RTKLIB_SRC}/ppp.c
    ${RTKLIB_SRC}/ppp_ar.c
    ${RTKLIB_SRC}/rtcm.c
    ${RTKLIB_SRC}/rtcm2.c
    ${RTKLIB_SRC}/rtcm3.c
    ${RTKLIB_SRC}/rtcm3e.c
    ${RTKLIB_SRC}/ionex.c
    ${RTKLIB_SRC}/tides.c
)

set (TARGET_NAME rnx2rtkp)

add_executable(${TARGET_NAME} ${SRC})

if(WIN32)
  target_link_libraries(${TARGET_NAME} wsock32 ws2_32 winmm)
endif()

target_compile_definitions(${TARGET_NAME} PRIVATE WIN32 TRACE ENAGLO ENAQZS ENAGAL ENACMP ENAIRN NFREQ=5)

if(WIN32)
   target_compile_options(${TARGET_NAME} PRIVATE -Wall -O3 -ansi -pedantic -g)
else()
   target_compile_options(${TARGET_NAME} PRIVATE -Wall -O3 -ansi -pedantic -Wno-unused-but-set-variable -g)
endif()