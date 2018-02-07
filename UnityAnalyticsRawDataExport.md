#Unity Analytics Raw Data Export

##Overview

Unity Analytics Raw Data Export gives you full access to raw event data. This lets you use the data in whatever way you choose, for example to construct custom queries or data visualizations. 

There are two ways you can access raw data export:

* The Unity Analytics dashboard user interface
* By calling the REST API

Raw Data Export provides data from June 2016 onwards. 

##Analytics dashboard user interface
The Unity Analytics dashboard provides a way to export and access your raw event data without writing any code. In your Unity Analytics dashboard ([analytics.cloud.unity3d.com](https://analytics.cloud.unity3d.com/)), select your project and navigate to __Analytics__ >  __Raw Data Export__.


![The __Raw Data Export__ screen](../uploads/Main/UnityAnalyticsRawDataExport_AccessingRawDataExport.png)


Then follow these steps in the __Export__ section of that screen:
in
1. Specify the __Data Set__ you want to export (such as appRunning, appStart, custom, deviceInfo, transaction or userInfo).
2. Specify the __Start Date__, or alternatively continue exporting data from a previous job by selecting the __Previous Job Id__ from the drop-down box.
3. Specify the __End Date__.
4. The file format defaults to JSON. Specify your preferred file format by clicking on and selecting an item from the drop-down menu under __Export as JSON__. 

![The __Export__ section and __Activity__ table on the __Raw Data Export__ screen](../uploads/Main/UnityAnalyticsRawDataExport_ExportAndActivity.png)



Raw Data Export automatically creates the job and displays it in the __Activity__ table on the screen.

Once the job is done, you can download your data by selecting the files from the __Download__ column.


##REST (Representational State Transfer) API

Every data point sent to Unity Analytics is stored in Unity's data store. The Raw Data Export APIs allow you to download your raw event data in files as the data is received and stored. 

###Requirements
Every request requires HTTP Basic authentication using your Unity Project ID (UPID) and API Key.

![](../uploads/Main/AnalyticsAuthentication.png)

###Limitations

* The request period (`startDate` to `endDate`) is limited to 31 days.
* Limits to usage may be subject to change.
* Unity Analytics retains the raw data files generated for a request for 14 days. (To access the data after 14 days has elapsed, make a new request.) 

###User workflow

To export raw data, call the Create Raw Data Export API. This request triggers an asynchronous job to process the data. The time this takes depends on how much data is being exported.

To get the current status or result, poll using the Get Raw Data Export API. Once the export is completed, you can get the result in the response of this API. The result contains the list of files and the corresponding download URLs. You can loop through the URLs and download the exported data.

**Notes:**

* All dates and times in requests or responses are in the UTC timezone.
* API requests or responses use the JSON format (which is formatted for readability in this document). The data file format is configurable. 
* Data is exported in .gzip compressed files.
* The URL base for the API is [https://analytics.cloud.unity3d.com](https://analytics.cloud.unity3d.com).

###Create Raw Data Export

A Raw Data Export is specific to a project and specific to a single dataset (event type). The request period is limited to 31 days.

Use the following HTTP method to create a Raw Data Export:

````
POST api/v2/projects/{UNITY_PROJECT_ID}/rawdataexports
````

Arguments are provided in the payload of the request, and are in JSON format with the Content-Type application/json.

|**Request argument** |**Required or optional** |**Type** |**Description** |
|:---|:---|:---|:---|
|__startDate__ |Required unless continueFrom is specified |string |The start date (inclusive) of the export. The date is expressed in YYYY-MM-DD format (ISO-8601). |
|__endDate__ |Required |String |The end data (exclusive) of the export. The date is expressed in YYYY-MM-DD format (ISO 8601). This is the date at which to close the query. When searching for the current day, use the following day’s date. |
|__format__ |Required |String |The output data format: json (newline-delimited json) or tsv. |
|__dataset__ |Required |String |One of the following event types: appStart, appRunning, deviceInfo, custom, transaction, or userInfo. |
|__continueFrom__ |Optional |String |The Raw Data Export ID to continue exporting data from. This is used for continuing a previous export from the point it finished. See Continuing for more information. Instead of specifying a startDate, a prior Raw Data Export ID could be specified in continueFrom. It is an error to specify both continueFrom and startDate. |

Template for a request using cURL on the command line:

````
curl --user {UNITY_PROJECT_ID}:{API_KEY} --request POST --header "Content-Type: application/json" --data {REQUEST_JSON}
https://analytics.cloud.unity3d.com/api/v2/projects/{UNITY_PROJECT_ID}/rawdataexports
````

Example values:

````
UNITY_PROJECT_ID = aa43ae0a-a7a7-4016-ae96-e253bb126aa8
API_KEY = 166291ff148b2878375a8e54aebb1549
REQUEST_JSON = { "startDate": "2016-05-15" , "endDate": "2016-05-16", "format": "tsv", "dataset": "appStart" }
````

An actual request using the example values:

````
curl --user aa43ae0a-a7a7-4016-ae96-e253bb126aa8:166291ff148b2878375a8e54aebb1549 --request POST --header "Content-Type: application/json" --data '{ "startDate": "2016-05-15" , "endDate": "2016-05-16", "format": "tsv", "dataset": "appStart" }' https://analytics.cloud.unity3d.com/api/v2/projects/aa43ae0a-a7a7-4016-ae96-e253bb126aa8/rawdataexports
````

The response uses the common Raw Data Export Response Attributes in JSON format.

####Raw Data Export Response Attributes

|**Response attribute** |**Type** |**Description** |
|:---|:---|:---|
|__id__ |String |The Raw Data Export ID. |
|__upid__ |String |The Unity Project ID. |
|__createdAt__ |String |The created time in ISO 8601 format. |
|__status__ |string |The current status of the export. Possible values are: running, completed, or failed. |
|__duration__ |Long |The time it took to export data (in milliseconds). |
|__request__ |Json |The request arguments. |
|__result__ |Json |The result contains attributes that detail the exported data. The result is only available after the export is successfully completed. See below for result attributes. |
|__result.size__ |Long |The total size of the data exported (in bytes). |
|__result.eventCount__ |Long |The total number of events exported. |
|__result.intraDay__ |Boolean |When the request includes the current day it might not contain all the data for the day. This attribute is TRUE if the data is incomplete for the last day.  |
|__result.fileList__ |Json |The list of files containing the data exported. The file list is empty when there is no data. |
|__result.fileList.name__ |String |The file name. |
|__result.fileList.url__ |String |The download URL for the file. The files are compressed in gzip format. |
|__result.fileList.size__ |Long |The size of the file in bytes. |
|__result.fileList.date__ |String |The file contains events for this specific date. This date is based on the submit time of the event. There may be multiple files for the same date. The date in is in ISO 8601 format. |


An example of response:

````
{  
   "id":"8228d1e9-31b3-4a5e-aabe-55d9c8afa052",
   "upid":"beff3f49-b9ed-41a4-91ea-677e9b85e71e",
   "createdAt":"2016-05-10T10:10:10.100+0000",
   "status":"running",
   "duration" : 0,
   "request":{  
      "startDate":"2016-05-01",
      "endDate":"2016-05-02",
      "format":"json",
      "dataset":"appRunning"
   }
}
````

####Continue creating from a prior Raw Data Export

When you are running periodic Raw Data Exports, you must provide the continueFrom argument instead of the startDate to make sure you are continuing from the previous Raw Data Export. Prior Raw Data Export IDs can be fetched via the GET APIs or accessed via the Dashboard.

![Prior Raw Data Exports in the Unity Analytics Project Dashboard](../uploads/Main/AnalyticsPriorRawData.png)

###Get Raw Data Export

Use the following HTTP method to get a specific Raw Data Export or ongoing export status:

````
GET api/v2/projects/{UNITY_PROJECT_ID}/rawdataexports/{raw_data_export_id} 
````
All required arguments are part of the URL path.

An example of a request:

````
curl --user {UNITY_PROJECT_ID}:${API_KEY} https://analytics.cloud.unity3d.com/api/v2/projects/{UNITY_PROJECT_ID}/rawdataexports/${ID}
````

The response is the Raw Data Export in JSON format. It is the same as the response in Create Raw Data Export.

An example of a response:

````
{  
   "id":"6601f70e-6a0b-48ed-909f-26711af82b49",
   "status":"completed",
   "createdAt":"2016-05-21T04:41:54.000+0000",
   "duration":8631714000,
   "request":{  
      "startDate":"2016-02-11T00:00:00.000+0000",
      "endDate":"2016-03-11T00:00:00.000+0000",
      "format":"tsv",
      "dataset":"custom"
   },
   "result":{  
      "size":78355,
      "eventCount":17473,
      "fileList":[  
         {  
            "name":"headers.gz",
            "url":"https://uca-export.s3.amazonaws.com/staging/devTest/custom/appid%3DUNITY_PROJECT_ID/jid%3D6601f70e-6a0b-48ed-909f-26711af82b49/headers.gz?AWSAccessKeyId=AKIAJUXGNF66F4XPWSWA&Expires=1463872651&Signature=PnzIeeI%2FNxSOlKkLVpLcfK%2FxVpU%3D",
            "size":105
         },
         {  
            "name":"part-4b0cf376-3478-4bc8-845e-f73aff5c0be4.gz",
            "url":"https://uca-export.s3.amazonaws.com/staging/devTest/custom/appid%3DUNITY_PROJECT_ID/jid%3D6601f70e-6a0b-48ed-909f-26711af82b49/part-4b0cf376-3478-4bc8-845e-f73aff5c0be4.gz?AWSAccessKeyId=AKIAJUXGNF66F4XPWSWA&Expires=1463872651&Signature=xZk3%2BzQNTQ6yjK2Mh%2FaH338ABn8%3D",
            "size":78250,
            "date":"2016-02-13T00:00:00.000+0000"
         }
      ],
      "intraDay":false
   }
}
````
###List all Raw Data Exports

Use this HTTP method to get the list of all Raw Data Exports for a specific project:

````
GET api/v2/projects/{UNITY_PROJECT_ID}/rawdataexports
````

All required arguments are part of the URL path.

An example of a request:

````
curl --user {UNITY_PROJECT_ID}:${API_KEY} https://analytics.cloud.unity3d.com/api/v2/projects/${UNITY_PROJECT_ID}/rawdataexports/
````

The response is a list of Raw Data Exports in JSON format. See Raw Data Export Response Attributes for the definition of each export list element.

An example of a response:

````
[
{  
   "id":"6601f70e-6a0b-48ed-909f-26711af82b49",
   "status":"completed",
   "createdAt":"2016-05-21T04:41:54.000+0000",
   "duration":8631714000,
   "request":{  
      "startDate":"2016-02-11T00:00:00.000+0000",
      "endDate":"2016-03-11T00:00:00.000+0000",
      "format":"tsv",
      "dataset":"custom"
   },
   "result":{  
      "size":78355,
      "eventCount":17473,
      "fileList":[  
         {  
            "name":"headers.gz",
            "url":"https://uca-export.s3.amazonaws.com/staging/devTest/custom/appid%3DUNITY_PROJECT_ID/jid%3D6601f70e-6a0b-48ed-909f-26711af82b49/headers.gz?AWSAccessKeyId=AKIAJUXGNF66F4XPWSWA&Expires=1463872651&Signature=PnzIeeI%2FNxSOlKkLVpLcfK%2FxVpU%3D",
            "size":105
         },
         {  
            "name":"part-4b0cf376-3478-4bc8-845e-f73aff5c0be4.gz",
            "url":"https://uca-export.s3.amazonaws.com/staging/devTest/custom/appid%3DUNITY_PROJECT_ID/jid%3D6601f70e-6a0b-48ed-909f-26711af82b49/part-4b0cf376-3478-4bc8-845e-f73aff5c0be4.gz?AWSAccessKeyId=AKIAJUXGNF66F4XPWSWA&Expires=1463872651&Signature=xZk3%2BzQNTQ6yjK2Mh%2FaH338ABn8%3D",
            "size":78250,
            "date":"2016-02-13T00:00:00.000+0000"
         }
      ],
      "intraDay":false
   }
},
{  
   "id":"6601f70e-6a0b-48ed-909f-26711af82b48",
   "status":"completed",
   "createdAt":"2016-05-21T04:41:54.000+0000",
   "duration":8631714000,
   "request":{  
      "startDate":"2016-02-11T00:00:00.000+0000",
      "endDate":"2016-03-11T00:00:00.000+0000",
      "format":"tsv",
      "dataset":"custom"
   },
   "result":{  
      "size":78355,
      "eventCount":17473,
      "fileList":[  
         {  
            "name":"headers.gz",
            "url":"https://uca-export.s3.amazonaws.com/staging/devTest/custom/appid%3DUNITY_PROJECT_ID/jid%3D6601f70e-6a0b-48ed-909f-26711af82b48/headers.gz?AWSAccessKeyId=AKIAJUXGNF66F4XPWSWA&Expires=1463872651&Signature=PnzIeeI%2FNxSOlKkLVpLcfK%2FxVpU%3D",
            "size":105
         },
         {  
            "name":"part-4b0cf376-3478-4bc8-845e-f73aff5c0be4.gz",
            "url":"https://uca-export.s3.amazonaws.com/staging/devTest/custom/appid%3DUNITY_PROJECT_ID/jid%3D6601f70e-6a0b-48ed-909f-26711af82b48/part-4b0cf376-3478-4bc8-845e-f73aff5c0be4.gz?AWSAccessKeyId=AKIAJUXGNF66F4XPWSWA&Expires=1463872651&Signature=xZk3%2BzQNTQ6yjK2Mh%2FaH338ABn8%3D",
            "size":78250,
            "date":"2016-02-13T00:00:00.000+0000"
         }
      ],
      "intraDay":false
   }
}
]
````

###TSV format

If you choose to export in TSV format, the headers are provided in a separate file in __headers.gz__. The data files do not include headers. 

An example headers file:

````
ts	appid	type	userid	sessionid	remote_ip	platform	sdk_ver	debug_device	user_agent	submit_time	name	custom_params
````

###Dataset

Each of the six data types (event types) differ. See below for their schema definitions. 

**Notes:**

* `ts` is the timestamp at which the event was generated on the device. Note that device-generated timestamps can be skewed due to the device clock and latency in receiving the event.
* `submit_time` is the timestamp at which the event was received by Unity Analytics.
* If a field in a record has no data, the value of that field is set to the default value for the data type of the field (`0` for numbers, `""` for strings, and `false` for bools). Nested fields, like the IAP `TransactionEvent.receipt` field, in JSON-format exports are an exception to this policy. In the JSON-format export of nested fields, any fields containing no data are not included in the JSON object for that record.

####AppStart event 

````
{
   "namespace":"com.unity.analytics.commons.schema",
   "name":"AppStartEvent",
   "type":"record",
   "fields":[
       {"name": "ts",   "type": "long", "default": 0}, 
       {"name": "appid", "type": "string", "default": ""},
       {"name": "type", "type": "string", "default": ""}, 
       {"name": "userid", "type": "string", "default": ""},
       {"name": "sessionid", "type": "string", "default": ""},
       {"name": "remote_ip", "type": "string", "default": ""},
       {"name": "platform", "type": "string", "default": ""},
       {"name": "sdk_ver", "type": "string", "default": ""},
       {"name": "debug_device", "type": "boolean", "default": false},
       {"name": "user_agent", "type": "string", "default": ""},
       {"name": "submit_time", "type": "long", "default": 0} 
   ]
}  
````

####AppRunning event

````
{
   "namespace":"com.unity.analytics.commons.schema",
   "name":"AppRunningEvent",
   "type":"record",
   "fields":[
       {"name": "ts",   "type": "long", "default": 0}, 
       {"name": "appid", "type": "string", "default": ""},
       {"name": "type", "type": "string", "default": ""},
       {"name": "userid", "type": "string", "default": ""},
       {"name": "sessionid", "type": "string", "default": ""},
       {"name": "remote_ip", "type": "string", "default": ""},
       {"name": "platform", "type": "string", "default": ""},
       {"name": "sdk_ver", "type": "string", "default": ""},
       {"name": "debug_device", "type": "boolean", "default": false},
       {"name": "user_agent", "type": "string", "default": ""},
       {"name": "submit_time", "type": "long", "default": 0}, 
       {"name": "duration", "type": "int", "default": 0}
   ]
}
````

####Custom event

````
{
   "namespace":"com.unity.analytics.commons.schema",
   "name":"CustomEvent",
   "type":"record",
   "fields":[
       {"name": "ts",   "type": "long", "default": 0}, 
       {"name": "appid", "type": "string", "default": ""},
       {"name": "type", "type": "string", "default": ""},
       {"name": "userid", "type": "string", "default": ""},
       {"name": "sessionid", "type": "string", "default": ""},
       {"name": "remote_ip", "type": "string", "default": ""},
       {"name": "platform", "type": "string", "default": ""},
       {"name": "sdk_ver", "type": "string", "default": ""},
       {"name": "debug_device", "type": "boolean", "default": false},
       {"name": "user_agent", "type": "string", "default": ""},
       {"name": "submit_time", "type": "long", "default": 0}, 
       {"name": "name", "type": "string", "default": ""},
       {
           "name":"custom_params",
           "type":["null",{
               "type":"map",
               "values": ["string","null"],
               "default": ""
           }],
           "default": null
       }
   ]
}
````

####DeviceInfo event

````
{
   "namespace":"com.unity.analytics.commons.schema",
   "name":"DeviceInfoEvent",
   "type":"record",
   "fields":[
       {"name": "ts",   "type": "long", "default": 0}, 
       {"name": "appid", "type": "string", "default": ""},
       {"name": "type", "type": "string", "default": ""}, 
       {"name": "userid", "type": "string", "default": ""},
       {"name": "sessionid", "type": "string", "default": ""},
       {"name": "remote_ip", "type": "string", "default": ""},
       {"name": "platform", "type": "string", "default": ""},
       {"name": "sdk_ver", "type": "string", "default": ""},
       {"name": "debug_device", "type": "boolean", "default": false},
       {"name": "user_agent", "type": "string", "default": ""},
       {"name": "submit_time", "type": "long", "default": 0}, 
       {"name": "debug_build", "type": "boolean", "default": false},
       {"name": "rooted_jailbroken", "type": "boolean", "default": false},
       {"name": "processor_type", "type": "string", "default": ""},
       {"name": "system_memory_size", "type": "string", "default": ""},
       {"name": "make", "type": "string", "default": ""},
       {"name": "app_ver", "type": "string", "default": ""},
       {"name": "deviceid", "type": "string", "default": ""},
       {"name": "license_type", "type": "string", "default": ""},
       {"name": "app_install_mode", "type": "string", "default": ""},
       {"name": "model", "type": "string", "default": ""},
       {"name": "engine_ver", "type": "string", "default": ""},
       {"name": "os_ver", "type": "string", "default": ""},
       {"name": "app_name", "type": "string", "default": ""},
       {"name": "timezone", "type": "string", "default": ""},
       {"name": "ads_tracking", "type": "boolean", "default": false},
       {"name": "adsid", "type": "string", "default": ""}
   ]
}  
````

####Transaction event

````
{
   "namespace":"com.unity.analytics.commons.schema",
   "name":"TransactionEvent",
   "type":"record",
   "fields":[
       {"name": "ts",   "type": "long", "default": 0},
       {"name": "appid", "type": "string", "default": ""},
       {"name": "type", "type": "string", "default": ""},
       {"name": "userid", "type": "string", "default": ""},
       {"name": "sessionid", "type": "string", "default": ""},
       {"name": "remote_ip", "type": "string", "default": ""},
       {"name": "platform", "type": "string", "default": ""},
       {"name": "sdk_ver", "type": "string", "default": ""},
       {"name": "debug_device", "type": "boolean", "default": false},
       {"name": "user_agent", "type": "string", "default": ""},
       {"name": "submit_time", "type": "long", "default": 0},        {
           "name":"receipt",
           "type":["null",{
               "type":"record",
               "name": "receiptRecord",
               "fields":[
                   {"name": "data", "type": "string", "default": ""},
                   {"name": "signature", "type": "string", "default": ""}
               ]
           }],
           "default": null
       },
       {"name": "currency", "type": "string", "default": "USD"},
       {"name": "amount", "type": "float", "default": 0},
       {"name": "transactionid", "type": "long", "default": 0},
       {"name": "productid", "type": "string", "default": ""}
   ]
}
````

####UserInfo event

````
{
   "namespace":"com.unity.analytics.commons.schema",
   "name":"UserInfoEvent",
   "type":"record",
   "fields":[
       {"name": "ts",   "type": "long", "default": 0},
       {"name": "appid", "type": "string", "default": ""},
       {"name": "type", "type": "string", "default": ""},
       {"name": "userid", "type": "string", "default": ""},
       {"name": "sessionid", "type": "string", "default": ""},
       {"name": "remote_ip", "type": "string", "default": ""},
       {"name": "platform", "type": "string", "default": ""},
       {"name": "sdk_ver", "type": "string", "default": ""},
       {"name": "debug_device", "type": "boolean", "default": false},
       {"name": "user_agent", "type": "string", "default": ""},
       {"name": "submit_time", "type": "long", "default": 0},
       {"name": "sex", "type": "string", "default": ""},
       {"name": "custom_userid", "type": "string", "default": ""},
       {"name": "birth_year", "type": "int", "default": 0}
   ]
}   

````

# Dictionary

| Data field| Definition | Dataset |
|:---|:---|:---| 
| ts| The timestamp (in milliseconds) at which the event was generated on the device. Note that device-generated timestamps can be skewed due to the device clock and latency in receiving the event | All datasets |
| appid| The ID that is assigned to each app on the Unity Analytics Dashboard | All datasets |
| type| The type of event being queried (i.e. Custom, DeviceInfo, Transaction, etc) | All datasets |
| userid| Unity Analytics generated identifier for a userid | All datasets |
| sessionid| Unity Analytics generated identifier for the session. If a game is reopened after more than 30 minutes of inactivity, a new session ID is generated | All datasets |
| remote_ip| The IP address that the session was played from | All datasets |
| platform| The platform that the session was played on | All datasets |
| sdk_ver| Version of Unity Analytics SDK that is being used for this event. If the sdk_ver begins with a "u" then it is from the Analytics tool built engine. Otherwise, it is from the Analytics plugin for Unity versions older than 5.2  | All datasets |
| debug_device| A boolean that shows whether the event was sent from a development build. Set to TRUE for events coming from Unity Editor | All datasets |
| user_agent| The User-Agent request-header field | All datasets |
| submit_time| The timestamp (in milliseconds) at which the event was received by Unity Analytics | All datasets |
| duration| The duration (number of seconds) that this session has been running for, calculated by the SDK | AppRunning |
| name| The name of the Custom Event (e.g. “LevelComplete”) | Custom |
| custom_params| The list of Custom Event parameters and their corresponding values.  | Custom |
| sex| The sex of the user | UserInfo |
| custom_userid| Set when app explicitly provides userid via SetUserId (string userId) | UserInfo |
| birth_year| The birth year of the user | UserInfo |
| receipt| Includes data returned by platform app stores, such as App Store and Google Play | Transaction |
| currency| The currency code for the payment (eg. USD, EUR, CAD, etc) in ISO 4217 code | Transaction |
| amount| The total decimal amount of currency spent | Transaction |
| transactionid| Unique identifier for this transaction, set by SDK. Each transaction is given a unique ID, not to be confused with the store’s transaction ID | Transaction |
| productid| The store-specific product identifier of an in-app purchase (eg. com.mygame.100coins) | Transaction |
| debug_build| A boolean that shows whether the event was sent from a development build. Set to TRUE for events coming from Unity Editor | DeviceInfo |
| rooted_jailbroken| A boolean that is set to TRUE in case of rooted / jailbroken phone not sent for normal phone | DeviceInfo |
| processor_type| Device processor type | DeviceInfo |
| system_memory_size| Device system memory | DeviceInfo |
| make| Maker of the device (eg. "OSXEditor") | DeviceInfo |
| app_ver| Version of the application (eg. "1.0") | DeviceInfo |
| deviceid| A unique device identifier | DeviceInfo |
| license_type| Type of license (eg. “advanced_pro”) | DeviceInfo |
| app_install_mode| Tells if app is installed via app store ("store"), adhoc ("adhoc"), developer install ("dev_release"), simulator ("simulator") or enterprise ("enterprise") | DeviceInfo |
| model| Device model (eg. "MacBookPro11,3") | DeviceInfo |
| engine_ver| Unity engine version (eg. "5.5.0a3") | DeviceInfo |
| os_ver| OS Version (eg. "Mac OS X 10.11.5") | DeviceInfo |
| app_name| Bundle identifier or package name (eg. "com.Company.ProductName") | DeviceInfo |
| timezone|  ISO code (eg. “GMT-7”) | DeviceInfo |
| ads_tracking| A boolean value that indicates whether the user has limited ad tracking | DeviceInfo |
| adsid| Advertising Id. On iOS, collected when Unity Ads is enabled. On Android, all the time | DeviceInfo |

---

* <span class="page-edit">2017-08-01  <!-- include IncludeTextAmendPageYesEdit --></span>

* <span class="page-history">2017-06-21 - Inclusion of empty nested fields in JSON exports changed in Unity [2017.1](https://docs.unity3d.com/2017.1/Documentation/Manual/30_search.html?q=newin20171) <span class="search-words">NewIn20171</span></span>
