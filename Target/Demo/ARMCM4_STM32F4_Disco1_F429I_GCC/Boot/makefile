#****************************************************************************************
#|  Description: Makefile for GNU ARM Embedded toolchain.
#|    File Name: makefile
#|    Target:   STM32F429I-DISC1 (Discovery kit) on Windows with arm-none-eabi-gcc
#|
#|---------------------------------------------------------------------------------------
#|                          C O P Y R I G H T
#|---------------------------------------------------------------------------------------
#|   Copyright (c) 2021  by Feaser    http://www.feaser.com    All rights reserved
#|
#|---------------------------------------------------------------------------------------
#|                            L I C E N S E
#|---------------------------------------------------------------------------------------
#| This file is part of OpenBLT. OpenBLT is free software: you can redistribute it and/or
#| modify it under the terms of the GNU General Public License as published by the Free
#| Software Foundation, either version 3 of the License, or (at your option) any later
#| version.
#|
#| OpenBLT is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY;
#| without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR
#| PURPOSE. See the GNU General Public License for more details.
#|
#| You have received a copy of the GNU General Public License along with OpenBLT. It 
#| should be located in ".\Doc\license.html". If not, contact Feaser to obtain a copy.
#|
#****************************************************************************************
SHELL = powershell.exe

#|--------------------------------------------------------------------------------------|
#| Configure project name                                                               |
#|--------------------------------------------------------------------------------------|
PROJ_NAME=openblt_stm32f429


#|--------------------------------------------------------------------------------------|
#| Configure tool path                                                                  |
#|--------------------------------------------------------------------------------------|
# This demo has been adapted for the STM32F429I-DISC1 board.
# Configure the path to where the arm-none-eabi-gcc program is located. If the program
# is available on the path, then the TOOL_PATH variable can be left empty.
# For Windows PowerShell: use backslashes (e.g., C:\path\to\bin\) or forward slashes.
# Make sure to add a forward or backslash at the end.
# format, open the directory in the Windows command prompt and run the following command:
#  cmd /c for %A in ("%cd%") do @echo %~sA 
#TOOL_PATH=/opt/gcc-arm-none-eabi-8-2018-q4-major/bin/
#TOOL_PATH=C:/PROGRA~2/GNUTOO~1/82018-~1/bin/
TOOL_PATH=C:/ST/STM32CubeIDE_1.19.0/STM32CubeIDE/plugins/com.st.stm32cube.ide.mcu.externaltools.gnu-tools-for-stm32.13.3.rel1.win32_1.0.0.202411081344/tools/bin/


#|--------------------------------------------------------------------------------------|
#| Collect project files                                                                |
#|--------------------------------------------------------------------------------------|
# Recursive wildcard function implementation. Example usages:
#   $(call rwildcard, , *.c *.h)   
#     --> Returns all *.c and *.h files in the current directory and below
#   $(call rwildcard, /lib/, *.c)
#     --> Returns all *.c files in the /lib directory and below
rwildcard = $(strip $(foreach d,$(wildcard $1*),$(call rwildcard,$d/,$2) $(filter $(subst *,%,$2),$d)))

