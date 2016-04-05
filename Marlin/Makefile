# Makefile for building Marlin with avr-gcc and avr-g++
# Copyright (C) 2015-2016 Aleph Objects Inc.

# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

CC = ${bindir}/avr-gcc
CFLAGS = -c -g -Os -w -std=gnu11 -ffunction-sections -fdata-sections -MMD

CXX = ${bindir}/avr-g++
CXXFLAGS = -c -g -Os -w -std=gnu++11 -fno-exceptions -ffunction-sections -fdata-sections -fno-threadsafe-statics

CPPFLAGS = -mmcu=atmega2560 -DF_CPU=16000000L -DARDUINO=10608 -DARDUINO_AVR_RAMBO -DARDUINO_ARCH_AVR   "-I${ardcoresdir}" "-I${rambodir}"

AR = ${bindir}/avr-ar
ARFLAGS = rcs  "${coredir}/core.a"

OBJCOPY = ${bindir}/avr-objcopy
OBJFLAGS = -O ihex

ARD = ${toolsdir}/arduino-builder
ADRFLAGS = -logger=machine -hardware "${hardwdir}" -tools "${toolsbdir}" -tools "${avrdir}" -built-in-libraries "${libdir}" -libraries "${libdir}" -fqbn=arduino:avr:rambo -vid-pid=0X27B1_0X0001 -ide-version=10608 -build-path "${builddir}" -warnings=none -prefs=build.warn_data_percentage=75 -verbose "${basedir}/Marlin.ino"

CTAGS = ${ctagsdir}/ctags
CTAGSFLAGS = -u --language-force=c++ -f - --c++-kinds=svpf --fields=KSTtzns --line-directives "${preprocdir}/ctags_target_for_gcc_minus_e.cpp"

RM_RF = rm -rf
MKDIR_P = mkdir -p
LN_F = ln -f

basedir = .
# required for arduino-builder -dump-prefs -build-path argument
builddir = $(shell pwd)/obj
objdir = ${basedir}/obj
sketchdir = ${objdir}/sketch
preprocdir = ${objdir}/preproc
arddir = ${basedir}${basedir}/ArduinoAddons/Arduino_1.6.x
libdir = ${arddir}/libraries
hardwdir = ${arddir}/hardware
coresdir = ${hardwdir}/arduino/avr/cores
ardcoresdir = ${coresdir}/arduino
rambodir = ${hardwdir}/arduino/avr/variants/rambo
coredir = ${objdir}/core
toolsdir = ${hardwdir}/tools
avrdir = ${toolsdir}/avr
bindir = ${avrdir}/bin
toolsbdir = ${toolsdir}/tools-builder
ctagsdir = ${toolsbdir}/ctags/5.8-arduino10
nulldir = /dev/null

