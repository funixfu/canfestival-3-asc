#! gmake

#
# Copyright (C) 2014 François Beaulier
# 
# This file is part of canfestival, a library implementing the canopen
# stack
# 
# This library is free software; you can redistribute it and/or
# modify it under the terms of the GNU Lesser General Public
# License as published by the Free Software Foundation; either
# version 2.1 of the License, or (at your option) any later version.
# 
# This library is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
# Lesser General Public License for more details.
# 
# You should have received a copy of the GNU Lesser General Public
# License along with this library; if not, write to the Free Software
# Foundation, Inc., 59 Temple Place, Suite 330, Boston, MA  02111-1307  USA
# 

CC = arm-none-eabi-gcc
PROG_CFLAGS =  -fPIC

LIB_ROOT = ../../include/cm3/stlib

INCLUDES = -I../../include \
		   -I../../include/cm3 \
           -I$(LIB_ROOT)/STM32F10x_StdPeriph_Driver/inc \
           -I$(LIB_ROOT)/CMSIS/CM3/DeviceSupport/ST/STM32F10x/ \
           -I$(LIB_ROOT)/CMSIS/CM3/CoreSupport/ \
		   -I.

# For medium density F103           
# DEFINES = -DSTM32F10X_MD -DUSE_STDPERIPH_DRIVER

# For Connectivity line F105, external clock with 8Mhz crystal
DEFINES = -DSTM32F10X_CL -DUSE_STDPERIPH_DRIVER -DHSE_VALUE=8000000ul

CFLAGS = $(PROG_CFLAGS) $(DEFINES)

OBJS = cm3.o 

all: driver

driver: $(OBJS)

libcandriver.a: $(OBJS)
	@echo " "
	@echo "*********************************************"
	@echo "**Building libcandriver for arm cortex-M3
	@echo "*********************************************"
	ar rc $@ $(OBJS)
	ranlib $@

%.o: %.c
	@echo " "
	@echo "*********************************************"
	@echo "**Compiling $< -> $@"
	@echo "*********************************************"
	$(CC) $(CFLAGS) $(INCLUDES) -c -o $@ $<

clean:
	rm -f $(OBJS)

mrproper: clean

