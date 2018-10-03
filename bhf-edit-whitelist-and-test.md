# EDIP Proxy - Re-writing URLs
All traffic between iPipeline and MRAS must be routed through EDIP proxy hosted at BHF. Here are the steps needed to implement - _<responsible>_ indicates who is responsible for this step.
1. Requests from iPipeline to MRAS endpoints will be directed to the EDIP Proxy. ___<iPipeline>___ 
2. MRAS response content containing references to MRAS resources for access by iPipeline must be re-written to point to the equivalent EDIP Proxy URL. This includes URLs in **_all response content_** including HTML and Javascript. ___<Brighthouse>___
2.1 For example, IF01 response sent by MRAS to iPipeline containing the MRAS URL to the content iPipeline will embed in an iFrame will need to be re-written to point to the EDIP proxy. ___<Brighthouse>___

# EDIP Proxy - Whitelist
---
Must be accessible from the Internet:
```
 ais/screens/*
 ais/bootstrap/*
 ais/images/*
 ais/html/*
 ais/css/*
 ais/js/*
```
Must be accessible from BHF:
```
 ais/ais-tools/*
 ais/ais-admin/*
 ais/uwb/*
```
Must be accessible from iPipeline:
```
 ais/jaxws/*
 ais/services/*
```

# Suggested EDIP Proxy Test Procedure (for BHF)
----
* Test web service endpoints with WSDL
  * https://<edip_proxy>:port/allfinanz/services/IF01.wsdl
  * https://<edip_proxy>:port/allfinanz/services/IF02.wsdl
* Send IF01 Request
  * Install Smartbear SoapUI - the Free version in fine! 
  * Send sample IFO1 request to AIS 
  * Verify IF01 response received
* Send IF02 Request
  * Extract redirect URL from IF01 response _(Note: Not currently set - contact Paul.)_
  * Paste into browser
  * Test Tele-interview sceens
  * Complete Tele-interview 
    * Will get page re-direct error as no iGo URL available yet.
* Send IF02 Request
  * Verify vIF02 response received

# BHF Requested Information
----
|Item |Following * 2 (one set each for source & target)        | |
|-----|--------------------------------------------------------|-|
|1	  |URLs to connect	                                       |Connnection URLs from iPipeline to AIS|
|     |                                                        |https://<hostname>:<port>/<context>/services/IF01|
|     |                                                        |https://<hostname>:<port>/<context>/services/IF02|
|     |                                                        |Connnection URLs from Internet to AIS|
|     |                                     |https://<hostname>:<port>/<context>/screens/externalOpenCase|
|     |                                     |For example, System Integration Testing (SIT) Environment URL:|
|     |                                     |https://bhf-01-ais-sit-pub.allfinanz.com/allfinanz/services/IF01|
|     |                                     |https://bhf-01-ais-sit-pub.allfinanz.com/allfinanz/services/IF02|
|     |                                     |https://bhf-01-ais-sit-pub.allfinanz.com/allfinanz/screens/externalOpenCase
|     |                                     |Public access via Internet as part of iPipeline Plan B
|2	  |Credentials to connect/connection pattern|	HTTPS
|3	  |Sample Payload (request & response)|	attached IF01 / IF02 request / response samples
|4    |Interface Requirements / Definition Document (IRD) from Source & target each|"https://bhf-01-ais-sit-pub.allfinanz.com/allfinanz/services/IF01.wsdl
|     |                                     |https://bhf-01-ais-sit-pub.allfinanz.com/allfinanz/services/IF02.wsdl"
|5	  |Types of responses - synchronous or asynchronous	|Synchronous
|6	  |Success & failure responses	|See attached. Note that these are samples only.
|7	  |Carrier ID	|None
|8	  |API key	|None
|9	  |Algorithm for generation of HMAC	|None
|10	  |Secret key to hash content	|None
|11	  |Header elements to be set up for API calls |None
