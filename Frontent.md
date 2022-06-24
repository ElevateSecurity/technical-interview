Build a Minimal Frontend App
=============================
The goal of this exercise is to create a minimalist frontend application that pulls data from a number of different APIs and then displays the consolidated information back out. For this exercise, you'll need to connect to mock security incident APIs as listed in the Incident Source endpoint section below. You'll build a frontend app that queries these service endpoints, normalizes the data, and merges / groups the results together.

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

Your task is to build a frontend app that queries each incident type via HTTP and returns a merged & grouped list of results attributed to each employee. How should the data be presented back to the user, you may ask? That is entirely up to you based on what you believe the end-user would gain the most value out of. We expect that the assignment will take about 2-3 hours to complete. Please reach out to us by email for questions.

Here are the requirements:

* Must query security incidents via HTTP
* Must group results by `employee_id`, and group incidents by priority level for each `employee_id`. Note: include the priority level even if the the incident count for that `(employee, priority level)` is 0 as demonstrated below in the example output (`low` priority is still included for employee 4506)
* Results should be sorted by incident timestamp (the incidents endpoint ```/incidents/<type>``` already returns incidents sorted by the timestamp - you can take advantage of this fact)
* New incidents should take at most an hour to be reflected in the results from your new endpoint.
* Must visualize results almost immediately (~ 1 second). Please note that the endpoints themselves take several seconds to return data, and might sometimes fail.

You can write the app in whichever language and whichever libraries/framework you feel most comfortable with and it should display the results back to the user.


We expect a **git repository with the source code of your solution**, containing a `README.md` file with the following information:
* Instructions on how to run
* Paragraph with overall approach and other approaches you considered
* Paragraph on how you would enhance this code if you needed it to run in production

**Good luck and most importantly, have fun!**