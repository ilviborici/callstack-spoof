# Callstack spoofing + Indirect Syscalls POC
This project consists of a simple C++ self-Injecting dropper focused on EDR evasion. To implement it, I have combined the use of  **``Windows Thread Pooling``**  to hide the call stack and the use of  **``indirect syscalls``**  to avoid hooking in the NTDLL.


It performs a jump to ntdll to utilize one of the syscall instructions. This should be considered a malicious action; however, upon executing the return in ntdll, we return to the code of tpWorker, which is located within ntdll. Thus, from the perspective of the antivirus (AV), ntdll would appear to be making a call to another part of ntdll, which is not considered malicious.


## To compile:

```bash
nasm -f win64 ./syscalls.asm -o ./syscalls.obj
g++ -o output.exe main.cpp syscalls.obj
```

## ⚠️Attention:

This POC has been developed for Windows 10. To use it in a real environment the syscalls should be adapted for the corresponding Windows version.
