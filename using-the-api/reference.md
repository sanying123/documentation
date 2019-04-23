# ShiftLeft Vulnerability API

The ShiftLeft Vulnerability API allows ShiftLeft to access your organization’s applications to analyze, identify and provide data on your code's vulnerabilities. A vulnerability is a potentially exploitable path in the code base. 

The API returns a list of vulnerabilities, by organization or application version, with all the necessary information for you to take action on a code exploitable area. 

## Example of an API Query Return

```json
       {
           "applicationId": "project1549413585aa",
           "vulnerability": {
               "firstDetected": "041718202019.28",
               "vulnerabilityId": "database-write/e0ec210246d63ea44e28c01ed6113a66",
               "category": "a1-injection",
               "title": "Unsanitized database write in `DataLoader.run`",
               "description": "Attacker-controlled data is used in a database query without any sanitation or encoding. This could be intended behavior and thus has a low score. Injection flaws, such as SQL, NoSQL, OS, and LDAP injection, occur when untrusted data is sent to an interpreter as part of a command or query. By injecting hostile data, an attacker may trick the interpreter into executing unintended commands or accessing data without proper authorization which can result in data loss, corruption, or disclosure to unauthorized parties, loss of accountability, denial of access or even a complete host takeover.",
               "score": 1,
               "severity": "LOW_IMPACT",
               "securityEvents": "1",
               "blockedEvents": "1",
               "calls	": "1",
               "locationURL": "/account/{accountId}/addInterest",
               "locationMethod": "addInterest",
               "status": "FIXED",
               "assignedTo": "example@shiftleft.io",
           }
       },
```

where:

* `applicationId`: Unique identification for each application within your organization.
* `vulnerability`:
	* `firstDetected`: UNIX timestamp of the date and time when ShiftLeft first detected this vulnerability.
	* `vulnerabilityId`: Unique ID of this particular vulnerability accross all organizations.
	* `category`: Vulnerability OWASP category.
	* `title`: Vulnerability title.
	* `description`: Vulnerability description.
	* `score`: Vulnerability float score, from 1-9, representing the OWASP severity.
	* `severity`: Either `LOW_IMPACT`, `MEDIUM_IMPACT`, `HIGH_IMPACT` indicating the score level assigned by ShiftLeft.
	*  `securityEvents`: Count of security relevant events for the vulnerable endpoint.
	*  `blockedEvents`: Count of security relevant events that were blocked.
	*  `calls`: Total calls on the vulnerable endpoint. Represents regular traffic as well as any detected attacks.
	*  `locationURL`: Published location of the affected endpoint.
	*  `locationMethod`: Starting method of the vulnerable code path.
	*  `status`: UI configurable status of the vulnerability (ie. assignees, fixed or ignore state, etc.)
	*  `assignedTo`: Email address of individual assigned to fix or triage this vulnerability.
	

## Pagination

The ShiftLeft Vulnerability API endpoints are always paginated. Results shown in sequential pages containing a maximum of 50 results. The results are displayed in three categories according to severity. Pagination information is provided with each response 

```json
{
	"page": "1",
 	"totalResults": "155",
  	"results": [],
  	"lowImpactResults": "104",
	"mediumImpactResults": "21",
	"highImpactResults": "30"
}
```

## Listing an Organization's Vulnerabilities

You use the following request to return vulnerabilities by organization

POST `/api/v3/public/orgs/{organization id}/vulnerabilities/`

The result returns vulnerabilities with the following criteria

* Belonging to the latest analyzed version of any app
* Of any severity
* Of any category
* With any description
* With or without calls
* With or without blocked calls
* Arbitrarily sorted
* Only the first page (50 results)

To obtain a specific page of results, use

POST `/api/v3/public/orgs/{organization id}/vulnerabilities/page/{page number}`

If the page is outside of the possible range, you receive an empty result set.

### Filtering an Organization's Vulnerabilities

You can filter returns in the body of the query

```json
{
        "orderByDirection": "DESC",
        "applicationId": [
            "project1549413585aa"
        ],
        "statusFilter": [
            "FIXED", "ASSIGNED"
        ],
        "severityFilter": [],
        "titleFilter": "",
        "assignedToFilter": [],
        "includeCalls": true
    }
},
```

* `orderByDirection`: Either `DESC` or `ASC` is applied to the `firstDetected` field of a vulnerability.
* `applicationId`: If included, only returns results for these application IDs.
* `statusFilter`: If present, only returns results for vulnerabilities with these statuses.
* `severityFilter`: If present, only returns results for vulnerabilities of these severities.
* `titleFilter`: If present, the vulnerability title is partially-matched. Note that using this parameter can make the query return slower.
* `assignedToFilter`: If present, only returns vulnerabilities that have been assigned to the passed emails.
* `includeCalls`: True by default. Indicates that `securityEvents`, `blockedEvents` and `calls` are returned as part of the results. Note that using these parameters can make the query return slower.

## Listing an Application's Vulnerabilities

You use the following request to return vulnerabilities by an application

POST `/api/v3/public/orgs/{organization id}/application/{application id}/vulnerabilities/`

This will result on a default query returning vulnerabilities with the following criteria:

* Belonging to the latest analyzed version this app.
* Of any Severity
* Of any category
* With Any Description
* With or without calls
* With or without blocked calls.
* Arbitrarily sorted
* Only the first page (50 results)

To obtain a specific page of results, use

POST `/api/v3/public/orgs/{organization id}/application/{application id}/vulnerabilities/page/{page number}`

To obtain results for a specific application version, use 

POST `/api/v3/public/orgs/{organization id}/application/{application id}/version/{version}/vulnerabilities`

Note that this request also supports `/page/{page number}`.

If either of these pages are outside of the possible range, you receive an empty result set.

### Filtering an Application's Vulnerabilities

You can filter returns in the body of the query

```json
{
        "orderByDirection": "DESC",
        "statusFilter": [
            "FIXED", "ASSIGNED"
        ],
        "severityFilter": [],
        "titleFilter": "",
        "assignedToFilter": [],
        "includeTraffic": true
    }
},
```

* `orderByDirection`: Either `DESC` or `ASC` is applied to the `firstDetected` field of a vulnerability.
* `applicationId`: If included, only returns results for these application IDs.
* `statusFilter`: If present, only returns results for vulnerabilities with these statuses.
* `severityFilter`: If present, only returns results for vulnerabilities of these severities.
* `titleFilter`: If present, the vulnerability title is partially-matched. Note that using this parameter can make the query return slower.
* `assignedToFilter`: If present, only returns vulnerabilities that have been assigned to the passed emails.
* `includeCalls`: True by default. Indicates that `securityEvents`, `blockedEvents` and `calls` are returned as part of the results. Note that using these parameters can make the query return slower.
