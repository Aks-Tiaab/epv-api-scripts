# Account Onboard Utility

> **Note:** The content of the sample_accounts.csv is for example only and does not represent real accounts

## Main capabilities
-----------------
- The tool Uses REST API and can support v9.8 of PVWA and up
- The tool supports basic Account and Safe Creation, much like the Password Upload Utility
- The tool supports Template Safe (currently one for all Accounts)
- The tool can take a simple CSV file with only the relevant Account information

In order to run the tool you need to run some simple commands in Powershell.
The Tool supports two modes: [*Create*](#create-command) and [*Update*](#update-command)

The tool will create a log file in the same folder of the script called: _"Account_Onboarding_Utility.log"_
Running the toll with common parameters of Debug and Verbose will add more information to the log

## Parameters:
```powershell
Accounts_Onboard_Utility.ps1 -PVWAURL <string> [-<Create / Update>] [-TemplateSafe] [-CsvPath] [-CsvDelimiter] [-DisableSSLVerify] [-NoSafeCreation]
```
- PVWAURL
	- The URL of the PVWA that you are working with. 
	- Note that the URL needs to include 'PasswordVault', for example: "https://myPVWA.myDomain.com/PasswordVault"
	- When working with PVWA behind a load balancer, note that the session must be defined as sticky session. Alternatively, work with a single node PVWA
- DisableSSLVerify
	**(NOT RECOMMENDED)**
	- In cases when you want to test the script on a PVWA environment that does not include a valid SSL certificate, you can use this parameter
- Create / Update 
	The supported actions for onboarding of accounts
- CsvPath
	- The CSV Path for the accounts to be onboarded
- CsvDelimiter
	- The CSV delimiter to be used.
	- Available values: comma, tab
	- Default value: _comma delimited_
- TemplateSafe
	- The Template safe to copy properties from
	- Using this parameter requires that the template safe exists
	- The process will create any new safe according to the Template Safe including managing CPM and Safe Members
- NoSafeCreation
	- In case used, safes that do not exist will not be created

### Create Command:
```powershell
Accounts_Onboard_Utility.ps1 -PVWAURL <string> -Create [-AuthType <string>] [-OTP <string>] [-TemplateSafe <string>] [-CsvPath <string>] [-CsvDelimiter <string>] [-DisableSSLVerify] [-NoSafeCreation] [<CommonParameters>]
```

If you just want to Create Accounts (including creating the Safes if they don’t exist):
```powershell
& .\Accounts_Onboard_Utility.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault"  -CsvPath .\accounts.csv -Create
```

If you want to Create Accounts and Safes according to a Safe Template:
```powershell
& .\Accounts_Onboard_Utility.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -CsvPath .\accounts.csv -Create -TemplateSafe “MyTemplateSafe”
```

If you want to Create Accounts but not create the safes (if they don’t exist):
```powershell
& .\Accounts_Onboard_Utility.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -CsvPath .\accounts.csv -Create -NoSafeCreation
```

### Update Command:
```powershell
Accounts_Onboard_Utility.ps1 -PVWAURL <string> -Update [-AuthType <string>] [-OTP <string>] [-TemplateSafe <string>] [-CsvPath <string>] [-CsvDelimiter <string>] [-DisableSSLVerify] [-NoSafeCreation] [<CommonParameters>]
```

If you want to Create and Update Accounts (and safes):
```powershell
& .\Accounts_Onboard_Utility.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -CsvPath .\accounts.csv -Update
```

If you want to Create and Update Accounts (without Safe creation):
```powershell
& .\Accounts_Onboard_Utility.ps1 -PVWAURL "https://myPVWA.myDomain.com/PasswordVault" -CsvPath .\accounts.csv -Update -NoSafeCreation
```
