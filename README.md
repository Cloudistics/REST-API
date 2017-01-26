# Cloudistics Web Services (CWS)

Cloudistics web services provides API access to the Cloudistics on-premises cloud platform. It provides access to virtual datacenter and infrastructure resources and is used to create resizable resources, manage workloads and retrieve information about the underlying infrastructure. CWS will continue to grow as new capabilities are added to the platform.

### Base URL

The CWS REST API access is over HTTPS to ensure privacy:

```
https://manage.cloudistics.com/api/latest/
```

### Authentication

CWS requires a security token to use the API. 

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/applications
```

Tokens can be found in your account under Settings > Developer Options.

### Filtering

CWS allows filtering of the responses through optional request parameters. Please see the "URL Params" section within the definition of the REST API endpoint to see if filtering is available for it.

| Parameter | Description | 
| ---|---|
| start&#8209;index | Returns results starting at the specified index in the result set.<br>The starting index in a result set is always 0.<br>Default: 0<br>Example: If there are 2 applications in an organization and you request to List all Applications with a starting index of 1 only the second application will be returned in the response. |
| limit&#8209;count | Limit the number of results returned in the response from the REST API request.<br>Default: 1000<br>Example: If there are 2 applications in an organization and you request to List all Applications with a limit count of 1 only the first application will be returned in the response. |
| start&#8209;timestamp | Only returns results from the request where the result has a property timestamp greater than or equal to the start timestamp provided.<br>Example: If you request to Get Events with a start timestamp of '2017-01-10'T'12:00:00' the response will only contain events that have been created after January 10, 2017 at 12:00 PM. |
| end&#8209;timestamp | Only returns results from the REST API request where the result has a property timestamp less than or equal to the end timestamp provided.<br>Example: If you request to Get Events with a end timestamp of '2017-01-12'T'12:00:00' the response will only contain events that have been created before January 12, 2017 at 12:00 PM. |
| datacenters | This is a comma-delimited list of datacenter UUIDs to filter the results by. Only returns results from the REST API request where the result is in a datacenter specified. |

## Cloudistics Virtual Data Centers (VDC) API Reference 

The Cloudistics Virtual Data Center (VDC) API Reference provides descriptions, syntax, and usage examples for each of the actions and data types for Cloudistics VDCs.
The topic for each action shows the Query API request parameters and the JSON response.

### Calls

* [List all Applications](#list-all-applications)
* [Get Application Information](#get-application-information)
* [Get Application Statistics](#get-application-statistics)
* [Get Application Disk Statistics](#get-application-disk-statistics)
* [Get Firewall Profiles for Application](#get-firewall-profiles-for-application)
* [Edit Application](#edit-application)
* [Create Application from Template](#create-application-from-template)
* [Start Application](#start-application)
* [Stop Application](#stop-application)
* [Restart Application](#restart-application)
* [Suspend Application](#suspend-application)
* [Resume Application](#resume-application)
* [Delete Application](#delete-application)
* [Shutdown Application](#shutdown-application)
* [Get Snapshots for Application](#get-snapshots-for-application)
* [Get Snapshot Information](#get-snapshot-information)
* [Create Snapshot for Application](#create-snapshot-for-application)
* [Delete Snapshot for Application](#delete-snapshot-for-application)
* [List all Tags](#list-all-tags)
* [Get Tag Information](#get-tag-information)
* [List all Categories](#list-all-categories)
* [Get Category Information](#get-category-information)
* [List all Virtual Datacenters](#list-all-virtual-datacenters)
* [Get Virtual Datacenter Information](#get-virtual-datacenter-information)
* [List all Migration Zones](#list-all-migration-zones)
* [Get Migration Zone Information](#get-migration-zone-information)
* [List all Vnets](#list-all-vnets)
* [Get Vnet Information](#get-vnet-information)
* [Get Firewall Profiles for Vnet](#get-firewall-profiles-for-vnet)
* [List all Flash Pools](#list-all-flash-pools)
* [Get Flash Pool Information](#get-flash-pool-information)
* [List all Templates](#list-all-templates)
* [Get Template Information](#get-template-information)
* [Get Action Information](#get-action-information)
* [Get Events](#get-events)

### List all Applications
Returns json data about applications within an organization.

* **URL**

  `/api/latest/applications`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

   `datacenters=[comma-delimited list of datacenter UUIDs]`

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "e696855c-186f-4c2a-a381-1637195bef3f",
    "name": "CentOS 7.5 Application",
    "description": "This application was created from a CentOS template.",
    "vcpus": 4,
    "memory": 1073741824,
    "categoryUuid": "a55bb4da-7cad-40cb-95e0-37db93c7aa5e",
    "tags": [
      {
        "uuid": "fa527c37-3582-41e5-afcb-4b181b8e39aa"
      }
    ],
    "datacenterUuid": "101552a2-e436-415a-a1cd-a11e5cb1e06e",
    "migrationZoneUuid": "6c47337b-9ee0-434d-90a6-2743b1bcdf9a",
    "flashPoolUuid": "0b9512cd-7e40-4fd8-a2c2-74189d6b57a3",
    "status": "Running",
    "networkServiceAppVnetUuid": "1d11b1cf-c2c6-4848-93cf-28b9e16f896d",
    "disks": [
      {
        "uuid": "ac8e01aa-a667-46cf-8a7a-7082c5c9a6f3",
        "name": "Disk 0",
        "size": 1073741824,
        "isBoot": true
      }
    ],
    "vnics": [
      {
        "uuid": "3fdb865d-edc3-48c5-acc0-656f82c097e0",
        "type": "Virtual Networking",
        "networks": [
          {
            "vnetUuid": "ff724194-931c-4c02-928e-e37821e74a8a",
            "firewallProfileUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd",
            "ipAddress": "127.0.0.1",
            "macAddress": "08:62:66:2b:88:b3"
          }
        ]
      }
    ],
    "autoSnapshotPolicy": {
      "localRetentionCount": 20,
      "intervalInMinutes": 60
    },
    "disasterRecoveryPolicy": {
      "isEnabled": true,
      "destinationFlashPoolUuid": "71d97374-20e5-42bc-af61-8c916dd515a7",
      "retentionCount": {
        "all": 20,
        "daily": 365,
        "weekly": 104,
        "monthly": 60,
        "yearly": 10
      }
    }
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/applications \
     -d 'limit-count=10'
```

