**O~2~**

**Interface Specification**

**37229 Product Offering Qualification API**

Version 1.3

**\
**[[[[]{#_Toc159915941 .anchor}]{#_Toc156645503 .anchor}]{#_Toc153600109
.anchor}]{#_Toc153595979 .anchor}DOCUMENT INFORMATION

  -------------------------- ----------------------------
  **Document Author:**       Dolly Khurana
  **Owner while current:**   <SOAServiceFactory@o2.com>
  **Retention period:**      3 years
  -------------------------- ----------------------------

[[[[[]{#_Toc143240777 .anchor}]{#_Toc159915942 .anchor}]{#_Toc156645504
.anchor}]{#_Toc153600110 .anchor}]{#_Toc153595980 .anchor}CHANGE HISTORY

  ------------- ------------ ---------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Version**   **Date**     **Changed by**   **Changes**

  0.1           28-07-2020   Dolly Khurana    Initial version

  0.2           14/08/2020   Dolly Khurana    Internal review complete

  0.3           20/08/2020   Pronisa Baruah   Updated to
                                              
                                              -   Introduce a new function “Get Bolton Business Policies” for Bolton’s
                                              
                                              -   Correct the error codes for the Get Valid Bolton offerings function in section 4.1.2
                                              

  0.4           27/08/2020   Pronisa Baruah   Error response structure added.

  0.5           01/09/2020   Pronisa Baruah   To introduce new functions
                                              
                                              -   Get Valid Tariff Offerings
                                              
                                              -   Get Tariff Business Policies and
                                              
                                              -   Get Tariff Compatible Products
                                              
                                              The error code typo ‘s’ removed in “Get Valid Bolton Offerings” & “Get Bolton Business Policies” functions

  0.6           17/09/2020   Pronisa Baruah   -   To add offerCode and externalId fields in the offeringType.
                                              
                                              -   Get Tariff & Bolton business policy messages updated
                                              

  0.7           30/09/2020   Pronisa Baruah   -   To add customer in treatment check for Get Bolton business policies.
                                              

  0.8           03-11-2020   Apoorva          Resource definition and method names updated for the below API’s.
                                              
                                              -   .Get Valid Bolton Offerings
                                              
                                              -   .Get Bolton Business Policies
                                              
                                              -   .Get Tariff Business Policies
                                              
                                              -   Get Valid Tariff Offerings
                                              
                                              -   Get Tariff Compatible Products
                                              

  0.9           12-11-2020   Dolly Khurana    Updated the Get Valid Product Offerings API to include new elements as part of 34.8 IMI Textback service changes

  1.0           14-12-2020   Dolly Khurana    Updated the offering chars field in Get Valid Product Offerings API as part of 34.8 IMI Textback service changes
                                              
                             Rajesh Kota      Baseline and signed off version for R3.1

  1.1           22-01-2021   Dolly Khurana    Updated Get Valid Product Offerings sample for mandatory chars

  1.2           20-04-2021   Dolly Khurana    Updated Get Valid Product Offerings sample to remove chars array

  1.3           01-06-2022   Dolly Khurana    Added an optional request element “returnConflicts” in Get Valid Product Offerings API in order to query all the offers including the conflicts with the existing products.
  ------------- ------------ ---------------- -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------

[[[[[[]{#_Toc143240778 .anchor}]{#_Toc237660663 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}RELATED DOCUMENTS

  -------- -------------------------------------------------------------------------------- ------------- -----------------------------------------------
  **ID**   **Name**                                                                         **Version**   **Description**
  1        R3 - 163.1 HTK IVR 62.1 HTK SIM Swap Interface Agreement v1.7                    1.7           HTK IVR & SIM Swap Interface Agreement
  2        R3 - IF34.8 IMI PAYM & PAYG Tariffs & Bolt Ons to BSS Interface Agreement v0.7   o.7           IMI PAYM & PAYG & Boltons Interface Agreement
  3        NC.O2.INT Telecom Business API Specification                                     0.28          Netcracker TB API specification
  -------- -------------------------------------------------------------------------------- ------------- -----------------------------------------------

[[[[[[]{#_Toc143240779 .anchor}]{#_Toc237660664 .anchor}]{#_Toc159915944
.anchor}]{#_Toc156645506 .anchor}]{#_Toc153600112
.anchor}]{#_Toc153595982 .anchor}DESIGN LEAD SIGN-OFF

  --------------- ------------------------------------- ----------- ------------
  **Name:**       Rajesh Kota
  **Role:**       Integration(SOA) Solution Architect
  **APPROVED:**   YES
  --------------- ------------------------------------- ----------- ------------

[[[[[[]{#_Toc143240780 .anchor}]{#_Toc237660665 .anchor}]{#_Toc159915945
.anchor}]{#_Toc156645507 .anchor}]{#_Toc153600113
.anchor}]{#_Toc153595983 .anchor}DESIGN GOVERNANCE SIGN-OFF

  --------------- ------------------------------------- ----------- ------------
  **Name:**       Rajesh Kota
  **Role:**       Integration(SOA) Solution Architect
  **APPROVED:**   YES
  --------------- ------------------------------------- ----------- ------------

[[[[[[]{#_Toc143240781 .anchor}]{#_Toc237660666 .anchor}]{#_Toc159915946
.anchor}]{#_Toc156645508 .anchor}]{#_Toc153600114
.anchor}]{#_Toc153595984 .anchor}ADDITIONAL APPROVAL SIGNATORIES

  ------------ --------------------------- -------------- ------------
  **Name**     **Role**                    **Approved**   **Date**
  Tony Brand   Solution Designer for AO2   YES            14/12/2020
  ------------ --------------------------- -------------- ------------

Contents

[CHANGE HISTORY 2](#_Toc143240777)

[RELATED DOCUMENTS 3](#_Toc143240778)

[DESIGN LEAD SIGN-OFF 3](#_Toc143240779)

[DESIGN GOVERNANCE SIGN-OFF 3](#_Toc143240780)

[ADDITIONAL APPROVAL SIGNATORIES 3](#_Toc143240781)

[1 Definitions and abbreviations 5](#definitions-and-abbreviations)

[1.1 Definitions 5](#definitions)

[2 Introduction 5](#introduction)

[2.1 Overview 5](#overview)

[3 Resources Summary 5](#resources-summary)

[3.1 HTTP Request Headers 6](#http-request-headers)

[4 Resource Definition 6](#resource-definition)

[4.1 Get Valid Product Offerings 6](#get-valid-product-offerings)

[4.1.1 Input () and Output () parameters
6](#input-and-output-parameters)

[4.1.2 Success and Fault Definitions 6](#success-and-fault-definitions)

[4.1.3 Sample Request and Responses 7](#sample-request-and-responses)

[4.2 Data Types 14](#data-types)

[4.2.1 offeringType 14](#offeringtype)

[4.2.2 offeringGroupType 14](#offeringgrouptype)

[4.2.3 offeringCharsType 14](#offeringcharstype)

[4.2.4 allowancesType 15](#allowancestype)

[4.2.5 priceType 15](#pricetype)

[4.2.6 conflictType 15](#conflicttype)

[5 Error Response Structure 16](#error-response-structure)

[5.1 errorType 16](#errortype)

[5.2 faultTraceType 16](#faulttracetype)

[6 Appendix A – OfferingType Mandatory Fields By Method
17](#appendix-a-offeringtype-mandatory-fields-by-method)

[7 Appendix B – Business Policy Code and Reason for Product Offering
17](#appendix-b-business-policy-code-and-reason-for-product-offering)

[8 Appendix C – Business Policy Code and Reason for Tariff Offering
17](#appendix-c-business-policy-code-and-reason-for-tariff-offering)

[9 Appendix D – Product Type Mandatory Fields By Method
18](#appendix-d-product-type-mandatory-fields-by-method)

**\
**

Definitions and abbreviations
=============================

Definitions
-----------

  ---------- ---------------------------------
  **Term**   **Definition**
  ReST       Representational state transfer
  JSON       JavaScript Object Notation
  ---------- ---------------------------------

Introduction
============

Overview
--------

This Product Offering Qualification API documented here define and
describe the functionality related to the product offerings of the PAYM
consumer subscriber. This API supports following capabilities.

-   Retrieve the valid productofferings available for the subscriber

-   Validate if the product offering can be added to customer’s account

-   Retrieve the valid Tariff offerings available for the subscriber

-   Validate if the subscriber’s tariff change is allowed

-   Determine the subscriber’s current tariff Bolton products that are
    compatible to the new tariff.

Resources Summary
=================

  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Resource Purpose**                     **Resource URI**
  ---------------------------------------- -----------------------------------------------------------------------------------------------------------------------------------------
                                           

  Get Valid Product Offerings              GET /api/productOfferingQualificationManagement/v1/productOffering/{msisdn}

  Get Product Offering Business Policies   Get
                                           
                                           /*api/productOfferingQualificationManagement/v1/productOffering/{msisdn}/businessPolicies*

  Get Valid Tariff Offerings               *GET *
                                           
                                           */api/productOfferingQualificationManagement/v1/productOffering/{msisdn}/tariffOfferings*

  Get Tariff Offering Business Policies    *GET /api/productOfferingQualificationManagement/v1/productOffering/{msisdn}/tariff/businessPolicies*

  Get Tariff Compatible Products           *GET*
                                           
                                           */api/productOfferingQualificationManagement/v1/productOffering/{msisdn}/tariff/compatibleProducts?newTariffOfferId={newTariffOfferId}*
  ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

[[[[[[[[[]{#_Toc156645515 .anchor}]{#_Toc153600121
.anchor}]{#_Toc153595991 .anchor}]{#_Toc114648206
.anchor}]{#_Toc35403885 .anchor}]{#_Toc6999696 .anchor}]{#_Toc92863832
.anchor}]{#_Toc92860516 .anchor}]{#_Toc92860444 .anchor}

HTTP Request Headers 
---------------------

Each service operation accepts O2 standard HTTP headers. Refer to
‘***API Management Gateway - Consumer Application Connectivity Guide***’
for the full list of headers to be sent.

Resource Definition
===================

Get Valid Product Offerings
---------------------------

  ------------------------------------------------------------------------------------------------------------------
  **Resource URI**   GET
                     
                     /api/productOfferingQualificationManagement/v1/productOffering/{msisdn}
  ------------------ -----------------------------------------------------------------------------------------------
  **Description**    This function returns the list of product offerings that the customer can add to its account.

  **Content Type**   application/json
  ------------------------------------------------------------------------------------------------------------------

### Input () and Output () parameters

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**                       **Is Mandatory**   **Type**   **Description**
  -------------------- ----------------------------------- ------------------ ---------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  msisdn               String                              Yes                Path       Mobile phone number for which the product offerings will be returned. It should be international format.
                                                                                         
                                                                                         E.g. 447720342101

  tariffOfferId        String                              No                 Query      Id of the target tariff offer. This field should be passed only when compatible products for the new tariff offer is required.

  returnConflicts      String                              No                 Query      Flag to request the conflict offerings in SOA response. If this flag is not sent, SOA will filter out the offerings which has conflicts with customer’s existing products.
                                                                                         
                                                                                         Allowed value is:
                                                                                         
                                                                                         “Y”

  myOfferings          [offeringType](#offeringtype)\[\]   No                 Body       This is an array of product offerings. Refer to [Appendix A](#_Appendix_A_–_1) for offering details returned.
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Success and Fault Definitions

  **HTTP Status Code**   **Error Code**                              **Description**                                                                          **Category**
  ---------------------- ------------------------------------------- ---------------------------------------------------------------------------------------- --------------
  200                    N/A                                         N/A                                                                                      Success
  200                    productofferingqualification-37229-3602-E   Subscriber is not active.                                                                Business
  400                    productofferingqualification-37229-4501-V   Invalid Request. Please check the input and resubmit.                                    Validation
  400                    productofferingqualification-37229-4000-V   The requested application or channel is either not recognised or invalid.                Validation
  408                    productofferingqualification-37229-2502-F   Backend service call timed out. Please try again later.                                  Technical
  503                    productofferingqualification-37229-2501-F   One or more back end services are not available at the moment. Please try again later.   Technical
  404                    productofferingqualification-37229-3601-E   Subscriber is either not recognised or cannot be found.                                  Business
  500                    productofferingqualification-37229-3612-E   Internal service error has occurred.                                                     Technical

### Sample Request and Responses

#### Success scenario

URI:

GET

/api/productOfferingQualificationManagement/v1/productOffering/*447720342101*

**Request**

  ------------------
  No request body.
  ------------------

**Response**

**HTTP/1.1**: 200 OK

  ----------------------------------------------
  {
  
  "myOfferings":\[
  
  {
  
  "offerId":"20000019",
  
  "offerCode":"3GBBOLTON:1",
  
  "externalId":"3GBBOLTON",
  
  "name":"3GB Data Bolt On",
  
  "description":"3GB Snacking Data Bolt On ",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"200"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155212058013161778",
  
  "offeringGroupName":"Data Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"Data",
  
  "value":"3221225472"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"22000002",
  
  "offerCode":"100MMS:1",
  
  "externalId":"100MMS",
  
  "name":"100 MMS",
  
  "description":"100 MMS",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"100"
  
  }
  
  > \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155490440913240014",
  
  "offeringGroupName":"MMS Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"MMS",
  
  "value":"100"
  
  }
  
  \]
  
  }
  
  \]
  
  }
  ----------------------------------------------

#### Success scenario – where conflicts offerId’s are returned

URI:

GET

/api/productOfferingQualificationManagement/v1/productOffering/*447720342101?returnConflicts=’Y’*

**Request**

  ------------------
  No request body.
  ------------------

**Response**

**HTTP/1.1**: 200 OK

  --------------------------------------------------
  {
  
  "myOfferings":\[
  
  {
  
  "offerId":"20000019",
  
  "offerCode":"3GBBOLTON:1",
  
  "externalId":"3GBBOLTON",
  
  "name":"3GB Data Bolt On",
  
  "description":"3GB Snacking Data Bolt On ",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"200"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155212058013161778",
  
  "offeringGroupName":"Data Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"Data",
  
  "value":"3221225472"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"22000002",
  
  "offerCode":"100MMS:1",
  
  "externalId":"100MMS",
  
  "name":"100 MMS",
  
  "description":"100 MMS",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"100"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155490440913240014",
  
  "offeringGroupName":"MMS Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"MMS",
  
  "value":"100"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"90081021",
  
  "offerCode":"O2TRAVEL:1",
  
  "externalId":"O2TRAVEL",
  
  "name":"O2 Travel",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"MRC",
  
  "value":"0"
  
  }
  
  \],
  
  "conflicts":\[
  
  {
  
  "offerId":"20000030"
  
  },
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155490460613240017",
  
  "offeringGroupName":"Roaming Recurrent Bolt Ons"
  
  }
  
  }
  
  \]
  
  }
  --------------------------------------------------

#### Success scenario – with Perk Product and mandatory characteristic

URI:

GET

/api/productOfferingQualificationManagement/v1/productOffering/*447720342101*

**Request**

  ------------------
  No request body.
  ------------------

**Response**

**HTTP/1.1**: 200 OK

  ----------------------------------------------
  {
  
  "myOfferings":\[
  
  {
  
  "offerId":"20000019",
  
  "offerCode":"3GBBOLTON:1",
  
  "externalId":"3GBBOLTON",
  
  "name":"3GB Data Bolt On",
  
  "description":"3GB Snacking Data Bolt On ",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"200"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155212058013161778",
  
  "offeringGroupName":"Data Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"Data",
  
  "value":"3221225472"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"22000002",
  
  "offerCode":"100MMS:1",
  
  "externalId":"100MMS",
  
  "name":"100 MMS",
  
  "description":"100 MMS",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"NRC",
  
  "value":"100"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9155490440913240014",
  
  "offeringGroupName":"MMS Snacking Bolt Ons"
  
  },
  
  "allowances":\[
  
  {
  
  "name":"MMS",
  
  "value":"100"
  
  }
  
  \]
  
  },
  
  {
  
  "offerId":"26000005",
  
  "offerCode":"CAFYN:1",
  
  "externalId":"CAFYN",
  
  "name":"Cafeyn",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"MRC",
  
  "value":"300"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9158073895513816860",
  
  "offeringGroupName":"Books & Magazines"
  
  },
  
  "chars":
  
  {
  
  "name":"Extra Type",
  
  "value":\[
  
  "Free Only"
  
  \],
  
  "mandatory":"true"
  
  }
  
  },
  
  {
  
  "offerId":"26000008",
  
  "offerCode":"MCAFMSS:1",
  
  "externalId":"MCAFMSS",
  
  "name":"McAfee",
  
  "price":\[
  
  {
  
  "category":"Normal",
  
  "type":"MRC",
  
  "value":"500"
  
  }
  
  \],
  
  "offeringGroup":{
  
  "offeringGroupId":"9158073896513816860",
  
  "offeringGroupName":"Digital Productivity"
  
  },
  
  "chars":
  
  {
  
  "name":"Extra Type",
  
  "value":\[
  
  "Paid Only"
  
  \],
  
  "mandatory":"true"
  
  }
  
  }
  
  \]
  
  }
  ----------------------------------------------

#### Fault scenario – MSISDN Not Found

URI:

GET

/api/productOfferingQualificationManagement/v1/productOffering/*447720342107*

**Request**

  -----------------
  No request body
  -----------------

**Response:**

**HTTP/1.1**: 404 Not Found

  -----------------------------------------------------------------------
  {
  
  "error": {
  
  "code": "productofferingqualification-37229-3601-E",
  
  "message": "Subscriber is either not recognised or cannot be found.”,
  
  "faultTrace": \[
  
  {
  
  "faultCode": "404",
  
  "faultDescription": "Not Found"
  
  }
  
  \]
  
  }
  
  }
  -----------------------------------------------------------------------

[[[[[[[[[[[[[[]{#_Appendix_Ig_– .anchor}]{#_Appendix_H_–
.anchor}]{#_Appendix_Hf_- .anchor}]{#_Appendix_H_-
.anchor}]{#_Appendix_G_- .anchor}]{#_Appendix_Fe_–
.anchor}]{#_Appendix_GF_– .anchor}]{#_Appendix_F_–
.anchor}]{#_Appendix_E_– .anchor}]{#_Appendix_E–_
.anchor}]{#_Appendix_CB_– .anchor}]{#_Appendix_C_–
.anchor}]{#_Appendix_B_– .anchor}]{#_Appendix__A .anchor}

Data Types
----------

### offeringType

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**                             **Is Mandatory**   **Description**
  -------------------- ----------------------------------------- ------------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------
  offerId              String                                    Yes                Id of the offering.

  offerCode            String                                    No                 Unique offering code. This is the unique combination of the offering and price point version.
                                                                                    
                                                                                    E.g. SIMO12\_2019:8182:1

  externalId           String                                    No                 Unique identifier of the offering. This can be used by external systems to identify one or more variants of the given offering.
                                                                                    
                                                                                    E.g. SIMO12\_2018

  name                 String                                    No                 Name of the offering.

  description          String                                    No                 Description of the offering.

  price                [priceType\[\]](#pricetype)               No                 This is an array of different price points returned for the offering i.e. normal price and discounted price if applicable.

  conflicts            [conflictType\[\]](#conflicttype)         No                 This is the list of current product offering Id’s present on the customer’s tariff which are conflicting with the given offering.

  offeringGroup        [offeringGroupType](#offeringgrouptype)   No                 This specifies the offering group.

  chars                [offeringCharsType](#offeringcharstype)   No                 This specifies the characteristics of the offering. This is a set of mandatory key-value characteristics applicable for the offering. E.g. Spend Cap variants.

  allowances           [allowancesType](#allowancestype)\[\]     No                 This is an array of different allowances associated with the offering. The allowances are –
                                                                                    
                                                                                    -   Voice
                                                                                    
                                                                                    -   Text
                                                                                    
                                                                                    -   MMS
                                                                                    
                                                                                    -   Data
                                                                                    
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### offeringGroupType

  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ ----------------------------
  offeringGroupId      String          Yes                Id of the offering group
  offeringGroupName    String          Yes                Name of the offering group

### offeringCharsType

  ----------------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ --------------------------------------------------------------------
  name                 String          Yes                Characteristic Name

  value                String\[\]      No                 This contains characteristic values

  mandatory            String          Yes                It indicates that characteristic is mandatory when adding an Offer
                                                          
                                                          Valid values: true, false.
  ----------------------------------------------------------------------------------------------------------------------------

### allowancesType

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ ---------------------------------------------------------------------------------------------------------------------------------
  name                 String          Yes                Name of the allowance. The valid values for this field are –
                                                          
                                                          -   Voice
                                                          
                                                          -   Text
                                                          
                                                          -   MMS
                                                          
                                                          -   Data
                                                          

  value                String          Yes                Value of the allowance. The following are the units of each allowance
                                                          
                                                          -   Voice – seconds
                                                          
                                                          -   Text – Number of texts
                                                          
                                                          -   MMS – Number of MMS
                                                          
                                                          -   Data – bytes
                                                          
                                                          For unlimited allowance, the value returned will be “-1”. As of today, there are no product offerings with unlimited allowance.
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### priceType

  ---------------------------------------------------------------------------------------------------------------------
  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ -------------------------------------------------------------
  category             String          Yes                Price point category. The valid values for this field are –
                                                          
                                                          -   Normal
                                                          
                                                          -   Discounted
                                                          

  type                 String          Yes                Price point type. The valid values for this field are –
                                                          
                                                          -   MRC (Monthly Recurring)
                                                          
                                                          -   NRC (Non-Recurring)
                                                          

  value                String          Yes                Price point value in pence
  ---------------------------------------------------------------------------------------------------------------------

[[[[]{#_myProductsType .anchor}]{#_productType_1
.anchor}]{#_tariffOfferingsType .anchor}]{#_businessPoliciesType
.anchor}

### conflictType

  **Parameter name**   **Data Type**   **Is Mandatory**   **Description**
  -------------------- --------------- ------------------ -------------------------------------------------------------------------------
  offerId              String          Yes                Offer Id of the existing product which is conflicting with the given offering

Error Response Structure
========================

errorType
---------

  **Name**     **Type**                                **Is Mandatory**   **Description**
  ------------ --------------------------------------- ------------------ ---------------------------------------------------------------------------------------------------------------------
  code         String                                  Yes                Error Code. Refer to Success and Fault definition section of each method to see the HTTP Responses and Error Codes.
  message      String                                  Yes                Error Message. Refer to Success and Fault definition section of each method to see the Error Messages.
  faultTrace   [faultTraceType\[\]](#faulttracetype)   No                 Additional troubleshooting details.

faultTraceType
--------------

  **Name**           **Type**   **Is Mandatory**   **Description**
  ------------------ ---------- ------------------ ----------------------------------------------
  faultCode          String     Yes                Fault code for the internal component
  faultDescription   String     No                 Fault Description for the internal component

**Sample Error Response:**

**HTTP/1.1**: 404 Not Found

  -----------------------------------------------------------------------
  {
  
  "error": {
  
  "code": "productofferingqualification-37229-3601-E",
  
  "message": "Subscriber is either not recognised or cannot be found.”,
  
  "faultTrace": \[
  
  {
  
  "faultCode": "404",
  
  "faultDescription": "Not Found"
  
  }
  
  \]
  
  }
  
  }
  -----------------------------------------------------------------------

[]{#_Appendix_A_–_1 .anchor}

Appendix A – OfferingType Mandatory Fields By Method
====================================================

  **Offering Attributes**   **Get Valid Product Offerings**   **Get Valid Tariff Offerings**   **Get Tariff Compatible Products**
  ------------------------- --------------------------------- -------------------------------- ------------------------------------
  offerId                   Y                                 Y                                Y
  offerCode                 Y                                 Y                                Y
  externalId                Y                                 Y                                Y
  name                      Y                                 Y                                N
  description               Y                                 Y                                N
  price                     Y                                 Y                                N
  conflicts                 N                                 N/A                              N/A
  offeringGroup             Y                                 Y                                Y
  chars                     N                                 N                                N
  allowances                N                                 N                                N

[]{#_Toc48909972 .anchor}

Appendix B – Business Policy Code and Reason for Product Offering
=================================================================

  **Reason Code**   **Reason Description**
  ----------------- -----------------------------------------------
  5000              Customer current plan is not active.
  5001              Customer current plan is in suspended status.
  5002              A customer has Bankruptcy status.
  5003              A customer has Long Term Illness status.
  5004              A customer has Bereavement status.
  5005              A customer has Financial Difficulty status.
  5006              A customer is in treatment.

Appendix C – Business Policy Code and Reason for Tariff Offering
================================================================

  **Reason Code**   **Reason Description**
  ----------------- ---------------------------------------------------------------------------------
  5000              Customer current plan is not active.
  5001              Customer current plan is in suspended status.
  5002              A customer is in fraud status.
  5003              A customer has deceased status.
  5004              A customer is in treatment.
  5005              A customer has already done the tariff transfer within the last 30 days period.
  5006              A customer has a pending change (e.g. tariff change) on their account.

[]{#_Toc49516550 .anchor}

Appendix D – Product Type Mandatory Fields By Method
====================================================

  **Product Attributes**   **Get Tariff Compatible Products**
  ------------------------ -----------------------------------------------------------------------------------------------------------
  productId                Y
  offer                    Y (Refer to [Appendix A](#appendix-a-offeringtype-mandatory-fields-by-method) for offer details returned)
  productName              Y
  description              Y
  price                    N
  startDate                N
  endDate                  N
  productType              Y
  status                   Y
  chars                    N
  allowances               N
