Recompile 64bit Linux Kernel
========================


----------


> **Data Storage Technologies and Networks**  
> **Assignment 2**
> 
> *Name* :        **Rohan Noronha**  
> *ID No* :        **2012C6PS600G **


----------


Steps followed:
------------------

 + Check the existing system kernel release using the command `uname -r`  
 
<center>![alt text](https://raw.githubusercontent.com/No-Rona/DSTN-Assgn/master/Asgn2/initial_kernal.JPG "initial kernel")<center>

+ Download latest kernel stable release from [The Linux Kernel Archives](https://www.kernel.org/ "Kernel Archives") (*Here we download version 4.4*) 

<center>![alt text](https://raw.githubusercontent.com/No-Rona/DSTN-Assgn/master/Asgn2/kernel_archive.JPG "www.kernel.org")<center>
Unzip the contents of the folder with the command `tar -xvJf linux-4.4.tar.xz`

+ Install **fakeroot** (*creates a psuedo root environment*) and **libncurses** (*to create user-interface in text mode*) using the following commands
`sudo apt-get install fakeroot kernel-package`
`sudo apt-get install libncurses5-dev`

<center>![alt text](https://raw.githubusercontent.com/No-Rona/DSTN-Assgn/master/Asgn2/libncurses5.JPG "install necessary packages")<center>

+ Inside the unzipped directory run `make menuconfig`and select `save` to save the configuration as a .config file.  (*Without making modifications*)

<center>![alt text](https://raw.githubusercontent.com/No-Rona/DSTN-Assgn/master/Asgn2/menuconfig_visual.JPG "menuconfig user-interface")<center>
<center>![alt text](https://raw.githubusercontent.com/No-Rona/DSTN-Assgn/master/Asgn2/menuconfig_save.JPG "save .config file")<center>

+ Run the command
`fakeroot make-kpkg -j 1 --initrd --append-to-version=your-name kernel-image kernel-headers`
  This command does the following
  1. builds the kernel
  2. creates the necessary .deb files for installation
  3. appends **your-name** string to the kernel release

<center>![alt text](https://raw.githubusercontent.com/No-Rona/DSTN-Assgn/master/Asgn2/make-install_fakeroot.JPG "build kernel")<center>

+ In the parent directory, the header and image `.deb` files are created. Install them using the `dpkg -i` command.
  In this case the commands were
  ```
  dpkg -i linux-image-4.4.02012c6ps600g_4.4.02012c6ps600g-10.00.Custom_amd64.deb
  dpkg -i linux-headers-4.4.02012c6ps600g_4.4.02012c6ps600g-10.00.Custom_amd64.deb
  ```
<center>![alt text](https://raw.githubusercontent.com/No-Rona/DSTN-Assgn/master/Asgn2/load_headers_img.JPG "install new kernel")<center>  

+ Reboot the system and check if the new kernel has been installed

<center>![alt text](https://raw.githubusercontent.com/No-Rona/DSTN-Assgn/master/Asgn2/final_kernal.JPG "ALL DONE!")<center>  

**Note:** 
Check the necessary kernel modules  in `/lib/modules` and the kernel files in `/usr/src` to make sure the correct kernel has been built.