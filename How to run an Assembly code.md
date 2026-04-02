## Insalling the tools
1. `sudo apt install nasm biniutils`
2. create an assembly code `hello.asm:

  
    `section .data
        msg db "Hello, Linux Assembly!", 0xA  
        len equ $ - msg                        
    section .text
        global _start

    _start:
        ; syscall: sys_write (1)
        mov rax, 1          ; system call number
        mov rdi, 1          ; file descriptor (stdout)
        mov rsi, msg        ; pointer to string
        mov rdx, len        ; length of string
        syscall             ; call the kernel
        ;syscall: sys_exit (60)
        mov rax, 60
        xor rdi, rdi
        syscall
`
3. Running the code:
   1. Assemble: `nasm -f elf64 hello.asm -o hello.o`
   2. Link: `hello.o -o hello`
   3. Excute: `./hello`
   