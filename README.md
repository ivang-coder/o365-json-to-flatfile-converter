# Office 365 JSON Flatfile converter
## Summary 
This Python script converts JSON-formated Microsoft Office Endpoint list to flatfiles compatible with firewalls and various security appliances i.e. Palo Alto Networks, Cisco, etc.
The flatfiles are generated in a common (universal) format. To ease administrative burden you might opt to run HTTP, FTP, SFTP and TFTP servers preferrably on a single box/container to allow various systems access the flatfiles.
## Prerequisites
### RHEL and the likes
`sudo yum install python3`
### Ubuntu
`sudo apt-get install python3`
## Recommendations
Microsoft updates O365 IPs and FQDNs quite frequently, https://docs.microsoft.com/en-us/office365/enterprise/office-365-ip-web-service
* It's recommended to run the script hourly.
* A non-root user, i.e. user-py, with restricted privileges to run background and maintenance tasks is preferrable.
* The script can be placed anywhere but a non-system directory like **/opt** for third-party packages suits the most
* The output files should be directed to a shared location with read access or a folder owned by HTTP/FTP server that is accessible by security appliances and their External Dynamic Lists
## Before running 
1. Amend User Variables
2. Confirm location paths are accessible
### User Variables
\_\_VersionPath\_\_ - path where client ID and latest version number will be stored

\_\_OutputPath\_\_ -  path where flatfiles will be stored

\_\_Server\_\_ - local email server FQDN/IP. **No authentication is currently supported**

\_\_Port\_\_ - email server port

\_\_StartTls\_\_ - establish secure TLS connection

\_\_EmailFrom\_\_ - email sender

\_\_EmailTo\_\_ - email recepient(s)

## Flatfile name format
*o365_endpoints_[ipv4|ipv6|url]\_[Common|Exchange|SharePoint|Skype]\_[tcp|udp]_[various ports].txt*
## The files and their function
**/o365-json-to-flatfile-converter.py** - the main script

**/o365_endpoints_clientid_latestversion.txt** - this file is created upon first run and contains version ID. Every run the version ID is compared with the online version ID as a part of initial check. If a new version is identified, the script downloads the JSON file and starts processing. To avoid overwhelming administrative mailbox, an email is generated only when a new version of JSON file has been identified and processed.
## License
MIT License
## Author
Ivan Gladushko