* **Notes:**

  None


### Get Application Information
  Returns json data about an application.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]`

* **Method:**

  `GET`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "uuid": "e696855c-186f-4c2a-a381-1637195bef3f",
  "name": "CentOS 7.5 Application",
  "description": "This application was created from a CentOS template.",
  "vcpus": 4,
  "memory": 1073741824,
  "categoryUuid": "a55bb4da-7cad-40cb-95e0-37db93c7aa5e",
  "tags": [
    {
      "uuid": "fa527c37-3582-41e5-afcb-4b181b8e39aa"
    }
  ],
  "datacenterUuid": "101552a2-e436-415a-a1cd-a11e5cb1e06e",
  "migrationZoneUuid": "6c47337b-9ee0-434d-90a6-2743b1bcdf9a",
  "flashPoolUuid": "0b9512cd-7e40-4fd8-a2c2-74189d6b57a3",
  "status": "Running",
  "networkServiceAppVnetUuid": "1d11b1cf-c2c6-4848-93cf-28b9e16f896d",
  "disks": [
    {
      "uuid": "ac8e01aa-a667-46cf-8a7a-7082c5c9a6f3",
      "name": "Disk 0",
      "size": 1073741824,
      "isBoot": true
    }
  ],
  "vnics": [
    {
      "uuid": "3fdb865d-edc3-48c5-acc0-656f82c097e0",
      "type": "Virtual Networking",
      "networks": [
        {
          "vnetUuid": "ff724194-931c-4c02-928e-e37821e74a8a",
          "firewallProfileUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd",
          "ipAddress": "127.0.0.1",
          "macAddress": "08:62:66:2b:88:b3"
        }
      ]
    }
  ],
  "autoSnapshotPolicy": {
    "localRetentionCount": 20,
    "intervalInMinutes": 60
  },
  "disasterRecoveryPolicy": {
    "isEnabled": true,
    "destinationFlashPoolUuid": "71d97374-20e5-42bc-af61-8c916dd515a7",
    "retentionCount": {
      "all": 20,
      "daily": 365,
      "weekly": 104,
      "monthly": 60,
      "yearly": 10
    }
  }
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]
```

