# Task 9 - Create a service key for API endpoints and auth info

<pre>

</pre>

<pre>
jq '.credentials.endpoints|keys|join(",")' < service_key
</pre>

<pre>
cf service-key cis cis_key | sed 1,2d | jq '.credentials.endpoints|keys|join(",")' | sed "s/\"//g"
</pre>