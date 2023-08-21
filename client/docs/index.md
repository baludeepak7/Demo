**O~2~**

**SOA Service**

**Specification**

**ValidateCustomerAccount\_1\_0**

**SOA Repository Number: 37200**

Version 0.5

ALL RIGHTS RESERVED

This is an unpublished work. No part of this document may be copied,
photocopied, reproduced, translated, or reduced to any electronic or
machine-readable form without the prior permission of O2 Ltd.

INTELLECTUAL PROPERTY RIGHTS

**IPRs essential or potentially essential to the present document may
have been declared to O2. The information pertaining to these essential
IPRs, if any, is publicly available for O2 Partners and non-partners,
and can be obtained on application through the O2 Partner Management
process\
**[[[[]{#_Toc159915941 .anchor}]{#_Toc156645503 .anchor}]{#_Toc153600109
.anchor}]{#_Toc153595979 .anchor}**DOCUMENT INFORMATION**

  -------------------------- ----------------------------
  **Document Author:**       Service Factory
  **Owner while current:**   <SOAServiceFactory@o2.com>
  **Retention period:**      3 years
  -------------------------- ----------------------------

[[[[[[[[[[]{#_Toc6395708 .anchor}]{#_Toc159915942
.anchor}]{#_Toc156645504 .anchor}]{#_Toc153600110
.anchor}]{#_Toc153595980 .anchor}]{#_Toc6395709 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}CHANGE HISTORY

  ------------- --------------- ---------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------
  **Version**   **Date**        **Changed by**         **Changes**
  0.1           14-Mar-2019     Shravan Urabinahatti   Initial version created
  0.2           28-Mar -2019    Shravan Urabinahatti   Incorporated SD comments
  0.3           15-April-2019   Dolly Khurana          Added getSubscriberFraudAndDeceasedCheckStatus\_1 operation as part of Ofcom Consumer Switching project
  0.4           26-May-2020     Apoorva N              Updated the document as part of the AO2 R3 Text to Switch
  0.5           12-Dec-2022     Akshay Rajendra        Updated the isSingleSubscriptionAccount\_1 operation to return an additional element “isVIPCustomer” in the response as part of Project EECC – Legacy.
  ------------- --------------- ---------------------- --------------------------------------------------------------------------------------------------------------------------------------------------------

RELATED DOCUMENTS

  -------- ------------------------------------------------ ------------- ---------------------------
  **ID**   **Name**                                         **Version**   **Description**
  1        AO2 Release 3 BSS Transformation Service Model   1.7           Service Model
  2        NC.O2.INT Telecom Business API Specification     0.22          NC Specification document
  -------- ------------------------------------------------ ------------- ---------------------------

[[[[[]{#_Toc6395710 .anchor}]{#_Toc159915945 .anchor}]{#_Toc156645507
.anchor}]{#_Toc153600113 .anchor}]{#_Toc153595983 .anchor}DESIGN
GOVERNANCE SIGN-OFF

  --------------- --------------- ----------- --
  **Name:**       Rajesh Kota
  **Role:**       SOA Architect
  **APPROVED:**   YES NO
  --------------- --------------- ----------- --

[[[[[]{#_Toc6395711 .anchor}]{#_Toc159915946 .anchor}]{#_Toc156645508
.anchor}]{#_Toc153600114 .anchor}]{#_Toc153595984 .anchor}ADDITIONAL
APPROVAL SIGNATORIES

  ----------------------- ------------------------- -------------- ----------
  **Name**                **Role**                  **Approved**   **Date**
  Apostolidis Apostolos   Solution Designer – AO2   YES NO         
  ----------------------- ------------------------- -------------- ----------

Contents

[CHANGE HISTORY 2](#_Toc6395708)

[RELATED DOCUMENTS 2](#_Toc6395709)

[DESIGN GOVERNANCE SIGN-OFF 2](#_Toc6395710)

[ADDITIONAL APPROVAL SIGNATORIES 2](#_Toc6395711)

[1 Business context 4](#business-context)

[2 Definitions and abbreviations 4](#definitions-and-abbreviations)

[3 Service Overview 4](#service-overview)

[3.1 Namespaces 4](#namespaces)

[3.2 isSingleSubscriptionAccount\_1 4](#issinglesubscriptionaccount_1)

[3.2.1 Message/data security 5](#messagedata-security)

[3.2.2 Caching 5](#caching)

[3.2.3 Timeout and retry 5](#timeout-and-retry)

[3.2.4 Service Availability 5](#service-availability)

[3.2.5 Error codes 5](#error-codes)

[3.2.6 Sample messages 6](#sample-messages)

[3.3 getSubscriberFraudAndDeceasedStatus\_1
7](#getsubscriberfraudanddeceasedstatus_1)

[3.3.1 Status Codes 7](#status-codes)

[3.3.2 Message/data security 8](#messagedata-security-1)

[3.3.3 Caching 8](#caching-1)

[3.3.4 Timeout and retry 8](#timeout-and-retry-1)

[3.3.5 Service Availability 8](#service-availability-1)

[3.3.6 Error codes 8](#error-codes-1)

[3.3.7 Sample messages 8](#sample-messages-1)

[3.4 XML SCHEMA DATA TYPE DEFINITION
9](#xml-schema-data-type-definition)

[3.4.1 isSingleSubscriptionAccount\_1 structure
9](#issinglesubscriptionaccount_1-structure)

[3.4.2 isSingleSubscriptionAccount\_1Response Structure
9](#issinglesubscriptionaccount_1response-structure)

[3.4.3 getSubscriberFraudAndDeceasedStatus\_1 structure
10](#getsubscriberfraudanddeceasedstatus_1-structure)

[3.4.4 getSubscriberFraudAndDeceasedStaus\_1Response Structure
10](#getsubscriberfraudanddeceasedstaus_1response-structure)

[3.4.1 subscriberFraudAndDeceasedDetailsType Structure
11](#subscriberfraudanddeceaseddetailstype-structure)

[3.4.2 subscriberFraudAndDeceasedDetailType Structure
11](#subscriberfraudanddeceaseddetailtype-structure)

[3.4.3 subscriberDetailsType Structure
11](#subscriberdetailstype-structure)

[3.4.4 subscriberDetailType Structure
11](#subscriberdetailtype-structure)

[3.4.5 errorDetailType Structure 11](#errordetailtype-structure)

**\
**

Business context
================

.

Definitions and abbreviations
=============================

  ---------- -----------------------------------
  **Term**   **Definition**
  XSD        XML Schema Definition
  WSDL       Web Services Description Language
  SOA        Service Oriented Architecture
             
  ---------- -----------------------------------

Service Overview
================

The SOA service ValidateCustomerAccount\_1\_0 allows to validate the
customer account to verify if the account is a single subscription
account or not.

Namespaces
----------

  Namespace URI                                        Prefix
  ---------------------------------------------------- --------
  http://soa.o2.co.uk/validatecustomeraccountdata\_1   vcd
  <http://soa.o2.co.uk/coredata_1>                     xcore
  <http://www.w3.org/2001/XMLSchema>                   xsd
  http://schemas.xmlsoap.org/wsdl/soap/                soap
  http://schemas.xmlsoap.org/wsdl/                     wsdl

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

[]{#_Hlk122087674 .anchor}Additionally, this operation returns
“isVIPCustomer” flag in response for VIP Business MSISDN only when
explicitly queried in request.

For new stack, only consumer PAYM subscriber requests are supported by
this operation.

#### Input message: isSingleSubscriptionAccount\_1 {#input-message-issinglesubscriptionaccount_1 .ListParagraph}

  Element                          Type                                           Occurrence   Description
  -------------------------------- ---------------------------------------------- ------------ ----------------------------------------------------------------------------------------------
  isSingleSubscriptionAccount\_1   vcd:isSingleSubscriptionAccount\_1 structure   1..1         The request container to accept the MSISDN which must be validated for single msisdn account

#### Output message: isSingleSubscriptionAccount \_1Response {#output-message-issinglesubscriptionaccount-_1response .ListParagraph}

  Element Name                             Element Type                                                                                     Occurrence   Description
  ---------------------------------------- ------------------------------------------------------------------------------------------------ ------------ ------------------------------------------------------------
  isSingleSubscriptionAccount\_1Response   [vcd:isSingleSubscriptionAccount\_1Response](#issinglesubscriptionaccount_1response-structure)   1..1         The response container for result of single MSISDN account

#### Referenced faults {#referenced-faults .ListParagraph}

  Element Name                          Element Type         Occurrence   Description
  ------------------------------------- -------------------- ------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------
  isSingleSubscriptionAccount\_1Fault   xcore:SOAFaultType   NA           The back-end fault is wrapped into SOA fault as defined in coredata. Other faults and policy exceptions may be defined for this service during implementation.

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

  Error No                                Error Description                                                                        Error Category
  --------------------------------------- ---------------------------------------------------------------------------------------- ----------------
  validatecustomeraccount -37200-4501-V   Invalid Request. Please check the input and resubmit                                     Validation
  validatecustomeraccount -37200-2501-F   One or more back end services are not available at the moment. Please try again later.   Fatal
  validatecustomeraccount -37200-2502-F   Service call timed out. Please try again later.                                          Fatal
  validatecustomeraccount -37200-3000-E   Unable to retrieve the details for the input MSISDN                                      Error
  validatecustomeraccount -37200-3612-E   Internal service error has occurred.                                                     Error
  validatecustomeraccount-37200-3999-E    Unknown/Uncaught error has occurred.                                                     Error

### Sample messages

***Sample request*** ***1:***

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

xmlns:xcore=http://soa.o2.co.uk/coredata\_1
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

xmlns:xcore=http://soa.o2.co.uk/coredata\_1
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

getSubscriberFraudAndDeceasedStatus\_1
--------------------------------------

This operation is used to query the fraud and deceased status for the
given MSISDN(s) for Postpay consumer (PAYM), Postpay Business and Prepay
(PAYG) customers. This operation supports up to 24 MSISDN’s.

For postpay consumer (PAYM)and business MSISDN, if the Fraud Status
=YES, then the Deceased Check will not be performed and will return with
Deceased Check= NOT CHECKED.

For new stack, only consumer PAYM subscriber requests are supported by
this operation.

#### Input message: getSubscriberFraudAndDeceasedStatus\_1 {#input-message-getsubscriberfraudanddeceasedstatus_1 .ListParagraph}

  Element                                  Type                                                                                        Occurrence   Description
  ---------------------------------------- ------------------------------------------------------------------------------------------- ------------ ---------------------------------------------------------------------------------------------------------------
  getSubscriberFraudAndDeceasedStatus\_1   [vcd:getSubscriberAndDeceasedStatus\_1](#getsubscriberfraudanddeceasedstatus_1-structure)   1..1         The request container to accept the Subscriber details which has to be validate for Fraud and Deceased check.

#### Output message: isSingleSubscriptionAccount \_1Response {#output-message-issinglesubscriptionaccount-_1response-1 .ListParagraph}

  Element Name                                     Element Type                                         Occurrence   Description
  ------------------------------------------------ ---------------------------------------------------- ------------ -----------------------------------------------------------------------
  getSubscriberFraudAndDeceasedStatus\_1Response   vcd:getSubscriberFraudAndDeceasedStatus\_1Response   1..1         The response container for result of Fraud and Deceased Check status.

#### Referenced faults {#referenced-faults-1 .ListParagraph}

  Element Name                                  Element Type         Occurrence   Description
  --------------------------------------------- -------------------- ------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------
  getSubscriberFraudAndDeceasedStatus\_1Fault   xcore:SOAFaultType   NA           The back-end fault is wrapped into SOA fault as defined in coredata. Other faults and policy exceptions may be defined for this service during implementation.

### Status Codes

  **Code**                               **Description**
  -------------------------------------- ------------------------------------------------
  validatecustomeraccount-37200-0000-S   Fraud and Deceased Info returned successfully
  validatecustomeraccount-37200-6000-W   Fraud and Deceased Info returned with Error(s)

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

  Error No                                Error Description                                                                        Error Category
  --------------------------------------- ---------------------------------------------------------------------------------------- ----------------
  validatecustomeraccount -37200-4501-V   Invalid Request. Please check the input and resubmit                                     Validation
  validatecustomeraccount -37200-2501-F   One or more back end services are not available at the moment. Please try again later.   Fatal
  validatecustomeraccount -37200-2502-F   Service call timed out. Please try again later.                                          Fatal
  validatecustomeraccount -37200-3000-E   Unable to retrieve the details for the input MSISDN                                      Error
  validatecustomeraccount -37200-3612-E   Internal service error has occurred.                                                     Error
  validatecustomeraccount-37200-3999-E    Unknown/Uncaught error has occurred.                                                     Error

### Sample messages

***Sample request:***

&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;soapenv:Envelope
xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"&gt;

&lt;soapenv:Header&gt;

PLEASE REFER TO 'O2 SOA Services - Consuming Applications Guide' FOR A
LIST OF SOAP HEADERS TO BE SENT.

&lt;/soapenv:Header&gt;

&lt;soapenv:Body&gt;

&lt;vcd:getSubscriberFraudAndDeceasedStatus\_1
xmlns:vcd="http://soa.o2.co.uk/validatecustomeraccountdata\_1"
xmlns:xcore="http://soa.o2.co.uk/coredata\_1"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://soa.o2.co.uk/validatecustomeraccountdata\_1
validatecustomeraccountdata\_1\_0.xsd "&gt;

&lt;vcd:subscriberDetails&gt;

&lt;vcd:subscriberDetail&gt;

&lt;vcd:segment&gt;PAYM\_CON&lt;/vcd:segment&gt;

&lt;vcd:msisdn&gt;44709120009&lt;/vcd:msisdn&gt;

&lt;/vcd:subscriberDetail&gt;

&lt;/vcd:subscriberDetails&gt;

&lt;/vcd:getSubscriberFraudAndDeceasedStatus\_1&gt;

&lt;/soapenv:Body&gt;

&lt;/soapenv:Envelope&gt;

***Sample response:***

&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;?xml version="1.0" encoding="UTF-8"?&gt;

&lt;soapenv:Envelope
xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"&gt;

&lt;soapenv:Header&gt;

PLEASE REFER TO 'O2 SOA Services - Consuming Applications Guide' FOR A
LIST OF SOAP HEADERS TO BE SENT.

&lt;/soapenv:Header&gt;

&lt;soapenv:Body&gt;

&lt;vcd:getSubscriberFraudAndDeceasedStatus\_1Response
xmlns:vcd="http://soa.o2.co.uk/validatecustomeraccountdata\_1"
xmlns:xcore="http://soa.o2.co.uk/coredata\_1"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://soa.o2.co.uk/validatecustomeraccountdata\_1
validatecustomeraccountdata\_1\_0.xsd "&gt;

&lt;vcd:resultStatus&gt;

&lt;xcore:statusCode&gt;validatecustomeraccount-37200-0000-S&lt;/xcore:statusCode&gt;

&lt;xcore:externalDescription&gt;Fraud and Deceased Info returned
successfully&lt;/xcore:externalDescription&gt;

&lt;/vcd:resultStatus&gt;

&lt;vcd:subscriberFraudAndDeceasedDetails&gt;

&lt;vcd:subscriberFraudAndDeceasedDetail&gt;

&lt;vcd:msisdn&gt;44709120009&lt;/vcd:msisdn&gt;

&lt;vcd:segment&gt;PAYM\_CON&lt;/vcd:segment&gt;

&lt;vcd:isFraud&gt;YES&lt;/vcd:isFraud&gt;

&lt;vcd:isDeceased&gt;YES&lt;/vcd:isDeceased&gt;

&lt;/vcd:subscriberFraudAndDeceasedDetail&gt;

&lt;/vcd:subscriberFraudAndDeceasedDetails&gt;

&lt;/vcd:getSubscriberFraudAndDeceasedStatus\_1Response&gt;

&lt;/soapenv:Body&gt;

&lt;/soapenv:Envelope&gt;

***Sample Fault ***

***&lt;***soapenv:Envelope
xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/"

xmlns:mnd="http://soa.o2.co.uk/validatecuatomeraccountdata\_1"&gt;

&lt;soapenv:Body&gt;

&lt;soapenv:Fault&gt;

&lt;faultcode
xmlns:env="http://schemas.xmlsoap.org/soap/envelope"&gt;env:Server&lt;/faultcode&gt;

&lt;faultstring&gt;One or more back end services are not available at
the moment. Please try again later&lt;/faultstring&gt;

&lt;detail&gt;

&lt;vcd:getSubscriberFraudAndDeceasedStatus\_1Fault
xmlns:vcd="http://soa.o2.co.uk/validatecustomeraccountdata\_1"
xmlns:xcore="http://soa.o2.co.uk/coredata\_1"
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xsi:schemaLocation="http://soa.o2.co.uk/validatecustomeraccountdata\_1
validatecustomeraccountdata\_1\_0.xsd "&gt;

&lt;xcore:SOAFaultOriginator&gt;OSB&lt;/xcore:SOAFaultOriginator&gt;

&lt;xcore:SOAFaultCode&gt;validatecustomeraccount-37200-2501-F&lt;/xcore:SOAFaultCode&gt;

&lt;xcore:faultDescription&gt;One or more back end services are not
available at the moment. Please try again&lt;/xcore:faultDescription&gt;

&lt;xcore:SOATransactionID&gt;7b2c7bec-1412-44a3-a600-b966a4ba05b7&lt;/xcore:SOATransactionID&gt;

&lt;/vcd:getSubscriberFraudAndDeceasedStatus\_1Fault&gt;

&lt;/detail&gt;

&lt;/soapenv:Fault&gt;

&lt;/soapenv:Body&gt;

&lt;/soapenv:Envelope&gt;

XML SCHEMA DATA TYPE DEFINITION
-------------------------------

### isSingleSubscriptionAccount\_1 structure

  ------------------------ ----------------------------------- ------------ ----------------------------------------------------------------------------------------------------------------------
  Element                  Type                                Occurrence   Description
  msisdn                   xcore:msisdnType                    1..1         Customer msisdn in international format.
  retrieveAdditionalInfo   xcore: retrieveAdditionalInfoType   0..1         This is an optional element which can be used query the additional information like details of VIP (DISE) customers.
  ------------------------ ----------------------------------- ------------ ----------------------------------------------------------------------------------------------------------------------

### isSingleSubscriptionAccount\_1Response Structure

  ---------------------------- ------------------ ------------ ----------------------------------------------------------------------------------------
  Element Name                 Element Type       Occurrence   Description

  msisdn                       xcore:msisdnType   1..1         Customer msisdn in international format.

  isSingleSubcriptionAccount   xsd:boolean        1..1         The status if the msisdn is a single msisdn billing account or not.
                                                               
                                                               Note: For Prepay MSISDN’s this value will always be true

  subscriptionCount            xsd:integer        1..1         The subscription count i.e. the count of subscriptions/MSISDN’s on the billing account

  isVIPCustomer                xsd:boolean        0..1         This element indicates if Business customer is a VIP(DISE).
  ---------------------------- ------------------ ------------ ----------------------------------------------------------------------------------------

### getSubscriberFraudAndDeceasedStatus\_1 structure

  ------------------------ --------------------------------------------------------------- ------------ -------------------------------------------------------------------------------------------------------------------------
  Element                  Type                                                            Occurrence   Description
  subscriberDetails        [vcd:subscriberDetailsType](#subscriberdetailstype-structure)   1..1         Subscriber Details like MSISDN,segment etc.
  retrieveAdditionalInfo   xcore: retrieveAdditionalInfoType                               0..1         This is an optional element to query the additional information like customer ID. This includes optional parametername.
  ------------------------ --------------------------------------------------------------- ------------ -------------------------------------------------------------------------------------------------------------------------

### getSubscriberFraudAndDeceasedStaus\_1Response Structure

  ----------------------------------- ----------------------------------------------------------------------------------------------- ------------ ---------------------------------------------------------------------------------------
  Element Name                        Element Type                                                                                    Occurrence   Description
  resultStatus                        xcore:serviceResultType                                                                         1..1         Result Status which includes statusCode, externalDescription and internalDescription.
  subscriberFraudAndDeceasedDetails   [vcd:subscriberFraudAndDeceasedDetailsType](#subscriberfraudanddeceaseddetailstype-structure)   1..1         The status if the msisdn is Fraud or Deceased.
  additionalInfo                      vcd:additinalInfoType                                                                           0..1         This element returns additional information like customer ID if explicitly requested.
  ----------------------------------- ----------------------------------------------------------------------------------------------- ------------ ---------------------------------------------------------------------------------------

### subscriberFraudAndDeceasedDetailsType Structure

  ------------------ --------------------------------------------------------------------------------------------- ------------ -------------------------------------------------------
  Element Name       Element Type                                                                                  Occurrence   Description
  subscriberDetail   [vcd:subscriberFraudAndDeceasedDetailType](#subscriberfraudanddeceaseddetailtype-structure)   1..3         Subscriber Fraud and Deceased Details type structure.
  ------------------ --------------------------------------------------------------------------------------------- ------------ -------------------------------------------------------

### subscriberFraudAndDeceasedDetailType Structure

  -------------- -------------------------------------------------------------------------- ------------ ---------------------------------------------------------------------
  Element Name   Element Type                                                               Occurrence   Description

  msisdn         xcore:msisdnType                                                           1..\*        Customer msisdn in international format.

  segment        xcore:segment\_2Type                                                       1..1         The Segement type
                                                                                                         
                                                                                                         PAYM\_CON - For Postpay Consumer Customers

  isFraud        xsd:string                                                                 0..1         This element tells the Fraud status of the MSISDN:
                                                                                                         
                                                                                                         -   YES
                                                                                                         
                                                                                                         -   NO
                                                                                                         

  isDeceased     xsd:string                                                                 0..1         This element tells the Deceased status of the MSISDN:
                                                                                                         
                                                                                                         -   YES
                                                                                                         
                                                                                                         -   NO
                                                                                                         

  errorDetails   [vcd:errorDetailsType](#getsubscriberfraudanddeceasedstatus_1-structure)   0..1         Error Details if Fraud or Decesed check are not performed properly.
  -------------- -------------------------------------------------------------------------- ------------ ---------------------------------------------------------------------

### subscriberDetailsType Structure

  ------------------ ------------------------------------------------------------- ------------ -----------------------------------
  Element Name       Element Type                                                  Occurrence   Description
  subscriberDetail   [vcd:subscriberDetailType](#subscriberdetailtype-structure)   1..3         Subscriber Detail for a customer.
  ------------------ ------------------------------------------------------------- ------------ -----------------------------------

### subscriberDetailType Structure

  -------------- ---------------------- ------------ --------------------------------------------
  Element Name   Element Type           Occurrence   Description

  segment        xcore:segment\_2Type   1..1         The Segement type
                                                     
                                                     PAYM\_CON - For Postpay Consumer Customers

  msisdn         xcore:msisdnType       1..\*        Customer msisdn in international format.
  -------------- ---------------------- ------------ --------------------------------------------

### errorDetailType Structure

  ------------------ -------------- ------------ -------------------------------------------------------------
  Element Name       Element Type   Occurrence   Description
  errorCode          xsd:string     1..1         Error Code
  errorDescription   xsd:string     1..1         Error description which tells the reason of error occurred.
  ------------------ -------------- ------------ -------------------------------------------------------------

### additinalInfoType Structure

  -------------- -------------- ------------ ---------------------------------------
  Element Name   Element Type   Occurrence   Description
  customerId     xsd:string     0..1         Customer Id for the requested msisdn.
  -------------- -------------- ------------ ---------------------------------------

### retrieveAdditionalInfoType Structure

  --------------- ---------------------------------------------- ------------ ---------------------------------------------------------------------
  Element Name    Element Type                                   Occurrence   Description

  parameterName   [xsd:string](#_orderSummary_2Type_Structure)   1..\*        Indicate the additional information to be returned in the response.
                                                                              
                                                                              isSingleSubscriptionAccount\_1 operation allowed value(s):
                                                                              
                                                                              -   vipCustomer
                                                                              
                                                                              getSubscriberFraudAndDeceasedStatus\_1 allowed value(s):
                                                                              
                                                                              -   customerId
                                                                              
                                                                              Note : The parmaterName is case sensitive
  --------------- ---------------------------------------------- ------------ ---------------------------------------------------------------------
