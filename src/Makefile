TARGET = app
BUILD_DIR = build

DEBUG = 1
OPT = -Og

#######################################
# toolchain
#######################################
PREFIX = arm-none-eabi-
ifdef GCC_PATH
	CC = $(GCC_PATH)/$(PREFIX)gcc
	AS = $(GCC_PATH)/$(PREFIX)gcc -x assembler-with-cpp
	CP = $(GCC_PATH)/$(PREFIX)objcopy
	SZ = $(GCC_PATH)/$(PREFIX)size
else
	CC = $(PREFIX)gcc
	AS = $(PREFIX)gcc -x assembler-with-cpp
	CP = $(PREFIX)objcopy
	SZ = $(PREFIX)size
endif
HEX = $(CP) -O ihex
BIN = $(CP) -O binary -S

#######################################
# shell commands
#######################################
RM = rm -fR
ifeq ($(OS), Windows_NT)
	RM = cmd.exe /C del /q
endif

#######################################
# source files
#######################################
ASM_SOURCES =

ASMM_SOURCES = \
	kernel/dispatch.S

C_SOURCES = \
	application/usermain.c \
	boot/boot2.c \
	boot/reset_hdr.c \
	boot/vector_tbl.c \
	kernel/context.c \
	kernel/inittsk.c \
	kernel/scheduler.c \
	kernel/syslib.c \
	kernel/systimer.c \
	kernel/task_mange.c \
	kernel/task_queue.c \
	kernel/task_sync.c

#######################################
# header files
#######################################
ASM_INCLUDES =
C_INCLUDES = -Iinclude

#######################################
# macros
#######################################
AS_DEFS =
C_DEFS =

#######################################
# compiler options
#######################################
C_STANDARD = -std=c11

CPU = -mcpu=cortex-m0plus
MCU = $(CPU)

AS_FLAGS = $(MCU) $(AS_DEFS) $(ASM_INCLUDES) $(OPT)
CFLAGS = $(MCU) $(C_DEFS) $(C_INCLUDES) $(OPT)

ifeq ($(DEBUG), 1)
	AS_FLAGS += -g -gdwarf-2
	CFLAGS += -g -gdwarf-2
endif

CFLAGS += -MMD -MP -MF"$(@:%.o=%.d)"

#######################################
# linker options
#######################################
LD_SCRIPT = linker/pico_memmap.ld
LDFLAGS = $(MCU) -T$(LD_SCRIPT) -nostartfiles

#######################################
# build
#######################################
all: $(BUILD_DIR)/$(TARGET).elf $(BUILD_DIR)/$(TARGET).hex $(BUILD_DIR)/$(TARGET).bin

OBJECTS = $(addprefix $(BUILD_DIR)/,$(notdir $(C_SOURCES:.c=.o)))
vpath %c $(sort $(dir $(C_SOURCES)))
OBJECTS += $(addprefix $(BUILD_DIR)/,$(notdir $(ASM_SOURCES:.s=.o)))
vpath %s $(sort $(dir $(ASM_SOURCES)))
OBJECTS += $(addprefix $(BUILD_DIR)/,$(notdir $(ASMM_SOURCES:.S=.o)))
vpath %S $(sort $(dir $(ASMM_SOURCES)))

$(BUILD_DIR)/%.o: %.c Makefile | $(BUILD_DIR)
	$(CC) -c $(CFLAGS) -Wa,-a,-ad,-alms=$(BUILD_DIR)/$(notdir $(<:.c=.lst)) $< -o $@

$(BUILD_DIR)/%.o: %.s Makefile | $(BUILD_DIR)
	$(AS) $(AS_FLAGS) -c $< -o $@
$(BUILD_DIR)/%.o: %.S Makefile | $(BUILD_DIR)
	$(AS) $(AS_FLAGS) -c $< -o $@

$(BUILD_DIR)/$(TARGET).elf: $(OBJECTS) Makefile
	$(CC) $(OBJECTS) $(LDFLAGS) -o $@
	$(SZ) $@

$(BUILD_DIR)/%.hex: $(BUILD_DIR)/%.elf | $(BUILD_DIR)
	$(HEX) $< $@

$(BUILD_DIR)/%.bin: $(BUILD_DIR)/%.elf | $(BUILD_DIR)
	$(BIN) $< $@

$(BUILD_DIR):
	mkdir $@

#######################################
# clean up
#######################################
clean:
	-$(RM) $(BUILD_DIR)

#######################################
# dependencies
#######################################
-include $(wildcard $(BUILD_DIR)/*.d)
