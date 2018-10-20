# RPG Auto Screen Generator

This is part of my `RPG Utils` series to help overcome some of the day-to-day activities which can be automated.
Those are starting with developemnt, I would advice not to use this utility, but to build their own code. For he rest, here's a simple soultion that will save you and your company lots of time. This utility will develop the subfile screens, maintainance screens and all the logic behind the program within few minutes. 

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.

### Prerequisites

You need to have AS400 Machine access (duh!)  
Create a RPGUtils Source File to store the files.
```
CRTSRCPF RPGUTILS
```

### Program and Object Descriptions  
  
  * `AUTOSCRAF`  
  This is a PF source which will hold the data to generate programs and screens.  
  Create four files based on this source AUTOSCRAF1, AUTOSCRAF2, AUTOSCRAF3, AUTOSCRAF4  

  * `AUTOSCRAF1/2/3/4`  
  This contain the data to be inserted into source files created before. (Use name as reference)  

  * `AUTOSCRC`  
  This is a dirver CL program.  

  * `AUTOSCRC`  
  Command file. Use this source to create the command, use any name, but make sure you are calling the above CL as program.  

  * `AUTOSCRP`  
  Main program that contains all the logic.  

  * `CPYBK`  
  A copybook to store prototype definations and other. If you use any other library that RPGUTILS, please change the path in above RPG program for this copy book.  


### Installing

**Step 1.**
Upload all files to AS400 server, use ftp. <em>DO NOT CHANGE THE MODE TO BINARY</em>.
```
  open pub400.com
  username
  password
  cd /QSYS.LIB
  cd YOURLIB.LIB
  cd RPGUTILS.FILE
  mput *.MBR
  cd /home/YOURLIB/
  mput *.txt
  disconnect
  quit
```
**Step 2.**
Change the atribute type accordingly once uploaded.
```
  AUTOSCRAF   PF      
  AUTOSCRC    CLLE    
  AUTOSCRCC   CMD     
  AUTOSCRD    DSPF    
  AUTOSCRP    SQLRPGLE
  CPYBK       CPY       
```
**Step3.**
Use below command to compile.
```
CRTPF FILE(YOURLIB/AUTOSCRAF1) SRCFILE(YOURLIB/RPGUTILS) SRCMBR(AUTOSCRAF) 
CRTPF FILE(YOURLIB/AUTOSCRAF2) SRCFILE(YOURLIB/RPGUTILS) SRCMBR(AUTOSCRAF) 
CRTPF FILE(YOURLIB/AUTOSCRAF3) SRCFILE(YOURLIB/RPGUTILS) SRCMBR(AUTOSCRAF) 
CRTPF FILE(YOURLIB/AUTOSCRAF4) SRCFILE(YOURLIB/RPGUTILS) SRCMBR(AUTOSCRAF) 

CRTBNDCL PGM(YOURLIB/AUTOSCRC) SRCFILE(YOURLIB/RPGUTILS) SRCMBR(AUTOSCRC) REPLACE(*YES) 

CRTCMD CMD(YOURLIB/AUTOSCRC) PGM(*LIBL/AUTOSCRCC) SRCFILE(YOURLIB/RPGUTILS) SRCMBR(AUTOSCRCC) REPLACE(*YES) 

CRTDSPF FILE(YOURLIB/AUTOSCRD) SRCFILE(YOURLIB/RPGUTILS) SRCMBR(AUTOSCRD) REPLACE(*YES)              

CRTSQLRPGI OBJ(YOURLIB/AUTOSCRP) SRCFILE(YOURLIB/RPGUTILS) SRCMBR(AUTOSCRP) COMMIT(*NONE) OBJTYPE(*PGM) REPLACE(*NO)               

```

**Step 4.** 
Copy the data from the .txt files to AUTOSCRAF1/2/3/4
```
CPYFRMIMPF FROMSTMF('/home/YOURLIB/AUTOSCRAF1.txt') TOFILE(AUTOSCRAF1) MBROPT(*REPLACE) RCDDLM(*CRLF) RMVBLANK(*NONE)
CPYFRMIMPF FROMSTMF('/home/YOURLIB/AUTOSCRAF2.txt') TOFILE(AUTOSCRAF2) MBROPT(*REPLACE) RCDDLM(*CRLF) RMVBLANK(*NONE)
CPYFRMIMPF FROMSTMF('/home/YOURLIB/AUTOSCRAF3.txt') TOFILE(AUTOSCRAF3) MBROPT(*REPLACE) RCDDLM(*CRLF) RMVBLANK(*NONE)
CPYFRMIMPF FROMSTMF('/home/YOURLIB/AUTOSCRAF4.txt') TOFILE(AUTOSCRAF4) MBROPT(*REPLACE) RCDDLM(*CRLF) RMVBLANK(*NONE)
```


## Running

Your library needs to be added to library list. Use below code.
```
  ADDLIBLE YOURLIB
 ```
Call Program with a prefix and optional library.  
If library specified, it will be used to create the pg and dspf source files.  
Prefix if used to name the programs and display files.  
E.g. if prefix is FIRST, then the display files would be `FIRSTMD, FIRSTSD` and pgms would be `FIRSTMP, FIRSTSP`.  
```
  AUTOSCRC PGMPRFX(FIRST) LIBL(YOURLIB)  
```

You will need to provide information like file (for which the screen is to be generated), library where file is present.  
Also some optional additional information like Description, Author, Date etc.  

The next thing it will ask is about fields to be present in subfile and if you want to have any positions.
Alteast one field needs to be present in your subfile display.

Program will comiple the display files and program automatically.
You can then check by calling as below
```
  CALL FIRSTSP
```

## Troubleshooting
Check `YOURLIB/AUTOSCRF` file where the source will be generated for any errors/modifications.

## Authors

Ashish Bagaddeo

## License

This project is licensed under the Apache License v2.0 - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments
Thanks www.PUB400.com for hosting a public server.
