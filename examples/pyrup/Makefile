APPSOURCES =xf_pyr_up_tb.cpp xf_pyr_up_accel.cpp
EXECUTABLE = pyrup.elf
VERBOSE = #-verbose
PLATFORM = <path-to-reVISION-platform>
SDSCC_FLAGS = -sds-pf ${PLATFORM} -std=c++11  -sds-hw "xFPyrUp <0, 2160, 3840, 1>" xf_pyr_up_accel.cpp -files ./include/imgproc/xf_pyr_up.hpp -clkid 2 -sds-end -dmclkid 2
${VERBOSE}
CC = sds++ ${SDSCC_FLAGS}

IDIRS = -I. -I${SYSROOT}/usr/include -I ./include

LDIRS = --sysroot=${SYSROOT} -L=/lib -L=/usr/lib -Wl,-rpath-link=${SYSROOT}/lib,-rpath-link=${SYSROOT}/usr/lib
LLIBS = -lopencv_core -llzma -ltiff -lpng16 -lz -ljpeg -lopencv_imgproc -lopencv_imgcodecs -ldl -lrt -lwebp -lopencv_features2d -lopencv_flann
OLEVEL = -ggdb
CFLAGS = -Wall ${OLEVEL} -c ${IDIRS} -DHLS_NO_XIL_FPO_LIB -DXI_REL=${XI_REL}
LFLAGS = ${OLEVEL} ${LDIRS} ${LLIBS}
SOURCES := $(patsubst %,./%,$(APPSOURCES))
OBJECTS := $(APPSOURCES:.cpp=.o)
DEPS := $(OBJECTS:.o=.d)
.PHONY: all
all: ${EXECUTABLE}
${EXECUTABLE}: ${OBJECTS}
	${CC} ${OBJECTS} ${LFLAGS} -o $@
-include ${DEPS}
%.o: %.cpp
	${CC} ${CFLAGS} $< -o $@
clean:
	${RM} ${EXECUTABLE} ${OBJECTS}
ultraclean: clean
	${RM} -rf _sds sd_card ${EXECUTABLE}.bit
copy:
	/bin/cp -prf ${XLNX_SRC_PATH}/pyrup/example .
	/bin/cp -prf ${XLNX_SRC_PATH}/pyrup/src .
