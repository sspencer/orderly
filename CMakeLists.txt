# Copyright 2009, Lloyd Hilaiel.
# 
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are
# met:
# 
#  1. Redistributions of source code must retain the above copyright
#     notice, this list of conditions and the following disclaimer.
# 
#  2. Redistributions in binary form must reproduce the above copyright
#     notice, this list of conditions and the following disclaimer in
#     the documentation and/or other materials provided with the
#     distribution.
# 
#  3. Neither the name of Lloyd Hilaiel nor the names of its
#     contributors may be used to endorse or promote products derived
#     from this software without specific prior written permission.
# 
# THIS SOFTWARE IS PROVIDED BY THE AUTHOR ``AS IS'' AND ANY EXPRESS OR
# IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
# WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
# DISCLAIMED. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY DIRECT,
# INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
# (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
# SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION)
# HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT,
# STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING
# IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
# POSSIBILITY OF SUCH DAMAGE.

CMAKE_MINIMUM_REQUIRED(VERSION 2.6)

PROJECT(YetAnotherJSONParser)

SET (ORDERLY_MAJOR 0)
SET (ORDERLY_MINOR 0)
SET (ORDERLY_MICRO 1)

SET (ORDERLY_DIST_NAME "orderly-${ORDERLY_MAJOR}.${ORDERLY_MINOR}.${ORDERLY_MICRO}")

IF (NOT CMAKE_BUILD_TYPE)
  SET(CMAKE_BUILD_TYPE "Debug")
ENDIF (NOT CMAKE_BUILD_TYPE)

SET(CMAKE_C_FLAGS "-Wall")
IF (WIN32) 
  SET(linkFlags "/PDB:NONE /INCREMENTAL:NO /OPT:NOREF /OPT:NOICF")
  SET(CMAKE_EXE_LINKER_FLAGS    "${linkFlags}"
      CACHE STRING "ORDERLY linker flags" FORCE)
  SET(CMAKE_EXE_LINKER_FLAGS_DEBUG ""
      CACHE STRING "ORDERLY debug linker flags" FORCE)
  SET(CMAKE_EXE_LINKER_FLAGS_RELEASE
      CACHE STRING "ORDERLY release linker flags" FORCE)
  SET(CMAKE_SHARED_LINKER_FLAGS "${linkFlags}"
      CACHE STRING "ORDERLY shared linker flags" FORCE)
  SET(CMAKE_MODULE_LINKER_FLAGS "${linkFlags}"
      CACHE STRING "ORDERLY module linker flags" FORCE)

  SET(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} /wd4996 /wd4255 /wd4130 /wd4100 /wd4711")
  SET(CMAKE_C_FLAGS_DEBUG "/D DEBUG /Od /Z7")
  SET(CMAKE_C_FLAGS_RELEASE "/D NDEBUG /O2")
ELSE (WIN32)
  SET(CMAKE_C_FLAGS
      "${CMAKE_C_FLAGS} -fPIC -std=c99 -pedantic -Wpointer-arith -Wno-format-y2k -Wstrict-prototypes -Wmissing-declarations -Wnested-externs -Wextra	-Wundef -Wwrite-strings -Wold-style-definition -Wno-missing-field-initializers -Wredundant-decls -Wno-unused-parameter -Wno-sign-compare -Wmissing-prototypes")

  SET(CMAKE_C_FLAGS_DEBUG "-DDEBUG -g")
  SET(CMAKE_C_FLAGS_RELEASE "-DNDEBUG -O2 -Wuninitialized")
ENDIF (WIN32) 


ADD_SUBDIRECTORY(src)
ADD_SUBDIRECTORY(test)
ADD_SUBDIRECTORY(reformatter)
ADD_SUBDIRECTORY(checker)

#INCLUDE(ORDERLYDoc.cmake)

# a test target
#ADD_CUSTOM_TARGET(test
#                  ./run_tests.sh
#                  WORKING_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/test)