* **Notes:**

  None


### Get Application Statistics
  Returns json data about the statistics for an application.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/stats`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-timestamp=[date with pattern "yyyy-MM-dd'T'HH:mm:ss"]`

   `end-timestamp=[date with pattern "yyyy-MM-dd'T'HH:mm:ss"]`

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "timestamp": "2017-01-11'T'12:00:00",
    "cpuUtilization": 50,
    "memoryUtilization": 1073741824,
    "networkBandwidthReadsBytesPerSec": 0,
    "networkBandwidthWritesBytesPerSec": 0,
    "allDisksStorageUtilization": 1073741824,
    "allDisksStorageInstance": 1073741824,
    "allDisksIoQueueDepth": 100,
    "allDisksIopsRead": 200,
    "allDisksIopsWrite": 300,
    "allDisksStorageBandwidthReadsBytesPerSec": 0,
    "allDisksStorageBandwidthWritesBytesPerSec": 0
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/stats \
     -d 'start-timestamp=2017-01-11T12:00:00'
```

* **Notes:**

  None


### Get Application Disk Statistics
  Returns json data about the statistics for an application disk.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/disks/[DISK UUID]`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-timestamp=[date with pattern "yyyy-MM-dd'T'HH:mm:ss"]`

   `end-timestamp=[date with pattern "yyyy-MM-dd'T'HH:mm:ss"]`

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "timestamp": "2017-01-11'T'12:00:00",
    "storageUtilizationBytes": 1073741824,
    "storageInstanceBytes": 1073741824,
    "ioQueueDepth": 100,
    "iopsRead": 200,
    "iopsWrite": 300,
    "storageBandwidthReadBytesPerSec": 0,
    "storageBandwidthWriteBytesPerSec": 0,
    "storageLatencyMicroseconds": 0
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Disk with uuid ac8e01aa-a667-46cf-8a7a-7082c5c9a6f3 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/disks/[DISK UUID] \
     -d 'end-timestamp=2017-01-11T12:00:00'
```

* **Notes:**

  None


### Get Firewall Profiles for Application
  Returns json data about firewall profiles for an application.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/firewall-profiles`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "bd4341d9-89f2-481a-9b4a-03548aadaec1",
    "name": "Application Firewall Profile",
    "rules": [
      {
        "order": 0,
        "type": "Outgoing",
        "protocol": "UDP",
        "sourceRangeIps": [],
        "sourceRangePorts": [],
        "destinationRangeIps": [],
        "destinationRangePorts": [
          67,
          68
        ],
        "action": "Allow",
        "description": "Allow traffic from the application instances to the network service instance."
      }
    ]
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/firewall-profiles \
     -d 'limit-count=10'
```

* **Notes:**

  None


