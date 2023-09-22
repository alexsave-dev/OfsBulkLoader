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
 - Easy to maintain.

It can be effectively used for Transact data migration projects and for massive postings to Transact by means of OFS.

Please leave your comments, bug reports and cooperation proposals on alexsave@gmail.com.

You can also follow the author on https://www.linkedin.com/in/alexander-savelyev-b8875111/

# Gratitudes:
I'd like to gratitude everybody who made the input into my project!
Special thanks to:
 - Peter Vengher (https://www.linkedin.com/in/peter-vengher-41b07a10/), for his ideas and support in testing.   
 - Rafiq Qarakishiyev (https://www.linkedin.com/in/rafiq-qarakishiyev-337a98110/), for support in testing.
 - My son Aleksei Savelyev (https://www.linkedin.com/in/aleksei-savelyev-941165192/), for technical support. 

# Technical Notes
The solution has one jar file **OfsBulkLoader.jar** which has to be run from the command prompt by the user. The jar file has been compiled on Java version 1.8.0_301. The solution has been tested on following environments: 
- Transact R21, Windows 10, H2 database
- Transact R23, openSUSE Leap 15.5, MSSQL database 

The solution is compatible with Temenos Transact TAFJ environments on H2 and MSSQL databases. 

Prerequisite. Both Transact TSA.SERVICE's **TSM** and **OFS.MESSAGE.SERVICE** in any company have to be up and running to allow OFS messages to be posted into Transact.

# Installation
Create the file F.OFS.BULK.LOADER.IDS by following command in DBTools in JQL mode:
CREATE-FILE F.OFS.BULK.LOADER.IDS 3 4
![dbtools](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/a51d5c05-90c1-4d67-ad7e-d52e2f9ae22f)

Find the required release here: https://github.com/alexsave-dev/OfsBulkLoader/releases. The current Readme file stands for the most up-to-date release. Previous Readme files are put inside relevant release packs. 
Unzip the file OfsBulkLoader.zip into the directory UD. You should get the picture like this:

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/b25548a3-7cc8-4f03-8ded-bc734a188e96)


**Important. The file OfsBulkLoader.properties has to be always placed in the same directory with OfsBulkLoader.jar. The file keeps settings for OfsBulkLoader.jar execution. The current directory is the directory where the OfsBulkLoader.jar is located if you define relative paths for files and directories.**

Modify OfsBulkLoader.properties to setup the path to TAFJ directory in TAFJ.HOME:

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/cb6c1bf7-91b6-4eeb-9824-dcb0f04eb208)


## That's it. You can construct and post your first OFS to Transact!

# Data Preparation
Open the excel file in the directory **OfsBulkLoader/source/test.xlsx**. The file is given in GIT as an example. Please feel free to copy and modify it according to your requirements. The spreadsheet **"OFS"** contains OFS message details (highlighted in green) and other user level settings (highlighted in orange) to control the solution. Mandatory fields are highlighted in red. You'll find explanations and hints in comments to fields on the spreadsheet.

Go to the the spreadsheet **"DATA"** to prepare ID values as well as field values to be posted as a part of OFS messages.  

# Execution
After you are done with xlsx, go to the command prompt in the directory OfsBulkLoader and run the following command to process the specific xlsx file (the name of the xlsx file should be provided as a parameter): **java -jar ./OfsBulkLoader.jar ./source/your_file_name.xlsx**.   

![image](https://github.com/alexsave-dev/OfsBulkLoader/assets/65187677/b1f2c649-0579-4fd8-adc8-c1ad726a0013)


# Results and Logs
After the execution is over you can check the directory **OfsBulkLoader/log** for a log file.

The processed OFS file will be in the directory **OfsBulkLoader/ofs/archive** if the flag **POST.TO.TRANSACT=YES** in the spreadsheet. Otherwise the ready OFS file will be in the directory **OfsBulkLoader/ofs** without further processing. 

# Settings
**Important note: You don't need to change settings if you followed all instructions above and you are happy with existing structure of folders and other settings. If you decide to allocate the pack in another location then please change relevant paths.**

The file **OfsBulkLoader.properties** has to be always placed in the same directory with **OfsBulkLoader.jar**. The file keeps settings for **OfsBulkLoader.jar** execution. **The current directory is the directory where the **OfsBulkLoader.jar** is located if you define relative paths for files and directories.**
|Setting  |Default Value  |Description  |
|--|--|--|
|OFS.FILE.NAME|./ofs/ofs|The name of the ofs file|
|LOG.FILE.NAME|./log/log|The name of the log file|
|OFS.ARCHIVE.DIR|./ofs/archive|The path to the archive directory for ofs files|
|LOG.ARCHIVE.DIR|./log/archive|The path to the archive directory for log files|
|TAFJ.HOME|./log/archive|The path to TAFJ directory. **Important: please change it to the location of TAFJ folder on your server before first run**|
|CHECK.AGENT.SECONDS.DEFAULT|10|The interval in seconds to check whether the TSA service to post OFS messages into Transact is still running. It can be overriden by user interval defined in the spreadsheet.|
|DEBUG|FALSE|Please set the parameter to TRUE in case if extra details have to be provided for technical support|
|JDBC.URL.OVERRIDE||By default JDBC Url is taken from the relevant properties file in TAFJ/conf directory. If this setting is assigned then it overrides the default JDBC Url value. Usually this value is changed if additional connections options have to be given together with JDBC Url from TAFJ properties|
|FM.DELIMITER|\uF8FE|Please keep this value unchanged unless you get other instructions from technical support |

