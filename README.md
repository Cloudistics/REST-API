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

### Content type

CWS requires content type in headers for PUT or POST REST API calls

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/applications \
     -d '{"name": "CentOS 7.5 Application", "description": "This application was created from a CentOS template.", "vcpus": 4, "memory": 1073741824, "templateUuid": "3625edfa-1d41-488c-bbdc-13d35bdeb9ae", "categoryUuid": "a55bb4da-7cad-40cb-95e0-37db93c7aa5e", "tags": [{"uuid": "3402698b-d436-4b70-8fe7-d44fae37c68a"}], "datacenterUuid": "101552a2-e436-415a-a1cd-a11e5cb1e06e", "migrationZoneUuid": "6c47337b-9ee0-434d-90a6-2743b1bcdf9a", "flashPoolUuid": "d80fe07d-5858-4de8-98ce-8a8b9b6684a4", "networks": [{"type": "VNET", "networkUuid": "ff724194-931c-4c02-928e-e37821e74a8a", "firewallOverrideUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd"}], "hardwareAssistedVirtualizationEnabled": true, "vmMode": "Enhanced", "applicationGroupUuid":"0ec8fee4-133b-46e5-b892-4ddd7ff62ab3"}'
```

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/name \
     -d '{"name": "New Application name"}'
```

### Filtering

CWS allows filtering of the responses through optional request parameters. Please see the "URL Params" section within the definition of the REST API endpoint to see if filtering is available for it.

| Parameter | Description | 
| ---|---|
| start&#8209;index | Returns results starting at the specified index in the result set.<br>The starting index in a result set is always 0.<br>Default: 0<br>Example: If there are 2 applications in an organization and you request to List all Applications with a starting index of 1 only the second application will be returned in the response. |
| limit&#8209;count | Limit the number of results returned in the response from the REST API request.<br>Default: 1000<br>Example: If there are 2 applications in an organization and you request to List all Applications with a limit count of 1 only the first application will be returned in the response. |
| start&#8209;timestamp | Only returns results from the request where the result has a property timestamp greater than or equal to the start timestamp provided.<br>Example: If you request to Get Events with a start timestamp of '2017-01-10'T'12:00:00' the response will only contain events that have been created after January 10, 2017 at 12:00 PM. |
| end&#8209;timestamp | Only returns results from the REST API request where the result has a property timestamp less than or equal to the end timestamp provided.<br>Example: If you request to Get Events with a end timestamp of '2017-01-12'T'12:00:00' the response will only contain events that have been created before January 12, 2017 at 12:00 PM. |
| datacenters | This is a comma-delimited list of datacenter UUIDs to filter the results by. Only returns results from the REST API request where the result is in a datacenter specified. |
| application&#8209;groups | This is a comma-delimited list of application group UUIDs to filter the results by. Only returns results from the REST API request where the result is in a application group specified. |

## Cloudistics Virtual Data Centers (VDC) API Reference 

The Cloudistics Virtual Data Center (VDC) API Reference provides descriptions, syntax, and usage examples for each of the actions and data types for Cloudistics VDCs.
The topic for each action shows the Query API request parameters and the JSON response.

### Calls

