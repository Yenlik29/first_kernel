Что Вам понадобится:
- Компьютер, совместимый с x86,
- Linux,
- ассемблер NASM,
- GCC,
- ld (GNU Linker),
- GRUB.

После того, как все файлы готовы, надо собрать ядро:
1. $> nasm -f elf32 kernel.asm -o kasm.o
2. $> gcc -m32 -c kernel.c -o kc.o
3. $> ld -m elf_i386 -T link.ld -o kernel kasm.o kc.o
# GRUB требует, чтоб название с файла с ядром было названо kernel-version, thus:
4. $> mv kernel kernel-111
5. $> sudo cp kernel-111 /boot
# Найдите конфигурационный файл GRUB'а - grub.cfg (/boot/grub/) и допишите туда следующее:
menuentry 'kernel 701' {
    set root='hd0,msdos1'
    multiboot /boot/kernel-701 ro
}

ТЕПЕРЬ, перезагрузите компьютер, и можешь увидеть свое ядро в списке!
Удачи :)
