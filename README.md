BLOB_STORAGE_KEY: q5ReF+wTResource Group
Resource Group Name: DacityProject
2. SQL Database
DB name: dacitydb
Server: dacityservers.database.windows.net
DB region: us-east
Admin login: cmsadmin
Admin password: CMS4dmin
Resource group: DacityProject
DB workload env: Development
DB compute + storage: DTU - Basic
Press the "Next: Networking" button, then select "Public Endpoint", and set both of the Firewall rules that appear to "Yes".
Set everything else to default
Run SQL queries in sql_scripts/ directory after completion, starting from the users table. Don't forget to take screenshots.
3. Storage Account
Resource group: DacityProject
Storage account name: dacityimages (needs to be unique)
Advanced - Allow enabling anonymous access on individual containers: Enable
Advanced - Access tier: Cool
Network access: Enable public access from all networks (the default)
Create container named "images". Set its access level to Container.
From Security + networking > Access keys:
Blob Storage key: q5ReF+wTlEav71z/GFZnOJLyX8BhaAbAR7RdDA8eTEbf4c31VvzI+L1Yer+7RrlPht328XJBuNDP+AStgQJGSg==

4. Microsoft Entra ID
4.1. App Registration
Name: dacityEntraID
Who can use? "Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)"
4.2. Secret Creation
Secret description: test
Secret Key: cac228dc-3215-4ee7-9b64-23b99f572ff1
Client Secret: jDr8Q~WRCv_dJ0nIPCA3bTzscsl.G5yGcGVticC2
Application (client) ID: bdc8c578-c157-4138-b92f-588ce096717c

Application
Name: udacityapp.azurewebsites.net
Runtime stack: Python 3.10
Pricing Plan: Free F1
If you are getting a "Validation failed for a resource" error, pick a different region.
After creation:

Settings -> Environment variables - Add the following variables (sample values are included, replace them with your values):
BLOB_ACCOUNT:  DacityProject
BLOB_CONTAINER: dacityimageslEav71z/GFZnOJLyX8BhaAbAR7RdDA8eTEbf4c31VvzI+L1Yer+7RrlPht328XJBuNDP+AStgQJGSg==

SQL_SERVER: dacityservers.database.windows.net
SQL_DATABASE: dacitydb
SQL_USER_NAME: cmsadmin
SQL_PASSWORD: CMS4dmin
CLIENT_SECRET: jDr8Q~WRCv_dJ0nIPCA3bTzscsl.G5yGcGVticC2
SECRET_KEY: cac228dc-3215-4ee7-9b64-23b99f572ff1
CLIENT_ID: bdc8c578-c157-4138-b92f-588ce096717c
Deployment Center
Source: GitHub
Pick the repo that contains the starter files.
6. Setting up OAuth2
At this point, your application should already be running. You should already be able to log in with username admin and password pass and you can create new posts or update existing ones.

The next part is getting the OAuth2 login to work.

Go to Microsoft Entra ID > App Registrations, click on the App Registration created earlier, and then pick Authentication from the left sidebar.

6.1. Microsoft Entra ID - Authentication - Add a Platform - Web
Redirect URIs: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/getAToken
logout URL: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/login
