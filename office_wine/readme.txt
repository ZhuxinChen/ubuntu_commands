??
VQ7F3-PR8M4-KR2Q2-FPMPJ-DPPX3
#http://craigacgomez.blogspot.sg/2012/09/installing-microsoft-office-2010-in.html

sudo apt-get install mesa-utils mesa-utils-extra libgl1-mesa-glx:i386 libgl1-mesa-dev ia32-libs

 sudo ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /usr/lib/i386-linux-gnu/mesa/libGL.so

sudo ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so /usr/lib/i386-linux-gnu/libGL.so


sudo add-apt-repository ppa:ubuntu-wine/ppa

sudo apt-get update


sudo apt-get install wine

export WINEPREFIX="/home/cgomez/.wineprefixes/office2010/"

export WINEARCH="win32"

winetricks

...
...



 Installing Microsoft Office 2010 in Wine - Ubuntu 12.04/12.10 64-bit/32-bit
I love using Linux... and Ubuntu is my favourite flavour... it's quite user-friendly and definitely powerful... and I prefer the debian packaging over RPM.

Now, Ubuntu ships with LibreOffice which is an amazing productivity suite, or you could install OpenOffice. For the most case, these work great for me. But since I work in a world dominated by Microsoft Office, I have to stick with the Microsoft document formats like Excel, Word, Powerpoint, Visio, etc. LibreOffice can definitely read and edit all these document types, but with the Microsoft Office XML documents (docx, xlsx, pptx...), formatting is often an issue. LibreOffice (and even OpenOffice) often cannot keep the formatting and styles intact, and this can be a real problem at time.

For me, moving to Windows is not an option I would choose, and running virtual machines really doesn't cut it. Fortunately, Wine 1.5 supports Microsoft Office 2010 quite seamlessly and it works great. So, here's what I did to get Microsoft Office 2010 up and running in Wine 1.5 under Ubuntu 12.04/12.10 64-bit/32-bit.

Install mesa OpenGL and the 32-bit libraries (Ubuntu 64-bit only)

    $ sudo apt-get install mesa-utils mesa-utils-extra libgl1-mesa-glx:i386 libgl1-mesa-dev ia32-libs

Install mesa OpenGL (Ubuntu 32-bit only)

    $ sudo apt-get install mesa-utils mesa-utils-extra libgl1-mesa-glx libgl1-mesa-dev

Create softlinks for the 32-bit OpenGL libraries (Ubuntu 64-bit only)

    $ sudo ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so.1 /usr/lib/i386-linux-gnu/mesa/libGL.so
    $ sudo ln -s /usr/lib/i386-linux-gnu/mesa/libGL.so /usr/lib/i386-linux-gnu/libGL.so

Add the official Wine PPA to get the latest Wine version

    $ sudo add-apt-repository ppa:ubuntu-wine/ppa
    $ sudo apt-get update
    $ sudo apt-get install wine

Create a 32-bit Wine prefix. This is important since only Microsoft Office 2010 32-bit works on Wine and you need a 32-bit Wine environment to run 32-bit Windows applications. The WINEPREFIX can be a location of your choice.

    $ export WINEPREFIX="/home/cgomez/.wineprefixes/office2010/"
    $ export WINEARCH="win32"

Start up Winetricks via the same command window to install some required dependencies

    $ winetricks

In the WineTricks window which opens, select "Select the default wineprefix" and click OK. The new window which opens should have the WINEPREFIX location in the title

    Winetricks - current prefix is "/home/cgomez/.wineprefixes/office2010/"

Now select "Install a Windows DLL or component" and then select "dotnet20" and "msxml6" and follow the on-screen instructions.

Once that is done select "Install a font" and then select "corefonts"

Now, navigate to the location of the Microsoft Office 2010 installation and type

    $ wine setup.exe

Follow the onscreen instructions and complete the installation. 

Once that is complete, start up Winetricks via the same command window to configure some required libraries.

    $ winetricks

Select "Run winecfg". Then select the "Libraries" tab. 

You should see "*msxml6 (native, built-in)" in the "Existing overrides" section. Highlight it and click Edit and select "Native (Windows)" and click OK. Now, it should show up as "*msxml6 (native)"

Then add the "riched20" and "gdiplus" libraries from the "New override for library" section and make sure these are also set as "Native"

Once that is complete, you should be able to run the Office programs you installed via the dash/menu icons.
Posted 22nd September 2012 by Craig Gomez 



WINEARCH=win32 WINEPREFIX=~/.wine winecfg

