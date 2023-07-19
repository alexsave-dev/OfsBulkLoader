﻿# About the solution
The OFS Bulk Loader soluton easily allows generate and post bulk OFS messages into Temenos Transact™/T24™, hereinafter **Transact**.  All OFS settings and details are defined in XLSX file of specific format. Once XLSX file is defined OFS messages can be posted to Transact by running *one and only command* in the command prompt. The solution is compliant with Transact OFS module, ready for use, easy to install, and easy to maintain. It can be effectively used for Transact data migration projects and for massive postings to Transact by means of OFS. Please leave your comments, bug reports and cooperation proposals on alexsave@gmail.com. You can also follow the author on https://www.linkedin.com/in/alexander-savelyev-b8875111/
# Technical Notes
The solution has two jar files. **Util_OfsBulkLoader.jar** is deployed on Transact websever, the **OfsBulkLoader.jar** has to be run from the command prompt by the user. Jar files from the pack have been compiled on Java version 1.8.0_301. The solution has been tested on Transact R21 on Windows. All directories mentioned below have to be available for read/write to both jar files. TSA.SERVICE>TSM has to be up and running to allow OFS messages to be posted into Transact.

# Installation
Deploy the **Util_OfsBulkLoader.jar** on your web server. For example for jBoss the jar file can be copied to the directory with local jars as following:
The resource-root path should be added to module.xml file as following:
Please restart jBoss afterwards. Please contact your administrator in case of any difficulties. Please follow relevant deployment instructions if you have the webserver of a different provider.  
Create following three records in Transact:
Unzip the file ... into the directory UD. You should get the picture like this:
Important note: All settings are already done to run the solution in the directory UD without any extra modificaton. If you decide to copy the pack to different location then please change settings. Settings will be described in the relevant section below.
That's it. You can construct and post your first OFS to Transact!

# Data Preparation
All instrustion below are given taking into assumption that the solution  is present in the directory OfsBulkLoader in UD. All below mentioned directories have the relevant path from OfsBulkLoader. 

Open the excel file in the directory **./source/test.xlsx**. The file is given as an example. Please feel free to copy and modify it according to your requirements. The spreadsheet **"OFS"** contains OFS message details (highlighted in green) and other user level settings (highlighted in orange) to control the solution. Mandatory fiels are highlighted in red. You'll find explanations and hints in comments to fields on the spreadsheet.

Go to the the spreadsheet **"DATA"** to prepare ID values as well as field values to be posted as a part of OFS messages.  

# Execution
After you are done with xlsx, go to the command prompt in the directory OfsBulkLoader and run the following command to process the xlsx file above: **java -jar ./OfsBulkLoader.jar ./source/test.xlsx**

# Results and Logs
After the execution is over you can check the directory ./log for a log file.

The processed OFS file wil be in the directory ./ofs/archive if the flag POST.TO.TRANSACT=YES in the spresheet. Otherwise the file will be in the directory ./ofs

# Settings
There are two fles with settings for the solution. The file **Transact_OfsBulkLoader.properties** has to be always placed in the directory UD. The file keeps following default settings for Transact part of the solution:
|Setting  |Default Value  |Description  |
|--|--|--|
|OFS.FILE.PATH|./OfsBulkLoader/ofs/ofs|The path to the ofs file to be processed by Transact if it's required|
|LOG.FILE.PATH|./OfsBulkLoader/log/log|The path to the log file|
|OFS.ARCHIVE.DIR|./OfsBulkLoader/ofs/archive|The path to the archive directory for log files|
|DELIMITER|^|The technical delimiter used in the ofs file as a separator. **Please don't modify it until you start use ^ as the value in OFS messages**|

The file **OfsBulkLoader.properties** has to be always placed in the same directory with OfsBulkLoader.jar. The file keeps following default settings for OfsBulkLoader.jar execution:
|Setting  |Default Value  |Description  |
|--|--|--|
|OFS.FILE.PATH|./ofs/ofs|The path to the ofs file to be processed by Transact if it's required|
|LOG.FILE.PATH|./log/log|The path to the log file|
|OFS.ARCHIVE.DIR|./ofs/archive|The path to the archive directory for ofs files|
|LOG.ARCHIVE.DIR|./log/archive|The path to the archive directory for log files|
|DBTOOLS.USER|DBtools_user|The DBTools username. **Important: please change it to your real DBTools username**|
|DBTOOLS.PASSWORD|DBtools_password|The DBTools username. **Important: please change it to your real DBTools password**|
|DELIMITER|^|The technical delimiter used in the ofs file as a separator. **Please don't modify it until you start use ^ as the value in OFS messages**|
|CHECK.AGENT.SECONDS.DEFAULT|10|The interval in seconds to check whether the TSA service to post OFS messages into Transact is still running. It can be overriden user interval defined in the spreadsheet.|
|TSA.SERVICE|BNK/OFS.BULK.LOADER|The name of dedicated TSA.SERVICE to post OFS messages in Transact|
# Disclaimer
The following disclaimer outlines the terms and conditions governing the use of our solution. By using our solution, you acknowledge and agree to the terms stated below:

1.  Limited Responsibility: Our company shall not be held responsible for any damage, loss, or liability incurred by the client's systems or data arising from the use of our solution. We provide the solution on an "as is" basis, without any warranties or guarantees.
    
2.  Third-Party Dependencies: Our solution may rely on third-party components, software, or services. We do not guarantee the performance, reliability, or compatibility of these third-party elements, and we shall not be responsible for any issues caused by them.
    
3.  User Responsibilities: The client is solely responsible for the proper use, configuration, and maintenance of their systems. It is the client's responsibility to ensure the compatibility of our solution with their existing infrastructure, networks, and software.
    
4.  Limitation of Liability: In no event shall our company or its employees, contractors, or affiliates be liable for any indirect, incidental, special, or consequential damages arising from the use of our solution, even if advised of the possibility of such damages.
    
5.  Security and Data Protection: While we take reasonable measures to secure our solution, we do not guarantee the absolute security of client systems or data. The client is responsible for implementing appropriate security measures to protect their systems and data.
    
6.  Support and Maintenance: Our company may provide support and maintenance services for our solution, but we do not guarantee the availability or timeliness of such services. Any support or maintenance provided is subject to separate agreements and terms.
    
7.  Modifications and Updates: We reserve the right to modify, update, or discontinue our solution at any time without prior notice. We shall not be liable for any damages or losses resulting from such modifications or discontinuation.
    
8.  Compliance with Laws: The client is responsible for ensuring that their use of our solution complies with all applicable laws, regulations, and industry standards. Our company shall not be liable for any violations or legal issues arising from the client's use of our solution.

By using our solution, you agree to indemnify, defend, and hold harmless our company and its employees, contractors, and affiliates from any claims, liabilities, damages, or expenses arising from your use of our solution in violation of these terms.



