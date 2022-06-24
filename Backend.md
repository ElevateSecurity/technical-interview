Build a Security Incident API
=============================
A security incident is an event that may indicate unauthorized access, use, disclosure, modification, or destruction of information, implying an organization's systems or data may have been compromised. The sources for these incidents may come from various services, and the data itself is often represented differently across these services. In this problem, you'll build an API that queries these service endpoints, normalizes the data, and merges / groups the results together.

Getting Started
===============

For this problem, the various services mentioned above will be served by a mock server available on `https://incident-api.use1stag.elevatesecurity.io`.

### Authentication

The provided API mock is protected by Basic Auth authentication, the username and password should have been delivered as part of the assignment, please contact us if you did not get the credentials or have trouble accessing the API.

The server supports two main endpoints:

### Incident source endpoints

* ```GET /incidents/<type>``` - returns incidents for the specified incident `<type>`. These are the incident types:
  * `denial`: https://incident-api.use1stag.elevatesecurity.io/incidents/denial/
  * `intrusion`: https://incident-api.use1stag.elevatesecurity.io/incidents/intrusion/
  * `executable`: https://incident-api.use1stag.elevatesecurity.io/incidents/executable/
  * `misuse`: https://incident-api.use1stag.elevatesecurity.io/incidents/misuse/
  * `unauthorized`: https://incident-api.use1stag.elevatesecurity.io/incidents/unauthorized/
  * `probing`: https://incident-api.use1stag.elevatesecurity.io/incidents/probing/
  * `other`: https://incident-api.use1stag.elevatesecurity.io/incidents/other/

Each incident has an identity (in some form), timestamp, and priority level associated with it somewhere in its data (among other fields), which you will use later to sort and group your results. There are 4 priority levels ```low```, ```medium```, ```high```, and ```critical```.

### Identity endpoint

In some cases, a incident may represent an identity as an IP Address instead of an employee ID; the following endpoint returns an `IP Address` -> `employee_id` mapping so that you can make that conversion when producing your results.

* ```GET /identities``` - returns a mapping from `IP Address` to `employee_id` for all employees

Feel free to play around with the endpoints to better understand the format of the responses.

Problem
=======

Your task is to build an API that queries each incident type via HTTP and returns a merged & grouped list of results attributed to each employee. We expect that the assignment will take about 2-3 hours to complete. Please reach out to us by email for questions.

Here are the requirements:

* Must query security incidents via HTTP
* Must group results by `employee_id`, and group incidents by priority level for each `employee_id`. Note: include the priority level even if the the incident count for that `(employee, priority level)` is 0 as demonstrated below in the example output (`low` priority is still included for employee 4506)
* Results should be sorted by incident timestamp (the incidents endpoint ```/incidents/<type>``` already returns incidents sorted by the timestamp - you can take advantage of this fact)
* New incidents should take at most an hour to be reflected in the results from your new endpoint.
* Must return results almost immediately (~ 1 second). Please note that the endpoints themselves take several seconds to return data, and might sometimes fail.

You can write the API in whichever language and whichever libraries/framework you feel most comfortable with, and it should expose a single endpoint on port 9000:

* ```GET /incidents``` - returns all types of incidents sorted by timestamp and grouped by employee and priority level for each employee.

The output should be formatted as such:

```
{
    "4506": {
        "low": {
            "count": 0,
            "incidents": []
        }
        "medium": {
            "count": 3,
            "incidents": [
                {
                "type": "executable"
                "priority": "medium",
                "machine_ip": "17.99.238.86",
                "timestamp": 1500020421.9333,
                }
                ...
            ]
        }
        "high": {
            ...
        }
        ...
    },
    "9704": {
        "low": {
            "count": 10,
            "incidents": [
                {
                    ...
                },
                ...
            ]
        }
    },
    ...
}
```

We expect a **git repository with the source code of your solution**, containing a `README.md` file with the following information:
* Instructions on how to run
* Paragraph with overall approach and other approaches you considered
* Paragraph on how you would enhance this code if you needed it to run in production

**Good luck and most importantly, have fun!**