# Task 3

https://groups.community.sap.com/t5/application-development/sap-developer-challenge-apis-task-3-have-a-northbreeze-product/m-p/277972#M2727

Simple POST with the response parsed and encoded with jq.

<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  -X POST "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/selectProduct" \
  --silent \
  -H "Content-Type: application/json" \
  -d '{"communityid":"johna69"}' | jq                
{
  "@odata.context": "$metadata#Edm.String",
  "value": "Guaraná Fantástica"
}
</pre>

Pull the value

<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  -X POST "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/selectProduct" \
  --silent \
  -H "Content-Type: application/json" \
  -d '{"communityid":"johna69"}' | jq '.value'       
"Guaraná Fantástica"
</pre>

Complete command with encoding
<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  -X POST "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/selectProduct" \
  --silent \
  -H "Content-Type: application/json" \
  -d '{"communityid":"johna69"}' | jq '.value | @uri'

  "Guaran%C3%A1%20Fant%C3%A1stica"
</pre>
