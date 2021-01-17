
ARMGNU = arm-none-eabi
#ARMGNU = arm-linux-gnueabi

# AOPS = --warn --fatal-warnings -mcpu=cortex-m0
AOPS = -nostdlib -target armv6-none-none-eabi
COPS = -Wall -Werror -O2 -nostdlib -ffreestanding -target armv6-none-none-eabi

all : notmain.bin

clean:
	rm -f *.bin
	rm -f *.o
	rm -f *.elf
	rm -f *.list

#---------------------------------

flash.o : flash.s
	clang $(AOPS) -c flash.s

notmain.o : notmain.c
	clang $(COPS) -mthumb -c notmain.c -o notmain.o

notmain.bin : flash.ld flash.o notmain.o
	clang -fno-exceptions -fno-unwind-tables -nostdlib -target armv6-none-none-eabi -o notmain.elf -T flash.ld flash.o notmain.o
	llvm-objdump -D notmain.elf > notmain.list
	llvm-objcopy notmain.elf notmain.bin -O binary


