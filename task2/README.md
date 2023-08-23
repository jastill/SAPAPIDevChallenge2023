# Task 2

https://groups.community.sap.com/t5/application-development/sap-developer-challenge-apis-task-2-calculate-northbreeze/m-p/277325 

curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products?$top=5" \
  | jq '.value|.[].UnitsInStock'


This uses bc, caculator after using paste to create a long sum:

curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products?$top=5" \
  | jq '.value|.[] |select(.Discontinued == false)|.UnitsInStock' | paste -sd+ - | bc

  3018

This uses sum:

curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products?$top=5" \
  | jq '.value|.[] |select(.Discontinued == false)|.UnitsInStock' | sum

26175 1

hmmmm....o

This uses jq add

