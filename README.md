# RDSDS( Reference Data Set Distribution Service)

RDSDS is Client/Server Mode, this introduction will show how to deploy RDSDS with Binary Code.

# DSDS-Client-Binary
RDSDS Client use ELIXIR AAI for authentication, make sure the client environment installed browser service. At the moment, RDSDS is running on ELIXIR Test environment, please be confirmed if you belong to ELIXIR Test VO (Virtual Organisation), if you can more details via https://perun.elixir-czech.cz/fed/registrar//registrar/?vo=elixir_test

Support: Windows 10 Pro, Centos 7, Fedora 28, Ubuntu and MacOS

If you can't run this file. Please check the file format, if it is plain text file, please execute this command : chomd +x 

# DSDS WorkFlow
![image](https://github.com/EMBL-EBI-TSI/DSDS-Client-Binary/blob/master/images/DSDSWorkflow.jpeg)

# Login with ELIXIR AAI or Google Account
![image](https://github.com/EMBL-EBI-TSI/DSDS-Client-Binary/blob/master/images/SSO.png)
![image](https://github.com/EMBL-EBI-TSI/DSDS-Client-Binary/blob/master/images/SSO_1.png)

# Commandlines

***JSON template***
````
{
"SourceSiteName": "EMBL-EBI",
"TransferSource": "gsiftp://dsds-gridftp1.ebi.ac.uk:2811/gridftp/100files",
"Protocol": "gridftp",
"Hostname": "dsds-gridftp1.ebi.ac.uk",
"Port": "2811",
"FilePath": "/gridftp/100files",
"CreatorName": "Jinny Chien",
"CreatorEmail": "jinnychien@ebi.ac.uk",
"DatasetName": "marinemetagenomics"
}
````

Login to a client shell:
````
./dsds-client-cmd
(dsds>)_
````

***Register single dataset***
````
(dsds>)reg <filename.json
````

***Register multiple datasets***

````
(dsds>)reg <filename.json
````
<br />

### Unregister a Data Set
If the data set status is not released, Data Provider can unregister it<br />

***Unregister dataset***
````
(dsds>)unreg -d datasetPID
````
<br />

### Declare a file to the Data Set
After Data Provider registered and got dataset PID. Then they can add file definition does not verify existence. This action does not check remote file’s existence.<br />

***JSON template***
````
{
“FileName”: “/ERR268/ERR268106/ERR268106.fastq.gz”,
“DatasetPID”: “embl-ebi-20161117-23456”
}
````

***declare to add a single file/multiple files to the dataset***
````
(dsds>)declare <filename.json 
````

***declare to add multiple dataset***
````
 (dsds>)declare <filename.json
````
<br />

### Index a file/folder to the Data Set
After Data Provider registered and got dataset PID. Then they can add a file or folder (recursive) and verify files existence (remote sites).<br />

***Index to add a file/folder to the dataset***
````
(dsds>)index -d datasetPID 
````

***Index a nominated folder to the dataset***
````
(dsds>)index -d datasetPID -folder foldername
````
<br />

### List details of the Data Set or Subscriber
This command will perform the file list of the specific dataset PID or list the subscribered dataset PID or the details of the specific dataset PID<br />

***List files of the dataset***
````
(dsds>)list -d datasetPID
````

***List different version files of the dataset***
````
(dsds>)list -d datasetPID -v releaseversion
````

***List active subscribed datasetPID***
````
(dsds>)list -u username
````

***Show detail of subscribed datasetPID***
````
(dsds>)list -u username -d datasetPID
````
<br />

### Verify the Data Set
Data Provider can verify that the defined dataset is available to be released and check the integrity <br />

***Verify file existence before dataset releases***
````
(dsds>)verify -d datasetPID
````

***Verify integrity checking after releasing***
````
(dsds>)verify -d datasetPID -v release_version
````
<br />

### Compare the difference
Data consumer search different version files of dataset to get the transfer list and perform the data transfer<br />

***Find difference between release versions***
````
(dsds>)diff -d datasetPID -f release_version -t release_version
````
<br />

### Release the Data Set
When data set is released, data transfer will be performed in backgrpund<br />

***Release the dataset and subscribers will get the notification when the registered dataset updates***
````
(dsds>)release -d datasetPID -v release_version
````

<br />

### Delete the file
Data Provider can delete one file from a dataset that they have not released yet. If the dataset is released, there will be a warning reminder<br />

***Delete a single file of the dataset***
````
(dsds>)delete -d datasetPID -f filename
````
<br />

### Subscription
Data consumer subscribes which data set he/she wants, then they will get the Emial notification on every release and data transfer will be run in background. <br />

***Add subscriber JSON template***
````
{
"FullName": "Kevin EBI",
"Username": "Kevin",
"Email": "jinnychien@ebi.ac.uk",
"Organisation": "EMBL-EBI",
"Hostname": "hx-gridftp-test.ebi.ac.uk",
"Port": "2811",
"FilePath": "/data01/test/test_folder/"
}
````

***Add subscriber***
````
(dsds>)adduser <filename.json
````

***Update subscriber***
````
(dsds>)updateuser <filename.json
````

***Delete subscriber***
````
(dsds>)deluser -u username
````

***Activate subscriber***
````
(dsds>)activate -u username
````

***Subscribe users and datasetPID***
````
(dsds>)sub -u username -d datasetPID
````

***Unsubscribe users and datasetPID***
````
(dsds>)unsub -u username -d datasetPID
````
<br />

### Show all command lines information
Display all available command list and its description to help Data Provider to choose.<br />

***Show all useful comment line information***
````
(dsds>)help
````
***Show help for specific command***
````
(dsds>)help <command>
````

