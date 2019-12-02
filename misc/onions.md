# onions


## Note I did this on a linux machine, procedures for windows will be different


## Description
>Ogres are like files -- they have layers!


We are given an image called shrek.jpg but if you rename the file to shrek.txt and view it, you can see at the very end it isn't just a jpg file.  You can also use a tool like binwalk.  After installing binwalk via a package manager, run the command '''binwalk shrek.jpg'''.  You should get the following output: 

'''
DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01
275566        0x4346E         7-zip archive data, version 0.4
'''

Now we have to extract the zip file from the jpg.  To do this use the following command: '''dd if=shrek.jpg bs=1 skip=275566 of=stuff.zip'''.  This takes the file shrek.jpg, skips to the decimal position 275566 where the zip file starts that was given to us by binwalk, and puts it into a file called stuff.zip with a block size of 1.  Then if you open stuff.zip you should see flag.tar.gz, if you untar that file using '''tar xvzf flag.tar.gz''' or by clicking on it you should get flag.cpio.  Unzip that and you should get flag.imza, unzip that and you should get a file named flag.  If you run binwalk on it you can see it is a bzip2 file.  Unzip that file, and you get flag1.txt.  Well we have to decompress it, so install bzip2 from your package manager, and run '''bzip2 -d flag1.txt'''.  Open the resulting file, and you should get the flag!

flag: TUCTF{F1L3S4R3L1K30N10NSTH3YH4V3L4Y3RS}

[shrek.jpg]()