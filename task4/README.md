# Task 4

https://groups.community.sap.com/t5/application-development/sap-developer-challenge-apis-task-4-discover-the-date-and-time/m-p/278745

You should then write a script to parse the downloaded specification, to determine the API endpoints ("paths") that have both of the following properties:
the endpoint is accessible with the HTTP GET method
responses returned from the endpoint are in JSON

<pre>
jq '.paths|to_entries|select(.[].value.get != null)|select(.[].value.get.produces|any(index("application/json")) !=null )' <DateAndTime.json
</pre>


Stripping that down a little:

<pre>
jq '.paths|to_entries|select(.[].value.get != null)|.[].value.get.produces' <DateAndTime.json
</pre>

This gives us each of the entries, but the select seems to fail on a null/0 check!

<pre>
[
  "application/json"
]
[
  "application/json"
]
[
  "application/json"
]