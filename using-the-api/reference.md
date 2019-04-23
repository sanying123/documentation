# ShiftLeft Vulnerability API

This API allows ShiftLeft to access each version of your organization’s applications to identify vulnerabilities and provide runtime protection. With this information, you can then take action securing your code. A vulnerability is a potentially exploitable path in the code base. 

Each API query returns vulnerabilities with all the necessary data for you to take action on a code exploitable area.

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

* `applicationId`: Unique identification string for each application within your organization.
* `vulnerability`:
	* `firstDetected`: UNIX timestamp of the date and time when ShiftLeft first detected this vulnerability.
	* `vulnerabilityId`: Unique ID of this particular vulnerability accross all organizations.
	* `category`: OWASP vulnerability category.
	* `title`: Vulnerability title.
	* `description`: Vulnerability description.
	* `score`: Vulnerability float score from 1-9 representing the OWASP severity.
	* `severity`: Either `LOW_IMPACT`, `MEDIUM_IMPACT`, `HIGH_IMPACT` indicating the score level assigned by ShiftLeft.
	*  `securityEvents`: Count of security relevant events for the vulnerable endpoint.
	*  `blockedEvents`: Count of security relevant events that were blocked.
	*  `calls`: Total calls on the vulnerable endpoint. Represents regular traffic as well as any detected attacks.
	*  `locationURL`: Published location of the affected endpoint.
	*  `locationMethod`: Starting method of the vulnerable code path.
	*  `status`: UI configurable status of the vulnerability (ie. assignees, fixed or ignore state, etc.)
	*  `assignedTo`: Email address of individual assigned to fix or triage this vulnerability.
	

## Pagination

The ShiftLeft Vulnerability API endpoints are always paginated, with query results possibles shown in pages of 50 results. These results are displayed in there categories according to severity. Pagination information is provided with each response 

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

## Returning an Organization's Vulnerabilities

You can use the following request to return vulnerabilities by organization

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

To obtain an arbitrary page, use

POST `/api/v3/public/orgs/{organization id}/vulnerabilities/page/{page number}`

If the page is outside of the possible range you will obtain an empty result set.

### Filtering

You can filter  returns in the body of the query

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

* `orderByDirection`: either `DESC` or `ASC` will be applied to the `firstDetected` field of a vulnerability.
* `applicationId`: if included in this list, only results for these application IDs will be returned.
* `statusFilter`: if present, only results for vulnerabilities in these statuses will be returned
* `severityFilter`: if present, only results for vulnerabilities of these severities will be returned
* `titleFilter`: if present the vulnerability title will be partially-matched with this, it might make the query slower.
* `assignedToFilter`: if present, only vulnerabilities that have been assigned to the passed emails will be returned.
* `includeCalls`: true by default, this indicates that `securityEvents`, `blockedEvents` and `calls` will be returned as part of the results, omitting them might be beneficial if you do not need them as they slow a bit the query.

## Application vulnerabilities

Application level vulnerabilities is an endpoint that allows you to perform the exact same kind of query than for Organizations but it limits results displayed to one Application.

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

To obtain an arbitrary page 

POST `/api/v3/public/orgs/{organization id}/application/{application id}/vulnerabilities/page/{page number}`

To obtain an arbitrary version (also supports `/page/{page number}` at the end)

POST `/api/v3/public/orgs/{organization id}/application/{application id}/version/{version}/vulnerabilities`

if the page is outside of the possible range you will obtain an empty result set.

#### Filtering

The filtering criteria can be passed in the body of the query:

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

* `orderByDirection`: either `DESC` or `ASC` will be applied to the `firstDetected` field of a vulnerability.
* `applicationId`: if included in this list, only results for these application IDs will be returned.
* `statusFilter`: if present, only results for vulnerabilities in these statuses will be returned
* `severityFilter`: if present, only results for vulnerabilities of these severities will be returned
* `titleFilter`: if present the vulnerability title will be partially-matched with this, it might make the query slower.
* `assignedToFilter`: if present, only vulnerabilities that have been assigned to the passed emails will be returned.
* `includeCalls`: true by default, this indicates that `securityEvents`, `blockedEvents` and `calls` will be returned as part of the results, omitting them might be beneficial if you do not need them as they slow a bit the query.
