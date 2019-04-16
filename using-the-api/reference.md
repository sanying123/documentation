## Summary

This API aims at allowing access to each of your organization’s vulnerabilities and runtime information on them.

The main piece of security information in ShiftLeft is called a Vulnerability, it represents a potentially exploitable path in your code base, this API allows you to get said vulnerabilities for all of the versions of all the applications in your organization,

### Data
The various queries on this API will return Vulnerabilities which contain all the necessary data for you to take action on a code exploitable area.

### A Vulnerability

```json
       {
           "applicationId": "project1549413585aa",
           "vulnerability": {
               "vulnerabilityId": "database-write/e0ec210246d63ea44e28c01ed6113a66",
               "category": "a1-injection",
               "title": "Unsanitized database write in `DataLoader.run`",
               "description": "Attacker-controlled data is used in a database query without any sanitation or encoding. This could be intended behavior and thus has a low score. Injection flaws, such as SQL, NoSQL, OS, and LDAP injection, occur when untrusted data is sent to an interpreter as part of a command or query. By injecting hostile data, an attacker may trick the interpreter into executing unintended commands or accessing data without proper authorization which can result in data loss, corruption, or disclosure to unauthorized parties, loss of accountability, denial of access or even a complete host takeover.",
               "score": 1,
               "severity": "LOW_IMPACT",
               "securityEvents": "1",
               "calls	": "1",
               "blockedEvents": "1",
               "locationURL": "/account/{accountId}/addInterest",
               "locationMethod": "addInterest",
               "status": "fixed",
               "assignedTo": "example@shiftleft.io",
           }
       },
```


* `projectId`: A unique identification string per project within your organization
* `vulnerability`:
	*  `vulnerabilityId`: An unique id for this particular vulnerability, it is unique accross all organization.
	*  `category`: an OWASP category in which this vulnerability fits?
	*  `title`: a friendly title for this vulnerability
	*  `description`: a more complete description of this vulnerability.
	*  `score`: a float score from 1-9 representing the OWASP severity of this vulnerability
	*  `severity`: one of `LOW_IMPACT`, `MEDIUM_IMPACT`, `HIGH_IMPACT` which are the levels ShiftLeft assigns according to score.
	*  `securityEvents `: an integer containing the amount of incidents to the vulnerable endpoint, this counts.
	*  `blockedEvents `: an integer containing the amount of blocked incidents to the vulnerable endpoint, this counts.
	*  `calls `: the amount of total hits to the vulnerable endpoints (including the ones that are not necesarily attacks.
	*  `locationURL `: where the affected endpoint is published.
	*  `locationMethod `: the method affected by this vulnerability.
	*  `status`: a status set throught the ShiftLeft UI
	*  `assignedTo`: if this vulnerability is assigned to someone the field will be set to that person's email.
	
A vulnerability is found on an Application through analysis and can be in various versions of the same Application, our API will allow you to slice the applications of your organization in various dimansions to obtain the data you need:

### Pagination

Our endpoints are always paginated, given the amount of results possibles for any query we offer our results in pages of 50 at a time with pagination information along each response, additionally we clasify results in 3 groups according to severity:

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

### Organization vulnerabilities

The outmost endoints allows querying/filtering for vulnerabilities at an organization level:

POST `/api/v3/public/organizations/{organization id}/vulnerabilities/`

This will result on a default query returning vulnerabilities with the following criteria:

* Belonging to the latest analyzed version of any app.
* Of any Severity
* Of any category
* With Any Description
* With or without traffic
* With or without blocked incidents.
* Arbitrarily sorted
* Only the first page (50 results)

To obtain an arbitrary page 

POST `/api/v3/public/organizations/{organization id}/vulnerabilities/page/{page number}`

if the page is outside of the possible range you will obtain an empty result set.

#### Filtering

The filtering criteria can be passed in the body of the query:

```json
{
        "orderBy": "severity",
        "orderByDirection": "DESC",
        "applicationId": [
            "project1549413585aa"
        ],
        "statusFilter": [
            "fixed", "assigned"
        ],
        "severityFilter": [],
        "titleFilter": "",
        "assignedToFilter": [],
        "includeTraffic": true
    }
},
```

* `orderBy`: the response field used to sort the results, can be any of the vulnerability fields.
* `orderByDirection`: either `DESC` or `ASC` will be applied to the `orderBy` field.
* `applicationId`: if included in this list, only results for these application IDs will be returned.
* `statusFilter`: if present, only results for vulnerabilities in these statuses will be returned
* `severityFilter`: if present, only results for vulnerabilities of these severities will be returned
* `titleFilter`: if present the vulnerability title will be partially-matched with this, it might make the query slower.
* `assignedToFilter`: if present, only vulnerabilities that have been assigned to the passed emails will be returned.
* `includeTraffic`: true by default, this indicates that `incidentCount` and `trafficCount` will be returned as part of the results, omitting them might be beneficial if you do not need them as they slow a bit the query.

## Application vulnerabilities

Application level vulnerabilities is an endpoint that allows you to perform the exact same kind of query than for Organizations but it limits results displayed to one Application.

POST `/api/v3/public/organizations/{organization id}/application/{application id}/vulnerabilities/`

This will result on a default query returning vulnerabilities with the following criteria:

* Belonging to the latest analyzed version this app.
* Of any Severity
* Of any category
* With Any Description
* With or without traffic
* With or without blocked incidents.
* Arbitrarily sorted
* Only the first page (50 results)

To obtain an arbitrary page 

POST `/api/v3/public/organizations/{organization id}/application/{application id}/vulnerabilities/page/{page number}`

To obtain an arbitrary version (also supports `/page/{page number}` at the end)

POST `/api/v3/public/organizations/{organization id}/application/{application id}/version/{version}/vulnerabilities`

if the page is outside of the possible range you will obtain an empty result set.

#### Filtering

The filtering criteria can be passed in the body of the query:

```json
{
        "orderBy": "severity",
        "orderByDirection": "DESC",
        "statusFilter": [
            "fixed", "assigned"
        ],
        "severityFilter": [],
        "titleFilter": "",
        "assignedToFilter": [],
        "includeTraffic": true
    }
},
```

* `orderBy`: the response field used to sort the results, can be any of the vulnerability fields.
* `orderByDirection`: either `DESC` or `ASC` will be applied to the `orderBy` field.
* `applicationId`: if included in this list, only results for these application IDs will be returned.
* `statusFilter`: if present, only results for vulnerabilities in these statuses will be returned
* `severityFilter`: if present, only results for vulnerabilities of these severities will be returned
* `titleFilter`: if present the vulnerability title will be partially-matched with this, it might make the query slower.
* `assignedToFilter`: if present, only vulnerabilities that have been assigned to the passed emails will be returned.
* `includeTraffic`: true by default, this indicates that `incidentCount` and `trafficCount` will be returned as part of the results, omitting them might be beneficial if you do not need them as they slow a bit the query.