### Edit Application
  Updates properties for an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "name": "CentOS 7.5 Application",
  "description": "This application was created from a CentOS template.",
  "vcpus": 4,
  "memory": 1073741824,
  "categoryUuid": "a55bb4da-7cad-40cb-95e0-37db93c7aa5e",
  "addTags": [
    {
      "uuid": "3402698b-d436-4b70-8fe7-d44fae37c68a"
    }
  ],
  "removeTags": [
    {
      "uuid": "fa527c37-3582-41e5-afcb-4b181b8e39aa"
    }
  ],
  "datacenterUuid": "101552a2-e436-415a-a1cd-a11e5cb1e06e",
  "migrationZoneUuid": "6c47337b-9ee0-434d-90a6-2743b1bcdf9a",
  "addDisks": [
    {
      "name": "Disk 3",
      "size": 1073741824
    },
    {
      "name": "Disk 4",
      "size": 1073741824
    }
  ],
  "removeDisks": [
    {
      "uuid": "ac8e01aa-a667-46cf-8a7a-7082c5c9a6f3"
    }
  ],
  "networks": [
    {
      "type": "Virtual Networking",
      "vnetUuid": "ff724194-931c-4c02-928e-e37821e74a8a",
      "firewallProfileUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd"
    }
  ]
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:** `Application successfully updated.`

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Error editing application instance. You cannot modify the datacenter if the application is running.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID] \
     -d '{"name": "CentOS 7.5 Application", "description": "This application was created from a CentOS template.", "vcpus": 4, "memory": 1073741824, "categoryUuid": "a55bb4da-7cad-40cb-95e0-37db93c7aa5e", "addTags": [{"uuid": "3402698b-d436-4b70-8fe7-d44fae37c68a"}], "removeTags": [{ "uuid": "fa527c37-3582-41e5-afcb-4b181b8e39aa"}], "datacenterUuid": "101552a2-e436-415a-a1cd-a11e5cb1e06e", "migrationZoneUuid": "6c47337b-9ee0-434d-90a6-2743b1bcdf9a", "addDisks": [{"name": "Disk 3", "size": 1073741824}, {"name": "Disk 4", "size": 1073741824}], "removeDisks": [{"uuid": "ac8e01aa-a667-46cf-8a7a-7082c5c9a6f3"}], "networks": [{"type": "Virtual Networking", "vnetUuid": "ff724194-931c-4c02-928e-e37821e74a8a", "firewallProfileUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd"}]}'
```

* **Notes:**

  * Optional fields in the request are "description", "addTags", "removeTags", "addDisks" and "removeDisks".
  * Networking "type" options are "Virtual Networking", "Node-Only" or "Bridged". If virtual networking is chosen, "vnetUuid" is required and "firewallProfileUuid" is optional.
  * The success response will return a status code of 200 if only the "name", "description", "datacenterUuid" and/or "migrationZoneUuid" were updated. If any of the other properties were updated the success response will be 202 Accepted.


### Create Application from Template
  Create an application from template and returns json data about the action.

* **URL**

  `/api/latest/applications/`

* **Method:**

  `POST`

*  **URL Params**

  None

* **Data Params**

```json
{
  "name": "CentOS 7.5 Application",
  "description": "This application was created from a CentOS template.",
  "vcpus": 4,
  "memory": 1073741824,
  "templateUuid": "3625edfa-1d41-488c-bbdc-13d35bdeb9ae",
  "categoryUuid": "a55bb4da-7cad-40cb-95e0-37db93c7aa5e",
  "tags": [
    {
      "uuid": "3402698b-d436-4b70-8fe7-d44fae37c68a"
    }
  ],
  "datacenterUuid": "101552a2-e436-415a-a1cd-a11e5cb1e06e",
  "migrationZoneUuid": "6c47337b-9ee0-434d-90a6-2743b1bcdf9a",
  "flashPoolUuid": "d80fe07d-5858-4de8-98ce-8a8b9b6684a4",
  "networks": [
    {
      "type": "Virtual Networking",
      "vnetUuid": "ff724194-931c-4c02-928e-e37821e74a8a",
      "firewallProfileUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd"
    }
  ]
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Template with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Error creating application instance from template. There does not exist a valid hypervisor that can fit this application instance.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/applications \
     -d '{"name": "CentOS 7.5 Application", "description": "This application was created from a CentOS template.", "vcpus": 4, "memory": 1073741824, "templateUuid": "3625edfa-1d41-488c-bbdc-13d35bdeb9ae", "categoryUuid": "a55bb4da-7cad-40cb-95e0-37db93c7aa5e", "tags": [{"uuid": "3402698b-d436-4b70-8fe7-d44fae37c68a"}], "datacenterUuid": "101552a2-e436-415a-a1cd-a11e5cb1e06e", "migrationZoneUuid": "6c47337b-9ee0-434d-90a6-2743b1bcdf9a", "flashPoolUuid": "d80fe07d-5858-4de8-98ce-8a8b9b6684a4", "networks": [{"type": "Virtual Networking", "vnetUuid": "ff724194-931c-4c02-928e-e37821e74a8a", "firewallProfileUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd"}]}'
```

* **Notes:**

  * Optional fields in the request are "description" and "tags".
  * Networking "type" options are "Virtual Networking", "Node-Only" or "Bridged". If virtual networking is chosen, "vnetUuid" is required and "firewallProfileUuid" is optional.


### Start Application
  Start an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/start`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to start application that is already running.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/start
```

* **Notes:**

  * Request will fail if the application has no migration zone or networking mode. Edit the application first, then issue a start application request again.


### Stop Application
  Stops an application forcefully and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/stop`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to stop application that is shut off.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/stop
```

* **Notes:**

  None


### Restart Application
  Restarts an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/restart`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to restart application that is not running.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/restart
```

* **Notes:**

  None


### Suspend Application
  Suspends an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/suspend`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to pause application that is not running.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/suspend
```

* **Notes:**

  None


### Resume Application
  Resumes an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/resume`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to resume application that is not paused.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/resume
```

* **Notes:**

  None


### Delete Application
  Deletes an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]`

* **Method:**

  `DELETE`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:** `Application successfully deleted.`

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to delete application that is a networking services application.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X DELETE https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]
```

* **Notes:**

  * When disaster recovery is enabled for the application, disaster recovery snapshots will always be retained.
  * The success response will return a status code of 200 if the application instance is not a networking services application and it had failed to create properly. Otherwise, the success response will be 202 Accepted.


### Shutdown Application
  Shutdown an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/shutdown`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to shutdown application that is running and unreachable.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOEKN]" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/shutdown
