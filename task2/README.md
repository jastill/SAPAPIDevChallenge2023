# Task 2

https://groups.community.sap.com/t5/application-development/sap-developer-challenge-apis-task-2-calculate-northbreeze/m-p/277325 

<pre>
curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products?$top=5" \
  | jq '.value|.[].UnitsInStock'
</pre>

This uses bc, caculator after using paste to create a long sum:

<pre>
curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products?$top=5" \
  | jq '.value|.[] |select(.Discontinued == false)|.UnitsInStock' | paste -sd+ - | bc

  3018
</pre>

Is it wrong I find this output somewhat satisfying:
<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products?$top=5" \
  | jq '.value|.[] |select(.Discontinued == false)|.UnitsInStock' | paste -sd+ -
39+17+13+53+120+15+6+31+22+86+24+35+39+29+42+25+40+3+104+61+76+15+49+10+0+9+112+111+20+112+11+17+69+123+85+17+27+5+95+36+15+10+65+20+38+21+115+21+36+62+79+19+113+17+24+22+76+4+52+6+26+15+26+14+101+4+125+57+32
</pre>

This uses sum:

<pre>
curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products?$top=5" \
  | jq '.value|.[] |select(.Discontinued == false)|.UnitsInStock' | sum

26175 1
</pre>

hmmmm...., something is amiss. sum is not what stackoverflow users suggested it was....

<pre>
NAME
     cksum, sum – display file checksums and block counts

SYNOPSIS
     cksum [-o 1 | 2 | 3] [file ...]
     sum [file ...]

DESCRIPTION
     The cksum utility writes to the standard output three whitespace separated fields for each input file.  These fields are a checksum CRC, the total number of octets in the file and the file name.
     If no file name is specified, the standard input is used and no file name is written.

     The sum utility is identical to the cksum utility, except that it defaults to using historic algorithm 1, as described below.  It is provided for compatibility only.

     The options are as follows:

     -o      Use historic algorithms instead of the (superior) default one.

             Algorithm 1 is the algorithm used by historic BSD systems as the sum(1) algorithm and by historic AT&T System V UNIX systems as the sum(1) algorithm when using the -r option.  This is a
             16-bit checksum, with a right rotation before each addition; overflow is discarded.
</pre>

A little awk (a long time since I've used awk):

<pre>
  ➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products?$top=5" \
  | jq '.value|.[] |select(.Discontinued == false)|.UnitsInStock'|awk '{s+=$1} END {print s}'
3018
</pre>

It has been pointed out that I have left the odata $top=5 in the url..... 

<pre>
... would return ALL the products (which is actually what you want anyway), not the top 5, because inside double quotes, variables are expanded, i.e. the Products?$top=5 part is expanded into just Products?=5 , i.e. $top would 'disappear' :-)
</pre>

Which gives us :

<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products" \ 
  | jq '.value|.[] |select(.Discontinued == false)|.UnitsInStock' | paste -sd+ - | bc
3018
</pre>

Now to try with jq add.... initial attempts failed as the input to add was not an arry of values..

<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗ curl \
  --silent \
  --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/odata/v4/northbreeze/Products" \
  | jq '.value|[.[] |select(.Discontinued == false)|.UnitsInStock]| add'
3018
</pre>

[map](https://jqlang.github.io/jq/manual/) can be used to replace <pre>[.[]|f]</pre> and is a cleaner solution

<pre>
➜  SAPAPIDevChallenge2023 git:(main) ✗ curl --include --header "CommunityID: johna69" --url "https://developer-challenge.cfapps.eu10.hana.ondemand.com/v1/hash(value='3018')" 
HTTP/2 200 
content-type: text/plain; charset=utf-8
date: Wed, 23 Aug 2023 12:13:33 GMT
etag: W/"40-1+u++FQXxmDM2940LVohynLWEqI"
x-correlation-id: efdab279-f591-4712-59f6-f31ee6659c42
x-powered-by: Express
x-vcap-request-id: efdab279-f591-4712-59f6-f31ee6659c42
content-length: 64
strict-transport-security: max-age=31536000; includeSubDomains; preload;

2501c9e941c7b5b1592d69fe59c284781bc83b560ef449b984ab7adc1a0e097a%  
</pre>