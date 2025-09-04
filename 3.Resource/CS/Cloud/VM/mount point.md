
- when I create a directory inside the VM filesystem
- That directory lives on the VM’s virtual disk (.vmdk)
- when I power off and on the VM, the directory statys 

Temporary or RAM-backed mount 

-  some directories are special (e.g, /tmp, /run) - they are in memory 
- After reboot, those contents do disappear, because they live in RAM 