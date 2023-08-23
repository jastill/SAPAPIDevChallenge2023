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