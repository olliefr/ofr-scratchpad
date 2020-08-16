# Install PrinceXML in WSL Ubuntu Linux

1. [Download PrinceXML](https://www.princexml.com/download/) for `Ubuntu 20.04 / 64-bit deb` file.
   
   ```Shell
   $ wget https://www.princexml.com/download/prince_13.5-1_ubuntu20.04_amd64.deb
   ```

2. Install `gdebi`, if it wasn't already installed. Note, that the package name actually is `gdebi-core`. The `gdebi` package is *enormous* and hopefully is not necessary.

   ```Shell
   $ sudo apt install gdebi-core
   ```
   
3. Follow the [Installation Guide](https://www.princexml.com/doc/installing/#installing-prince-on-linux-freebsd) to install using `gdebi`. This tool, unlike `dpkg`, will automatically download and install all necessary dependencies.
    
      * **(Optional)** Dry run to see what dependencies are missing:
    
        ```Shell
        $ sudo gdebi --apt-line prince_13.5-1_ubuntu20.04_amd64.deb
        Reading package lists... Done
        Building dependency tree
        Reading state information... Done
        Reading state information... Done
        libgif7 libjbig0 libjpeg-turbo8 libjpeg8 liblcms2-2 libpixman-1-0 libtiff5 libwebp6
        ```

      * These dependencies look reasonable, so *install* PrinceXML *and* the dependencies:
    
        ```Shell
        $ sudo gdebi prince_13.5-1_ubuntu20.04_amd64.deb
        ```
    
      * Verify the installation:
       
        ```Shell
        $ prince  --version
        Prince 13.5
        Copyright 2002-2020 YesLogic Pty. Ltd.
        Non-commercial License
        ```
        
&mdash;&hairsp;Oliver Frolovs, 2020