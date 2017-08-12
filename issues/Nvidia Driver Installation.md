# Install the Nvidia Driver in Fedora

1. Download the Driver Package from the Nvidia website. Choose the correct parameter of your display driver and finally you will download a **.run** file such as **NVIDIA-Linux-x86_64-384.59.run**.

2. To execute the file, open the terminal and input

``` sh
sh ./NVIDIA-Linux-x86_64-384.59.run
```

    you will find *ERROR: You appear to be running an X server; please exit X before installing.*.

3. To close the X server, you must exit the GUI from the OS.

    Press **Ctrl** + **Alt** + **F2** to cut back to the Text os terminal

    Input: *"init 3"*  to close the X Server.

``` sh
init 3
```

    > init 0 : shutdown  
    > init 3 : switch to the multiple user  
    > init 5 : switch to the GUI  
    > init 6 : reboot

4. Re exec the .run file, there is new error:
    
    ERROR: The Nouveau kernel driver is currently in use by your system. This driver is incompatible with the NVIDIA driver. Please......

  To fix this issue, you need modify the */etc/modprobe.d/blacklist.conf* file to prevent the Nouveau module loaded.

      1) add "blacklist nouveau" in the "blacklist.conf"
      2) comment "blacklist nvidiafb" in the "blacklist.conf"
      3) rebuild initramfs image:

      # mv /boot/initramfs-$(uname -r).img /boot/initramfs-$(uname -r).img.bak
      # dracut /boot/initramfs-$(uname -r).img $(uname -r)

5. Re exec the .run file, there is another new error:

    ERROR: Unable to load the kernel module 'nvidia.ko'. This happens most frequently when this kernel module was built against the wrong...

  To fix this issue, you need provide the kernel source code header to make the display driver built successfully.

``` sh
dnf install kernel-devel
```

Input the install the kernel-devel, there is new folder created in */usr/src/kernels/4.11.xxxx*. As I launch my fedora with the Kernel 4.11.11-300.fc26.x86_64, so the downloaded kernel folder with the same version.

Re exec the .run file.

``` sh
sh ./NVIDIA-XXXX.run --kernel-source-path=/usr/src/kernels/4.11.11-300.fc26.x86_64 -k $(uname -r)
```

The error message still exists. Review the Nvidia Log file *var/log/nvidia-installer.log* and you will find there is message: *The display driver is built by the kernel 4.11.8-300.fc26.x86_64*.

So we need to download the target kernel version source file.

``` sh
dnf install kernel-devel kernel-devel-4.11-8-300.fc26x86_64
```

Re exec the .run file. It indicate success.

6. Return the GUI

```sh
init 5
```
