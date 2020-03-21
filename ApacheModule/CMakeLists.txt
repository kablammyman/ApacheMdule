project(ApacheModule)
include_directories($ENV{MY_STRING_UTILS} )

include_directories(${CMAKE_SOURCE_DIR}/include) 
IF(WIN32)
include_directories(C:/wamp64/bin/apache/apache2.4.18/include) 
set(MY_STRING_LIB_32_D $ENV{MY_X86_DEBUG_LIBS}/StringUtils.lib)
set(MY_STRING_LIB_64_D $ENV{MY_X64_DEBUG_LIBS}/StringUtils.lib)
set(MY_STRING_LIB_32_R $ENV{MY_X86_RELEASE_LIBS}/StringUtils.lib)
set(MY_STRING_LIB_64_R $ENV{MY_X64_RELEASE_LIBS}/StringUtils.lib)
#LINK_DIRECTORIES(C:/wamp64/bin/apache/apache2.4.18/lib/*.lib)
set(APACHE_LIBS C:/wamp64/bin/apache/apache2.4.18/lib/*.lib)

ELSE()
include_directories(/usr/include) 
#notice the "lib" in front of my stuff
set(MY_STRING_LIB_32_D $ENV{MY_X86_DEBUG_LIBS}/libStringUtils.a)
set(MY_STRING_LIB_64_D $ENV{MY_X64_DEBUG_LIBS}/libStringUtils.a)
set(MY_STRING_LIB_32_R $ENV{MY_X86_RELEASE_LIBS}/libStringUtils.a)
set(MY_STRING_LIB_64_R $ENV{MY_X64_RELEASE_LIBS}/libStringUtils.a)
#LINK_DIRECTORIES(your/library/dir/*.a)
set(APACHE_LIBS your/library/dir/*.a)

ENDIF()

#there are many libs apache needs to make a module, so scoop them up
#LINK_DIRECTORIES(APACHE_LIBS_DIR)

file(GLOB SOURCES
	${PROJECT_SOURCE_DIR}/*.h
	${PROJECT_SOURCE_DIR}/*.cpp)
ADD_LIBRARY(ApacheModule SHARED ${SOURCES})
#shared makes it a .dll, without that, its just a .lib

target_link_libraries (ApacheModule debug ${APACHE_LIBS}  ${MY_STRING_LIB_64_D} )
target_link_libraries (ApacheModule optimized ${APACHE_LIBS}  ${MY_STRING_LIB_64_D} )