```

* **Notes:**

  None


### Get Snapshots for Application
  Returns json data about snapshots for an application.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/snapshots`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "b576c8de-c70f-46d9-9a27-667416b2f788",
    "name": "Snapshot One",
    "createdTimestamp": "2016-11-15'T'12:00:00",
    "size": 1073741824,
    "type": "Local",
    "generated": "Manual",
    "disasterRecovery": {
      "transferStatus": "Transferring",
      "transferPercentage": 50
    }
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/snapshots \
     -d 'limit-count=10'
```

* **Notes:**

  * When disaster recovery is enabled for the application, the "disasterRecovery" field will be populated.
  * For the "type" field the values are either "Local" or "Disaster Recovery".
  * For the "generated" field the values are either "Manual" or "Automatic".


### Get Snapshot Information
  Returns json data about a snapshot.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/snapshots/[SNAPSHOT UUID]`

* **Method:**

  `GET`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "uuid": "b576c8de-c70f-46d9-9a27-667416b2f788",
  "name": "Snapshot One",
  "createdTimestamp": "2016-11-15'T'12:00:00",
  "size": 1073741824,
  "type": "Local",
  "generated": "Manual",
  "disasterRecovery": {
    "transferStatus": "Transferring",
    "transferPercentage": 50
  }
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Snapshot with uuid b576c8de-c70f-46d9-9a27-667416b2f788 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/snapshots/[SNAPSHOT UUID]
```

* **Notes:**

  * When disaster recovery is enabled for the application, the "disasterRecovery" field will be populated.
  * For the "type" field the values are either "Local" or "Disaster Recovery".
  * For the "generated" field the values are either "Manual" or "Automatic".


### Create Snapshot for Application
  Create snapshot for an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/snapshots`

* **Method:**

  `POST`

*  **URL Params**

   None

* **Data Params**

```json
{"name": "New Snapshot"}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to create snapshot for application that is unresponsive.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/snapshots \
     -d '{"name": "New Snapshot"}'
```

