# Task 0

Practice and play around with CURL


➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --include \
  --header "CommunityID: johnastill" \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/v1/hash(value='this-is-the-year-of-the-api')"
HTTP/2 200 
content-type: text/plain; charset=utf-8
date: Tue, 22 Aug 2023 14:58:08 GMT
etag: W/"40-IZJKKqeJ616gkdZQRWUNNQDaBv0"
x-correlation-id: 4e9f80d2-8449-4161-7b38-c566d94b0c09
x-powered-by: Express
x-vcap-request-id: 4e9f80d2-8449-4161-7b38-c566d94b0c09
content-length: 64
strict-transport-security: max-age=31536000; includeSubDomains; preload;

74c4fcad15573feaea6278ed2a76f8dc5838f3927b080bf210236b97efbfe75b%   

Let's try with the correct community id.

<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗  curl \
  --include \
  --header "CommunityID: johna69" \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/v1/hash(value='this-is-the-year-of-the-api')"
HTTP/2 200 
content-type: text/plain; charset=utf-8
date: Wed, 23 Aug 2023 11:18:40 GMT
etag: W/"40-QYqlnahYEPi2Xjkc7X89BTzzJ9s"
x-correlation-id: c88352ee-7507-4e51-693a-402d7ae25d6e
x-powered-by: Express
x-vcap-request-id: c88352ee-7507-4e51-693a-402d7ae25d6e
content-length: 64
strict-transport-security: max-age=31536000; includeSubDomains; preload;

040cc7ca1dbc73fab0350dc28a047b5d649995cbd082711085b6d9f4b0cb3918%   
</pre>