# jenkins-DDNS-update
This repository contains a Jenkinsfile which instructs Jenkins to periodically run [scripts](https://github.com/haomingyin/namecheap-DDNS) to update the DDNS record.

## Job Description

### Domain
haomingyin.com

### IP
The IP of the service which runs this Jenkinsfile

### Frequency
Once a day at a random time which is managed by Jenkins

### DDNS Records To Be Updated
* mac
* jenkins