* **Notes:**

  None


### Delete Snapshot for Application
  Delete snapshot for an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/snapshots/[SNAPSHOT UUID]`

* **Method:**

  `DELETE`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:** `{"actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"}`

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

  * **Code:** 500 Internal Server Error <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to delete snapshot for application that a template is currently being created from.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X DELETE https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/snapshots/[SNAPSHOT UUID]
```

* **Notes:**

  None


### List all Tags
  Returns json data about tags within an organization.

* **URL**

  `/api/latest/tags`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

   `datacenters=[comma-delimited list of datacenter UUIDs]`

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "f3432ab9-ed3e-438f-927a-bd16129ceae2",
    "name": "Tag"
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/tags \
     -d 'limit-count=10'
```

* **Notes:**

  None


### Get Tag Information
  Returns json data about a tag.

* **URL**

  `/api/latest/tags/[TAG UUID]`

* **Method:**

  `GET`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "uuid": "f3432ab9-ed3e-438f-927a-bd16129ceae2",
  "name": "Tag"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Tag with uuid f3432ab9-ed3e-438f-927a-bd16129ceae2 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/tags/[TAG UUID]
```

* **Notes:**

  None


### List all Categories
  Returns json data about categories within an organization.

* **URL**

  `/api/latest/categories`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

   `datacenters=[comma-delimited list of datacenter UUIDs]`

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "0213159e-0591-428e-be60-ab1eac553115",
    "name": "Category"
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/categories \
     -d 'limit-count=10'
```

* **Notes:**

  None


### Get Category Information
  Returns json data about a category.

* **URL**

  `/api/latest/categories/[CATEGORY UUID]`

* **Method:**

  `GET`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "uuid": "0213159e-0591-428e-be60-ab1eac553115",
  "name": "Category"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Category with uuid 0213159e-0591-428e-be60-ab1eac553115 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/categories/[CATEGORY UUID]
```

* **Notes:**

  None


### List all Virtual Datacenters
  Returns json data about virtual datacenters within an organization.

* **URL**

  `/api/latest/datacenters`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "8ffb9733-c941-4007-a0dd-6b0981aceea1",
    "name": "Datacenter",
    "allocations": {
      "migrationZones": [
        {
          "migrationZoneUuid": "8ffb9733-c941-4007-a0dd-6b0981aceea1",
          "categoryUuid": "6aa39a35-af3d-4f6d-b38a-284f7da8a28a",
          "vcpu": 4,
          "memory": 1073741824
        }
      ],
      "flashPools": [
        {
          "flashPoolUuid": "06fd6c19-d83c-40d5-9f81-0712dce483b0",
          "size": 1073741824
        }
      ]
    }
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/datacenters \
     -d 'limit-count=10'
```

* **Notes:**

  None


### Get Virtual Datacenter Information
  Returns json data about a virtual datacenter.

* **URL**

  `/api/latest/datacenters/[VDC UUID]`

* **Method:**

  `GET`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "uuid": "8ffb9733-c941-4007-a0dd-6b0981aceea1",
  "name": "Datacenter",
  "allocations": {
    "migrationZones": [
      {
        "migrationZoneUuid": "8ffb9733-c941-4007-a0dd-6b0981aceea1",
        "categoryUuid": "6aa39a35-af3d-4f6d-b38a-284f7da8a28a",
        "vcpu": 4,
        "memory": 1073741824
      }
    ],
    "flashPools": [
      {
        "flashPoolUuid": "06fd6c19-d83c-40d5-9f81-0712dce483b0",
        "size": 1073741824
      }
    ]
  }
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Datacenter with uuid 8ffb9733-c941-4007-a0dd-6b0981aceea1 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/datacenters/[VDC UUID]
```

* **Notes:**

  None


### List all Migration Zones
  Returns json data about migration zones within an organization.

