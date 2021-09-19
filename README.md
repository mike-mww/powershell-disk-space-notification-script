# PowerShell Disk Space Notification Script
PowerShell script developed to send email notifications when disk drive capacity reaches below a certain percentage.

## Getting Started
### Prerequisities
* Windows 10 Pro or higher / Windows Server 2016 or higher
* [PowerShell 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616) or higher

## Built with
* [PowerShell 7.1.4](https://github.com/PowerShell/PowerShell/releases/tag/v7.1.4)

## Usage
#### Minimum requirements
```
# Supplying inline SMTP configuration
Powershell.exe -File "[PATH TO FILE]\disk-space-notification-script.ps1" -ToEmail "[TO EMAIL]" -FromEmail "[FROM EMAIL]" -SmtpServer "[SMTP SERVER]" -SmtpPort [SMTP PORT] -SmtpUsername "[SMTP USERNAME]" -SmtpPassword "[SMTP PASSWORD]"

# With SMTP configuration details set as parameter defaults within the script
Powershell.exe -File "[PATH TO FILE]\disk-space-notification-script.ps1" -ToEmail "[TO EMAIL]" -FromEmail "[FROM EMAIL]"
```

#### Specifying volumes
```
# Specify a single volume
Powershell.exe -File "[PATH TO FILE]\disk-space-notification-script.ps1" -ToEmail "[TO EMAIL]" -FromEmail "[FROM EMAIL]" -Volumes [VOLUME ONE]

# Specify multiple volumes
Powershell.exe -File "[PATH TO FILE]\disk-space-notification-script.ps1" -ToEmail "[TO EMAIL]" -FromEmail "[FROM EMAIL]" -Volumes [VOLUME ONE, VOLUME TWO, ...]
```

#### Setting a custom threshold percentage
```
Powershell.exe -File "[PATH TO FILE]\disk-space-notification-script.ps1" -ToEmail "[TO EMAIL]" -FromEmail "[FROM EMAIL]" -Threshold [PERCENTAGE NUMBER]
```

#### Logging
```
# Enable logging
Powershell.exe -File "[PATH TO FILE]\disk-space-notification-script.ps1" -ToEmail "[TO EMAIL]" -FromEmail "[FROM EMAIL]" -EnableLogging

# Enable logging and designate a custom log file
Powershell.exe -File "[PATH TO FILE]\disk-space-notification-script.ps1" -ToEmail "[TO EMAIL]" -FromEmail "[FROM EMAIL]" -EnableLogging -LogFile "[PATH TO LOG FILE]"
```

### SMTP configuration caveat
SMTP configuration details for the **SmtpServer**, **SmtpPort**, **SmtpUsername**, and **SmtpPassword** parameters are required in order to send email notification messages. These values can be supplied to inline parameters, however, it is recommended to set the default parameter values within the script.

### API
#### Parameters
* ***Volumes*** (array) (Default: null)\
An array of one or more specific volumes to scan (ex: C,J,S). If not included or left unspecified, all system volumes with a valid drive letter will be scanned.

* ***Threshold*** (int) (Default: 25 | Range: 1,100)\
Specify the threshold percentage of available disk space per volume. Volumes below this threshold will trigger the email notification message.

* ***ToEmail*** (string) (Default: "" | Required)\
The recipient email address for email notification messages.

* ***FromEmail*** (string) (Default: "" | Required)\
The sender email address for email notification messages.

* ***SmtpServer*** (string) (Default: "[SMTP SERVER]")\
Set the SMTP server to send email notification messages from.

* ***SmtpPort*** (int) (Default: 465)\
Set the SMTP server port number. 

* ***SmtpUsername*** (string) (Default: "[SMTP USERNAME]")\
Set the SMTP server username.

* ***SmtpPassword*** (string) (Default: "[SMTP PASSWORD]")\
Set the SMTP server password.

* ***EnableLogging*** (switch) (Default: null)\
Switch parameter to enable logging when included in the command line string.

* ***LogFile*** (string) (Default: ".\disk-space-notification-script.log")\
Set the path and filename for the log file when logging is enabled. By default, logs will be generated in a log file adjacent to the script file.