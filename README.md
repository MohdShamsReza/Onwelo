# Onwelo
Assignment The csv files are sent by the client to the email address you have access to. The files are to be downloaded automatically because they have a fixed name. The files are to be saved on the Azure platform.

**1. What tools will you use to download the files, where will you save them?**
Answer:
Tools can be used.
 - **Python**: For scripting the automation.
 - **IMAP Library (imaplib)**: To access and read emails.
 - **Azure Storage Blob Library** (azure-storage-blob): To upload files to Azure Blob Storage.


**2. What will be the connection between the tools you choose?**
Answer:
The connection between the tools can be established using Python as the primary scripting language (Python, imaplib, and azure-storage-blob) to manage file downloads from email and uploads to Azure Blob storage.
 - **Python**: Central hub that runs the entire process.
 - **IMAP Library**: Connects to the email server to fetch emails and attachments.
 - **Azure Storage Blob Library**: Connects to Azure Blob Storage to upload the fetched attachments.
 - **Local File System**: Temporary storage for downloaded files before they are uploaded to Azure.

After saving, the files are to be cleaned of rows that are empty, and after cleaning, the file is to be saved in such a way that they are available in the SQL serverless database. You should connect PowerBi to this server and publish the report online.

**1. With what tools will you do this and what will the connection between them look like?**
Answer:
**Tools & Connections:**
 - Python and Email Server: Python script using imaplib to connect and download attachments from the email server.
 - Python and Local Filesystem: Save and temporarily store downloaded CSV files, clean them using pandas.
 - Python and Azure Blob Storage: Upload cleaned CSV files to Azure Blob Storage using azure-storage-blob.
 - Python and Azure SQL Database: Upload cleaned data to Azure SQL Serverless Database using pyodbc or sqlalchemy.
 - Power BI and Azure SQL Database: Connect Power BI to Azure SQL Database to create and publish reports.

**Process flow:**
 - Download Files from Email: Using Python with imaplib library connect to email server to local machine.
 - Clean CSV Files: Using pandas library of Python, read local file for data cleaning.
 - Upload Cleaned file to Azure SQL Serverless Database using pyodbc / sqlalchemy library of Python
 - Create and Publish Power BI Reports using Power BI Desktop and Power BI Service with Azure with direct query mode
   
**2. How will the connection between the SQL database and PowerBi online report look like?**
Answer:
Open the Power BI appllication and connect to Azure database as
 - Import: Data is imported into Power BI if data size is small
 - DirectQuery: it will fetch the data everytime when you we access the report
Prepare the dashboard and publish the report to Power BI service. You can schedule the refresh frequency according to your requirements from Power BI service,

In addition, write how the particular items will be run and what tool you will use to monitor the entire process and inform the user via email about the execution or error in the process.
 - **Azure Function**: To runs the Python script, downloads CSV, cleans the files, and uploads the CSV files to Azure Blob. Sends email notifications on success or failure.
 - **Azure Logic Apps**: To ensure the Azure Function runs on schedule and handles the notifications.
 - **Azure Monitor**: Tracks the overall health and performance, and triggers alerts based on specific conditions.
 - **Email Service**: Notifies the user about the execution status or any errors in the process.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
Alternate approach to above assignment (except POWER BI) If the mail server is Outlook, we can consider using the 
 - Microsoft Graph API: To read outlook and download attachments
 - Azure Storage: Storage account and blob container in Azure to store the file
 - Azure Function: Create Azure function to read email, download file and store the file

If the mail server is Outlook, we can consider using the Microsoft Graph API (to read outlook and download attachments).
Workflow would like to be:

**Setup:**
 - Email Account: API will be configured to access MS Outlook.
 - Azure Storage: Storage account and blob container in Azure to store the file.
 - Azure Function: Create Azure function to read email, download file and store the file

**Execution flow:**
 - Trigger: Azure function will be triggered on scheduled time.
 - Authentication: Azure function will be authenticated with API to get the access outlook.
 - Email Access: Azure function fetches recent email from specified by email.
 - Attachment Processing: Function make sure the attached file is a CSV.
 - Download: If attached file is CSV, it will download the file.
 - File Upload: Upload the file to Azure Blob Storage container.
 - File Cleaning: Apply business rules.
 - Table creation: Create table using files by Azure Synapse Analytics (first time only, later will insert the file into existing table)
 - Power BI steps will be same as mentioned above