* **URL**

  `/api/latest/migration-zones`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

   `datacenters=[comma-delimited list of datacenter UUIDs]`

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "a70f296c-a714-4f3e-af40-1866437a9fb3",
    "name": "Migration Zone",
    "allocations": {
      "categories": [
        {
          "categoryUuid": "e011b462-f015-408d-af53-6a36597293ab",
          "cpuTotal": 4,
          "cpuAllocated": 2,
          "memoryTotal": 2147483648,
          "memoryAllocated": 1073741824
        }
      ],
      "datacenters": [
        {
          "datacenterUuid": "6b70d7bc-92bd-4140-a25e-e5727684d58b",
          "cpuAllocated": 2,
          "memoryAllocated": 1073741824
        }
      ]
    }
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/migration-zones -d 'limit-count=10'
```

* **Notes:**

  None


### Get Migration Zone Information
  Returns json data about a migration zone.

* **URL**

  `/api/latest/migration-zones/[MIGRATION ZONE UUID]`

* **Method:**

  `GET`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "uuid": "a70f296c-a714-4f3e-af40-1866437a9fb3",
  "name": "Migration Zone",
  "allocations": {
    "categories": [
      {
        "categoryUuid": "e011b462-f015-408d-af53-6a36597293ab",
        "cpuTotal": 4,
        "cpuAllocated": 2,
        "memoryTotal": 2147483648,
        "memoryAllocated": 1073741824
      }
    ],
    "datacenters": [
      {
        "datacenterUuid": "6b70d7bc-92bd-4140-a25e-e5727684d58b",
        "cpuAllocated": 2,
        "memoryAllocated": 1073741824
      }
    ]
  }
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Migration Zone with uuid a70f296c-a714-4f3e-af40-1866437a9fb3 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/migration-zones/[MIGRATION ZONE UUID]
```

* **Notes:**

  None


### List all Vnets
  Returns json data about vnets within an organization.

* **URL**

  `/api/latest/vnets`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "3c163fce-f56e-4a27-aa67-0141f5470b29",
    "name": "Vnet",
    "rangeIps": [
      "192.168.1.0",
      "192.168.1.254"
    ],
    "gateway": "192.168.1.255",
    "netmask": 24,
    "networkServiceAppUuid": "88900a57-47a7-47b1-a4ba-ce3c1286ea88",
    "firewallProfileUuid": "7bec6223-4340-42dd-9d51-36864dbf7419"
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/vnets \
     -d 'limit-count=10'
```

* **Notes:**

  None


### Get Vnet Information
  Returns json data about a vnet.

* **URL**

  `/api/latest/vnets/[VNET UUID]`

* **Method:**

  `GET`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "uuid": "3c163fce-f56e-4a27-aa67-0141f5470b29",
  "name": "Vnet",
  "rangeIps": [
    "192.168.1.0",
    "192.168.1.254"
  ],
  "gateway": "192.168.1.255",
  "netmask": 24,
  "networkServiceAppUuid": "88900a57-47a7-47b1-a4ba-ce3c1286ea88",
  "firewallProfileUuid": "7bec6223-4340-42dd-9d51-36864dbf7419"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Vnet with uuid 3c163fce-f56e-4a27-aa67-0141f5470b29 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]
```

* **Notes:**

  None


### Get Firewall Profiles for Vnet
  Returns json data about firewall profiles for a vnet.

* **URL**

  `/api/latest/vnets/[VNET UUID]/firewall-profiles`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "bd4341d9-89f2-481a-9b4a-03548aadaec1",
    "name": "Application Firewall Profile",
    "rules": [
      {
        "order": 0,
        "type": "Outgoing",
        "protocol": "UDP",
        "sourceRangeIps": [],
        "sourceRangePorts": [],
        "destinationRangeIps": [],
        "destinationRangePorts": [
          67,
          68
        ],
        "action": "Allow",
        "description": "Allow traffic from the application instances to the network service instance."
      }
    ]
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Vnet with uuid 3c163fce-f56e-4a27-aa67-0141f5470b29 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]/firewall-profiles \
     -d 'limit-count=10'
