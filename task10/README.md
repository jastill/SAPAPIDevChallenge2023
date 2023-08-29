# Task 10 - Request an OAuth access token

And just to remind you of where you are in this group of tasks, you've now done steps 1 and 2 of the steps introduced in Task 8. This time you're tackling step 3.
create an instance of the SAP Cloud Management Service, with a plan that contains the appropriate scope(s) that you need ✅
create a service key based on that instance ✅
use the details in the service key to request an access token
use the access token thus obtained to authenticate a call to the API endpoint

From help [documentation](https://help.sap.com/docs/btp/sap-business-technology-platform/getting-access-token-for-sap-cloud-management-service-apis)

## Sample Password Grant Type

<pre>
curl -L -X POST '<uaa_url>/oauth/token' \ 
-H 'Content-Type: application/x-www-form-urlencoded' \ 
-u '<clientid>:<clientsecret>' \ 
-d 'grant_type=password' \ 
-d 'username=<user email>' \
-d 'password=<password>'
</pre>

## Client Credentials Grant Type
<pre>
curl -L -X POST '<uaa_url>/oauth/token' \ 
-H 'Content-Type: application/x-www-form-urlencoded' \ 
-u '<clientid>:<clientsecret>' \ 
-d 'grant_type=client_credentials' \ 
</pre>

We want to use the Password Grant Type

<pre>
curl -L -X POST https://<uaa>.authentication.eu10.hana.ondemand.com/oauth/token -H 'Content-Type: application/x-www-form-urlencoded' -u '<clientid>:<secret>' -d 'grant_type=password' -d 'username=<emailAddress>' -d 'password=<password>' | jq '.expires_in/3600 | ceil'

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  6849    0  6776  100    73  10961    118 --:--:-- --:--:-- --:--:-- 11154
12
</pre>