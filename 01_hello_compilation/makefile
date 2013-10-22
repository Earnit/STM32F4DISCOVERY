TOOLS_PREFIX=arm-none-eabi-
GCC = $(TOOLS_PREFIX)gcc
OBJCOPY = $(TOOLS_PREFIX)objcopy

CFLAGS  = -g -O0 -Wall -nostdlib 
CFLAGS += -mcpu=cortex-m4 -mthumb -mlittle-endian
CFLAGS += -DSTM32F40_41xxx

INCLUDE = -I. -I./CMSIS/inc

LDFLAGS = -L. -Tstm32_flash.ld

SRC = main.c ./CMSIS/src/system_stm32f4xx.c ./CMSIS/src/startup_stm32f40_41xxx.s

all: hello_compilation

hello_compilation:
	@echo Build file: [$@]
	$(GCC) $(CFLAGS) $(INCLUDE) $(SRC) $(LDFLAGS) -o $@.elf
	$(OBJCOPY) -O ihex $@.elf $@.hex
	$(OBJCOPY) -O binary $@.elf $@.bin

show:
	@echo =====
	@echo SRC: $(SRC)
	@echo GCC: $(GCC)
	@echo OBJCOPY: $(OBJCOPY)
	@echo CFLAGS: $(CFLAGS)
	@echo INCLUDE: $(INCLUDE)
	@echo LDFLAGS: $(LDFLAGS)

clean:
	rm -f ./*.o
	rm -f ./*.elf
	rm -f ./*.hex
	rm -f ./*.bin
