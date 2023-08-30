# About the solution
The OFS Bulk Loader soluton easily allows generate and post bulk OFS messages into Temenos Transact™/T24™, hereinafter **Transact**.  All OFS settings and details are defined in XLSX file of specific format. Once XLSX file is defined OFS messages can be posted to Transact by running *one and only command* in the command prompt. 

Make OFS and other settings:

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/80bc8040-dde2-4d6c-9140-e118321e33e6)

Prepare the data:

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/ebc5581f-4d8a-48cd-a334-16eeec46b03a)

Run the command: **java -jar ./OfsBulkLoader.jar ./source/test.xlsx**

### Enjoy the result :)

## The solution is:

 - Compliant with Transact OFS module  
 - Ready for use  
 - Easy to install 
 -  Easy to maintain.

It can be effectively used for Transact data migration projects and for massive postings to Transact by means of OFS.

Please leave your comments, bug reports and cooperation proposals on alexsave@gmail.com.

You can also follow the author on https://www.linkedin.com/in/alexander-savelyev-b8875111/
# Technical Notes
The solution has two jar files. **Util_OfsBulkLoader.jar** is deployed on Transact websever, the **OfsBulkLoader.jar** has to be run from the command prompt by the user. Jar files from the pack have been compiled on Java version 1.8.0_301. The solution has been tested on following environments: 
- Transact R21, Windows 10, H2 database
- Transact R23, openSUSE Leap 15.5, MSSQL database 

The solution is compatible with Temenos Transact TAFJ environments on H2, MSSQL and Oracle databases. 

Prerequisite. Transact **TSA.SERVICE>TSM** has to be up and running to allow OFS messages to be posted into Transact.

# Installation
Find the required release here: https://github.com/alexsave-dev/OfsBulkLoader/releases. The current Readme file stands for the most up-to-date release. Previous Readme files are put inside relevant release packs. Deploy the **Util_OfsBulkLoader.jar** on your web server. For example for jBoss the jar file can be copied to the directory with local jars as following:

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/e0f0d819-8e51-4dab-964a-1a7b3ad184a0)

The resource-root path should be added to module.xml file as following:

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/2a05b3d8-0aab-4c51-94a0-ad6c5638dfb0)

Please restart jBoss afterwards. Please contact your administrator in case of any difficulties. Please follow relevant deployment instructions if you have the webserver of a different provider.  
Create following three records in Transact:

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/26f5c04d-dc46-4259-9ad4-7b78fe81150d)

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/0e31ded7-747b-4d9e-8087-eb6213a04c7d)

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/b13c69c6-a939-4e75-afd3-320159640214)

**Please assign the relevant user and workload profile for the TSA.SERVICE>BNK/OFS.BULK.LOADER**

Unzip the file OBL.zip into the directory UD. You should get the picture like this:

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/f356d82e-2498-4bba-a397-6fc2a237677a)

**Important. The file OfsBulkLoader.properties has to be always placed in the same directory with OfsBulkLoader.jar. The file keeps settings for OfsBulkLoader.jar execution. The current directory is the directory where the OfsBulkLoader.jar is located if you define relative paths for files and directories.**

Modify OfsBulkLoader.properties to setup the path to TAFJ directory in TAFJ.HOME:
OFS.FILE.NAME=./ofs/ofs
LOG.FILE.NAME=./log/log
OFS.ARCHIVE.DIR=./ofs/archive
LOG.ARCHIVE.DIR=./log/archive
**TAFJ.HOME=../../TAFJ**
DELIMITER=^
CHECK.AGENT.SECONDS.DEFAULT=10
TSA.SERVICE=BNK/OFS.BULK.LOADER
DEBUG=FALSE
JDBC.URL.OVERRIDE=
FM.DELIMITER=\uF8FE

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/59dfcb4e-43bf-4042-a593-fd6a28f0fd20)



## That's it. You can construct and post your first OFS to Transact!

# Data Preparation
Open the excel file in the directory **OfsBulkLoader/source/test.xlsx**. The file is given in GIT as an example. Please feel free to copy and modify it according to your requirements. The spreadsheet **"OFS"** contains OFS message details (highlighted in green) and other user level settings (highlighted in orange) to control the solution. Mandatory fields are highlighted in red. You'll find explanations and hints in comments to fields on the spreadsheet.

Go to the the spreadsheet **"DATA"** to prepare ID values as well as field values to be posted as a part of OFS messages.  

# Execution
After you are done with xlsx, go to the command prompt in the directory OfsBulkLoader and run the following command to process the specific xlsx file (the name of the xlsx file should be provided as a parameter): **java -jar ./OfsBulkLoader.jar ./source/your_file_name.xlsx**.   

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/b1f2c649-0579-4fd8-adc8-c1ad726a0013)


# Results and Logs
After the execution is over you can check the directory **OfsBulkLoader/log** for a log file.

The processed OFS file will be in the directory **OfsBulkLoader/ofs/archive** if the flag **POST.TO.TRANSACT=YES** in the spreadsheet. Otherwise the ready OFS file will in the directory **OfsBulkLoader/ofs** without further processing. 

# Settings
**Important note: You don't need to change settings if you followed all instructions above and you are happy with existing structure of folders and other settings. If you decide to allocate the pack in another location then please change relevant paths.**

There are two fles with settings for the solution. 
The file **Transact_OfsBulkLoader.properties** has to be always placed in the directory UD. The file keeps settings for Transact part of the solution. **The current directory is UD if you define relative paths for files and directories.**
|Setting  |Default Value  |Description  |
|--|--|--|
|OFS.FILE.NAME|./OfsBulkLoader/ofs/ofs|The name of the ofs file|
|LOG.FILE.NAME|./OfsBulkLoader/log/log|The name of the log file|
|OFS.ARCHIVE.DIR|./OfsBulkLoader/ofs/archive|The path to the archive directory for log files|
|DELIMITER|^|The technical delimiter used in the ofs file as a separator. **Please don't modify it until you start use ^ as the value in OFS messages**|

The file **OfsBulkLoader.properties** has to be always placed in the same directory with **OfsBulkLoader.jar**. The file keeps settings for **OfsBulkLoader.jar** execution. **The current directory is the directory where the **OfsBulkLoader.jar** is located if you define relative paths for files and directories.**
|Setting  |Default Value  |Description  |
|--|--|--|
|OFS.FILE.NAME|./ofs/ofs|The name of the ofs file|
|LOG.FILE.NAME|./log/log|The name of the log file|
|OFS.ARCHIVE.DIR|./ofs/archive|The path to the archive directory for ofs files|
|LOG.ARCHIVE.DIR|./log/archive|The path to the archive directory for log files|
|TAFJ.HOME|./log/archive|The path to TAFJ directory. **Important: please change it to the location of TAFJ folder on your server before first run**|
|DBTOOLS.USER|youruser|The DBTools username. **Important: please change it to your real DBTools username before first run**|
|DBTOOLS.PASSWORD|Pa!12345678|The DBTools username. **Important: please change it to your real DBTools password before first run**|
|DELIMITER|^|The technical delimiter used in the ofs file as a separator. **Please don't modify it until you start use ^ as the value in OFS messages**|
|CHECK.AGENT.SECONDS.DEFAULT|10|The interval in seconds to check whether the TSA service to post OFS messages into Transact is still running. It can be overriden by user interval defined in the spreadsheet.|
|TSA.SERVICE|BNK/OFS.BULK.LOADER|The name of dedicated TSA.SERVICE to post OFS messages in Transact|
