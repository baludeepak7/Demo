	**O2**

	**SOA Service**

	**Specification**

	**ValidateCustomerAccount\_1\_0**

	**SOA Repository Number: 37200**

	Version 0.5

	ALL RIGHTS RESERVED

	This is an unpublished work. No part of this document may be copied,
	photocopied, reproduced, translated, or reduced to any electronic or
	machine-readable form without the prior permission of O2 Ltd.

	**DOCUMENT INFORMATION**

	|     Document   Author:        |     Service   Factory           |
	|-------------------------------|---------------------------------|
	|     Owner   while current:    |     SOAServiceFactory@o2.com    |
	|     Retention   period:       |     3 years                     |

	**CHANGE HISTORY**
	|     Version    |     Date             |     Changed   by            |     Changes                                                                                                                                                      |
	|----------------|----------------------|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
	|     0.1        |     14-Mar-2019      |     Shravan Urabinahatti    |     Initial version created                                                                                                                                      |
	|     0.2        |     28-Mar -2019     |     Shravan Urabinahatti    |     Incorporated SD comments                                                                                                                                     |
	|     0.3        |     15-April-2019    |     Dolly Khurana           |     Added   getSubscriberFraudAndDeceasedCheckStatus_1 operation as part of Ofcom   Consumer Switching project                                                   |
	|     0.4        |     26-May-2020      |     Apoorva   N             |     Updated   the document as part of the AO2 R3 Text to Switch                                                                                                  |
	|     0.5        |     12-Dec-2022      |     Akshay   Rajendra       |     Updated   the isSingleSubscriptionAccount_1 operation to return an additional element “isVIPCustomer”   in the response as part of Project EECC – Legacy.    |


	Service Overview
	================

	The SOA service ValidateCustomerAccount\_1\_0 allows to validate the
	customer account to verify if the account is a single subscription
	account or not.

	Namespaces
	----------

	|     Namespace URI                                        |     Prefix    |
	|----------------------------------------------------------|---------------|
	|     http://soa.o2.co.uk/validatecustomeraccountdata_1    |     vcd       |
	|     http://soa.o2.co.uk/coredata_1                       |     xcore     |
	|     http://www.w3.org/2001/XMLSchema                     |     xsd       |
	|     http://schemas.xmlsoap.org/wsdl/soap/                |     soap      |
	|     http://schemas.xmlsoap.org/wsdl/                     |     wsdl      |

	.

	isSingleSubscriptionAccount\_1
	------------------------------

	This operation can be used to validate whether the requested MSISDN is
	associated with the single subscription billing account or not. The
	operation currently supports prepay, postpay consumer and business
	customer requests.

	For the prepay MSISDN, the response will always be returned as single
	MSISDN account as PAYG only has the concept of a single MSISDN on an
	account and therefore no PPB call is required. For Consumer Postpay
	MSISDNs, the validation would be done for the account associated with
	the requested MSISDN. For Business MSISDNs, the validation would be done
	across the hierarchy (Group/Corporate/Account) of the customer account.

	Additionally, this operation returns “isVIPCustomer” flag in response for VIP Business MSISDN only when explicitly queried in request.

	For new stack, only consumer PAYM subscriber requests are supported by
	this operation.

	#### Input message: isSingleSubscriptionAccount\_1 

	|     Element                          |     Type                                             |     Occurrence    |     Description                                                                                        |
	|--------------------------------------|------------------------------------------------------|-------------------|--------------------------------------------------------------------------------------------------------|
	|     isSingleSubscriptionAccount_1    |     vcd:isSingleSubscriptionAccount_1   structure    |     1..1          |     The request container to accept the MSISDN which   must be validated for single msisdn account     |
	  

	#### Output message: isSingleSubscriptionAccount \_1Response

	|     Element Name                             |     Element Type                                 |     Occurrence    |     Description                                                     |
	|----------------------------------------------|--------------------------------------------------|-------------------|---------------------------------------------------------------------|
	|     isSingleSubscriptionAccount_1Response    |     vcd:isSingleSubscriptionAccount_1Response    |     1..1          |     The   response container for result of single MSISDN account    |


	#### Referenced faults

	|     Element Name                          |     Element Type          |     Occurrence    |     Description                                                                                                                                                           |
	|-------------------------------------------|---------------------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
	|     isSingleSubscriptionAccount_1Fault    |     xcore:SOAFaultType    |     NA            |     The back-end fault is wrapped into SOA fault as   defined in coredata. Other faults and policy exceptions may be defined for   this service during implementation.    |

	### Message/data security

	There is no sensitive data to be passed in the request and returned in
	the response for this operation. Hence there is no need to encrypt the
	data.

	### Caching

	This operation returns up-to date information that is present at the
	time of request i.e. information returned is not from a cache but rather
	from the actual system.

	### Timeout and retry

	This operation is idempotent. Upon timeout of a service request, the
	consuming application can safely retry.

	### Service Availability

	This operation is available 24/7 except during planned outage.

	### Error codes

	This operation returns errors or failures in the standard format as per
	xcore: SOAFaultType. The error codes and short descriptions are listed
	below.

	|     Error No                                 |     Error Description                                                                           |     Error Category    |     Description                                                                                                                                                           |
	|----------------------------------------------|-------------------------------------------------------------------------------------------------|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
	|     validatecustomeraccount -37200-4501-V    |     Invalid   Request. Please check the input and resubmit                                      |     Validation        |     The back-end fault is wrapped into SOA fault as   defined in coredata. Other faults and policy exceptions may be defined for   this service during implementation.    |
	|     validatecustomeraccount -37200-2501-F    |     One or more back end services are not available at the moment. Please   try again later.    |     Fatal             |                                                                                                                                                                           |
	|     validatecustomeraccount -37200-2502-F    |     Service call timed out. Please try again later.                                             |     Fatal             |                                                                                                                                                                           |
	|     validatecustomeraccount -37200-3000-E    |     Unable to retrieve the details for the input MSISDN                                         |     Error             |                                                                                                                                                                           |
	|     validatecustomeraccount -37200-3612-E    |     Internal service error has occurred.                                                        |     Error             |                                                                                                                                                                           |
	|     validatecustomeraccount-37200-3999-E     |     Unknown/Uncaught   error has occurred.                                                      |     Error             |                                                                                                                                                                           |



	### Sample messages

	***Sample request 1:***

	&lt;?xml version="1.0" encoding="UTF-8"?&gt;

	&lt;soapenv:Envelope
	xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"&gt;

	&lt;soapenv:Header&gt;

	PLEASE REFER TO 'O2 SOA Services - Consuming Applications Guide' FOR A
	LIST OF SOAP HEADERS TO BE SENT.

	&lt;/soapenv:Header&gt;

	&lt;/soapenv:Body&gt;

	&lt;vcd:isSingleSubscriptionAccount\_1

	xmlns:vcd="http://soa.o2.co.uk/validatecustomeraccountdata\_1"

	xmlns:xcore=<http://soa.o2.co.uk/coredata_1>
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

	xsi:schemaLocation="http://soa.o2.co.uk/validatecustomeraccountdata\_1
	validatecustomeraccountdata\_1\_0.xsd "&gt;

	&lt;vcd:msisdn&gt;+44709120009&lt;/vcd:msisdn&gt;

	&lt;/vcd:isSingleSubscriptionAccount\_1&gt;

	&lt;/soapenv:Body&gt;

	&lt;/soapenv:Envelope&gt;

	***Sample response:***

	&lt;?xml version="1.0" encoding="UTF-8"?&gt;

	&lt;soapenv:Envelope
	xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"&gt;

	&lt;soapenv:Header xmlns:cor="http://soa.o2.co.uk/coredata\_1"&gt;

	&lt;cor:SOATransactionID&gt;

	c96be514-3c99-4111-ac02-517a2bc5f92f

	&lt;/cor:SOATransactionID&gt;

	&lt;/soapenv:Header&gt;

	&lt;soapenv:Body xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

	&lt;vcd:isSingleSubscriptionAccount\_1Response

	xmlns:vcd="http://soa.o2.co.uk/validatecustomeraccountdata\_1"

	xmlns:xcore=<http://soa.o2.co.uk/coredata_1>
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

	xsi:schemaLocation="http://soa.o2.co.uk/validatecustomeraccountdata\_1
	validatecustomeraccountdata\_1\_0.xsd "&gt;

	&lt;vcd:msisdn&gt;+44709120009&lt;/vcd:msisdn&gt;

	&lt;vcd:isSingleSubcriptionAccount&gt;true&lt;/vcd:isSingleSubcriptionAccount&gt;

	&lt;vcd:subscriptionCount&gt;1&lt;/vcd:subscriptionCount&gt;

	&lt;/vcd:isSingleSubscriptionAccount\_1Response&gt;

	&lt;/soapenv:Body&gt;

	&lt;/soapenv:Envelope&gt;

	***Sample request 2: isVIPCustomer flag returned in response for VIP
	DISE MSISDN.***

	&lt;?xml version="1.0" encoding="UTF-8"?&gt;

	&lt;soapenv:Envelope
	xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"&gt;

	&lt;soapenv:Header&gt;

	PLEASE REFER TO 'O2 SOA Services - Consuming Applications Guide' FOR A
	LIST OF SOAP HEADERS TO BE SENT.

	&lt;/soapenv:Header&gt;

	&lt;/soapenv:Body&gt;

	&lt;vcd:isSingleSubscriptionAccount\_1

	xmlns:vcd="http://soa.o2.co.uk/validatecustomeraccountdata\_1"

	xmlns:xcore=<http://soa.o2.co.uk/coredata_1>
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

	xsi:schemaLocation="http://soa.o2.co.uk/validatecustomeraccountdata\_1
	validatecustomeraccountdata\_1\_0.xsd "&gt;

	&lt;vcd:msisdn&gt;+44709120009&lt;/vcd:msisdn&gt;

	&lt;vcd: retrieveAdditionalInfo&gt;vipCustomer&lt;/vcd:
	retrieveAdditionalInfo&gt;

	&lt;/vcd:isSingleSubscriptionAccount\_1&gt;

	&lt;/soapenv:Body&gt;

	&lt;/soapenv:Envelope&gt;

	***Sample response:***

	&lt;?xml version="1.0" encoding="UTF-8"?&gt;

	&lt;soapenv:Envelope
	xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"&gt;

	&lt;soapenv:Header xmlns:cor="http://soa.o2.co.uk/coredata\_1"&gt;

	&lt;cor:SOATransactionID&gt;

	c96be514-3c99-4111-ac02-517a2bc5f92f

	&lt;/cor:SOATransactionID&gt;

	&lt;/soapenv:Header&gt;

	&lt;soapenv:Body xmlns:xsd="http://www.w3.org/2001/XMLSchema"&gt;

	&lt;vcd:isSingleSubscriptionAccount\_1Response

	xmlns:vcd="http://soa.o2.co.uk/validatecustomeraccountdata\_1"

	xmlns:xcore=<http://soa.o2.co.uk/coredata_1>
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

	xsi:schemaLocation="http://soa.o2.co.uk/validatecustomeraccountdata\_1
	validatecustomeraccountdata\_1\_0.xsd "&gt;

	&lt;vcd:msisdn&gt;+44709120009&lt;/vcd:msisdn&gt;

	&lt;vcd:isSingleSubcriptionAccount&gt;true&lt;/vcd:isSingleSubcriptionAccount&gt;

	&lt;vcd:subscriptionCount&gt;1&lt;/vcd:subscriptionCount&gt;

	&lt;vcd:isVIPCustomer&gt;true&lt;/vcd:isVIPCustomer&gt;

	&lt;/vcd:isSingleSubscriptionAccount\_1Response&gt;

	&lt;/soapenv:Body&gt;

	&lt;/soapenv:Envelope&gt;

	***Sample fault:***

	&lt;?xml version="1.0" encoding="UTF-8"?&gt;

	&lt;soapenv:Envelope
	xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"&gt;

	&lt;soapenv:Header

	xmlns:cor="http://soa.o2.co.uk/coredata\_1"&gt;

	&lt;cor:SOATransactionID&gt;

	> bdd9d407-ef6d-4b9b-9853-08335cb83ddd
	>
	> &lt;/cor:SOATransactionID&gt;

	&lt;/soapenv:Header&gt;

	&lt;soapenv:Body

	xmlns:cor="h[tp://soa.o2.co.uk/coredata\_1"](tp://soa.o2.co.uk/coredata_1%22%20)
	mlns:vcd="http://soa.o2.co.uk/ validatecustomeraccountdata\_1"&gt;

	&lt;soapenv:Fault&gt;

	&lt;faultcode
	xmlns:env="http://schemas.xmlsoap.org/soap/envelope"&gt;env:Server&lt;/faultcode&gt;

	&lt;faultstring&gt;

	Unknown/Uncaught error has occurred.

	&lt;/faultstring&gt;

	&lt;detail&gt;

	&lt;scd:isSingleSubsriptionAccount\_1Fault

	> xmlns:vcd="http://soa.o2.co.uk/validatecustomeraccountdata\_1"
	>
	> xmlns:xcore="ht[p://soa.o2.co.uk/coredata\_1"
	> x](p://soa.o2.co.uk/coredata_1%22%20x)lns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	>
	> xsi:schemaLocation="http://soa.o2.co.uk/validatecustomeraccountdata\_1
	> sendcampaignnotificationdata\_1\_0.xsd "&gt;
	>
	> &lt;xcore:SOAFaultOriginator&gt;
	>
	> xcore:SOAFaultOriginator
	>
	> &lt;/xcore:SOAFaultOriginator&gt;
	>
	> &lt;xcore:SOAFaultCode&gt;
	>
	> validatecustomeraccount-37200-3999-E

	&lt;/xcore:SOAFaultCode&gt;

	&lt;xcore:faultDescription&gt;

	> Unknown/Uncaught error has occurred.
	>
	> &lt;/xcore:faultDescription&gt;
	>
	> &lt;xcore:faultTrace&gt;
	>
	> xcore:faultTrace

	&lt;/xcore:faultTrace&gt;

	> &lt;xcore:SOATransactionID&gt;
	>
	> bdd9d407-ef6d-4b9b-9853-08335cb83ddd

	&lt;/xcore:SOATransactionID&gt;

	> &lt;/scd:isSingleSubscriptionAccount\_1Fault&gt;

	&lt;/detail&gt;

	&lt;/soapenv:Fault&gt;

	&lt;/soapenv:Body&gt;

	&lt;/soapenv:Envelope&gt;

	XML SCHEMA DATA TYPE DEFINITION
	-------------------------------

	### isSingleSubscriptionAccount\_1 structure

	  |     Element                   |     Type                                 |     Occurrence    |     Description                                                                                                                |
	|-------------------------------|------------------------------------------|-------------------|--------------------------------------------------------------------------------------------------------------------------------|
	|     msisdn                    |     xcore:msisdnType                     |     1..1          |     Customer   msisdn in international format.                                                                                 |
	|     retrieveAdditionalInfo    |     xcore: retrieveAdditionalInfoType    |     0..1          |     This is an optional element which can be used   query the additional information like details of VIP (DISE) customers.     |

	### isSingleSubscriptionAccount\_1Response Structure

	  |     Element   Name                |     Element   Type      |     Occurrence    |     Description                                                                                                                             |
	|-----------------------------------|-------------------------|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
	|     msisdn                        |     xcore:msisdnType    |     1..1          |     Customer   msisdn in international format.                                                                                              |
	|     isSingleSubcriptionAccount    |     xsd:boolean         |     1..1          |     The status if the msisdn is a   single msisdn billing account or not.     Note: For Prepay MSISDN’s   this value will always be true    |
	|     subscriptionCount             |     xsd:integer         |     1..1          |     The subscription count i.e. the   count of subscriptions/MSISDN’s on the billing account                                                |
	|     isVIPCustomer                 |     xsd:boolean         |     0..1          |     This element indicates if   Business customer is a VIP(DISE).                                                                           |

	### subscriberDetailsType Structure

	  |     Element   Name      |     Element   Type              |     Occurrence    |     Description                          |
	|-------------------------|---------------------------------|-------------------|------------------------------------------|
	|     subscriberDetail    |     vcd:subscriberDetailType    |     1..3          |     Subscriber Detail for a customer.    |

	### subscriberDetailType Structure

	  |     Element   Name    |     Element   Type         |     Occurrence    |     Description                                                               |
	|-----------------------|----------------------------|-------------------|-------------------------------------------------------------------------------|
	|     segment           |     xcore:segment_2Type    |     1..1          |     The Segement type      PAYM_CON - For Postpay Consumer Customers          |
	|     msisdn            |     xcore:msisdnType       |     1..*          |     Customer msisdn in international format.                                  |


	### errorDetailType Structure

	  |     Element   Name      |     Element   Type    |     Occurrence    |     Description                                                      |
	|-------------------------|-----------------------|-------------------|----------------------------------------------------------------------|
	|     errorCode           |     xsd:string        |     1..1          |     Error Code                                                       |
	|     errorDescription    |     xsd:string        |     1..1          |     Error description which tells the reason of error   occurred.    |


	### additinalInfoType Structure

	  |     Element   Name    |     Element   Type    |     Occurrence    |     Description                               |
	|-----------------------|-----------------------|-------------------|-----------------------------------------------|
	|     customerId        |     xsd:string        |     0..1          |     Customer Id for the requested msisdn.     |


	### retrieveAdditionalInfoType Structure
	|     Element   Name    |     Element   Type    |     Occurrence    |     Description                                                                                                                                                                     |
	|-----------------------|-----------------------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
	| parameterName         | xsd:string            | 1..*              | isSingleSubscriptionAccount_1 operation allowed value(s): •vipCustomer  																										      |
	|						|						|					| Note : The parmaterName is case sensitive 																																		  |
																		| Note : The parmaterName is case sensitive 																																		  |
