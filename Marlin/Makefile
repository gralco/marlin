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

CC = ${avrdir}/avr-gcc
CFLAGS = -c -g -Os -Wall -ffunction-sections -fdata-sections -mmcu=atmega2560 -DF_CPU=16000000L -MMD -DUSB_VID=null -DUSB_PID=null -DARDUINO=105 -I${coresdir} -I${hardwdir}/rambo/variants/standard

CXX = ${avrdir}/avr-g++
CXXFLAGS = -c -g -Os -Wall -fno-exceptions -ffunction-sections -fdata-sections -mmcu=atmega2560 -DF_CPU=16000000L -MMD -DUSB_VID=null -DUSB_PID=null -DARDUINO=105 -I${coresdir} -I${hardwdir}/rambo/variants/standard

AR = ${avrdir}/avr-ar
ARFLAGS = rcs ${objdir}/core.a

OBJCOPY = ${avrdir}/avr-objcopy
OBJFLAGS = -O ihex

MKDIR_P = mkdir -p
LN_F = ln -f

basedir = .
objdir = ${basedir}/obj
arddir = ${basedir}./ArduinoAddons/Arduino_1.0.x
libdir = ${arddir}/libraries
hardwdir = ${arddir}/hardware
coresdir = ${hardwdir}/rambo/cores/arduino
avrdir = ${hardwdir}/tools/avr/bin

DEST ?= ${basedir}
MACHINE = Nutmeg_Single
NOW = $(shell date +"%b_%d_%y")

