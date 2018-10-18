# RPG Auto Screen Generator

This is part of my RPG Utils series to help overcome some of the day-to-day activities which can be automated.
During my previous assignments with various companies, I found that there are many static files thats get created during any project.
Initial data is added via SQL or any other method. But the problem arises when we have to modify the data. Now, usually the static files are not maintained by the developer, but by any other team. Now options to them are either SQL or UPDDTA or any other third party tool which in many cases, are error prone.

Imagine you are have a static file with 20, 40, 60 fields. Now developing program for maintainance of this file would take much of your project work time. That is not how we (coders) do the things.

So i present to you a utility that can generate subfiles, programs and all the logic behind the scene withing few mins. Isn't that awesome. 

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

You need to have AS400 Machine access (duh!)  
Create a RPGUtils library to store the files.
```
CRTLIB RPGUTILS
```

### Program and Object Descriptions  
  
  **AUTOSCRAF.pf**  
  This is a PF source which will hold the data to generate programs and screens. 
  Create four files based on this source AUTOSCRAF1, AUTOSCRAF2, AUTOSCRAF3, AUTOSCRAF4

  **AUTOSCRAF1/2/3/4.pfd**  
  This contain the data to be inserted into source files created before. (Use name as reference)

  **AUTOSCRC.cl**  
  This is a dirver CL program. 

  **AUTOSCRC.cd**  
  Command file. Use this source to create the command, use any name, but make sure you are calling the above CL as program.

  **AUTOSCRP.rpg**  
  Main program that contains all the logic. 

  **CPYBK.cpb**  
  A copybook to store prototype definations and other. If you use any other library that RPGUTILS, please change the path in above RPG program for this copy book.


### Installing

**Step 1.**
Upload all files to AS400 server, use ftp.
```
  open pub400.com
  username
  password
  cd /qsys.lib	
  cd RPGUTILS.LIB 				
  cd 	iCORESRC.FILE
  mput *.rpg
  disconnect
  quit
```
**Step 2.**
Compile Objects according to their extensions and change the atribute type accordingly once uploaded.
Below are the file extensions as per their format:  
```
  .rpg  -> RPGLE/SQLRPGLE (RPG Program)  
  .cl   -> CLLE (CL Program)  
  .cd   -> CMD (Command File)  (Use the command source, but name the command at your choice)
  .pf   -> PF (PF Source)  (Create 4 files based on this pf, AUTOSCRAF1, AUTOSCRAF2, AUTOSCRAF3, AUTOSCRAF4
  .dspf -> DSPF (Display File)  
  
  (leave these, should not be compiled)
  .cpb  -> CPY (Copybook)  
  .pfd  -> PF Data (Data to be added to given file)  
```
**Step 3.** 
Copy the data from the .pfd files to AUTOSCRAF1, AUTOSCRAF2, AUTOSCRAF3 and AUTOSCRAF4

**Step 4.**
Use below steps to test.


## Running the tests

Your library needs to be added to library list. Use below code.
```
  ADDLIBLE RPGUTILS
 ```
 

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system


## Contributing


## Authors

Ashish Bagaddeo

## License

This project is licensed under the Apache License v2.0 - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

