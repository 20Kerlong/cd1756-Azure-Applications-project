Resource Group
Resource Group Name: kms
2. SQL Database
DB name: kmsdb
Server: kmsservers.database.windows.net
DB region: us-east
Admin login: cmsadmin
Admin password: CMS4dmin
Resource group: kms
DB workload env: Development
DB compute + storage: DTU - Basic
Press the "Next: Networking" button, then select "Public Endpoint", and set both of the Firewall rules that appear to "Yes".
Set everything else to default
Run SQL queries in sql_scripts/ directory after completion, starting from the users table. Don't forget to take screenshots.
3. Storage Account
Resource group: kms
Storage account name: kmsimages (needs to be unique)
Advanced - Allow enabling anonymous access on individual containers: Enable
Advanced - Access tier: Cool
Network access: Enable public access from all networks (the default)
Create container named "images". Set its access level to Container.
From Security + networking > Access keys:
Blob Storage key: gecXg4FWjsyl8hR1/CPvIDEFq3t4OPRmBOuW44XytJCPCcdqizbuq907xH3J1k3HCYBgjBI7qZ2l+ASts5l+oQ==

4. Microsoft Entra ID
4.1. App Registration
Name: kmsEntraID
Who can use? "Accounts in any organizational directory (Any Microsoft Entra ID tenant - Multitenant) and personal Microsoft accounts (e.g. Skype, Xbox)"
4.2. Secret Creation
Secret description: test
Secret Key: 945f2a17-b79f-40f9-899b-e7b0151b9e76
Client Secret: 42F8Q~BMAmO-rdtnPmmXINEPYH3GhRnU9Mzz4ad1
Application (client) ID: 9fa4b8c7-771b-458e-a3c0-9324a62fef94

Application
Name: kmsapp.azurewebsites.net
Runtime stack: Python 3.10
Pricing Plan: Free F1
If you are getting a "Validation failed for a resource" error, pick a different region.
After creation:

Settings -> Environment variables - Add the following variables (sample values are included, replace them with your values):
BLOB_ACCOUNT: kmsimages
BLOB_CONTAINER: images
BLOB_STORAGE_KEY: N1L3GpGK4J+EAkf2Bwu9QJXhS2JQF3mkK3Y1CUE7ah79tTmtUUDFnMKCBrVHSxGXpyw0J6QS2eEt+AStxkseeA==

SQL_SERVER: kmsservers.database.windows.net
SQL_DATABASE: cms
SQL_USER_NAME: cmsadmin
SQL_PASSWORD: CMS4dmin
CLIENT_SECRET: 42F8Q~BMAmO-rdtnPmmXINEPYH3GhRnU9Mzz4ad1
SECRET_KEY: 945f2a17-b79f-40f9-899b-e7b0151b9e76
CLIENT_ID: 9fa4b8c7-771b-458e-a3c0-9324a62fef94
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

Go to Microsoft Entra ID > App Registrations, click on the App Registration created earlier, and then pick Authentication from the left sidebar.

6.1. Microsoft Entra ID - Authentication - Add a Platform - Web
Redirect URIs: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/getAToken
logout URL: https://[IP ADDRESS FROM VM or WEB APP ADDRESS]/login
