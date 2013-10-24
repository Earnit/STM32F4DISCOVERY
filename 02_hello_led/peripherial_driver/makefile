TOOLS_PREFIX=arm-none-eabi-
GCC = $(TOOLS_PREFIX)gcc
OBJCOPY = $(TOOLS_PREFIX)objcopy
AR = $(TOOLS_PREFIX)ar

CFLAGS  = -g -O0 -Wall -nostdlib 
CFLAGS += -mcpu=cortex-m4 -mthumb -mlittle-endian
CFLAGS += -mthumb-interwork -mfloat-abi=hard -mfpu=fpv4-sp-d16 -ffreestanding
CFLAGS += -DSTM32F40_41xxx -DUSE_STDPERIPH_DRIVER

INCLUDE = -Iinc -I../CMSIS/inc

SRC_DIR = src
OBJ_DIR = obj

ALL_SRC = $(wildcard $(SRC_DIR)/*.c)
# Remove inappropriate files from compilation STM32F407VGT6 doesn't provide this functionality
UNUSED_SRC = $(SRC_DIR)/stm32f4xx_dma2d.c $(SRC_DIR)/stm32f4xx_fmc.c $(SRC_DIR)/stm32f4xx_ltdc.c $(SRC_DIR)/stm32f4xx_sai.c
SRC = $(filter-out $(UNUSED_SRC), $(ALL_SRC))
OBJ = $(patsubst $(SRC_DIR)/%.c, $(OBJ_DIR)/%.o, $(SRC))

.PHONY: libstm32f4.a

all: libstm32f4.a

$(OBJ) : $(SRC)
	@echo Build file: [$@]
	$(GCC) $(CFLAGS) $(INCLUDE) -c $(patsubst $(OBJ_DIR)/%.o, $(SRC_DIR)/%.c, $@) -o $@

libstm32f4.a: $(OBJ)
	$(AR) -r $@ $(OBJ)

show:
	@echo =====
	@echo SRC: $(SRC)
	@echo SRC: $(OBJ)
	@echo GCC: $(GCC)
	@echo OBJCOPY: $(OBJCOPY)
	@echo CFLAGS: $(CFLAGS)
	@echo INCLUDE: $(INCLUDE)
	@echo LDFLAGS: $(LDFLAGS)

clean:
	rm -f $(OBJ_DIR)/*.o
	rm -f libstm32f4.a
