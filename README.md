<img src="https://zupimages.net/up/20/37/uwy6.png" width="80"/>
<img src="https://i.pinimg.com/originals/bc/00/a8/bc00a8bd0a4be6cd29680d02c70f0539.png" width="100" align="right"/>

# nexus-report-plugin
[![Build Status](https://travis-ci.org/groupe-edf/nexus-report-plugin.svg?branch=master)](https://travis-ci.org/github/groupe-edf/nexus-report-plugin)
[![Coverage Status](https://coveralls.io/repos/github/groupe-edf/nexus-report-plugin/badge.svg?branch=master)](https://coveralls.io/github/groupe-edf/nexus-report-plugin?branch=master)

Download a statistics report of your repositories.

## Build
You don't need to build the code to install the plugin, you can find the .kar file in the last release.

If you want to build the plugin by yourself, you can check it out and run `mvn clean install -PbuildKar` in nexus-report-plugin.

## Installation
Copy the .kar file in `deploy/` folder of your Nexus server and restart the server.

## Permission
The users needs the **"nx-report-download"** permission to perform this action.
You can create a new role with it or add it to an existing one.
Of course, an administrator has this permission by default.

## Usage
### Excel
If one of yours roles has the permission "nx-report-download", you should see a **"Report"** button (1) on the left side menu.
When you click on it a list of your granted repositories will be displayed. You have the possibility to sort it (2) or filter it (3) with the field at the top-right.
When you click on a repository of the list, it will download the report associated to this repository.

### JSON
Since 0.1.2, it is possible to get the informations in JSON format contacting the api `/service/rest/v1/report/json/`.
This api is available in System API on the UI, but you cannot get it directly with the "Report" button.
the right "nx-report-download" and an access to the repository are needed to get the JSON report.

## Examples
### Excel

<img src="https://zupimages.net/up/20/36/egx2.png" width="900"/>

### JSON

**Curl**

`curl -X GET "http://localhost:8081/service/rest/v1/report/json/maven-releases" -H  "accept: application/json"`

**Response code**

`200`

**Response headers**

```
 content-length: 735  content-type: application/json  date: Wed, 30 Sep 2020 23:21:09 GMT  server: Nexus/3.24.0-02 (OSS)  x-content-type-options: nosniff 
```

**Response body**

```
[
  {
    "group": "org.sonatype.nexus.plugins",
    "name": "nexus-report-plugin",
    "version": "0.1.2",
    "format": "maven2",
    "size": 3686343,
    "sizeMB": 3.52,
    "sizeGB": 0,
    "createdBy": "admin",
    "lastUpdated": "2020-10-01T01:17:52",
    "lastDownloaded": "never",
    "encoded": "bWF2ZW4tcmVsZWFzZXM6ODg0OTFjZDFkMTg1ZGQxMzYzMjY4ZjIyMGU0NWQ3ZGU"
  },
  {
    "group": "org.sonatype.nexus",
    "name": "nexus-ui-plugin",
    "version": "3.24.0-02",
    "format": "maven2",
    "size": 5494,
    "sizeMB": 0.01,
    "sizeGB": 0,
    "createdBy": "admin",
    "lastUpdated": "2020-10-01T01:20:41",
    "lastDownloaded": "never",
    "encoded": "bWF2ZW4tcmVsZWFzZXM6YzBhYzJhYjZjNWU5M2E0YTc2Zjc5OTEwMjllMDk0Yzg"
  }
]
```

**System/API**

<img src="https://zupimages.net/up/20/40/8n3y.png" width="900"/>

