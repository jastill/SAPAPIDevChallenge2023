
# Task 7 - Create a new directory in an SAP BTP account

<pre>
➜  task4 git:(main) ✗ btp get accounts/directory 555fe68d-29fc-4cab-ba2f-329d823e0407
Showing details for directory 555fe68d-29fc-4cab-ba2f-329d823e0407...

directory id:         xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
display name:         developer-challenge
description:          
directory features:   DEFAULT
created by:           xxxxxx@xxxx.xx
custom properties:    name:   value:   
                      task    7        
labels:               name:   value:   
                      task    [7]      
parent id:            xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
parent type:          global account
state:                OK
state message:        Directory created.
</pre>

<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \                                                         
  --include \
  --header "CommunityID: johnastill" \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/v1/hash(value='7')"
HTTP/2 200 
content-type: text/plain; charset=utf-8
date: Tue, 22 Aug 2023 15:02:48 GMT
etag: W/"40-YwC1Jq4OmennYxMQjOaZk27hUyY"
x-correlation-id: f00ce129-d239-4238-4db1-0b962511ca5f
x-powered-by: Express
x-vcap-request-id: f00ce129-d239-4238-4db1-0b962511ca5f
content-length: 64
strict-transport-security: max-age=31536000; includeSubDomains; preload;

152c5580a22889df1e531729c75674ebf347dd174a268b363c5f3cb9c6926aa0%   
</pre>


And once again use the right community id

<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗  curl \                                                         
  --include \
  --header "CommunityID: johna69" \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/v1/hash(value='7')"
HTTP/2 200 
content-type: text/plain; charset=utf-8
date: Wed, 23 Aug 2023 11:26:52 GMT
etag: W/"40-H2I6pUuQ3gB1yb8YXEIlTYGaHso"
x-correlation-id: ef623a0b-ac28-4a23-4752-5c40eb60bc69
x-powered-by: Express
x-vcap-request-id: ef623a0b-ac28-4a23-4752-5c40eb60bc69
content-length: 64
strict-transport-security: max-age=31536000; includeSubDomains; preload;

c92127d77c5bc18545bc499ef1ac397f615a3593ed73ffe8876e72c8c957ce84% 
</pre>