# Collect all application files in the current directory and its subdirectories, but 
# exclude flash-layout.c as this one is directly included in a source file, when used.
PROJ_FILES  = $(filter-out flash_layout.c, $(call rwildcard, , *.c *.h *.s))
# Collect bootloader core files
PROJ_FILES += $(wildcard ../../../Source/*.c)
PROJ_FILES += $(wildcard ../../../Source/*.h)
# Collect bootloader port files
PROJ_FILES += $(wildcard ../../../Source/ARMCM4_STM32F4/*.c)
PROJ_FILES += $(wildcard ../../../Source/ARMCM4_STM32F4/*.h)
# Collect bootloader port compiler specific files
PROJ_FILES += $(wildcard ../../../Source/ARMCM4_STM32F4/GCC/*.c)
PROJ_FILES += $(wildcard ../../../Source/ARMCM4_STM32F4/GCC/*.h)
# Collect UIP third party library files
PROJ_FILES += ../../../Source/third_party/uip/uip/clock.h
PROJ_FILES += ../../../Source/third_party/uip/uip/lc-addrlabels.h
PROJ_FILES += ../../../Source/third_party/uip/uip/lc-switch.h
PROJ_FILES += ../../../Source/third_party/uip/uip/lc.h
PROJ_FILES += ../../../Source/third_party/uip/uip/pt.h
PROJ_FILES += ../../../Source/third_party/uip/uip/uip-fw.h
PROJ_FILES += ../../../Source/third_party/uip/uip/uip-neighbor.h
PROJ_FILES += ../../../Source/third_party/uip/uip/uip-split.h
PROJ_FILES += ../../../Source/third_party/uip/uip/uip.c
PROJ_FILES += ../../../Source/third_party/uip/uip/uip.h
PROJ_FILES += ../../../Source/third_party/uip/uip/uip_arch.h
PROJ_FILES += ../../../Source/third_party/uip/uip/uip_arp.c
PROJ_FILES += ../../../Source/third_party/uip/uip/uip_arp.h
PROJ_FILES += ../../../Source/third_party/uip/uip/uip_timer.c
PROJ_FILES += ../../../Source/third_party/uip/uip/uip_timer.h
PROJ_FILES += ../../../Source/third_party/uip/uip/uiplib.c
PROJ_FILES += ../../../Source/third_party/uip/uip/uiplib.h
PROJ_FILES += ../../../Source/third_party/uip/uip/uipopt.h
PROJ_FILES += ../../../Source/third_party/uip/apps/dhcpc/dhcpc.c
PROJ_FILES += ../../../Source/third_party/uip/apps/dhcpc/dhcpc.h
# Collect TinyUSB third party library files
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/*.c)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/*.h)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/class/vendor/*.c)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/class/vendor/*.h)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/common/*.c)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/common/*.h)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/device/*.c)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/device/*.h)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/osal/*.c)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/osal/*.h)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/portable/*.c)
PROJ_FILES += $(wildcard ../../../Source/third_party/tinyusb/src/portable/*.h)
PROJ_FILES += ../../../Source/third_party/tinyusb/src/portable/synopsys/dwc2/dcd_dwc2.c
PROJ_FILES += ../../../Source/third_party/tinyusb/src/portable/synopsys/dwc2/dwc2_common.c
PROJ_FILES += ../../../Source/third_party/tinyusb/src/portable/synopsys/dwc2/dwc2_common.h
PROJ_FILES += ../../../Source/third_party/tinyusb/src/portable/synopsys/dwc2/dwc2_stm32.h
PROJ_FILES += ../../../Source/third_party/tinyusb/src/portable/synopsys/dwc2/dwc2_type.h


#|--------------------------------------------------------------------------------------|
#| Toolchain binaries                                                                   |
#|--------------------------------------------------------------------------------------|
RM = Remove-Item
CC = $(TOOL_PATH)arm-none-eabi-gcc
LN = $(TOOL_PATH)arm-none-eabi-gcc
OC = $(TOOL_PATH)arm-none-eabi-objcopy
OD = $(TOOL_PATH)arm-none-eabi-objdump
AS = $(TOOL_PATH)arm-none-eabi-gcc
SZ = $(TOOL_PATH)arm-none-eabi-size


#|--------------------------------------------------------------------------------------|
#| Filter project files
#|--------------------------------------------------------------------------------------|
PROJ_ASRCS  = $(filter %.s,$(foreach file,$(PROJ_FILES),$(notdir $(file))))
PROJ_CSRCS  = $(filter %.c,$(foreach file,$(PROJ_FILES),$(notdir $(file))))


#|--------------------------------------------------------------------------------------|
#| Set important path variables                                                         |
#|--------------------------------------------------------------------------------------|
VPATH    = $(foreach path,$(sort $(foreach file,$(PROJ_FILES),$(dir $(file)))) $(subst \,/,$(OBJ_PATH)),$(path) :)
OBJ_PATH = obj
BIN_PATH = bin
MAP_FILE := $(BIN_PATH)/$(PROJ_NAME).map
INC_PATH = $(patsubst %/,%,$(patsubst %,-I%,$(sort $(foreach file,$(filter %.h,$(PROJ_FILES)),$(dir $(file))))))
LIB_PATH  = 


#|--------------------------------------------------------------------------------------|
#| Options for toolchain binaries                                                       |
#|--------------------------------------------------------------------------------------|
STDFLAGS    = -mcpu=cortex-m4 -mthumb -mfloat-abi=hard -mfpu=fpv4-sp-d16 -fno-strict-aliasing
STDFLAGS   += -fdata-sections -ffunction-sections -Wall -g3
OPTFLAGS    = -Og
DEPFLAGS    = -MT $@ -MMD -MP -MF $(OBJ_PATH)/$*.d
CFLAGS      = $(STDFLAGS) $(OPTFLAGS)
CFLAGS     += -DUSE_FULL_LL_DRIVER -DUSE_HAL_DRIVER -DSTM32F429xx
CFLAGS     += -D__weak="__attribute__((weak))" -D__packed="__attribute__((__packed__))"
CFLAGS     += $(INC_PATH)
AFLAGS      = $(CFLAGS)
LFLAGS      = $(STDFLAGS) $(OPTFLAGS)
LFLAGS     += -T"STM32F429ZITx_FLASH.ld" -Xlinker -Map -Xlinker $(MAP_FILE)
LFLAGS     += -specs="nano.specs" -Xlinker --gc-sections $(LIB_PATH)
OFLAGS      = -O srec
ODFLAGS     = -x
SZFLAGS     = -B -d
RMFLAGS     = -Force -Recurse -ErrorAction SilentlyContinue


#|--------------------------------------------------------------------------------------|
#| Specify library files                                                                |
#|--------------------------------------------------------------------------------------|
LIBS = 


#|--------------------------------------------------------------------------------------|
#| Define targets                                                                       |
#|--------------------------------------------------------------------------------------|
AOBJS = $(patsubst %.s,%.o,$(PROJ_ASRCS))
COBJS = $(patsubst %.c,%.o,$(PROJ_CSRCS))

#|--------------------------------------------------------------------------------------|
#| Dependency generation (include early so Make knows about dependencies)               |
#|--------------------------------------------------------------------------------------|
DEPFILES := $(PROJ_CSRCS:%.c=$(OBJ_PATH)/%.d)
.PRECIOUS: $(DEPFILES)
-include $(DEPFILES)


#|--------------------------------------------------------------------------------------|
#| Make ALL                                                                             |
#|--------------------------------------------------------------------------------------|
.PHONY: all
all: $(BIN_PATH)/$(PROJ_NAME).srec

$(OBJ_PATH):
	@powershell -Command "if (-not (Test-Path -Path '$(OBJ_PATH)')) { New-Item -ItemType Directory -Path '$(OBJ_PATH)' | Out-Null }"

$(BIN_PATH):
	@powershell -Command "if (-not (Test-Path -Path '$(BIN_PATH)')) { New-Item -ItemType Directory -Path '$(BIN_PATH)' | Out-Null }"

$(BIN_PATH)/$(PROJ_NAME).srec :  $(BIN_PATH)  $(BIN_PATH)/$(PROJ_NAME).elf
	@cmd /c $(OC) $< $(OFLAGS) $@
	@cmd /c  $(OD) $(ODFLAGS) $< > $(BIN_PATH)/$(PROJ_NAME).map
	@powershell -Command "Write-Host '+++ Summary of memory consumption:'"
	@cmd /c  $(SZ) $(SZFLAGS) $<
	@powershell -Command "Write-Host '+++ Build complete [$(notdir $@)]'"

$(BIN_PATH)/$(PROJ_NAME).elf :  $(BIN_PATH)  #$(AOBJS) $(COBJS) 
	@powershell -Command "Write-Host '+++ Linking [$(notdir $@)]'"
	@echo  $(LN) $(LFLAGS) -o $@ $(patsubst %.o,$(OBJ_PATH)/%.o,$(^F)) $(LIBS)
	@cmd /c $(LN) $(LFLAGS) -o $@ $(patsubst %.o,$(OBJ_PATH)/%.o,$(^F)) $(LIBS)


#|--------------------------------------------------------------------------------------|
#| Compile and assemble                                                                 |
#|--------------------------------------------------------------------------------------|
$(AOBJS): %.o: %.s $(OBJ_PATH)
	@powershell -Command "Write-Host '+++ Assembling [$(notdir $<)]'"
	@cmd /c $(AS) $(AFLAGS) -c $< -o $(OBJ_PATH)/$(@F)

$(COBJS): %.o: %.c $(OBJ_PATH)
	@powershell -Command "Write-Host '+++ Compiling [$(notdir $<)]'"
	@cmd /c $(CC) $(DEPFLAGS) $(CFLAGS) -c $< -o $(OBJ_PATH)/$(@F)


#|--------------------------------------------------------------------------------------|
#| Make CLEAN                                                                           |
#|--------------------------------------------------------------------------------------|
.PHONY: clean
clean: 
	@powershell -Command "Write-Host '+++ Cleaning build environment'"
	@powershell -Command "if (Test-Path -Path '$(OBJ_PATH)') { Remove-Item -Force -Recurse -ErrorAction SilentlyContinue '$(OBJ_PATH)' }; if (Test-Path -Path '$(BIN_PATH)/$(PROJ_NAME).elf') { Remove-Item -Force -ErrorAction SilentlyContinue '$(BIN_PATH)/$(PROJ_NAME).elf' }; if (Test-Path -Path '$(BIN_PATH)/$(PROJ_NAME).map') { Remove-Item -Force -ErrorAction SilentlyContinue '$(BIN_PATH)/$(PROJ_NAME).map' }; if (Test-Path -Path '$(BIN_PATH)/$(PROJ_NAME).srec') { Remove-Item -Force -ErrorAction SilentlyContinue '$(BIN_PATH)/$(PROJ_NAME).srec' }"
	@powershell -Command "Write-Host '+++ Clean complete'"

	
#|--------------------------------------------------------------------------------------|
#| Dependency generation rule (generate .d files if they don't exist)                   |
#|--------------------------------------------------------------------------------------|
$(OBJ_PATH)/%.d: %.c
	@cmd /c $(CC) $(DEPFLAGS) $(CFLAGS) -E $< > $@	

