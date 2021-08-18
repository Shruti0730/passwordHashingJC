# passwordHashingJC
## Table of contents
* Password Hashing Application Overview
* Test cases for password hashing application
* Defects in password hashing application

## General info
The following is the requirement specification that was used in building the password hashing
application. It describes what the application should do.

● When launched, the application should wait for http connections.

● It should answer on the PORT specified in the PORT environment variable.

● It should support three endpoints:

○   A POST to /hash should accept a password. It should return a job identifier
immediately. It should then wait 5 seconds and compute the password hash.
The hashing algorithm should be SHA512.

○   A GET to /hash should accept a job identifier. It should return the base64
encoded password hash for the corresponding POST request.

○   A GET to /stats should accept no data. It should return a JSON data structure
for the total hash requests since the server started and the average time of a
hash request in milliseconds.

● The software should be able to process multiple connections simultaneously.

● The software should support a graceful shutdown request. Meaning, it should allow any in-flight
password hashing to complete, reject any new requests, respond with a 200 and shutdown.

● No additional password requests should be allowed when shutdown is pending.
	
	
## Setup
Obtaining the Password Hashing Application
We are storing the password hashing application in a public S3 bucket. You can get it in the
following manner:

**Mac/Linux example:**

$ wget --no-check-certificate --no-proxy
‘https://s3.amazonaws.com/qa-broken-hashserve/broken-hashserve.tgz’

**Windows example:**

On modern Windows systems with PowerShell 3.x, curl/wget/iwr are just aliases for
Invoke-WebRequest. It has equivalent curl/wget/iwr parameters and output; they are just
named different things. On Windows 10, you will also need to install 7zip or equivalent
extraction tool to unpack the *.tgz archive.
C:/> iwr -Uri https://s3.amazonaws.com/qa-broken-hashserve/broken-hashserve.tgz
-UseBasicParsing -o ./broken-hashserve.tgz

**Password Hashing Application Execution:**

The broken-hashserve.tgz archive contains binaries for Linux, Windows & Mac OS
X operating systems. Unpack and use the binary corresponding to your OS of choice.
You must set a PORT environment variable before executing the application. It will
crash otherwise.

**Mac/Linux example:**

** JumpCloud Confidential, please do not distribute this document in any form.**
$ export PORT=8088

**Windows example:**

1. C:/> SET PORT=8088
2. Use the Control Panel to set a System or User variable for
PORT. Remember to reopen your cmd window after doing this.