```

* **Notes:**

  None


### List all Flash Pools
  Returns json data about flash pools within an organization.

* **URL**

  `/api/latest/flash-pools`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

   `datacenters=[comma-delimited list of datacenter UUIDs]`

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "082be6c5-b782-4b1e-825a-0d09328878ef",
    "name": "Flash Pool",
    "allocations": [
      {
        "datacenterUuid": "37d8bc9c-39a3-4585-9f2a-edaf0a8efd81",
        "size": 1073741824
      }
    ]
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/flash-pools \
     -d 'limit-count=10'
```

* **Notes:**

  None


### Get Flash Pool Information
  Returns json data about a flash pool.

* **URL**

  `/api/latest/flash-pools/[FLASH POOL UUID]`

* **Method:**

  `GET`

*  **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "uuid": "082be6c5-b782-4b1e-825a-0d09328878ef",
  "name": "Flash Pool",
  "allocations": [
    {
      "datacenterUuid": "37d8bc9c-39a3-4585-9f2a-edaf0a8efd81",
      "size": 1073741824
    }
  ]
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Flash Pool with uuid 082be6c5-b782-4b1e-825a-0d09328878ef does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/flash-pools/[FLASH POOL UUID]
```

* **Notes:**

  None


### List all Templates
  Returns json data about templates within an organization.

* **URL**

  `/api/latest/templates`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "d1253ae3-6698-4e01-b11c-735181c7e813",
    "name": "CentOS 7.2 - Docker 1.12",
    "description": "Cloudistics-ready CentOS 7.2 - Docker 1.12",
    "cpu": 4,
    "memory": 1073741824,
    "size": 1073741824,
    "dateCreated": "2016-11-15'T'12:00:00",
    "operatingSystem": {
      "type": "CentOS Linux",
      "version": "7"
    }
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/templates \
     -d 'limit-count=10'
```

* **Notes:**

  None


### Get Template Information
  Returns json data about a template.

* **URL**

  `/api/latest/templates/[TEMPLATE UUID]`

* **Method:**

  `GET`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
    "uuid": "d1253ae3-6698-4e01-b11c-735181c7e813",
    "name": "CentOS 7.2 - Docker 1.12",
    "description": "Cloudistics-ready CentOS 7.2 - Docker 1.12",
    "cpu": 4,
    "memory": 1073741824,
    "size": 1073741824,
    "dateCreated": "2016-11-15'T'12:00:00",
    "operatingSystem": {
      "type": "CentOS Linux",
      "version": "7"
    }
  }
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Template with uuid d1253ae3-6698-4e01-b11c-735181c7e813 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/templates/[TEMPLATE UUID]
```

* **Notes:**

  None


### Get Action Information
  Returns json data about an action performed through the REST API.

* **URL**

  `/api/latest/actions/[ACTION UUID]`

* **Method:**

  `GET`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{"status": "Completed"}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Action with uuid 71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/actions/[ACTION UUID]
```

* **Notes:**

  None


### Get Events
  Returns json data about the events for an organization.

* **URL**

  `/api/latest/events`

* **Method:**

  `GET`

*  **URL Params**

   **Optional:**

   `start-timestamp=[date with pattern "yyyy-MM-dd'T'HH:mm:ss"]`

   `end-timestamp=[date with pattern "yyyy-MM-dd'T'HH:mm:ss"]`

   `start-index=[positive integer]` *Defaults to 0*

   `limit-count=[positive integer]` *Defaults to 1000*

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "timestamp": "2016-11-15'T'12:00:00",
    "category": "Networking",
    "notification": "SDN router renamed",
    "description": "SDN router %old_router_name% has been renamed as %new_router_name% by user %issuer_user_name%. This request originated from IP address %issuer_ip_address%.",
    "metadata": {
      "old_router_name": "Old Router Name",
      "new_router_name": "New Router Name",
      "issuer_name": "Michael Nachmias",
      "issuer_ip_address": "127.0.0.1"
    }
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/events \
     -d 'start-timestamp=2017-01-11T12:00:00'
```

* **Notes:**

  None
