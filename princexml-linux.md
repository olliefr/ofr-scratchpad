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
    
      * _Dry run_ to see what dependencies are missing:
    
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
        $ prince --version
        Prince 13.5
        Copyright 2002-2020 YesLogic Pty. Ltd.
        Non-commercial License
        ```
        
4. Test the conversion with a sample document, as suggested by the [Installation Guide](https://www.princexml.com/doc/first-doc/):

     * Download the source file `lab_report.html`:

       ```Shell
       $ wget https://www.princexml.com/doc/first-doc/samples/lab_report.html
       ```
       
     * If the above fails, the content of the source file `lab_report.html` can also be copied from the [Installation Guide](https://www.princexml.com/doc/first-doc/#the-lab-report) and saved with a text editor.

     * Process the source file using the command line `prince` command to generate _unstyled_ PDF output file:

       ```Shell
       $ prince lab_report.html
       ```

     * The previous step will have created a `lab_report.pdf` file in the *current directory*. Its contents can be _inspected on its own_ or _compared with_ the sample PDF file offered in the [Installation Guide](https://www.princexml.com/doc/assets/samples/lab_report.pdf).

Now we have a working PrinceXML installation under WSL Linux!

&mdash;&hairsp;Oliver Frolovs, 2020