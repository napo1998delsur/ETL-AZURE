SQL-to-CSV-to-Azure-using-Python
Extract data from SQL Server, input in a CSV file, and upload the file to Azure to be consumed by Power BI.

projectDiagram

Requirements
Python 3.7.6
Libs: pyodbc, shutil, azure.storage.blob, numpy.
Azure Storage account type: Data Lake Storage Gen2.
SQL Server 2014.
Host with Win Server or Win 10 installed.
Implementing the Project Step by Step
SQL Server:
Create a view and name it like "v_name_of_view".
viewSql

Azure Portal:
Create a new storage account of type "Data Lake Storage Gen2".
createStorageAccount

Create a new SAS(Shared Access Signature) with write permissions.
sasAzure

Copy the "Blob service SAS URL", "Storage Account Name" and the "Access Key".
storageAccountURL

accessKey

Host Settings:
Install Python 3.7.6 - https://www.python.org/downloads/release/python-376/.
pythonInstall

Install Libs(pyodbc, shutil, azure.storage.blob, numpy) with pip, example: "pip install pyodbc".
pipInstall

Create the follow folder structure where you want to store your projects:
structureFolders

Put both scripts in "Scripts" Folder(CreateNewProject.py, FromSqlServer-ToCsv-ToAzure.py).
Edit the script CreateNewProject.py. Replace "account_url" to your "Blob service SAS URL", "account_name" to the name of the Storage Account, and "access_key" to your access_key, copied in the second step of "In Azure Portal".
replaceScriptCreateProject

Edit the script FromSqlServer-ToCsv-ToAzure.py. Replace the SQL Server connection info(where your view are stored) and Azure Connection(account_name, account_url and access_key).
replaceSqlServerInfoScript

replaceAzureConnectionInfoScript

Run "CreateNewProject.py".
Press 1 to input the project name(same name of view, without prefix v_);
Press 2 if you want to see the project name;
Press 3 if you want to create a description for the project;
Press 4 to create the structure folder of the project;
After, Press 1 to create the container in Azure and 3 to quit.
Consult logs in Analytics/Scripts/Logs and copy the "Azure Container URL". You will need this for the PowerBI steps.
containerURL

Access folder "Analytics/Projects/Your Project/Scripts".
Execute "FromSqlServer-ToCsv-ToAzure.py".
Check the log in "Analytics/Projects/Your Project/Logs".
Check the CSV File in "Analytics/Projects/Your Project/Files" and in the Azure Container.
Scheduling Script in Windows:
Get directory where Python is installed.
dirPython

Open the Windows Task Scheduler.
Create a new task.
Configure the Triggers.
Configure the Action like below:
taskSchd

Container Permission in Azure Portal:
Option 1- If you have Azure AD, you can add the "Storage Blog Data Reader" for a user in Access Control of the container.
roleStorageBlobDataReader

Option 2- Create a SAS(Shared Access Signature) in the container, to users access data(csv) in PowerBI using Access Key.