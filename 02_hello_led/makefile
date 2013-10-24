TOOLS_PREFIX=arm-none-eabi-
GCC = $(TOOLS_PREFIX)gcc
OBJCOPY = $(TOOLS_PREFIX)objcopy

CFLAGS  = -g -O0 -Wall -nostdlib 
CFLAGS += -mcpu=cortex-m4 -mlittle-endian -mthumb
CFLAGS += -mfloat-abi=hard -mfpu=fpv4-sp-d16
CFLAGS += -DSTM32F40_41xxx
CFLAGS += -mthumb-interwork

INCLUDE = -I. -I./CMSIS/inc -I./peripherial_driver/inc

LDFLAGS = -L. -L./peripherial_driver -Tstm32_flash.ld -lstm32f4

SRC = main.c ./CMSIS/src/system_stm32f4xx.c ./CMSIS/src/startup_stm32f40_41xxx.s 

all: lib hello_led

lib:
	$(MAKE) -j4 -C peripherial_driver

hello_led:
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
	$(MAKE) clean -C peripherial_driver
	rm -f ./*.o
	rm -f ./*.elf
	rm -f ./*.hex
	rm -f ./*.bin