* [List all Applications](#list-all-applications)
* [Get Application Information](#get-application-information)
* [Get Application Statistics](#get-application-statistics)
* [Get Application Disk Statistics](#get-application-disk-statistics)
* [Get Firewall Overrides for Application](#get-firewall-overrides-for-application)
* [Create Application from Template](#create-application-from-template)
* [Create Application from Snapshot](#create-application-from-snapshot)
* [Start Application](#start-application)
* [Stop Application](#stop-application)
* [Restart Application](#restart-application)
* [Suspend Application](#suspend-application)
* [Resume Application](#resume-application)
* [Delete Application](#delete-application)
* [Shutdown Application](#shutdown-application)
* [Rename Application](#rename-application)
* [Clone and Attach Disk to Application](#clone-and-attach-disk-to-application)
* [Edit Application Description](#edit-application-description)
* [Edit Application Datacenter](#edit-application-datacenter)
* [Edit Application Migration Zone](#edit-application-migration-zone)
* [Edit Application Boot Order](#edit-application-boot-order)
* [Edit Application vCpus](#edit-application-vcpus)
* [Edit Application Memory](#edit-application-memory)
* [Edit Application Compute Tags](#edit-application-compute-tags)
* [Edit Application Compute Category](#edit-application-compute-category)
* [Edit Application vNIC Name](#edit-application-vnic-name)
* [Edit Application vNIC Networking Type](#edit-application-vnic-networking-type)
* [Edit Application vNIC Firewall](#edit-application-vnic-firewall)
* [Edit Application vNIC MAC Address](#edit-application-vnic-mac-address)
* [Edit Application Disk Name](#edit-application-disk-name)
* [Edit Application Disk Size](#edit-application-disk-size)
* [Add Application Disk](#add-application-disk)
* [Add Application vNIC](#add-application-vnic)
* [Delete Application vNIC](#delete-application-vnic)
* [Delete Application Disk](#delete-application-disk)
* [Edit Application Hardware Assisted Virtualization Settings](#edit-application-hardware-assisted-virtualization-settings)
* [Edit Application Automatic Recovery Settings](#edit-application-automatic-recovery-settings)
* [Edit Application VM Mode](#edit-application-vm-mode)
* [Get Snapshots for Application](#get-snapshots-for-application)
* [Get Snapshot Information](#get-snapshot-information)
* [Create Snapshot for Application](#create-snapshot-for-application)
* [Delete Snapshot for Application](#delete-snapshot-for-application)
* [Rename Snapshot](#rename-snapshot)
* [List all Application Groups](#list-all-application-groups)
* [Get Application Group Information](#get-application-group-information)
* [Create Application Group](#create-application-group)
* [Rename Application Group](#rename-application-group)
* [Delete Application Group](#delete-application-group)
* [Assign Applications to Application Group](#assign-applications-to-application-group)
* [Remove Applications from Application Group](#remove-applications-from-application-group)
* [List all Tags](#list-all-tags)
* [Get Tag Information](#get-tag-information)
* [List all Categories](#list-all-categories)
* [Get Category Information](#get-category-information)
* [List all Virtual Datacenters](#list-all-virtual-datacenters)
* [Get Virtual Datacenter Information](#get-virtual-datacenter-information)
* [List all Migration Zones](#list-all-migration-zones)
* [Get Migration Zone Information](#get-migration-zone-information)
* [Get Migration Zone Statistics](#get-migration-zone-statistics)
* [List all VLANs](#list-all-vlans)
* [List all VNETs](#list-all-vnets)
* [Get VNET Information](#get-vnet-information)
* [Get Firewall Profile for VNET](#get-firewall-profile-for-vnet)
* [Get VLAN Information](#get-vlan-information)
* [Create VNET](#create-vnet)
* [Create VLAN](#create-vlan)
* [Rename Network](#rename-network)
* [Edit VNET Properties and DHCP](#edit-vnet-properties-and-dhcp)
* [Edit VNET Routing Service](#edit-vnet-routing-service)
* [Edit VNET Firewall Profile](#edit-vnet-firewall-profile)
* [Deploy NFV Instance to VNET](#deploy-nfv-instance-to-vnet)
* [Remove NFV Instance from VNET](#remove-nfv-instance-from-vnet)
* [Link NFV Instance to VNET](#link-nfv-instance-to-vnet)
* [Unlink NFV Instance from VNET](#unlink-nfv-instance-from-vnet)
* [Delete VNET](#delete-vnet)
* [Delete VLAN](#delete-vlan)
* [List all Flash Pools](#list-all-flash-pools)
* [Get Flash Pool Information](#get-flash-pool-information)
* [Get Flash Pool Statistics](#get-flash-pool-statistics)
* [List all Templates](#list-all-templates)
* [Get Template Information](#get-template-information)
* [Create Template from Application](#create-template-from-application)
* [Delete Template](#delete-template)
* [Import VM to Template](#import-vm-to-template)
* [Get Action Information](#get-action-information)
* [Get Events](#get-events)
* [Get Cloudistics Version](#get-version)
* [List all Locations](#list-all-locations)
* [Get Location Information](#get-location-information)
* [List all Compute Nodes](#list-all-compute-nodes)
* [Get Compute Node Information](#get-compute-node-information)
* [Get Compute Node Statistics](#get-compute-node-statistics)
* [List all Storage Blocks](#list-all-storage-blocks)
* [Get Storage Block Information](#get-storage-block-information)
* [List all Storage Controllers](#list-all-storage-controllers)
* [Get Storage Controller Information](#get-storage-controller-information)
* [List all Allocations](#list-all-allocations)
* [Get Operating System Versions](#get-operating-system-versions)

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

   `application-groups=[comma-delimited list of application group UUIDs]`

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "e696855c-186f-4c2a-a381-1637195bef3f",
    "name": "CentOS 7.5 Application"
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
      "size": 1073741824
    }
  ],
  "vnics": [
    {
      "uuid": "3fdb865d-edc3-48c5-acc0-656f82c097e0",
      "type": "VNET",
      "ipAddress": "127.0.0.1",
      "networks": [
        {
          "networkUuid": "ff724194-931c-4c02-928e-e37821e74a8a",
          "networkName": "Custom Vnet",
          "firewallOverrideUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd",
          "macAddress": "08:62:66:2b:88:b3"
        }
      ]
    },
    {
      "uuid": "ff3e8565-7f7a-478f-bff2-7e32060d9078",
      "type": "VLAN",
      "ipAddress": "127.0.0.2",
      "networks": [
        {
          "networkUuid": "c61386a5-431b-49d6-adb7-d33663f539ff",
          "firewallOverrideUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd",
          "macAddress": "09:79:12:2b:8e:y3"
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
  },
  "bootOrder": [
    {
      "diskUuid": "ac8e01aa-a667-46cf-8a7a-7082c5c9a6f3",
      "name": "Disk 0",
      "order": 1,
      "vnicUuid": null
    },
    {
      "vnicUuid": "3fdb865d-edc3-48c5-acc0-656f82c097e0",
      "name": "vNIC 0",
      "order": 2,
      "diskUuid": null
    },
    {
      "vnicUuid": "ff3e8565-7f7a-478f-bff2-7e32060d9078",
      "name": "vNIC 1",
      "order": 3,
      "diskUuid": null
    }
  ],
  "hardwareAssistedVirtualizationEnabled": true,
  "vmMode": "Enhanced",
  "applicationGroupUuid":"079c633d-b934-478a-8246-9d7826668c16"
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
    "vcpuUtilization" : 50,
    "memoryUtilizationBytes": 1073741824,
    "networkBandwidthReadBytesPerSecond": 0,
    "networkBandwidthWriteBytesPerSecond": 0,
    "allDisksStorageUtilizationBytes": 1073741824,
    "allDisksStorageInstanceBytes": 1073741824,
    "allDisksIoQueueDepth": 100,
    "allDisksIopsRead": 200,
    "allDisksIopsWrite": 300,
    "allDisksStorageBandwidthReadBytesPerSecond": 0,
    "allDisksStorageBandwidthWriteBytesPerSecond": 0
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


### Get Firewall Overrides for Application
  Returns json data about firewall overrides for an application.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/firewall-overrides`

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
     -G https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/firewall-overrides \
     -d 'limit-count=10'
```

* **Notes:**

  None


### Create Application from Template
  Creates an application from template and returns json data about the action.

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
      "name": "vNIC 0",
      "vnicUuid": "bf6199ea-a94b-4768-b24d-8994bf9bdf88",
      "type": "VNET",
      "networkUuid": "ff724194-931c-4c02-928e-e37821e74a8a",
      "firewallOverrideUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd",
      "automaticMACAssignment": false,
      "macAddress": "ab:ab:ab:ab:ab:ab"
    }
  ],
  "bootOrder": [
    {
      "diskUuid": "1b35fadb-7c63-46a6-9011-1df2a4f34918",
      "name": "Disk 1",
      "order": 1
    },
    {
      "vnicUuid": "bf6199ea-a94b-4768-b24d-8994bf9bdf88",
      "name": "vNIC 0",
      "order": 2
    },
    {
      "diskUuid": "694c1484-ced4-4810-bcb3-a302ffb45f12",
      "name": "Disk 2",
      "order": 3
    }
  ],
  "hardwareAssistedVirtualizationEnabled": true,
  "vmMode": "Enhanced",
  "applicationGroupUuid":"0ec8fee4-133b-46e5-b892-4ddd7ff62ab3"
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Template with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error creating application instance from template. There does not exist a valid hypervisor that can fit this application instance.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/applications \
     -d '{"name":"CentOS 7.5 Application","description":"This application was created from a CentOS template.","vcpus":4,"memory":1073741824,"templateUuid":"3625edfa-1d41-488c-bbdc-13d35bdeb9ae","categoryUuid":"a55bb4da-7cad-40cb-95e0-37db93c7aa5e","tags":[{"uuid":"3402698b-d436-4b70-8fe7-d44fae37c68a"}],"datacenterUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e","migrationZoneUuid":"6c47337b-9ee0-434d-90a6-2743b1bcdf9a","flashPoolUuid":"d80fe07d-5858-4de8-98ce-8a8b9b6684a4","networks":[{"name":"vNIC 0","vnicUuid":"bf6199ea-a94b-4768-b24d-8994bf9bdf88","type":"VNET","networkUuid":"ff724194-931c-4c02-928e-e37821e74a8a","firewallOverrideUuid":"1f6aa5ea-3e65-4767-a08f-fb454aa26afd","automaticMACAssignment":false,"macAddress":"ab:ab:ab:ab:ab:ab"}],"bootOrder":[{"diskUuid":"1b35fadb-7c63-46a6-9011-1df2a4f34918","name":"Disk 1","order":1},{"vnicUuid":"bf6199ea-a94b-4768-b24d-8994bf9bdf88","name":"vNIC 0","order":2},{"diskUuid":"694c1484-ced4-4810-bcb3-a302ffb45f12","name":"Disk 2","order":3}],"hardwareAssistedVirtualizationEnabled":true,"vmMode":"Enhanced","applicationGroupUuid":"0ec8fee4-133b-46e5-b892-4ddd7ff62ab3"}'
```

* **Notes:**

  * Optional fields in the request are "description" and "tags".
  * Networking "type" options are "VNET" or "VLAN". For both types, "networkUuid" is required and "firewallOverrideUuid" is optional. If "VLAN" networking is chosen, "firewallOverrideUuid" cannot be included.
  * The boot order should contain all existing template disk files and networks (vNICs) tied to the template. The following are failures that can happen with relation to the boot order:
    * If there is not at least one disk included in the boot order, the request will fail as at least one storage disk is required.
    * If there is not at least one network (vNIC) included in the boot order, the request will fail as at least one network is required.
    * If a template disk file tied to the template is not included in the boot order, the request will fail. The diskUuid property must be set to the uuid of the template disk file.
    * If a network (vNIC) tied to the template is not included in the boot order, the request will fail. the vnicUuid property must be set to the uuid of the template vNIC.
  * With multiple vNICs included in the networks and boot order, the name must start with "vNIC". For example, "vNIC 0". The name must be the same in both sections for a particular vNIC.
  * Each template vNIC must be included in both the networks section and the boot order section.
  * The vm mode options are 'Enhanced' or 'Compatibility'.


### Create Application from Snapshot
  Creates an application from snapshot and returns json data about the action.

* **URL**

  `/api/latest/applications/create-from-snapshot`

* **Method:**

  `POST`

*  **URL Params**

  None

* **Data Params**

```json
{
  "name": "CentOS 7.5 Application Snapshot",
  "description": "This application was created from a CentOS 7.5 Application snapshot.",
  "vcpus": 4,
  "memory": 1073741824,
  "snapshotUuid": "3625edfa-1d41-488c-bbdc-13d35bdeb9ae",
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
      "name": "vNIC 0",
      "vnicUuid": "bf6199ea-a94b-4768-b24d-8994bf9bdf88",
      "type": "VNET",
      "networkUuid": "ff724194-931c-4c02-928e-e37821e74a8a",
      "firewallOverrideUuid": "1f6aa5ea-3e65-4767-a08f-fb454aa26afd",
      "automaticMACAssignment": false,
      "macAddress": "ab:ab:ab:ab:ab:ab"
    }
  ],
  "bootOrder": [
    {
      "diskUuid": "1b35fadb-7c63-46a6-9011-1df2a4f34918",
      "name": "Disk 1",
      "order": 1
    },
    {
      "vnicUuid": "bf6199ea-a94b-4768-b24d-8994bf9bdf88",
      "name": "vNIC 0",
      "order": 2
    },
    {
      "diskUuid": "694c1484-ced4-4810-bcb3-a302ffb45f12",
      "name": "Disk 2",
      "order": 3
    }
  ],
  "hardwareAssistedVirtualizationEnabled": true,
  "vmMode": "Enhanced",
  "applicationGroupUuid":"0ec8fee4-133b-46e5-b892-4ddd7ff62ab3"
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Snapshot with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist for application with uuid 36a371c5-a9aa-4f4f-b1d1-ed782a11bc6a.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error creating application instance from snapshot. There does not exist a valid hypervisor that can fit this application instance.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/applications/create-from-snapshot \
     -d '{"name":"CentOS 7.5 Application Snapshot","description":"This application was created from a CentOS 7.5 Application snapshot.","vcpus":4,"memory":1073741824,"snapshotUuid":"3625edfa-1d41-488c-bbdc-13d35bdeb9ae","categoryUuid":"a55bb4da-7cad-40cb-95e0-37db93c7aa5e","tags":[{"uuid":"3402698b-d436-4b70-8fe7-d44fae37c68a"}],"datacenterUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e","migrationZoneUuid":"6c47337b-9ee0-434d-90a6-2743b1bcdf9a","flashPoolUuid":"d80fe07d-5858-4de8-98ce-8a8b9b6684a4","networks":[{"name":"vNIC 0","vnicUuid":"bf6199ea-a94b-4768-b24d-8994bf9bdf88","type":"VNET","networkUuid":"ff724194-931c-4c02-928e-e37821e74a8a","firewallOverrideUuid":"1f6aa5ea-3e65-4767-a08f-fb454aa26afd","automaticMACAssignment":false,"macAddress":"ab:ab:ab:ab:ab:ab"}],"bootOrder":[{"diskUuid":"1b35fadb-7c63-46a6-9011-1df2a4f34918","name":"Disk 1","order":1},{"vnicUuid":"bf6199ea-a94b-4768-b24d-8994bf9bdf88","name":"vNIC 0","order":2},{"diskUuid":"694c1484-ced4-4810-bcb3-a302ffb45f12","name":"Disk 2","order":3}],"hardwareAssistedVirtualizationEnabled":true,"vmMode":"Enhanced","applicationGroupUuid":"0ec8fee4-133b-46e5-b892-4ddd7ff62ab3"}'
```

* **Notes:**

  * Optional fields in the request are "description" and "tags".
  * Networking "type" options are "VNET" or "VLAN". For both types, "networkUuid" is required and "firewallOverrideUuid" is optional. If "VLAN" networking is chosen, "firewallOverrideUuid" cannot be included.
  * The boot order should contain all existing disks and networks (vNICs) tied to the application of the snapshot. The following are failures that can happen with relation to the boot order:
    * If there is not at least one disk included in the boot order, the request will fail as at least one storage disk is required.
    * If there is not at least one network (vNIC) included in the boot order, the request will fail as at least one network is required.
    * If a disk tied to the snapshot's application is not included in the boot order, the request will fail. The diskUuid property must be set to the uuid of the disk.
    * If a network (vNIC) tied to the snapshot's application is not included in the boot order, the request will fail. the vnicUuid property must be set to the uuid of the vNIC.
  * With multiple vNICs included in the networks and boot order, the name must start with "vNIC". For example, "vNIC 0". The name must be the same in both sections for a particular vNIC.
  * Each vNIC must be included in both the networks section and the boot order section.
  * The vm mode options are 'Enhanced' or 'Compatibility'.


### Start Application
  Starts an application and returns json data about the action.

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
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to start application that is already running.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

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
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to stop application that is shut off.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

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
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to restart application that is not running.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

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
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to pause application that is not running.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

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
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to resume application that is not paused.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

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
    **Content:**
```json
{
  "message": "Application successfully deleted."
}
```

  * **Code:** 202 Accepted <br />
    **Content:** 
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to delete application that is a networking services application.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X DELETE https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]
```

* **Notes:**

  * When disaster recovery is enabled for the application, disaster recovery snapshots will always be retained.
  * The success response will return a status code of 200 if the application instance is not a networking services application and it had failed to create properly. Otherwise, the success response will be 202 Accepted.


### Shutdown Application
  Shuts down an application and returns json data about the action.

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
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to shutdown application that is running and unreachable.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOEKN]" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/shutdown
```

* **Notes:**

  None

### Rename Application
  Renames an application

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/name`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "name": "New Application Name"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application name successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"An application with name New Application Name already exists for this organization.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/name \
     -d '{"name": "New Application name"}'
```

* **Notes:**

  None

### Clone and Attach Disk to Application
  Clones and attaches a disk to an application and returns json data about the action.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/clone-and-attach-disk`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "uuid": "8292f853-1c47-41ac-941c-b8fad35e8497"
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [uuid] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error cloning and attaching disk to application instance. The application is not eligible to have this disk cloned and attached.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/clone-and-attach-disk \
     -d '{"uuid": "8292f853-1c47-41ac-941c-b8fad35e8497"}'
```

* **Notes:**

  * The UUID in the request represents the unique identifier of the snapshot disk being cloned and attached to the application.
  * The object UUID in the response represents the UUID of the application the disk is being cloned and attached to.
  * The request will fail if the disk provided in the request is not a snapshot disk tied to an application.
  * The request will fail if the application is a auto-deployed NFV instance.
  * A snapshot disk is eligible to be cloned and attached to a specific application if it passes one of the following conditions:
    * The snapshot disk is tied directly to the application.
    * The application is present in the same virtual datacenter and lives on the same storage pool as the snapshot disk.
    * The application is present in the same virtual datacenter and has local snapshots on the same storage pool as the snapshot disk.
    * The application is present in the same virtual datacenter and has DR snapshots on the same storage pool as the snapshot disk.
  * To be able to locate the disk cloned and attached to the application, perform a delta of the disks before and after this action is performed. This can be done via the Get Application Information API request.


### Edit Application Description
  Updates an application's description

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/description`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "description": "New Application description"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application description successfully updated."
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
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/description \
     -d '{"description": "New Application description"}'
```

* **Notes:**

  None

### Edit Application Datacenter
  Updates an application's datacenter

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/datacenter`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "datacenterUuid": "20209870-b4f0-11e7-abc4-cec278b6b50a"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application datacenter successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to update application instance datacenter. Application must be shut off to complete this action.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/datacenter \
     -d '{"datacenterUuid": "20209870-b4f0-11e7-abc4-cec278b6b50a"}'
```

* **Notes:**

  * After a successful update, this application will no longer be assigned a migration zone, a category, or have any compute tags.
  

### Edit Application Migration Zone
  Updates an application's migration zone

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/migration-zone`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "migrationZoneUuid": "20209870-b4f0-11e7-abc4-cec278b6b50a"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application migration zone successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to update application instance migration zone. Application must be shut off to complete this action.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/migration-zone \
     -d '{"migrationZoneUuid": "20209870-b4f0-11e7-abc4-cec278b6b50a"}'
```

* **Notes:**

  * After a successful update, this application will no longer have a category or compute tags assigned to it.

### Edit Application Boot Order
  Updates an application's boot order

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/boot-order`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "bootOrder" : [
  {
    "diskUuid" : "ff678e0a-ae9f-11e7-abc4-cec278b6b50a",
    "order" : 1
  },
  {
    "diskUuid" : "20209f46-b4f0-11e7-abc4-cec278b6b50a",
    "order" : 2
  },
  {
    "vnicUuid" : "20209ae6-b4f0-11e7-abc4-cec278b6b50a",
    "order" : 3
  }
  ]
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application boot order successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Invalid Request","message":"This application disk with uuid ff678e0a-ae9f-11e7-abc4-cec278b6b50a does not exist in our database. Please try again.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to update application instance's boot order. Original boot order list does not match the new list provided.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/boot-order \
     -d '{"bootOrder" : [{"diskUuid" : "ff678e0a-ae9f-11e7-abc4-cec278b6b50a", "order" : 1}, {"diskUuid" : "20209f46-b4f0-11e7-abc4-cec278b6b50a", "order" : 2}, {"vnicUuid" : "20209ae6-b4f0-11e7-abc4-	cec278b6b50a", "order" : 3}]}'
```

* **Notes:**

  * This change will take effect the next time this application starts.


### Edit Application vCPUs
  Updates an application's vCPUs

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/vcpus`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "vcpus": 16
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application vcpus successfully updated."
}
```

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to update application instance vCPU provisioning. Application must be shut off to decrease this value.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/vcpus \
     -d '{"vcpus": 16}'
```

* **Notes:**

  * If the application is not shut off when this action is performed, a hotplug request will be made. The status of this request can be tracked using the actionUuid provided in the response.

### Edit Application Memory
  Updates an application's memory

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/memory`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "memory": 14858392
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application memory successfully updated."
}
```

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to update application instance's resource profile. Memory DIMM size must be a multiple of 128 MB.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/memory \
     -d '{"memory": 14858392}'
```

* **Notes:**

  * If the application is not shut off when this action is performed, a hotplug request will be made. The status of this request can be tracked using the actionUuid provided in the response.

### Edit Application Compute Tags
  Updates an application's compute tags

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/compute-tags`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
   "addTags":[
      {
         "uuid":"6ef0a804-b505-11e7-abc4-cec278b6b50a"
      }
   ],
   "removeTags":[
      {
         "uuid":"2020a02c-b4f0-11e7-abc4-cec278b6b50a"
      }
   ]
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application compute tags successfully updated."
}
```

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]",
  "message": "Application compute tags successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error removing compute tags from application. Tag with uuid 2020a02c-b4f0-11e7-abc4-cec278b6b50a is not assigned to this application.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/compute-tags \
     -d '{"addTags": [{"uuid" : "6ef0a804-b505-11e7-abc4-cec278b6b50a"}], "removeTags": [{"uuid" : "2020a02c-b4f0-11e7-abc4-cec278b6b50a"}]}'
```

* **Notes:**

  * If the application is not shut off when this action is performed, a hotplug request will be made. The status of this request can be tracked using the actionUuid provided in the response.

### Edit Application Compute Category
  Updates an application's compute category

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/compute-category`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

  * Request to change to a new category:

```json
{
  "categoryUuid" : "ff678e0a-ae9f-11e7-abc4-cec278b6b50a"
}
```

  * Request to change to 'Any' category:

```json
{
  "categoryUuid" : ""
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application compute category successfully updated."
}
```

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
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
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/compute-category \
     -d '{"categoryUuid": "ff678e0a-ae9f-11e7-abc4-cec278b6b50a"}'
```

* **Notes:**

  * If the application is not shut off when this action is performed, a hotplug request will be made. The status of this request can be tracked using the actionUuid provided in the response.


### Edit Application vNIC Name
  Renames an application vNIC

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]/name`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "name" : "New vNIC Name"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application vNIC name successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"An application vnic with name Br0 already exists for this organization.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]/name \
     -d '{"name" : "New vNIC Name"}'
```

* **Notes:**

  None

### Edit Application vNIC Networking Type
  Updates an application vNIC's networking

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]/type`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

  * Change to bridged or node-only:

```json
{
  "type" : "VLAN"
}
```

  * Change to VNET (networkUUID required): 

```json
{
  "type" : "VNET",
  "networkUuid" : "d0c8f53e-b5a2-11e7-abc4-cec278b6b50a"
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
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
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]/type \
     -d '{"type" : "VLAN"}'
```

* **Notes:**

  * When switching to networking mode, a networkUuid must be provided otherwise this request will fail


### Edit Application vNIC Firewall
  Updates an application vNIC's firewall override

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]/firewall`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**


```json
{
  "firewallOverrideUuid" : "ff678e0a-ae9f-11e7-abc4-cec278b6b50a"
}
```

* **Success Response:**

  * When application is shut off:
    * **Code:** 200 OK<br />
      **Content:**
```json
{
  "message": "Application vNIC firewall successfully updated."
}
```

  * When application is using resources:
    * **Code:** 202 Accepted <br />
      **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
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
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]/firewall \
     -d '{"firewallOverrideUuid" : "ff678e0a-ae9f-11e7-abc4-cec278b6b50a"}'
```

* **Notes:**

  None


### Edit Application vNIC MAC Address
  Updates an application vNIC's MAC address

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]/mac-address`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

  * Updating manual MAC address:

```json
{
  "macAddress" : "ab:ab:ab:ab:ab:ab",
  "automaticMACAssignment" : false
}
```

  * Updating to automatic MAC address:

```json
{
  "macAddress" : "",
  "automaticMACAssignment" : true
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
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
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]/mac-address \
     -d '{"macAddress" : "ab:ab:ab:ab:ab:ab", "automaticMACAssignment" : false}'
```

* **Notes:**

  * If attempting to change this vNIC's mac address to automatic assignment, macAddress parameter must be empty


### Edit Application Disk Name
  Renames an application disk

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/disks/[DISK_UUID]/name`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "name" : "Alpha disk"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application disk name successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"An application disk with name Alpha disk already exists for this organization.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/disks/[DISK_UUID]/name \
     -d '{"name" : "Alpha disk"}'
```

* **Notes:**

  None


### Edit Application Disk Size
  Updates an application disk's size

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/disks/[DISK_UUID]/size`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "size" : 32423438
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error resizing disk with UUID: d0c8f8d6-b5a2-11e7-abc4-cec278b6b50a. You may not decrease the size of an existing disk.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/disks/[DISK_UUID]/size \
     -d '{"size" : 32423438}'
```

* **Notes:**

  NONE

### Add Application Disk
  Creates a new disk for an application

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/disks`

* **Method:**

  `POST`

*  **URL Params**

   None

* **Data Params**

```json
{
  "name" : "Disk 2",
  "size" : 234820342
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error adding disk to application. You cannot add a disk to an application in compatibility mode that is not shut off.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/disks \
     -d '{"name": "Disk 2", "size" : 32423438}'
```

* **Notes:**

  NONE


### Add Application vNIC
  Creates a new vNIC for an application

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/vnics`

* **Method:**

  `POST`

*  **URL Params**

   None

* **Data Params**

  * Request to create a bridged or node-only vNIC:

```json
{
  "name" : "vNIC 2",
  "type" : "VLAN",
  "macAddress" : "ab:ab:ab:ab:ab:ab",
  "automaticMACAssignment" : false
}
```

 * Request to create a virtual networking vNIC:

```json
{
  "name" : "vNIC 2",
  "type" : "VNET",
  "networkUuid" : "d0c8f9c6-b5a2-11e7-abc4-cec278b6b50a",
  "firewallOverrideUuid" : "d0c8fcdc-b5a2-11e7-abc4-cec278b6b50a",
  "macAddress" : "",
  "automaticMACAssignment" : true
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error adding vNIC to application. There is a maximim of 64 vNICs for an application. Please update and try again.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/vnics \
     -d '{"name": "vNIC 2", "type" : "VNET", "networkUuid" : "d0c8f9c6-b5a2-11e7-abc4-cec278b6b50a", "firewallOverrideUuid" : "d0c8fcdc-b5a2-11e7-abc4-cec278b6b50a", "macAddress" : "", "automaticMACAssignment" : true}'
```

* **Notes:**

  NONE

### Delete Application vNIC
  Deletes a vNIC from an application

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]`

* **Method:**

  `DELETE`

*  **URL Params**

   None

* **Data Params**

   None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application vNIC successfully deleted."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to update application instance networking. Application must be shut off to complete this action.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X DELETE https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/vnics/[VNIC_UUID]
```

* **Notes:**

  * Application must be shut off to complete this action.
  * Application must have at least one vNIC remaining after this action


### Delete Application Disk
  Deletes a disk from an application

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/disks`

* **Method:**

  `DELETE`

*  **URL Params**

   None

* **Data Params**

   None

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error removing disk from application. At least one storage disk is required for an application.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X DELETE https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/disks/[DISK_UUID]
```

* **Notes:**

  * Application must have at least one disk remaining after this action


### Edit Application Hardware Assisted Virtualization Settings
  Updates an application's hardware assisted virtualization settings

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/hardware-assisted-virtualization`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "hardwareAssistedVirtualization" : true
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application hardware assisted virtualization settings successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to edit application hardware assisted virtualization settings because the application is not shutdown.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/hardware-assisted-virtualization \
     -d '{"hardwareAssistedVirtualization" : true}'
```

* **Notes:**

  * Application must be shut off to complete this action


### Edit Application Automatic Recovery Settings
  Updates an application's automatic recovery settings

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/automatic-recovery`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "automaticRecovery" : true
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application automatic recovery successfully updated."
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
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/automatic-recovery \
     -d '{"automaticRecovery" : true}'
```

* **Notes:**

  NONE

### Edit Application VM Mode
  Updates an application's VM mode

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/vm-mode`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
  "vmMode" : "Enhanced"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Application vm mode successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":""Unable to change vm mode because the application is not shutdown.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/vm-mode \
     -d '{"vmMode" : "Enhanced"}'
```

* **Notes:**

  * Application must be shut off to complete this action


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
      "uuid":"b576c8de-c70f-46d9-9a27-667416b2f788",
      "name":"Snapshot One"
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
   "uuid":"b576c8de-c70f-46d9-9a27-667416b2f788",
   "name":"Snapshot One",
   "createdTimestamp":"2016-11-15'T'12:00:00",
   "size":1073741824,
   "type":"Local",
   "generated":"Manual",
   "disasterRecovery":{
      "transferStatus":"Transferring",
      "transferPercentage":50
   },
   "bootOrder":[
      {
         "diskUuid":"1b35fadb-7c63-46a6-9011-1df2a4f34918",
         "name":"Disk 1",
         "order":1,
         "vnicUuid": null
      },
      {
         "vnicUuid":"bf6199ea-a94b-4768-b24d-8994bf9bdf88",
         "name":"vNIC 0",
         "order":2,
         "diskUuid": null
      },
      {
         "diskUuid":"694c1484-ced4-4810-bcb3-a302ffb45f12",
         "name":"Disk 2",
         "order":3,
         "vnicUuid": null
      }
   ]
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Snapshot with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist for application with uuid 36a371c5-a9aa-4f4f-b1d1-ed782a11bc6a.","fieldErrors":null}`

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
  Creates a snapshot for an application and returns json data about the action.

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
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to create snapshot for application that is unresponsive.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

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
  Deletes a snapshot for an application and returns json data about the action.

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
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[APPLICATION UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Snapshot with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist for application with uuid 36a371c5-a9aa-4f4f-b1d1-ed782a11bc6a.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Unable to delete snapshot for application that a template is currently being created from.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X DELETE https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/snapshots/[SNAPSHOT UUID]
```

* **Notes:**

  None


### Rename Snapshot
  Renames a snapshot for an application.

* **URL**

  `/api/latest/applications/[APPLICATION UUID]/snapshots/[SNAPSHOT UUID]/name`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
   "name":"New Snapshot Name"
}
```

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:**
```json
{
  "message": "Snapshot name updated successfully."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Snapshot with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist for application with uuid 36a371c5-a9aa-4f4f-b1d1-ed782a11bc6a.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error renaming snapshot. Unable to rename a DR snapshot.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/applications/[APPLICATION UUID]/snapshots/[SNAPSHOT UUID]/name \
     -d '{"name": "New Snapshot Name"}'
```

* **Notes:**

  * Only local snapshots can be renamed.
  * When renaming a local snapshot, if there are DR snapshots linked to it then they will be renamed as well.


### List all Application Groups
Returns json data about application groups within an organization.

* **URL**

  `/api/latest/application-groups`

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
[
  {
    "uuid": "e696855c-186f-4c2a-a381-1637195bef3f",
    "name": "Application Group"
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
     -G https://manage.cloudistics.com/api/latest/application-groups
```

* **Notes:**

  None


### Get Application Group Information
  Returns json data about an application group.

* **URL**

  `/api/latest/application-groups/[APPLICATION GROUP UUID]`

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
   "uuid":"e696855c-186f-4c2a-a381-1637195bef3f",
   "name":"Application Group",
   "datacenterUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application Group with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/application-groups/[APPLICATION GROUP UUID]
```

* **Notes:**

  None  


### Create Application Group
  Creates an application group.

* **URL**

  `/api/latest/application-groups/`

* **Method:**

  `POST`

*  **URL Params**

  None

* **Data Params**

```json
{
   "name":"New Application Group",
   "datacenterUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e"
}
```

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:**
```json
{
  "message": "Application group successfully created."
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Datacenter with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Application group with datacenter uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae already exists.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/application-groups \
     -d '{"name":"New Application Group", "datacenterUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e"}'
```

* **Notes:**

  * The request will fail if the datacenter already has an application group with this name.


### Rename Application Group
  Renames an application group.

* **URL**

  `/api/latest/application-groups/[APPLICATION GROUP UUID]/name`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
   "name":"New Application Group Name"
}
```

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:**
```json
{
  "message": "Application Group name successfully updated."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application Group with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/application-groups/[APPLICATION GROUP UUID]/name \
     -d '{"name": "New Application Group Name"}'
```

* **Notes:**

  None


### Delete Application Group
  Deletes an application group.

* **URL**

  `/api/latest/application-groups/[APPLICATION GROUP UUID]`

* **Method:**

  `DELETE`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:**
```json
{
  "message": "Application Group successfully deleted."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application Group with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X DELETE https://manage.cloudistics.com/api/latest/application-groups/[APPLICATION GROUP UUID]
```

* **Notes:**

  * Deleting an application group will not delete the applications in the group. Those applications will no longer belong to an application group after the application group is deleted.


### Assign Applications to Application Group
  Assigns applications to an application group.

* **URL**

  `/api/latest/application-groups/[APPLICATION GROUP UUID]/assign-applications`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
   "applications":[
      {
         "uuid":"fa527c37-3582-41e5-afcb-4b181b8e39aa"
      }
   ]
}
```

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:**
```json
{
  "message": "Assigned Applications to an Application Group successfully."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application Group with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Application's datacenter and application group's datacenter are not the same.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/application-groups/[APPLICATION GROUP UUID]/assign-applications \
     -d '{"applications":[{"uuid":"fa527c37-3582-41e5-afcb-4b181b8e39aa"}]}'
```

* **Notes:**

  * If more than one application is attempting to be assigned to an application group:
    * If one of the applications does not exist or does not belong to the same datacenter as the application group it is skipped.
  * If only one application is attempting to be assigned to an application group:
    * If that application does not exist or does not belong to the same datacenter as the application group the request will fail.


### Remove Applications from Application Group
  Removes applications from an application group.

* **URL**

  `/api/latest/application-groups/[APPLICATION GROUP UUID]/remove-applications`

* **Method:**

  `PUT`

*  **URL Params**

   None

* **Data Params**

```json
{
   "applications":[
      {
         "uuid":"fa527c37-3582-41e5-afcb-4b181b8e39aa"
      }
   ]
}
```

* **Success Response:**

  * **Code:** 200 OK <br />
    **Content:**
```json
{
  "message": "Removed Applications from an Application Group successfully."
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application Group with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Application is not in the application group requested to be removed from.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/application-groups/[APPLICATION GROUP UUID]/remove-applications \
     -d '{"applications":[{"uuid":"fa527c37-3582-41e5-afcb-4b181b8e39aa"}]}'
```

* **Notes:**

  * If more than one application is attempting to be removed from an application group:
    * If one of the applications does not exist or does not belong to the same datacenter as the application group it is skipped.
  * If only one application is attempting to be removed from an application group:
    * If that application does not exist or does not belong to the application group the request will fail.


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
    "name": "Datacenter"
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
    "name": "Migration Zone"
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


### Get Migration Zone Statistics
  Returns json data about the statistics for a migration zone.

* **URL**

  `/api/latest/migration-zones/[MIGRATION ZONE UUID]/stats`

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
    "memoryUtilization": 1073741824
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Migration Zone with uuid 21ed442c-be25-11e6-a4a6-cec0c932ce01 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/migration-zones/[MIGRATION ZONE UUID]/stats \
     -d 'start-timestamp=2017-01-11T12:00:00'
```

* **Notes:**

  None  


### List all VLANs
  Returns json data about VLANs within an organization.

* **URL**

  `/api/latest/vlans`

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
      "uuid": "14cf1c96-515e-4819-961c-c7cc7f410e9b",
      "name":"VLAN",
      "locationUuid":"48efa3d8-c2a5-43ab-9dac-b18158203d43",
      "vlanTag":999
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
     -G https://manage.cloudistics.com/api/latest/vlans \
     -d 'limit-count=10'
```

* **Notes:**

  None


### List all VNETs
  Returns json data about VNETs within an organization.

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
      "uuid":"14cf1c96-515e-4819-961c-c7cc7f410e9b",
      "name":"VNET"
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


### Get VLAN Information
  Returns json data about a VLAN.

* **URL**

  `/api/latest/vlans/[VLAN UUID]`

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
   "uuid": "14cf1c96-515e-4819-961c-c7cc7f410e9b",
   "name":"VLAN",
   "locationUuid":"48efa3d8-c2a5-43ab-9dac-b18158203d43",
   "vlanTag":999
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VLAN with uuid 3c163fce-f56e-4a27-aa67-0141f5470b29 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/vlans/[VLAN UUID]
```

* **Notes:**

  None


### Get VNET Information
  Returns json data about a VNET.

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
   "uuid":"14cf1c96-515e-4819-961c-c7cc7f410e9b",
   "name":"VNET",
   "networkAddress":"3.3.3.3",
   "subnetMask":"255.255.255.0",
   "usableIpRange":"3.3.3.0-3.3.3.255",
   "defaultGateway":"3.3.3.4",
   "automaticDeployment":true,
   "dhcpService":{
      "startIpRange":"3.3.3.33",
      "endIpRange":"3.3.3.40",
      "leaseTime":86400,
      "domainName":"Domain Name",
      "primaryDnsServerIpAddress":"6.6.6.6",
      "secondaryDnsServerIpAddress":"7.7.7.7",
      "staticBindings":[
         {
            "hostname":"Host Name",
            "macAddress":"08:62:66:2b:88:b3",
            "ipAddress":"127.0.0.1"
         }
      ]
   },
   "routingService":{
      "type":"VNET",
      "networkUuid":"23fe4063-fdfd-4210-8a72-8494f99b4cea",
      "addressMode":"Static",
      "ipAddress":"4.4.4.4",
      "subnetMask":"255.255.255.0",
      "gateway":"4.4.4.44"
   },
   "nfvInstanceUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e",
   "firewallProfileUuid":"3625edfa-1d41-488c-bbdc-13d35bdeb9ae"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3c163fce-f56e-4a27-aa67-0141f5470b29 does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]
```

* **Notes:**

  None


### Get Firewall Profile for VNET
  Returns json data about the firewall profile for a VNET.

* **URL**

  `/api/latest/vnets/[VNET UUID]/firewall-profile`

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
   "uuid":"bd4341d9-89f2-481a-9b4a-03548aadaec1",
   "name":"Application Firewall Profile",
   "rules":[
      {
         "order":0,
         "type":"Outgoing",
         "protocol":"UDP",
         "sourceRangeIps":[

         ],
         "sourceRangePorts":[

         ],
         "destinationRangeIps":[

         ],
         "destinationRangePorts":[
            67,
            68
         ],
         "action":"Allow",
         "description":"Allow traffic from the application instances to the network service instance."
      }
   ]
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3c163fce-f56e-4a27-aa67-0141f5470b29 does not exist.","fieldErrors":null}`

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


### Create VLAN
  Creates a VLAN and returns json data about the action.

* **URL**

  `/api/latest/vlans/`

* **Method:**

  `POST`

*  **URL Params**

  None

* **Data Params**

```json
{
   "name":"New VLAN",
   "locationUuid":"48efa3d8-c2a5-43ab-9dac-b18158203d43",
   "vlanTag":999
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "VLAN successfully created."
}
```
    
  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[VLAN UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"VLAN with name New Vlan already already exists for organization.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/vlans \
     -d '{"name":"New VLAN","locationUuid":"48efa3d8-c2a5-43ab-9dac-b18158203d43","vlanTag":999}'
```

* **Notes:**

  * The request will fail if a VLAN already exists for the tag in the specified location.


### Create VNET
  Creates a VNET and returns json data about the action.

* **URL**

  `/api/latest/vnets/`

* **Method:**

  `POST`

*  **URL Params**

  None

* **Data Params**

```json
{
   "name":"New VNET",
   "networkAddress":"3.3.3.3",
   "subnetMask":"255.255.255.0",
   "defaultGateway":"3.3.3.4",
   "automaticDeployment":true,
   "dhcpService":{
      "startIpRange":"3.3.3.33",
      "endIpRange":"3.3.3.40",
      "leaseTime":86400,
      "domainName":"Domain Name",
      "primaryDnsServerIpAddress":"6.6.6.6",
      "secondaryDnsServerIpAddress":"7.7.7.7",
      "staticBindings":[
         {
            "hostname":"Host Name",
            "macAddress":"08:62:66:2b:88:b3",
            "ipAddress":"127.0.0.1"
         }
      ]
   },
   "routingService":{
      "networkUuid":"23fe4063-fdfd-4210-8a72-8494f99b4cea",
      "addressMode":"Static",
      "ipAddress":"4.4.4.4",
      "subnetMask":"255.255.255.0",
      "gateway":"4.4.4.44",
      "firewallOverride":"5a457cf9-f486-4514-bcc4-334e9bc0011a"
   },
   "nfvInstance":{
      "datacenterUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e",
      "migrationZoneUuid":"6c47337b-9ee0-434d-90a6-2743b1bcdf9a",
      "flashPoolUuid":"0b9512cd-7e40-4fd8-a2c2-74189d6b57a3",
      "vcpus":4,
      "memory":1073741824,
      "tags":[
         {
            "uuid":"fa527c37-3582-41e5-afcb-4b181b8e39aa"
         }
      ],
      "categoryUuid":"a55bb4da-7cad-40cb-95e0-37db93c7aa5e",
      "enableAutomaticRecovery":true
   },
   "firewallProfileUuid":"3625edfa-1d41-488c-bbdc-13d35bdeb9ae",
   "firewallOverrideUuid":"e17ccfb1-a4bf-4941-9e81-dd6eee73e29f"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "VNET successfully created."
}
```
    
  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[VNET UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"VNET with name New Vnet already already exists for organization.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/vnets \
     -d '{"name":"New VNET","networkAddress":"3.3.3.3","subnetMask":"255.255.255.0","defaultGateway":"3.3.3.4","automaticDeployment":true,"dhcpService":{"startIpRange":"3.3.3.33","endIpRange":"3.3.3.40","leaseTime":86400,"domainName":"Domain Name","primaryDnsServerIpAddress":"6.6.6.6","secondaryDnsServerIpAddress":"7.7.7.7","staticBindings":[{"hostname":"Host Name","macAddress":"08:62:66:2b:88:b3","ipAddress":"127.0.0.1"}]},"routingService":{"networkUuid":"23fe4063-fdfd-4210-8a72-8494f99b4cea","addressMode":"Static","ipAddress":"4.4.4.4","subnetMask":"255.255.255.0","gateway":"4.4.4.44","firewallOverride":"5a457cf9-f486-4514-bcc4-334e9bc0011a"},"nfvInstance":{"datacenterUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e","migrationZoneUuid":"6c47337b-9ee0-434d-90a6-2743b1bcdf9a","flashPoolUuid":"0b9512cd-7e40-4fd8-a2c2-74189d6b57a3","vcpus":4,"memory":1073741824,"tags":[{"uuid":"fa527c37-3582-41e5-afcb-4b181b8e39aa"}],"categoryUuid":"a55bb4da-7cad-40cb-95e0-37db93c7aa5e","enableAutomaticRecovery":true},"firewallProfileUuid":"3625edfa-1d41-488c-bbdc-13d35bdeb9ae","firewallOverrideUuid":"e17ccfb1-a4bf-4941-9e81-dd6eee73e29f"}'
```

* **Notes:**

  * The NFV instance for the VNET can be automatically deployed or manually linked.
    * If the VNET is manually linked, the user only supplies the name, network address, default gateway, firewall profile and that it is not automatically deployed.
    * If the VNET is automatically deployed, the user follows the following rules on which fields are optional or not.
  * The DHCP service must be supplied if the user chooses to automatically deploy the VNET.
    * The start IP range and end IP range are required. All other fields are optional.
  * The Routing service must be supplied if the user chooses to automatically deploy the VNET.
    * The user must supply routing network.
    * The user must supply its address mode, either "Static" or "DHCP". If static is chosen the user must provide the IP address, subnet mask, and gateway. If DHCP is chosen the user cannot supply these options.
    * The external firewall override is not allowed when the routing service network is "VLAN", and is optional when the routing service network is "VNET".
  * The NFV instance is optional but can only be supplied if the user chooses to automatically deploy the VNET.
    * If the user decides to not supply it, it means the VNET is incomplete and they will need to deploy the NFV instance later to make it complete.
    * If the user does supply it, then the datacenter, migration zone, flash pool, cpus, memory, and whether to enable automatic recovery are required. The tags and category are optional.
  * The firewall profile is optional and can be supplied for both automatically deployed and manualy linked vnets.
  * The internal firewall override is optional and can be supplied for both automatically deployed and manualy linked vnets.
  * The response will only include the action information if the VNET is automatically deployed and complete (the NFV instance information is provided). Otherwise it will return a 200 OK response status that the changes were persisted to the database.


### Rename Network
  Rename a network.

* **URL**

  `/api/latest/networks/[NETWORK UUID]/name`

* **Method:**

  `PUT`

*  **URL Params**

  None

* **Data Params**

```json
{
   "name":"New Network Name"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "Network name updated successfully."
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Network with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Network with name New Network Name already already exists for organization.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/networks/[NETWORK UUID]/name \
     -d '{"name":"New Network Name"}'
```

* **Notes:**

  None


### Edit VNET Properties
  Edits a VNET's properties and returns json data about the action.

* **URL**

  `/api/latest/vnets/[VNET UUID]/properties-and-dhcp`

* **Method:**

  `PUT`

*  **URL Params**

  None

* **Data Params**

```json
{
  "networkAddress": "3.3.3.3",
  "subnetMask": "255.255.255.0",
  "defaultGateway": "3.3.3.4",
  "dhcpService" : {
     "startIpRange":"3.3.3.33",
     "endIpRange":"3.3.3.40",
     "leaseTime":86400,
     "domainName":"Domain Name",
     "primaryDnsServerIpAddress":"6.6.6.6",
     "secondaryDnsServerIpAddress":"7.7.7.7",
     "staticBindings":[
        {
           "hostname":"Host Name",
           "macAddress":"08:62:66:2b:88:b3",
           "ipAddress":"127.0.0.1"
        }
     ]
    }
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "VNET properties and dhcp updated successfully."
}
```
    
  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[VNET UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Invalid IP range. The range specified conflicts with another VNET's IP range","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]/properties-and-dhcp \
     -d '{"networkAddress":"3.3.3.3","subnetMask":"255.255.255.0","defaultGateway":"3.3.3.4"}'
```

* **Notes:**

  * This action can be performed on both automatically deployed and manually linked VNETs.
  * The request will fail if the IP range calculated using the network address and subnet mask does conflict with any other VNETs and network switches in the organization.
  * The response will only include the action information if the VNET is complete and the NFV instance is not shut off. Otherwise it will return a 200 OK response status that the changes were persisted to the database. For automatically deployed VNETs, when the subnet is changed, the dhcp range will be updated accordingly.

### Edit VNET Routing Service
  Edits a VNET's routing service and returns json data about the action.

* **URL**

  `/api/latest/vnets/[VNET UUID]/routing-service`

* **Method:**

  `PUT`

*  **URL Params**

  None

* **Data Params**

```json
{
   "networkUuid":"23fe4063-fdfd-4210-8a72-8494f99b4cea",
   "addressMode":"Static",
   "ipAddress":"4.4.4.4",
   "subnetMask":"255.255.255.0",
   "gateway":"4.4.4.44"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "VNET Routing service updated successfully."
}
```
    
  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[VNET UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error editing routing service for VNET because the vnet has an action in progress.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]/routing-service \
     -d '{"networkUuid":"23fe4063-fdfd-4210-8a72-8494f99b4cea","addressMode":"Static","ipAddress":"4.4.4.4","subnetMask":"255.255.255.0","gateway":"4.4.4.44"}'
```

* **Notes:**

  * This action can only be performed on automatically deployed VNETs.
  * The routing service network must be supplied.
  * The address mode must be either "Static" or "DHCP". If static is chosen the user must provide the IP address, subnet mask, and gateway. If DHCP is chosen the user cannot supply these options.
  * The response will only include the action information if the VNET is complete and is using resources (the NFV instance is running). Otherwise it will return a 200 OK response status that the changes were persisted to the database.


### Edit VNET Firewall Profile
  Edits a VNET's firewall profile and returns json data about the action.

* **URL**

  `/api/latest/vnets/[VNET UUID]/firewall-profile`

* **Method:**

  `PUT`

*  **URL Params**

  None

* **Data Params**

```json
{
  "uuid": "3625edfa-1d41-488c-bbdc-13d35bdeb9ae"
}
```

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "message": "VNET firewall profile updated successfully."
}
```
    
  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[VNET UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error editing firewall profile for VNET because because the VNET has an action in progress.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]/firewall-profile \
     -d '{"uuid": "3625edfa-1d41-488c-bbdc-13d35bdeb9ae"}'
```

* **Notes:**

  * This action can be performed on both automatically deployed and manually linked VNETs.
  * If a null value or empty string for the firewall profile uuid is provided, then the current firewall profile will be removed from the VNET.


### Deploy NFV Instance to VNET
  Deploys a NFV instance to a VNET and returns json data about the action.

* **URL**

  `/api/latest/vnets/[VNET UUID]/deploy-nfv-instance`

* **Method:**

  `PUT`

*  **URL Params**

  None

* **Data Params**

```json
{
  "routingService":{
    "networkUuid":"23fe4063-fdfd-4210-8a72-8494f99b4cea",
    "addressMode":"Static",
    "ipAddress":"4.4.4.4",
    "subnetMask":"255.255.255.0",
    "gateway":"4.4.4.44",
    "firewallOverride":"5a457cf9-f486-4514-bcc4-334e9bc0011a"
  },
  "nfvInstance":{
    "datacenterUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e",
    "migrationZoneUuid":"6c47337b-9ee0-434d-90a6-2743b1bcdf9a",
    "flashPoolUuid":"0b9512cd-7e40-4fd8-a2c2-74189d6b57a3",
    "vcpus":4,
    "memory":1073741824,
    "tags":[
      {
         "uuid":"fa527c37-3582-41e5-afcb-4b181b8e39aa"
      }
    ],
    "categoryUuid":"a55bb4da-7cad-40cb-95e0-37db93c7aa5e",
    "enableAutomaticRecovery":true
  },
  "firewallProfileUuid":"3625edfa-1d41-488c-bbdc-13d35bdeb9ae",
  "firewallOverrideUuid":"e17ccfb1-a4bf-4941-9e81-dd6eee73e29f"
}
```

* **Success Response:**
    
  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[VNET UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error deploying NFV instance to VNET that is not auto-deployed.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]/deploy-nfv-instance \
     -d '{"routingService":{"networkUuid":"23fe4063-fdfd-4210-8a72-8494f99b4cea","addressMode":"Static","ipAddress":"4.4.4.4","subnetMask":"255.255.255.0","gateway":"4.4.4.44","firewallOverride":"5a457cf9-f486-4514-bcc4-334e9bc0011a"},"nfvInstance":{"datacenterUuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e","migrationZoneUuid":"6c47337b-9ee0-434d-90a6-2743b1bcdf9a","flashPoolUuid":"0b9512cd-7e40-4fd8-a2c2-74189d6b57a3","vcpus":4,"memory":1073741824,"tags":[{"uuid":"fa527c37-3582-41e5-afcb-4b181b8e39aa"}],"categoryUuid":"a55bb4da-7cad-40cb-95e0-37db93c7aa5e","enableAutomaticRecovery":true}}'
```

* **Notes:**

  * This action can only be performed on automatically deployed VNETs that are incomplete (do not have a NFV instance).
  * The datacenter, migration zone, flash pool, cpus, memory, and whether to enable automatic recovery are required. The tags and category are optional.
  * The Routing service is optional. If not provided, the existing routing service options for target VNET will be used. If not provided and no routing service options exist for target vnet, the request will fail.
    * The user must supply routing network.
    * The user must supply its address mode, either "Static" or "DHCP". If static is chosen the user must provide the IP address, subnet mask, and gateway. If DHCP is chosen the user cannot supply these options.
    * The external firewall override is not allowed when the routing service network is "VLAN", and is optional when the routing service network is "VNET".
  * The internal firewall override is not allowed when the routing service network is "VLAN", and is optional when the routing service network is "VNET" type.


### Remove NFV Instance from VNET
  Removes a NFV instance from a vnet and returns json data about the action.

* **URL**

  `/api/latest/vnets/[VNET UUID]/remove-nfv-instance`

* **Method:**

  `PUT`

*  **URL Params**

  None

* **Data Params**

  None

* **Success Response:**
    
  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[VNET UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error removing NFV instance from VNET that is not auto-deployed.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]/remove-nfv-instance
```

* **Notes:**

  * This action can only be performed on automatically deployed VNETs that are complete (have a NFV instance).


### Link NFV Instance to VNET
  Links a NFV instance to a VNET.

* **URL**

  `/api/latest/vnets/[VNET UUID]/link-nfv-instance`

* **Method:**

  `PUT`

*  **URL Params**

  None

* **Data Params**

```json
{
   "uuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e"
}
```

* **Success Response:**
    
  * **Code:** 200 OK <br />
    **Content:**
```json
{
  "message": "NFV instance linked to VNET successfully."
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error linking NFV instance to VNET that is auto-deployed.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]/link-nfv-instance \
     -d '{"uuid":"101552a2-e436-415a-a1cd-a11e5cb1e06e"}'
```

* **Notes:**

  * This action can only be performed on manually linked VNETs that are incomplete (do not have a NFV instance).
  * The application being linked as an NFV instance to the VNET must have a vNIC with its networking type set to VNET with this VNET selected.


### Unlink NFV Instance from VNET
  Unlinks a NFV instance from a VNET.

* **URL**

  `/api/latest/vnets/[VNET UUID]/unlink-nfv-instance`

* **Method:**

  `PUT`

*  **URL Params**

  None

* **Data Params**

  None

* **Success Response:**
    
  * **Code:** 200 OK <br />
    **Content:**
```json
{
  "message": "NFV instance unlinked from VNET successfully."
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error unlinking NFV instance from VNET that is auto-deployed.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X PUT https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]/unlink-nfv-instance
```

* **Notes:**

  * This action can only be performed on manually linked VNETs that are complete (have a NFV instance).


### Delete VNET
  Deletes a vnet and returns json data about the action.

* **URL**

  `/api/latest/vnets/[VNET UUID]`

* **Method:**

  `DELETE`

*  **URL Params**

  None

* **Data Params**

  None

* **Success Response:**
    
  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[VNET UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VNET with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error deleting vnet that has applications running on it.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X DELETE https://manage.cloudistics.com/api/latest/vnets/[VNET UUID]
```

* **Notes:**

  * This action can be performed on any VNET.


### Delete VLAN
  Deletes a VLAN and returns json data about the action.

* **URL**

  `/api/latest/vlans/[VLAN UUID]`

* **Method:**

  `DELETE`

*  **URL Params**

  None

* **Data Params**

  None

* **Success Response:**
    
  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[VLAN UUID]"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"VLAN with uuid 3625edfa-1d41-488c-bbdc-13d35bdeb9ae does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error deleting VLAN that has applications running on it.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X DELETE https://manage.cloudistics.com/api/latest/vlans/[VLAN UUID]
```

* **Notes:**

  * This action can be performed on any VLAN.


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
    "name": "Flash Pool"
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


### Get Flash Pool Statistics
  Returns json data about the statistics for a flash pool.

* **URL**

  `/api/latest/flash-pools/[FLASH POOL UUID]/stats`

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
    "ioQueueDepth": 2299,
    "iopsRead": 1212,
    "iopsWrite": 1010,
    "storageBandwidthReadBytesPerSecond": 9900000,
    "storageBandwidthWriteBytesPerSecond": 6600000,
    "storageUtilizationBytes": 12345678
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Flash Pool with uuid 689baf34-71c9-11e6-9d70-feff819cdc9f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/flash-pools/[FLASH POOL UUID]/stats \
     -d 'start-timestamp=2017-01-11T12:00:00'
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
    "name": "CentOS 7.2 - Docker 1.12"
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

  * The boot order section will include all template disk files and template vNICs tied to the template. When creating an application from template using the REST API, each of these template disk files and template vNICs must be included in the application's boot order.


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
    },
    "bootOrder": [
      {
        "diskUuid": "23bc2f5c-ac38-44fb-a96f-fdcd7dde25bf",
        "name": "Disk 1",
        "order": 1,
        "vnicUuid": null
      },
      {
        "vnicUuid": "91d71039-42d3-4a2e-b9c1-cf6e01953eff",
        "name": "vNIC 0",
        "order": 2,
        "diskUuid": null
      }
    ],
    "vmMode": "Enhanced"
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

  * The boot order section will include all template disk files and template vNICs tied to the template. When creating an application from template using the REST API, each of these template disk files and template vNICs must be included in the application's boot order.


### Create Template from Application
  Creates a template from an application and returns json data about the action.

* **URL**

  `/api/latest/templates/`

* **Method:**

  `POST`

*  **URL Params**

  None

* **Data Params**

```json
{
  "name": "New Windows Template",
  "description": "This template was created from a Windows application",
  "vcpus": 4,
  "memory": 1073741824,
  "applicationUuid": "961e2710-ff80-4055-bf55-4d44eeaf48f9",
  "runSysPrep": true,
  "vmMode": "Enhanced",
  "customWindowsSysprepXml": "<?xml version='1.0' encoding='UTF-8'?><heading>Custom Windows Sysprep XML</heading><body>Perform Custom Windows Sysprep</body>",
  "bootOrder": [
    {
      "diskUuid": "91996f7f-4b24-441d-a589-ecd25074a648",
      "name": "Disk 1",
      "order": 1
    },
    {
      "vnicUuid": "dfbc17ef-f9ba-4cbe-a6ca-3bd1749096c6",
      "name": "vNIC 0",
      "order": 2
    }
  ]
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c"
}
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request: Invalid request data","message":"field: [name] error: [required field is empty or not provided]","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Disk with uuid 91996f7f-4b24-441d-a589-ecd25074a648 does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"Error creating template from application instance. An application template already exists with this name.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`
                                                                                                                                                                                              
* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/templates \
     -d '{"name": "New Windows Template", "description": "This template was created from a Windows application", "vcpus": 4, "memory": 1073741824, "applicationUuid": "961e2710-ff80-4055-bf55-4d44eeaf48f9", "runSysPrep": true, "vmMode": "Enhanced", "customWindowsSysprepXml": "<?xml version='1.0' encoding='UTF-8'?><heading>Custom Windows Sysprep XML</heading><body>Perform Custom Windows Sysprep</body>", "bootOrder": [{"diskUuid": "91996f7f-4b24-441d-a589-ecd25074a648", "name": "Disk 1", "order": 1}, {"vnicUuid": "dfbc17ef-f9ba-4cbe-a6ca-3bd1749096c6", "name": "vNIC 0", "order": 2}]}'
```

* **Notes:**

  * The boot order should contain all existing disks and vNICs tied to the application. The following are failures that can happen with relation to the boot order:
    * If there is not at least one disk tied to the application and not included in the boot order, the request will fail as all disks tied to the application are required. The diskUuid property must be set to the uuid of the application disk.
    * If there is not at least one vNIC tied to the application and not included in the boot order, the request will fail as all vNICs tied to the application are required. The vnicUuid property must be set to the uuid of the application vNIC.
    * The name and order are required for all boot order items.
  * Run sys prep cannot be set to true if the template is set to netbooted (the first boot order item is a vNIC).
  * Run sys prep cannot be set to true if the application is not shut off.
  * Custom Windows Sysprep XML can only be provided if the template is being created from a Windows application. The Custom Windows Sysprep XML file size must be less than or equal to 2 MB.
  * The options for vm mode are 'Enhanced' and 'Compatibility'.


### Delete Template
  Deletes a template and returns json data about the action.

* **URL**

  `/api/latest/templates/[TEMPLATE UUID]`

* **Method:**

  `DELETE`

*  **URL Params**

   None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[TEMPLATE UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application Template with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -X DELETE https://manage.cloudistics.com/api/latest/templates/[TEMPLATE UUID]
```

* **Notes:**

  None


### Import VM to Template
  Imports a VM to a template and returns json data about the action.

* **URL**

  `/api/latest/templates/import-vm`

* **Method:**

  `POST`

*  **URL Params**

   None

* **Data Params**

```json
{
   "name":"New Template",
   "description":"Template imported from VM",
   "cpu":4,
   "memory":1073741824,
   "operatingSystem":{
      "type":"Linux",
      "version":"Enterprise Linux 6/7"
   },
   "runSysPrep":true,
   "virtioDriversInstalled":true,
   "templateDiskFiles":[
      {
         "name":"disk2",
         "path":"/path/to/disk2.vmdk"
      },
      {
         "name":"disk1",
         "path":"/path/to/disk1.vmdk"
      }
   ],
   "sharedStorage":{
      "type":"CIFS",
      "hostname":"Hostname",
      "shareName":"Share Name",
      "username":"user",
      "password":"password",
      "domain":"Domain"
   }
}
```

* **Success Response:**

  * **Code:** 202 Accepted <br />
    **Content:**
```json
{
  "actionUuid": "71011d4e-a4f7-4ab1-95e0-9e8986fb3f2c",
  "objectUuid": "[TEMPLATE UUID]"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Application Template with uuid e696855c-186f-4c2a-a381-1637195bef3f does not exist.","fieldErrors":null}`

  * **Code:** 422 Unprocessable Entity <br />
    **Content:** `{"code":"Invalid Request","message":"A(n) application template already exists with name: New Application Template. Please update and try again.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -H "Content-Type: application/json" \
     -X POST https://manage.cloudistics.com/api/latest/templates/import-vm \
     -d '{"name":"New Template","description":"Template imported from VM","cpu":4,"memory":1073741824,"operatingSystem":{"type":"Linux","version":"Enterprise Linux 6/7"},"runSysPrep":true,"virtioDriversInstalled":true,"templateDiskFiles":[{"name":"disk2","path":"/path/to/disk2.vmdk"},{"name":"disk1","path":"/path/to/disk1.vmdk"}],"sharedStorage":{"type":"CIFS","hostname":"Hostname","shareName":"Share Name","username":"user","password":"password","domain":"Domain"}}'
```

* **Notes:**

  * All fields are required except the description.
  * Regarding the shared storage:
    * The type must be either "NFS" or "CIFS".
    * Only the hostname and share name are required within the shared storage.
  * Regarding the template disk files:
    * Their index in the array will specify its boot order. Its boot order value will be its index + 1.
    * The template disk files must specify a supported file extension (vmdk, vhd, vhdx, ova, img, raw, vdi, qed or qcow2).
  * A template vNIC will be created automatically and there is no need for it to be included in the request data. The template vNIC's boot order will be the number of disks + 1. For example, if there are two disks the template vNIC's boot order will be 3.
  * Please use the operating system version endpoint and determine which operating system type and version are appropriate for the VM that is being imported to a template. 


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
{
  "status": "Completed"
}
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
    "description": "SDN router Old Router Name has been renamed as New Router Name by user Michael Nachmias. This request originated from IP address 127.0.0.1."
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

  The maximum timespan between `start-timestamp` and `end-timestamp` is approximately two years. For timespans longer than two years, issue additional queries in two year increments.


### Get Cloudistics Version
  Returns json data about the Cloudistics version.

* **URL**

  `/api/latest/version`

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
  "version": "3.4.0"
}
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
     -G https://manage.cloudistics.com/api/latest/version
```

* **Notes:**

  None


### List all Locations
  Returns json data about locations within an organization.

* **URL**

  `/api/latest/locations`

* **Method:**

  `GET`

* **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "fc06d214-31e5-4ee1-987e-b1adcd6c13dc",
    "name": "Reston"
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
     -G https://manage.cloudistics.com/api/latest/locations
```

* **Notes:**

  None

### Get Location Information
  Returns json data about a location.

* **URL**

  `/api/latest/locations/[LOCATION UUID]`

* **Method:**

  `GET`

* **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "uuid": "fc06d214-31e5-4ee1-987e-b1adcd6c13dc",
  "name": "Reston"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Location with uuid fc06d214-31e5-4ee1-987e-b1adcd6c13dc does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/locations/[LOCATION UUID]
```

* **Notes:**

  None

### List all Compute Nodes
  Returns json data about compute nodes within an organization.

* **URL**

  `/api/latest/compute-nodes`

* **Method:**

  `GET`

* **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "2c8ba748-6f7f-11e5-9d70-feff819cdc9f",
    "name": "AlphaCompute"
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
     -G https://manage.cloudistics.com/api/latest/compute-nodes
```

* **Notes:**

  None

### Get Compute Node Information
  Returns json data about a compute node.

* **URL**

  `/api/latest/compute-nodes/[COMPUTE NODE UUID]`

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
  "uuid": "2c8ba748-6f7f-11e5-9d70-feff819cdc9f",
  "name": "AlphaCompute",
  "description": "once or twice",
  "locationUuid": "fc06d214-31e5-4ee1-987e-b1adcd6c13dc",
  "migrationZoneUuid": "21ed442c-be25-11e6-a4a6-cec0c932ce01",
  "categoryUuid": "b9422b16-be26-11e6-a4a6-cec0c932ce01",
  "tags": [
  "tags": [
    {
      "uuid": "b94221d4-be26-11e6-a4a6-cec0c932ce01"
    },
    {
      "uuid": "b9422954-be26-11e6-a4a6-cec0c932ce01"
    }
  ],
  "cpus": 24,
  "memory": 67645734912,
  "computeOperatingSystem": "Cloudistics Spark Hypervisor",
  "computeServiceVersion": "1.1.1",
  "maintenanceModeEnabled": false
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Compute Node with uuid 2c8ba748-6f7f-11e5-9d70-feff819cdc9f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/compute-nodes/[COMPUTE NODE UUID]
```

* **Notes:**

  None

### Get Compute Node Statistics
  Returns json data about the statistics for a compute node.

* **URL**

  `/api/latest/compute-nodes/[COMPUTE NODE UUID]/stats`

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
    "networkBandwidthReadBytesPerSecond": 100,
    "networkBandwidthWriteBytesPerSecond": 80
  }
]
```

* **Error Response:**

  * **Code:** 400 Bad Request <br />
    **Content:** `{"code":"Bad Request","message":"Invalid request parameter for REST API. Limit count must be a positive integer.","fieldErrors":null}`

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Compute Node with uuid 2c8ba748-6f7f-11e5-9d70-feff819cdc9f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/compute-nodes/[COMPUTE NODE UUID]/stats \
     -d 'start-timestamp=2017-01-11T12:00:00'
```

* **Notes:**

  None
  

### List all Storage Blocks
  Returns json data about storage blocks within an organization.

* **URL**

  `/api/latest/storage-blocks`

* **Method:**

  `GET`

* **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "2c8ba61c-5f7c-11e5-9d70-feff819cdc9f",
    "name": "Storage Unit 1"
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
     -G https://manage.cloudistics.com/api/latest/storage-blocks
```

* **Notes:**

  None

### Get Storage Block Information
  Returns json data about a storage block.

* **URL**

  `/api/latest/storage-blocks/[STORAGE BLOCK UUID]`

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
  "uuid": "2c8ba61c-5f7c-11e5-9d70-feff819cdc9f",
  "name": "Storage Unit 1",
  "locationUuid": "fc06d214-31e5-4ee1-987e-b1adcd6c13dc",
  "storagePoolUuid": "689baf34-71c9-11e6-9d70-feff819cdc9f"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Storage Block with uuid 2c8ba61c-5f7c-11e5-9d70-feff819cdc9f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/storage-blocks/[STORAGE BLOCK UUID]
```

* **Notes:**

  None

### List all Storage Controllers
  Returns json data about storage controllers within an organization.

* **URL**

  `/api/latest/storage-controllers`

* **Method:**

  `GET`

* **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
[
  {
    "uuid": "2c8ba61c-6f7f-11e5-9d70-feff819cdc9f",
    "name": "Controller 1"
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
     -G https://manage.cloudistics.com/api/latest/storage-controllers
```

* **Notes:**

  None

### Get Storage Controller Information
  Returns json data about a storage controller.

* **URL**

  `/api/latest/storage-controllers/[STORAGE CONTROLLER UUID]`

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
  "uuid": "2c8ba61c-6f7f-11e5-9d70-feff819cdc9f",
  "name": "Controller 1",
  "locationUuid": "fc06d214-31e5-4ee1-987e-b1adcd6c13dc",
  "storageBlockUuid": "2c8ba61c-5f7c-11e5-9d70-feff819cdc9f",
  "active": true,
  "computeOperatingSystem": "Cloudistics Spark Hypervisor",
  "computeServiceVersion": "1.1.1"
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 404 Not Found <br />
    **Content:** `{"code":"Resource Not Found","message":"Storage Controller with uuid 2c8ba61c-6f7f-11e5-9d70-feff819cdc9f does not exist.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/storage-controllers/[STORAGE CONTROLLER UUID]
```

* **Notes:**

  None

### List all Allocations
  Returns json data about allocations within an organization.

* **URL**

  `/api/latest/allocations`

* **Method:**

  `GET`

* **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
  "datacenters": [
    {
      "uuid": "21ed4350-be25-11e6-a4a6-cec0c932ce01",
      "name": "Datacenter 1",
      "migrationZones": [
        {
          "uuid": "21ed442c-be25-11e6-a4a6-cec0c932ce01",
          "name": "DevOpsMigrationZone",
          "categories": {
            "uuid": "b9422b16-be26-11e6-a4a6-cec0c932ce01",
            "name": "Default",
            "cpus": 2,
            "memory": 2147483648
          }
        },
        {
          "uuid": "21ed4530-be25-11e6-a4a6-cec0c932ce01",
          "name": "QaMigrationZone",
          "categories": {
            "uuid": "284f2702-be27-11e6-a4a6-cec0c932ce01",
            "name": "Cucamonga",
            "cpus": 2,
            "memory": 2147483648
          }
        }
      ],
      "storagePools": [
        {
          "uuid": "689baf34-71c9-11e6-9d70-feff819cdc9f",
          "name": "Flash Pool 1",
          "connectedMigrationZones": [
            {
              "uuid": "21ed442c-be25-11e6-a4a6-cec0c932ce01",
              "name": "DevOpsMigrationZone"
            },
            {
              "uuid": "21ed4530-be25-11e6-a4a6-cec0c932ce01",
              "name": "QaMigrationZone"
            }
          ],
          "storageBytes": 107374182400
        },
        {
          "uuid": "689baf34-71c9-11e6-9d70-feff819cdc8f",
          "name": "Flash Pool 2",
          "connectedMigrationZones": [
            {
              "uuid": "21ed442c-be25-11e6-a4a6-cec0c932ce01",
              "name": "DevOpsMigrationZone"
            },
            {
              "uuid": "21ed4530-be25-11e6-a4a6-cec0c932ce01",
              "name": "QaMigrationZone"
            }
          ],
          "storageBytes": 107374182400
        }
      ]
    }
  ]
}
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
     -G https://manage.cloudistics.com/api/latest/allocations
```

* **Notes:**

  None

### Get Operating System Versions
  Returns json data about operating system versions.

* **URL**

  `/api/latest/operating-system-versions`

* **Method:**

  `GET`

* **URL Params**

  None

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 OK<br />
    **Content:**
```json
{
   "osTypes":[
      "Linux",
      "Windows",
      "Other",
      "BSD"
   ],
   "osVersionsByOsType":{
      "BSD":[
         "FreeBSD 10.3"
      ],
      "Linux":[
         "Enterprise Linux 6/7",
         "Ubuntu 16.04"
      ],
      "Windows":[
         "Windows 7",
         "Windows 8",
         "Windows 8.1",
         "Windows 10",
         "Windows Server 2008R2",
         "Windows Server 2012",
         "Windows Server 2012R2",
         "Windows Server 2016"
      ],
      "Other":[
         "FreeNAS 9.10",
         "NetScaler"
      ]
   }
}
```

* **Error Response:**

  * **Code:** 403 Forbidden <br />
    **Content:** `{"code":"Access Denied","message":"Unable to access REST API. Invalid token.","fieldErrors":null}`

  * **Code:** 429 Too Many Requests <br />
    **Content:** `{"code":"Too Many Requests","message":"Unable to access REST API. Rate limit exceeded.","fieldErrors":null}`

* **Sample Call:**

```bash
curl -H "Authorization: Bearer [YOUR TOKEN]" \
     -G https://manage.cloudistics.com/api/latest/operating-system-versions
```

* **Notes:**

  None