all:
	$(MKDIR_P) ${objdir}
	$(MKDIR_P) ${objdir}/LiquidCrystal/
	$(MKDIR_P) ${objdir}/LiquidCrystal/utility/
	$(MKDIR_P) ${objdir}/SPI/
	$(MKDIR_P) ${objdir}/SPI/utility/
	$(MKDIR_P) ${objdir}/U8glib/
	$(MKDIR_P) ${objdir}/U8glib/utility/
	$(MKDIR_P) ${objdir}/Wire/
	$(MKDIR_P) ${objdir}/Wire/utility/
	$(LN_F) ${basedir}/Marlin.ino ${basedir}/Marlin.cpp
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/SdVolume.cpp -o ${objdir}/SdVolume.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/Servo.cpp -o ${objdir}/Servo.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/digipot_mcp4451.cpp -o ${objdir}/digipot_mcp4451.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/ultralcd.cpp -o ${objdir}/ultralcd.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/cardreader.cpp -o ${objdir}/cardreader.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/Marlin.cpp -o ${objdir}/Marlin.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/temperature.cpp -o ${objdir}/temperature.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/qr_solve.cpp -o ${objdir}/qr_solve.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/MarlinSerial.cpp -o ${objdir}/MarlinSerial.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/Sd2Card.cpp -o ${objdir}/Sd2Card.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/SdBaseFile.cpp -o ${objdir}/SdBaseFile.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/planner.cpp -o ${objdir}/planner.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/motion_control.cpp -o ${objdir}/motion_control.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/BlinkM.cpp -o ${objdir}/BlinkM.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/stepper.cpp -o ${objdir}/stepper.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/Marlin_main.cpp -o ${objdir}/Marlin_main.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/ConfigurationStore.cpp -o ${objdir}/ConfigurationStore.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/vector_3.cpp -o ${objdir}/vector_3.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/SdFile.cpp -o ${objdir}/SdFile.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/watchdog.cpp -o ${objdir}/watchdog.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/LiquidCrystalRus.cpp -o ${objdir}/LiquidCrystalRus.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI ${basedir}/SdFatUtil.cpp -o ${objdir}/SdFatUtil.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/Wire/utility ${libdir}/Wire/Wire.cpp -o ${objdir}/Wire/Wire.cpp.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/Wire/utility ${libdir}/Wire/utility/twi.c -o ${objdir}/Wire/utility/twi.c.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/U8glib.cpp -o ${objdir}/U8glib/U8glib.cpp.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_api.c -o ${objdir}/U8glib/utility/u8g_com_api.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7565_nhd_c12864.c -o ${objdir}/U8glib/utility/u8g_dev_st7565_nhd_c12864.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_sw_spi.c -o ${objdir}/U8glib/utility/u8g_com_arduino_sw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb8h2.c -o ${objdir}/U8glib/utility/u8g_pb8h2.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_atmega_hw_spi.c -o ${objdir}/U8glib/utility/u8g_com_atmega_hw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_flipdisc_2x7.c -o ${objdir}/U8glib/utility/u8g_dev_flipdisc_2x7.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_std_sw_spi.c -o ${objdir}/U8glib/utility/u8g_com_std_sw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_rect.c -o ${objdir}/U8glib/utility/u8g_rect.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb14v1.c -o ${objdir}/U8glib/utility/u8g_pb14v1.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7920_128x64.c -o ${objdir}/U8glib/utility/u8g_dev_st7920_128x64.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_api_16gr.c -o ${objdir}/U8glib/utility/u8g_com_api_16gr.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1351_128x128.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1351_128x128.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_ssd_i2c.c -o ${objdir}/U8glib/utility/u8g_com_arduino_ssd_i2c.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_common.c -o ${objdir}/U8glib/utility/u8g_com_arduino_common.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_fast_parallel.c -o ${objdir}/U8glib/utility/u8g_com_arduino_fast_parallel.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_scale.c -o ${objdir}/U8glib/utility/u8g_scale.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1306_64x48.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1306_64x48.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1309_128x64.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1309_128x64.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pbxh16.c -o ${objdir}/U8glib/utility/u8g_pbxh16.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_raspberrypi_hw_spi.c -o ${objdir}/U8glib/utility/u8g_com_raspberrypi_hw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_ellipse.c -o ${objdir}/U8glib/utility/u8g_ellipse.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_null.c -o ${objdir}/U8glib/utility/u8g_com_null.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_u16toa.c -o ${objdir}/U8glib/utility/u8g_u16toa.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_font_data.c -o ${objdir}/U8glib/utility/u8g_font_data.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1327_96x96_gr.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1327_96x96_gr.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_uc1608_240x64.c -o ${objdir}/U8glib/utility/u8g_dev_uc1608_240x64.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_circle.c -o ${objdir}/U8glib/utility/u8g_circle.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_uc1701_dogs102.c -o ${objdir}/U8glib/utility/u8g_dev_uc1701_dogs102.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ht1632.c -o ${objdir}/U8glib/utility/u8g_dev_ht1632.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1322_nhd31oled_bw.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1322_nhd31oled_bw.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb8h1f.c -o ${objdir}/U8glib/utility/u8g_pb8h1f.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_atmega_sw_spi.c -o ${objdir}/U8glib/utility/u8g_com_atmega_sw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/chessengine.c -o ${objdir}/U8glib/utility/chessengine.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_parallel.c -o ${objdir}/U8glib/utility/u8g_com_arduino_parallel.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_t6963_128x128.c -o ${objdir}/U8glib/utility/u8g_dev_t6963_128x128.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ks0108_128x64.c -o ${objdir}/U8glib/utility/u8g_dev_ks0108_128x64.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_uc1611_dogxl240.c -o ${objdir}/U8glib/utility/u8g_dev_uc1611_dogxl240.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb8v1.c -o ${objdir}/U8glib/utility/u8g_pb8v1.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7565_lm6063.c -o ${objdir}/U8glib/utility/u8g_dev_st7565_lm6063.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1306_128x32.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1306_128x32.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_lc7981_160x80.c -o ${objdir}/U8glib/utility/u8g_dev_lc7981_160x80.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7565_lm6059.c -o ${objdir}/U8glib/utility/u8g_dev_st7565_lm6059.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_bw.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_bw.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb8v2.c -o ${objdir}/U8glib/utility/u8g_pb8v2.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_lc7981_240x64.c -o ${objdir}/U8glib/utility/u8g_dev_lc7981_240x64.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_msp430_hw_spi.c -o ${objdir}/U8glib/utility/u8g_com_msp430_hw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_gr_new.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_gr_new.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_pcf8812_96x65.c -o ${objdir}/U8glib/utility/u8g_dev_pcf8812_96x65.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb16v2.c -o ${objdir}/U8glib/utility/u8g_pb16v2.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_st7920_spi.c -o ${objdir}/U8glib/utility/u8g_com_arduino_st7920_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_cursor.c -o ${objdir}/U8glib/utility/u8g_cursor.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_st7920_custom.c -o ${objdir}/U8glib/utility/u8g_com_arduino_st7920_custom.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_pcd8544_84x48.c -o ${objdir}/U8glib/utility/u8g_dev_pcd8544_84x48.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_port_d_wr.c -o ${objdir}/U8glib/utility/u8g_com_arduino_port_d_wr.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb8h1.c -o ${objdir}/U8glib/utility/u8g_pb8h1.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_t6963_240x128.c -o ${objdir}/U8glib/utility/u8g_dev_t6963_240x128.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_std_sw_spi.c -o ${objdir}/U8glib/utility/u8g_com_arduino_std_sw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pbxh24.c -o ${objdir}/U8glib/utility/u8g_pbxh24.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_hw_usart_spi.c -o ${objdir}/U8glib/utility/u8g_com_arduino_hw_usart_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_attiny85_hw_spi.c -o ${objdir}/U8glib/utility/u8g_com_arduino_attiny85_hw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_gprof.c -o ${objdir}/U8glib/utility/u8g_dev_gprof.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7565_dogm132.c -o ${objdir}/U8glib/utility/u8g_dev_st7565_dogm132.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_atmega_st7920_hw_spi.c -o ${objdir}/U8glib/utility/u8g_com_atmega_st7920_hw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7920_192x32.c -o ${objdir}/U8glib/utility/u8g_dev_st7920_192x32.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_i2c.c -o ${objdir}/U8glib/utility/u8g_com_i2c.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ili9325d_320x240.c -o ${objdir}/U8glib/utility/u8g_dev_ili9325d_320x240.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_uc1701_mini12864.c -o ${objdir}/U8glib/utility/u8g_dev_uc1701_mini12864.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_raspberrypi_ssd_i2c.c -o ${objdir}/U8glib/utility/u8g_com_raspberrypi_ssd_i2c.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_clip.c -o ${objdir}/U8glib/utility/u8g_clip.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_st7920_hw_spi.c -o ${objdir}/U8glib/utility/u8g_com_arduino_st7920_hw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb8h8.c -o ${objdir}/U8glib/utility/u8g_pb8h8.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_virtual_screen.c -o ${objdir}/U8glib/utility/u8g_virtual_screen.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_gr.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_gr.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_io.c -o ${objdir}/U8glib/utility/u8g_com_io.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_sbn1661_122x32.c -o ${objdir}/U8glib/utility/u8g_dev_sbn1661_122x32.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_tls8204_84x48.c -o ${objdir}/U8glib/utility/u8g_dev_tls8204_84x48.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_ll_api.c -o ${objdir}/U8glib/utility/u8g_ll_api.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_null.c -o ${objdir}/U8glib/utility/u8g_dev_null.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_t6963_240x64.c -o ${objdir}/U8glib/utility/u8g_dev_t6963_240x64.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_delay.c -o ${objdir}/U8glib/utility/u8g_delay.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_t6963_128x64.c -o ${objdir}/U8glib/utility/u8g_dev_t6963_128x64.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_u8toa.c -o ${objdir}/U8glib/utility/u8g_u8toa.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_line.c -o ${objdir}/U8glib/utility/u8g_line.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ld7032_60x32.c -o ${objdir}/U8glib/utility/u8g_dev_ld7032_60x32.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7687_c144mvgd.c -o ${objdir}/U8glib/utility/u8g_dev_st7687_c144mvgd.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_lc7981_240x128.c -o ${objdir}/U8glib/utility/u8g_dev_lc7981_240x128.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_no_en_parallel.c -o ${objdir}/U8glib/utility/u8g_com_arduino_no_en_parallel.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7920_202x32.c -o ${objdir}/U8glib/utility/u8g_dev_st7920_202x32.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_a2_micro_printer.c -o ${objdir}/U8glib/utility/u8g_dev_a2_micro_printer.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb32h1.c -o ${objdir}/U8glib/utility/u8g_pb32h1.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_uc1610_dogxl160.c -o ${objdir}/U8glib/utility/u8g_dev_uc1610_dogxl160.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1322_nhd31oled_gr.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1322_nhd31oled_gr.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_uc1601_c128032.c -o ${objdir}/U8glib/utility/u8g_dev_uc1601_c128032.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_uc_i2c.c -o ${objdir}/U8glib/utility/u8g_com_arduino_uc_i2c.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_rot.c -o ${objdir}/U8glib/utility/u8g_rot.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb.c -o ${objdir}/U8glib/utility/u8g_pb.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_font.c -o ${objdir}/U8glib/utility/u8g_font.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1306_128x64.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1306_128x64.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb16h1.c -o ${objdir}/U8glib/utility/u8g_pb16h1.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_atmega_st7920_spi.c -o ${objdir}/U8glib/utility/u8g_com_atmega_st7920_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb16v1.c -o ${objdir}/U8glib/utility/u8g_pb16v1.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_atmega_parallel.c -o ${objdir}/U8glib/utility/u8g_com_atmega_parallel.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7565_nhd_c12832.c -o ${objdir}/U8glib/utility/u8g_dev_st7565_nhd_c12832.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_bitmap.c -o ${objdir}/U8glib/utility/u8g_bitmap.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_lc7981_320x64.c -o ${objdir}/U8glib/utility/u8g_dev_lc7981_320x64.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_uc1611_dogm240.c -o ${objdir}/U8glib/utility/u8g_dev_uc1611_dogm240.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_polygon.c -o ${objdir}/U8glib/utility/u8g_polygon.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_bw_new.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_bw_new.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_t6963.c -o ${objdir}/U8glib/utility/u8g_com_arduino_t6963.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7565_dogm128.c -o ${objdir}/U8glib/utility/u8g_dev_st7565_dogm128.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_state.c -o ${objdir}/U8glib/utility/u8g_state.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_page.c -o ${objdir}/U8glib/utility/u8g_page.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_com_arduino_hw_spi.c -o ${objdir}/U8glib/utility/u8g_com_arduino_hw_spi.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_st7565_64128n.c -o ${objdir}/U8glib/utility/u8g_dev_st7565_64128n.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_ssd1353_160x128.c -o ${objdir}/U8glib/utility/u8g_dev_ssd1353_160x128.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_dev_uc1608_240x128.c -o ${objdir}/U8glib/utility/u8g_dev_uc1608_240x128.c.o 
	$(CC) $(CFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/U8glib/utility ${libdir}/U8glib/utility/u8g_pb16h2.c -o ${objdir}/U8glib/utility/u8g_pb16h2.c.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/LiquidCrystal/utility ${libdir}/LiquidCrystal/LiquidCrystal.cpp -o ${objdir}/LiquidCrystal/LiquidCrystal.cpp.o 
	$(CXX) $(CXXFLAGS) -I${libdir}/Wire -I${libdir}/U8glib -I${libdir}/LiquidCrystal -I${libdir}/SPI -I${libdir}/SPI/utility ${libdir}/SPI/SPI.cpp -o ${objdir}/SPI/SPI.cpp.o 
	$(CC) $(CFLAGS) ${coresdir}/WInterrupts.c -o ${objdir}/WInterrupts.c.o 
	$(CC) $(CFLAGS) ${coresdir}/wiring.c -o ${objdir}/wiring.c.o 
	$(CC) $(CFLAGS) ${coresdir}/wiring_pulse.c -o ${objdir}/wiring_pulse.c.o 
	$(CC) $(CFLAGS) ${coresdir}/wiring_shift.c -o ${objdir}/wiring_shift.c.o 
	$(CC) $(CFLAGS) ${coresdir}/wiring_analog.c -o ${objdir}/wiring_analog.c.o 
	$(CC) $(CFLAGS) ${coresdir}/wiring_digital.c -o ${objdir}/wiring_digital.c.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/HardwareSerial.cpp -o ${objdir}/HardwareSerial.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/WMath.cpp -o ${objdir}/WMath.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/Print.cpp -o ${objdir}/Print.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/USBCore.cpp -o ${objdir}/USBCore.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/CDC.cpp -o ${objdir}/CDC.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/main.cpp -o ${objdir}/main.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/WString.cpp -o ${objdir}/WString.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/new.cpp -o ${objdir}/new.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/HID.cpp -o ${objdir}/HID.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/IPAddress.cpp -o ${objdir}/IPAddress.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/Tone.cpp -o ${objdir}/Tone.cpp.o 
	$(CXX) $(CXXFLAGS) ${coresdir}/Stream.cpp -o ${objdir}/Stream.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/WInterrupts.c.o 
	$(AR) $(ARFLAGS) ${objdir}/wiring.c.o 
	$(AR) $(ARFLAGS) ${objdir}/wiring_pulse.c.o 
	$(AR) $(ARFLAGS) ${objdir}/wiring_shift.c.o 
	$(AR) $(ARFLAGS) ${objdir}/wiring_analog.c.o 
	$(AR) $(ARFLAGS) ${objdir}/wiring_digital.c.o 
	$(AR) $(ARFLAGS) ${objdir}/HardwareSerial.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/WMath.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/Print.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/USBCore.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/CDC.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/main.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/WString.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/new.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/HID.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/IPAddress.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/Tone.cpp.o 
	$(AR) $(ARFLAGS) ${objdir}/Stream.cpp.o 
	$(CC) -Os -Wl,--gc-sections,--relax -mmcu=atmega2560 -o ${objdir}/Marlin.cpp.elf ${objdir}/SdVolume.cpp.o ${objdir}/Servo.cpp.o ${objdir}/digipot_mcp4451.cpp.o ${objdir}/ultralcd.cpp.o ${objdir}/cardreader.cpp.o ${objdir}/Marlin.cpp.o ${objdir}/temperature.cpp.o ${objdir}/qr_solve.cpp.o ${objdir}/MarlinSerial.cpp.o ${objdir}/Sd2Card.cpp.o ${objdir}/SdBaseFile.cpp.o ${objdir}/planner.cpp.o ${objdir}/motion_control.cpp.o ${objdir}/BlinkM.cpp.o ${objdir}/stepper.cpp.o ${objdir}/Marlin_main.cpp.o ${objdir}/ConfigurationStore.cpp.o ${objdir}/vector_3.cpp.o ${objdir}/SdFile.cpp.o ${objdir}/watchdog.cpp.o ${objdir}/LiquidCrystalRus.cpp.o ${objdir}/SdFatUtil.cpp.o ${objdir}/Wire/Wire.cpp.o ${objdir}/Wire/utility/twi.c.o ${objdir}/U8glib/U8glib.cpp.o ${objdir}/U8glib/utility/u8g_com_api.c.o ${objdir}/U8glib/utility/u8g_dev_st7565_nhd_c12864.c.o ${objdir}/U8glib/utility/u8g_com_arduino_sw_spi.c.o ${objdir}/U8glib/utility/u8g_pb8h2.c.o ${objdir}/U8glib/utility/u8g_com_atmega_hw_spi.c.o ${objdir}/U8glib/utility/u8g_dev_flipdisc_2x7.c.o ${objdir}/U8glib/utility/u8g_com_std_sw_spi.c.o ${objdir}/U8glib/utility/u8g_rect.c.o ${objdir}/U8glib/utility/u8g_pb14v1.c.o ${objdir}/U8glib/utility/u8g_dev_st7920_128x64.c.o ${objdir}/U8glib/utility/u8g_com_api_16gr.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1351_128x128.c.o ${objdir}/U8glib/utility/u8g_com_arduino_ssd_i2c.c.o ${objdir}/U8glib/utility/u8g_com_arduino_common.c.o ${objdir}/U8glib/utility/u8g_com_arduino_fast_parallel.c.o ${objdir}/U8glib/utility/u8g_scale.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1306_64x48.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1309_128x64.c.o ${objdir}/U8glib/utility/u8g_pbxh16.c.o ${objdir}/U8glib/utility/u8g_com_raspberrypi_hw_spi.c.o ${objdir}/U8glib/utility/u8g_ellipse.c.o ${objdir}/U8glib/utility/u8g_com_null.c.o ${objdir}/U8glib/utility/u8g_u16toa.c.o ${objdir}/U8glib/utility/u8g_font_data.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1327_96x96_gr.c.o ${objdir}/U8glib/utility/u8g_dev_uc1608_240x64.c.o ${objdir}/U8glib/utility/u8g_circle.c.o ${objdir}/U8glib/utility/u8g_dev_uc1701_dogs102.c.o ${objdir}/U8glib/utility/u8g_dev_ht1632.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1322_nhd31oled_bw.c.o ${objdir}/U8glib/utility/u8g_pb8h1f.c.o ${objdir}/U8glib/utility/u8g_com_atmega_sw_spi.c.o ${objdir}/U8glib/utility/chessengine.c.o ${objdir}/U8glib/utility/u8g_com_arduino_parallel.c.o ${objdir}/U8glib/utility/u8g_dev_t6963_128x128.c.o ${objdir}/U8glib/utility/u8g_dev_ks0108_128x64.c.o ${objdir}/U8glib/utility/u8g_dev_uc1611_dogxl240.c.o ${objdir}/U8glib/utility/u8g_pb8v1.c.o ${objdir}/U8glib/utility/u8g_dev_st7565_lm6063.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1306_128x32.c.o ${objdir}/U8glib/utility/u8g_dev_lc7981_160x80.c.o ${objdir}/U8glib/utility/u8g_dev_st7565_lm6059.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_bw.c.o ${objdir}/U8glib/utility/u8g_pb8v2.c.o ${objdir}/U8glib/utility/u8g_dev_lc7981_240x64.c.o ${objdir}/U8glib/utility/u8g_com_msp430_hw_spi.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_gr_new.c.o ${objdir}/U8glib/utility/u8g_dev_pcf8812_96x65.c.o ${objdir}/U8glib/utility/u8g_pb16v2.c.o ${objdir}/U8glib/utility/u8g_com_arduino_st7920_spi.c.o ${objdir}/U8glib/utility/u8g_cursor.c.o ${objdir}/U8glib/utility/u8g_com_arduino_st7920_custom.c.o ${objdir}/U8glib/utility/u8g_dev_pcd8544_84x48.c.o ${objdir}/U8glib/utility/u8g_com_arduino_port_d_wr.c.o ${objdir}/U8glib/utility/u8g_pb8h1.c.o ${objdir}/U8glib/utility/u8g_dev_t6963_240x128.c.o ${objdir}/U8glib/utility/u8g_com_arduino_std_sw_spi.c.o ${objdir}/U8glib/utility/u8g_pbxh24.c.o ${objdir}/U8glib/utility/u8g_com_arduino_hw_usart_spi.c.o ${objdir}/U8glib/utility/u8g_com_arduino_attiny85_hw_spi.c.o ${objdir}/U8glib/utility/u8g_dev_gprof.c.o ${objdir}/U8glib/utility/u8g_dev_st7565_dogm132.c.o ${objdir}/U8glib/utility/u8g_com_atmega_st7920_hw_spi.c.o ${objdir}/U8glib/utility/u8g_dev_st7920_192x32.c.o ${objdir}/U8glib/utility/u8g_com_i2c.c.o ${objdir}/U8glib/utility/u8g_dev_ili9325d_320x240.c.o ${objdir}/U8glib/utility/u8g_dev_uc1701_mini12864.c.o ${objdir}/U8glib/utility/u8g_com_raspberrypi_ssd_i2c.c.o ${objdir}/U8glib/utility/u8g_clip.c.o ${objdir}/U8glib/utility/u8g_com_arduino_st7920_hw_spi.c.o ${objdir}/U8glib/utility/u8g_pb8h8.c.o ${objdir}/U8glib/utility/u8g_virtual_screen.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_gr.c.o ${objdir}/U8glib/utility/u8g_com_io.c.o ${objdir}/U8glib/utility/u8g_dev_sbn1661_122x32.c.o ${objdir}/U8glib/utility/u8g_dev_tls8204_84x48.c.o ${objdir}/U8glib/utility/u8g_ll_api.c.o ${objdir}/U8glib/utility/u8g_dev_null.c.o ${objdir}/U8glib/utility/u8g_dev_t6963_240x64.c.o ${objdir}/U8glib/utility/u8g_delay.c.o ${objdir}/U8glib/utility/u8g_dev_t6963_128x64.c.o ${objdir}/U8glib/utility/u8g_u8toa.c.o ${objdir}/U8glib/utility/u8g_line.c.o ${objdir}/U8glib/utility/u8g_dev_ld7032_60x32.c.o ${objdir}/U8glib/utility/u8g_dev_st7687_c144mvgd.c.o ${objdir}/U8glib/utility/u8g_dev_lc7981_240x128.c.o ${objdir}/U8glib/utility/u8g_com_arduino_no_en_parallel.c.o ${objdir}/U8glib/utility/u8g_dev_st7920_202x32.c.o ${objdir}/U8glib/utility/u8g_dev_a2_micro_printer.c.o ${objdir}/U8glib/utility/u8g_pb32h1.c.o ${objdir}/U8glib/utility/u8g_dev_uc1610_dogxl160.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1322_nhd31oled_gr.c.o ${objdir}/U8glib/utility/u8g_dev_uc1601_c128032.c.o ${objdir}/U8glib/utility/u8g_com_arduino_uc_i2c.c.o ${objdir}/U8glib/utility/u8g_rot.c.o ${objdir}/U8glib/utility/u8g_pb.c.o ${objdir}/U8glib/utility/u8g_font.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1306_128x64.c.o ${objdir}/U8glib/utility/u8g_pb16h1.c.o ${objdir}/U8glib/utility/u8g_com_atmega_st7920_spi.c.o ${objdir}/U8glib/utility/u8g_pb16v1.c.o ${objdir}/U8glib/utility/u8g_com_atmega_parallel.c.o ${objdir}/U8glib/utility/u8g_dev_st7565_nhd_c12832.c.o ${objdir}/U8glib/utility/u8g_bitmap.c.o ${objdir}/U8glib/utility/u8g_dev_lc7981_320x64.c.o ${objdir}/U8glib/utility/u8g_dev_uc1611_dogm240.c.o ${objdir}/U8glib/utility/u8g_polygon.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1325_nhd27oled_bw_new.c.o ${objdir}/U8glib/utility/u8g_com_arduino_t6963.c.o ${objdir}/U8glib/utility/u8g_dev_st7565_dogm128.c.o ${objdir}/U8glib/utility/u8g_state.c.o ${objdir}/U8glib/utility/u8g_page.c.o ${objdir}/U8glib/utility/u8g_com_arduino_hw_spi.c.o ${objdir}/U8glib/utility/u8g_dev_st7565_64128n.c.o ${objdir}/U8glib/utility/u8g_dev_ssd1353_160x128.c.o ${objdir}/U8glib/utility/u8g_dev_uc1608_240x128.c.o ${objdir}/U8glib/utility/u8g_pb16h2.c.o ${objdir}/LiquidCrystal/LiquidCrystal.cpp.o ${objdir}/SPI/SPI.cpp.o ${objdir}/core.a -L${objdir} -lm 
	$(OBJCOPY) -O ihex -j .eeprom --set-section-flags=.eeprom=alloc,load --no-change-warnings --change-section-lma .eeprom=0 ${objdir}/Marlin.cpp.elf ${objdir}/Marlin.cpp.eep 
	$(OBJCOPY) -O ihex -R .eeprom ${objdir}/Marlin.cpp.elf ${DEST}/Marlin_$(MACHINE)_$(NOW).hex

clean:
	rm -rf ${objdir}
	rm ${basedir}/Marlin.cpp
