##
# Copyright (c) 2011 Apple Inc. All rights reserved.
#
# @APPLE_LICENSE_HEADER_START@
#
# This file contains Original Code and/or Modifications of Original Code
# as defined in and that are subject to the Apple Public Source License
# Version 2.0 (the 'License'). You may not use this file except in
# compliance with the License. Please obtain a copy of the License at
# http://www.opensource.apple.com/apsl/ and read it before using this
# file.
#
# The Original Code and all software distributed under the License are
# distributed on an 'AS IS' basis, WITHOUT WARRANTY OF ANY KIND, EITHER
# EXPRESS OR IMPLIED, AND APPLE HEREBY DISCLAIMS ALL SUCH WARRANTIES,
# INCLUDING WITHOUT LIMITATION, ANY WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE, QUIET ENJOYMENT OR NON-INFRINGEMENT.
# Please see the License for the specific language governing rights and
# limitations under the License.
#
# @APPLE_LICENSE_HEADER_END@
##
TESTROOT = ../..
include ${TESTROOT}/include/common.makefile



#
# Test that fine grain re-exports works
#

all-check: all_$(OS_LION_FEATURES) check_$(OS_LION_FEATURES)

all: all_$(OS_LION_FEATURES)

check: check_$(OS_LION_FEATURES)

check_1:
	./main

all_1:
	# build frob
	${CC} ${CCFLAGS} -dynamiclib frob.c -o libfrob.dylib
	# build baz to re-export all of frob
	${CC} ${CCFLAGS} -dynamiclib baz.c -o libbaz.dylib -exported_symbols_list baz.exp libfrob.dylib
	# build bar to re-export all of baz
	${CC} ${CCFLAGS} -dynamiclib bar.c -o libbar.dylib -Wl,-reexport_library,libbaz.dylib
	# build foo to re-export all of bar
	${CC} ${CCFLAGS} -dynamiclib foo.c -o libfoo.dylib -exported_symbols_list foo.exp  libbar.dylib
	# buid main
	${CC} ${CCFLAGS} main.c -I${TESTROOT}/include libfoo.dylib -o main

check_:
	${PASS_IFF} true

all_:
	
clean:
	rm -rf libbar.dylib libfoo.dylib libbaz.dylib libfrob.dylib  main