DEST ?= ${basedir}
MACHINE = $(shell git rev-parse --abbrev-ref HEAD)
NOW = $(shell date +"%b_%d_%y")
VERSION = v$(shell grep -oP "\"1.*.*\" " ${basedir}/Default_Version.h | cut -d \" -f 2)
HASH = $(shell git rev-parse --verify HEAD --short)

all:
	$(RM_RF) ${sketchdir}/*  # required to build consecutively without running make clean
	$(LN_F) ${basedir}/Marlin.ino ${basedir}/Marlin.ino.cpp
	$(MKDIR_P) ${objdir}
	$(ARD) -dump-prefs $(ADRFLAGS)
	$(ARD) -compile $(ADRFLAGS)
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/Marlin.ino.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/M100_Free_Mem_Chk.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/Marlin.ino.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/MarlinSerial.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/Marlin_main.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/Sd2Card.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/SdBaseFile.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/SdFatUtil.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/SdFile.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/SdVolume.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/blinkm.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/buzzer.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/cardreader.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/configuration_store.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/dac_mcp4728.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/digipot_mcp4451.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/mesh_bed_leveling.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/planner.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/qr_solve.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/servo.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/stepper.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/stepper_dac.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/stepper_indirection.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/temperature.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/ultralcd.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/vector_3.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/watchdog.cpp" -o "${nulldir}"
	"$(CXX)" $(CXXFLAGS)  -w -x c++ -E -CC $(CPPFLAGS) "${basedir}/Marlin.ino.cpp" -o "${preprocdir}ctags_target_for_gcc_minus_e.cpp"
	"$(CTAGS)" $(CTAGSFLAGS)
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/M100_Free_Mem_Chk.cpp" -o "${objdir}/M100_Free_Mem_Chk.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/Marlin.ino.cpp" -o "${objdir}/Marlin.ino.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/MarlinSerial.cpp" -o "${objdir}/MarlinSerial.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/Marlin_main.cpp" -o "${objdir}/Marlin_main.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/Sd2Card.cpp" -o "${objdir}/Sd2Card.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/SdBaseFile.cpp" -o "${objdir}/SdBaseFile.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/SdFatUtil.cpp" -o "${objdir}/SdFatUtil.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/SdFile.cpp" -o "${objdir}/SdFile.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/SdVolume.cpp" -o "${objdir}/SdVolume.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/blinkm.cpp" -o "${objdir}/blinkm.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/buzzer.cpp" -o "${objdir}/buzzer.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/cardreader.cpp" -o "${objdir}/cardreader.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/configuration_store.cpp" -o "${objdir}/configuration_store.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/dac_mcp4728.cpp" -o "${objdir}/dac_mcp4728.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/digipot_mcp4451.cpp" -o "${objdir}/digipot_mcp4451.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/mesh_bed_leveling.cpp" -o "${objdir}/mesh_bed_leveling.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/planner.cpp" -o "${objdir}/planner.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/qr_solve.cpp" -o "${objdir}/qr_solve.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/servo.cpp" -o "${objdir}/servo.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/stepper.cpp" -o "${objdir}/stepper.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/stepper_dac.cpp" -o "${objdir}/stepper_dac.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/stepper_indirection.cpp" -o "${objdir}/stepper_indirection.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/temperature.cpp" -o "${objdir}/temperature.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/ultralcd.cpp" -o "${objdir}/ultralcd.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/vector_3.cpp" -o "${objdir}/vector_3.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${basedir}/watchdog.cpp" -o "${objdir}/watchdog.cpp.o"
	"$(CC)" -c -g -x assembler-with-cpp $(CPPFLAGS) "${ardcoresdir}/wiring_pulse.S" -o "${coredir}/wiring_pulse.S.o"
	"$(CC)" $(CFLAGS) $(CPPFLAGS) "${ardcoresdir}/WInterrupts.c" -o "${coredir}/WInterrupts.c.o"
	"$(CC)" $(CFLAGS) $(CPPFLAGS) "${ardcoresdir}/hooks.c" -o "${coredir}/hooks.c.o"
	"$(CC)" $(CFLAGS) $(CPPFLAGS) "${ardcoresdir}/wiring.c" -o "${coredir}/wiring.c.o"
	"$(CC)" $(CFLAGS) $(CPPFLAGS) "${ardcoresdir}/wiring_analog.c" -o "${coredir}/wiring_analog.c.o"
	"$(CC)" $(CFLAGS) $(CPPFLAGS) "${ardcoresdir}/wiring_digital.c" -o "${coredir}/wiring_digital.c.o"
	"$(CC)" $(CFLAGS) $(CPPFLAGS) "${ardcoresdir}/wiring_pulse.c" -o "${coredir}/wiring_pulse.c.o"
	"$(CC)" $(CFLAGS) $(CPPFLAGS) "${ardcoresdir}/wiring_shift.c" -o "${coredir}/wiring_shift.c.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/CDC.cpp" -o "${coredir}/CDC.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/HardwareSerial.cpp" -o "${coredir}/HardwareSerial.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/HardwareSerial0.cpp" -o "${coredir}/HardwareSerial0.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/HardwareSerial1.cpp" -o "${coredir}/HardwareSerial1.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/HardwareSerial2.cpp" -o "${coredir}/HardwareSerial2.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/HardwareSerial3.cpp" -o "${coredir}/HardwareSerial3.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/IPAddress.cpp" -o "${coredir}/IPAddress.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/PluggableUSB.cpp" -o "${coredir}/PluggableUSB.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/Print.cpp" -o "${coredir}/Print.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/Stream.cpp" -o "${coredir}/Stream.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/Tone.cpp" -o "${coredir}/Tone.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/USBCore.cpp" -o "${coredir}/USBCore.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/WMath.cpp" -o "${coredir}/WMath.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/WString.cpp" -o "${coredir}/WString.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/abi.cpp" -o "${coredir}/abi.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/main.cpp" -o "${coredir}/main.cpp.o"
	"$(CXX)" $(CXXFLAGS) -MMD $(CPPFLAGS) "${ardcoresdir}/new.cpp" -o "${coredir}/new.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/wiring_pulse.S.o"
	"$(AR)" $(ARFLAGS) "${coredir}/WInterrupts.c.o"
	"$(AR)" $(ARFLAGS) "${coredir}/hooks.c.o"
	"$(AR)" $(ARFLAGS) "${coredir}/wiring.c.o"
	"$(AR)" $(ARFLAGS) "${coredir}/wiring_analog.c.o"
	"$(AR)" $(ARFLAGS) "${coredir}/wiring_digital.c.o"
	"$(AR)" $(ARFLAGS) "${coredir}/wiring_pulse.c.o"
	"$(AR)" $(ARFLAGS) "${coredir}/wiring_shift.c.o"
	"$(AR)" $(ARFLAGS) "${coredir}/CDC.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/HardwareSerial.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/HardwareSerial0.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/HardwareSerial1.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/HardwareSerial2.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/HardwareSerial3.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/IPAddress.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/PluggableUSB.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/Print.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/Stream.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/Tone.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/USBCore.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/WMath.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/WString.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/abi.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/main.cpp.o"
	"$(AR)" $(ARFLAGS) "${coredir}/new.cpp.o"
	"$(CC)" -w -Os -Wl,--gc-sections,--relax -mmcu=atmega2560  -o "${objdir}/Marlin.ino.elf" "${objdir}/M100_Free_Mem_Chk.cpp.o" "${objdir}/Marlin.ino.cpp.o" "${objdir}/MarlinSerial.cpp.o" "${objdir}/Marlin_main.cpp.o" "${objdir}/Sd2Card.cpp.o" "${objdir}/SdBaseFile.cpp.o" "${objdir}/SdFatUtil.cpp.o" "${objdir}/SdFile.cpp.o" "${objdir}/SdVolume.cpp.o" "${objdir}/blinkm.cpp.o" "${objdir}/buzzer.cpp.o" "${objdir}/cardreader.cpp.o" "${objdir}/configuration_store.cpp.o" "${objdir}/dac_mcp4728.cpp.o" "${objdir}/digipot_mcp4451.cpp.o" "${objdir}/mesh_bed_leveling.cpp.o" "${objdir}/planner.cpp.o" "${objdir}/qr_solve.cpp.o" "${objdir}/servo.cpp.o" "${objdir}/stepper.cpp.o" "${objdir}/stepper_dac.cpp.o" "${objdir}/stepper_indirection.cpp.o" "${objdir}/temperature.cpp.o" "${objdir}/ultralcd.cpp.o" "${objdir}/vector_3.cpp.o" "${objdir}/watchdog.cpp.o" "${coredir}/core.a" "-L${objdir}" -lm
	"$(OBJCOPY)" $(OBJFLAGS) -j .eeprom --set-section-flags=.eeprom=alloc,load --no-change-warnings --change-section-lma .eeprom=0  "${objdir}/Marlin.ino.elf" "${objdir}/Marlin.ino.eep"
	if test ! -f ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH).hex; \
		then $(OBJCOPY) $(OBJFLAGS) -R .eeprom ${objdir}/Marlin.ino.elf ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH).hex; \
	elif test ! -f ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH)-2.hex; \
		then mv ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH).hex ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH)-2.hex \
		&& $(OBJCOPY) $(OBJFLAGS) -R .eeprom ${objdir}/Marlin.ino.elf ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH).hex; \
	else \
		for number in $$(seq 1 $(words $(wildcard ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH)-*.hex))); \
			do mv ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH)-$$(($(words $(wildcard ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH)-*.hex)) - $$number + 2)).hex ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH)-$$(($(words $(wildcard ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH)-*.hex)) - $$number + 3)).hex; \
		done \
		&& mv ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH).hex ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH)-2.hex \
		&& $(OBJCOPY) $(OBJFLAGS) -R .eeprom ${objdir}/Marlin.ino.elf ${DEST}/Marlin_$(MACHINE)_$(VERSION)_$(HASH).hex; \
	fi

clean:
	rm -rf ${objdir}
	rm ${basedir}/Marlin.ino.cpp
	rm ${basedir}/Marlin_*.hex
