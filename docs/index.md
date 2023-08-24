**CreateVOIPMigrationWorkOrder**

Revision: 1

Middleware Service Specification

Author: **Saleem Khan**

saleem.khan@virginmedia.co.uk

Date: **15-05-2019**

Document Version: **2.1**

Status: **Issued**[[[[]{#_Toc182625567 .anchor}]{#_Toc182625192
.anchor}]{#_Toc103152334 .anchor}]{#_Toc103152294 .anchor}

Document Purpose

The Service Specification document is a subjective document which
describes the interface, operations and implementation of a single
service.

It is produced by the Middleware Solution Designer and is the key input
to the Middleware Development Team.

It also serves the purpose of an as-built reference to describe the
production service and, as such, forms part of the SOA development
deliverables. Every service that is delivered to the SOA platform must
have an accompanying Service Specification which describes the service.

There must at all times be a base-lined version of each Service
Specification which is aligned with the latest production version of the
physical service.

There may also be one or (in the case of parallel development) more
working copies of a Service Specification which have been created as
part of an overall Solution Design for an objective purpose such as a
project. As new versions of a service are delivered to production the
relevant Service Specification would then become the base-lined version
and replace the previous version.

 {#section .Heading1-NC}

\
Table of Contents {#table-of-contents .Heading1-NC}
=================

1 Document Control 4

1.1 Document Information 4

1.2 Document History 4

1.3 SOA Governance Approval 5

1.4 For Review By 5

1.5 Distribution 5

1.6 References 5

1.7 Contributors to this document 5

1.8 Glossary 5

2 Introduction 6

2.1 Document Purpose 6

2.2 Audience 6

3 Integration Flow 7

4 REST Service Specification 8

4.1 Service Overview 8

**4.1.1** Function(s) 8

**4.1.2** Service Interface Definition 9

**4.1.3** Revision History 10

4.2 Operations 11

**4.2.1** CreateVOIPMigrationWorkOrder – POST 11

4.3 Basic Sanity Checks/Tests 19

**4.3.1** Header Validation Checks 19

**4.3.2** Functionality Checks 19

4.4 Technical Specification 20

**4.4.1** CreateVOIPMigrationWorkOrder – POST 20

5 Non-functional requirements 22

5.1 Security Requirements 22

5.2 Configuration Requirements 22

**5.2.1** Timeouts 22

5.3 Performance and Capacity Planning Requirements 22

6 Troubleshooting 23

\
Document Control
================

**\
**[[[[]{#_Toc159915941 .anchor}]{#_Toc156645503 .anchor}]{#_Toc153600109
.anchor}]{#_Toc153595979 .anchor}Document Information


  ------------------------------ -----------------------------------------------------------------
  **Title**                      CreateVOIPMigrationWorkOrder (Middleware Service Specification)
  **Author / (Last saved by)**   Saleem Khan / (Khan, Saleem)
  **Status**                     Issued
  ------------------------------ -----------------------------------------------------------------

[[[[[]{#_Toc143240777 .anchor}]{#_Toc159915942 .anchor}]{#_Toc156645504
.anchor}]{#_Toc153600110 .anchor}]{#_Toc153595980 .anchor}Document History


  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Version**   **Description / Change Comments**                                                                                                                                                                                                                        **Who**       **Date**
  ------------- -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- ------------- -----------------------
  0.1           1^st^ draft, circulated for internal review                                                                                                                                                                                                              Saleem Khan   08^th^ August 2018

  0.2           Mapping Sheet updated. Service CreateWorkOrder\_V3 (R 5) is updated to be used for ‘Workorder’ creation.                                                                                                                                                 Saleem Khan   23^rd^ August 2018

  0.3           Spec (along with the mapping sheet) updated after addressing DEV comments:                                                                                                                                                                               Saleem Khan   24^th^ September 2018
                                                                                                                                                                                                                                                                                       
                -   Workflow updated, failure from ‘CREATE\_WORKORDER’ is now only retrying itself and not going back to the previous state 'Get\_WORKORDER\_DATA’.                                                                                                                    
                                                                                                                                                                                                                                                                                       
                -   Configuration for workorder comments is removed from the service.                                                                                                                                                                                                  
                                                                                                                                                                                                                                                                                       

  1.0           Service updated to reflect the changes to the child service ‘GetVOIPLineMigrationDetails’ (original updates ware requested due to the MIDAS design changes).                                                                                             Saleem Khan   17^th^ December 2018

  1.1           Mapping Sheet Update, ‘ServiceCodeType’ changed from ‘SERVICE’ to ‘S’ as returned by the MiDaS by GetVOIPLineMigrationDetails.                                                                                                                           Saleem Khan   31^st^ January 2019

  1.2           Mapping Sheet updated for ‘CreateWorkorder\_V3 (R5).                                                                                                                                                                                                     Saleem Khan   1^st^ February 2019

  1.3           Mapping Sheet updated to address ‘Migration Work Order’ related issues.                                                                                                                                                                                  Saleem Khan   15^th^ February 2019
                                                                                                                                                                                                                                                                                       
                -   MiDaS (via ‘GetVOIPLineMigraitonDetails’ service) would send additional service and OTC codes to handle ‘EBUL devices.                                                                                                                                             
                                                                                                                                                                                                                                                                                       
                -   Logic for creating ‘Vulnerable Questioners’ is revised as well.                                                                                                                                                                                                    
                                                                                                                                                                                                                                                                                       
                -   Mapping to be updated to pass an additional field (i.e. ‘prerateWorkOrder’) to the ‘CreateWorkOrder\_V3 (R5)’ service to make sure no prorate charges are applied to along with the ‘Migration Work Order’.                                                        
                                                                                                                                                                                                                                                                                       

  1.4           Mapping Sheet updated to address ‘Migration Work Order’ related issues.                                                                                                                                                                                  Saleem Khan   18^th^ February 2019
                                                                                                                                                                                                                                                                                       
                -   Mapping Sheet updated for OTC code.                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                       

  1.5           Following Updates are made:                                                                                                                                                                                                                              Saleem Khan   28^th^ February 2019
                                                                                                                                                                                                                                                                                       
                -   Default vulnerability questioner is NOT to be mapped as this is already set in ‘CreateWorkOrder\_V3 (R5)’ service.                                                                                                                                                 
                                                                                                                                                                                                                                                                                       
                -   Timeout for the ‘CreateWorkOrder\_V3 (R5)’ is now updated from ‘3’ sec to 10 sec.                                                                                                                                                                                  
                                                                                                                                                                                                                                                                                       
                Note: Although we are expecting ‘CreateWorkOrder\_V3 (R5)’ service to respond in about 3 sec, this (parent Service) being an Asynchronous operation we are OK to provide more time to the child service without having an impact on the consumer APIs.                 

  1.6           Questioner updated for Defect \#5216, we are now sending 'L' instead of 'H' for home phone.                                                                                                                                                              Saleem Khan   04^th^ March 2019

  1.7           Value for the 'prorateWorkOrder' is now set to 'false' as requested by the solution Design.                                                                                                                                                              Saleem Khan   08^th^ March 2019

  1.8           Service updated, following updates are done:                                                                                                                                                                                                             Saleem Khan   04^th^ April 2019
                                                                                                                                                                                                                                                                                       
                -   Workflow removed from this service.                                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                       
                -   Retry while retrieving MIDAS data removed.                                                                                                                                                                                                                         
                                                                                                                                                                                                                                                                                       
                -   Integration to the Update MIDAS service introduced.                                                                                                                                                                                                                
                                                                                                                                                                                                                                                                                       

  1.9           Mapping updated for 2nd questionnaire, it is 'hasMobilePhone' to be used instead of "usesMobilePhone'.                                                                                                                                                   Saleem Khan   18^th^ April 2019

  2.0           Updated the Service Mapping to consume the questionnaire returned by GetVOIPLineMigration service                                                                                                                                                        Ali Kamal     2^nd^ May 2019

  2.1           Configuration updated for the MIDAS status updates                                                                                                                                                                                                       Saleem Khan   10^th^ May 2019
  ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

[[[[[[]{#_Toc143240778 .anchor}]{#_Toc237660663 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}SOA Governance Approval


***The SOA Governance Authority is required to sign off this service
specification, and ensure that it adheres to SOA standards, before any
further sign off can be sought.***

  **Name**     **Title / Department**   **Approval (Y/N)**
  ------------ ------------------------ --------------------
  Steve King   SOA Governance           

Where the reviewer is not approving the document explain what changes
are needed.

[[[[[[]{#_Toc143240778 .anchor}]{#_Toc237660663 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}For Review By


  **Name**                      **Title / Department**              **Approval (Y/N)**
  ----------------------------- ----------------------------------- --------------------
  Steve King                    Middleware Solution Design Lead     
  Lee Doel                      Middleware Development Lead         
  David Mortimer                Middleware Technical Architecture   
  Steve King                    SOA Governance Representative       
  Andrew Zielinski              MW Support Lead                     
  Sunil Kumar, Satheesh Kumar   Project Solution Designer           
  VMTS Test Team                VMTS Test Team                      

Where the reviewer is not approving the document explain what changes
are needed.

[[[[[[]{#_Toc143240778 .anchor}]{#_Toc237660663 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}Distribution


Distribution is to the reviewer list above plus the following:

  **Name**   **Title / Department**
  ---------- ------------------------
             
             

[[[[[[]{#_Toc143240778 .anchor}]{#_Toc237660663 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}References


  ------------------------- ------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Reference**             **Document**                                **Link / Path**
  []{#Ref01 .anchor}Ref01   SOA Principles and Policies                 [SOA Principles and Policies](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Standards/Governance/SOA%20Principles%20and%20Policies.doc)
  []{#Ref02 .anchor}Ref02   SOA Integration Architecture                [SOA Integration Architecture](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Standards/Governance/SOA%20Integration%20Architecture.doc)
  []{#Ref03 .anchor}Ref03   SOA Blueprint                               [SOA Blueprint](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Standards/Governance/SOA%20Solution%20Blueprint.doc)
  []{#Ref04 .anchor}Ref04   Master Service Error Code List              [Master Error List](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Development/Master%20Service%20Error%20Code%20List.xls)
  Ref05                     Performance Sheet                           [Performance](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Configuration%20Management/Service%20Performance%20and%20Capacity.xls)
  Ref06                     Single Customer Migration Solution Design   [SahrePoint Link](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Project%20Documentation/21CV/21CV%20Single%20Customer%20Migration/21CV_MaD_SCM_SD_v0%205.docx)
  Ref07                     Middleware Process Framework                [SharePoint](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Service%20Documentation/ProcessNewCustomerOrder/Middleware%20Process%20%20Framework%20-%20Requirements.doc)
  ------------------------- ------------------------------------------- ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

***Reference any documents that are referred to within this document or
linked to it, including the version number and where the document can be
found. This***[[[[[]{#_Toc183235881 .anchor}]{#_Toc103152502
.anchor}]{#_Toc103152333 .anchor}]{#_Toc103152293
.anchor}]{#_Toc103151773 .anchor} ***list shall include all input
documents used in its generation, such as the High Level Design,
Detailed Business Requirements and Detailed Solution Design.***

[[[[[[]{#_Toc143240778 .anchor}]{#_Toc237660663 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}Contributors to this document


The following people provided input into this document.

  ---------------- ----------------------------
  **Name**         **Role / Company**
  Raja Ali Kamal   Middleware Solution Design
  Fawad Sikandar   Middleware Solution Design
  ---------------- ----------------------------

[[[[[[]{#_Toc143240778 .anchor}]{#_Toc237660663 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}Glossary


  --------------------------------- --------------------------------------------------------------------
  **Term **                         **Description**
  Shall                             Mandatory
  Should                            Highly desirable, but not mandatory
  []{#_Ref252190675 .anchor}MiDaS   Migration Data Store – used to track migration related activities.
  --------------------------------- --------------------------------------------------------------------

Introduction
============

[[[[[[]{#_Toc143240778 .anchor}]{#_Toc237660663 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}Document Purpose


The Service Specification document is a subjective document which
describes the interface, operations and implementation of a single
service.

It also serves the purpose of an as-built reference to describe the
production service and, as such, forms part of the SOA development
deliverables. Every service that is delivered to the SOA platform must
have an accompanying Service Specification which describes the service.

[[[[[[]{#_Toc143240778 .anchor}]{#_Toc237660663 .anchor}]{#_Toc159915943
.anchor}]{#_Toc156645505 .anchor}]{#_Toc153600111
.anchor}]{#_Toc153595981 .anchor}Audience


This document is created for the following audience:

-   Governance Team

-   Design Team

-   Development Team

-   Testing Team

-   Support Team

\
Integration Flow
================

The CreateVOIPMigrationWorkOrder service is part of the integration flow
“Service Problem Management”. Please refer to the SOA Blueprint document
\[[Ref03](#Ref03)\] for details of the flow.

 {#section-1 .ListParagraph}

[[[[[[[[[[[[[]{#_Data_Mapping_Sheet .anchor}]{#_Invoke_OC_to
.anchor}]{#_Validation_Rules .anchor}]{#_Service_Interface_Definition
.anchor}]{#_REST_Service_Specification .anchor}]{#_Toc496780400
.anchor}]{#_Toc496780399 .anchor}]{#_Toc496780398
.anchor}]{#_Toc496780397 .anchor}]{#_Toc496780373
.anchor}]{#_Toc496780372 .anchor}]{#_Toc496780371
.anchor}]{#_Toc496780370 .anchor}

REST Service Specification 
===========================

Service Overview
----------------

### Function(s)

  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Operation Name**             **RESTFul Style Operation**   **Function(s)**                                                                                                                                                                                                                                                                                   **Limitations**
  ------------------------------ ----------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- -----------------
  CreateVOIPMigrationWorkOrder   POST                          This is a technical service used to facilitate the Migration process (by creating a workorder) for the customers from ‘TDM’ telephony service to the Voice over Cable (VoC) service. It also updates the Customer Migration status in MIDAS after attempting to create the Migration Workorder.   N/A
                                                                                                                                                                                                                                                                                                                                                                 
                                                               *Note: Please be aware that this service doesn’t check customer eligibility for migration before creating a ‘Migration Workorder’. It is therefore consumer’s responsibility to check the customer migration eligibility before calling this service to create a ‘Migration Workorder’.*          
  --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Service Interface Definition

The JSON schemas can be found in the below
[location](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Service%20Documentation/CreateVOIPMigrationWorkOrder)

-   CreateVOIPMigrationWorkOrderRequest.json

-   CreateVOIPMigrationWorkOrderResponse.json

The policies for RESTful interface as mentioned in Section 3 of [SOA
Principles and
Policies](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Standards/Governance/SOA%20Principles%20and%20Policies.doc)
must be adhered to.

#### Other Details

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
                                                    **Dependencies**                                                                                   
  -------------------- ---------------------------- ---------------------- -------------------------------------------------------- ------------------ ----------------------------- -------------------------------------------------------------------- -------------------------------------------------------------------------------------- ------------------------------
  **Operation Name**   **Operation Type**           **Back end systems**   **Other VM SOA platform services**                       **Message Type**   **Binding Information**       **Message Exchange Pattern**(Sync – SRR, Async- Define explicitly)   **RESTFul Service EndPoint **                                                          **HTTP Response codes**
                                                                                                                                                                                                                                                                                                                                                 
                       (Basic, Composed, Process)                                                                                   (XML/JSON/Other)   (SOAP, RESTFul, JMS, Other)                                                                                                                                                               

  POST                 Composed                     Middleware (MiDaS)     GetVOIPLineMigrationDetails                              JSON               RESTFul                       Sync – SRR                                                           http(s)://&lt;serverHost&gt;:&lt;serverPort&gt;/restapi/CreateVOIPMigrationWorkOrder   200 (Success),
                                                                                                                                                                                                                                                                                                                                                 
                                                    Middleware (ICOMS)     UpdateVOIPLineMigration. UpdateVOIPLineMigrationStatus                                                                                                                                                                                                                400, 404, 415, 500 (Failure)
  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Revision History

*This section tracks each revision of the service. This is different to
the document version number which may be incremented many times during
design and review stages for a particular service revision. The
intention of the section is to clearly document the delta between
revisions of the same service. This will only be used where the service
has been extended in a backward compatible way.*

There must at all times be a base-lined reversion of each Service
Specification which is aligned with the latest production version of the
physical service.

There may also be one or (in the case of parallel development) more
working copies of a Service Specification Versions and Revisions which
have been created as part of an overall Solution Design for an objective
purpose such as a project. As new versions and revisions of a service
are delivered to production the relevant Service Specification would
then become the base-lined version and replace the previous version.

  **Revision**   **Purpose**        **Description of Changes**
  -------------- ------------------ -------------------------------------------
  1              Initial revision   Initial version based on Solution Design.

 {#section-2 .ListParagraph}

Operations
----------

### CreateVOIPMigrationWorkOrder – POST

##### Request Header

The standard HTTP request headers should contain the following values:

-   content-type: application/json; charset=utf-8

The below set of custom HTTP headers are also to be passed, as described
in the table below.


**\
**


##### Response Header

**HTTP Status code**: [Please refer section
4.1.2](#_Service_Interface_Definition)



#### Validation Rules

Following parameters should NOT be ‘NULL’ or ‘BLANK’ in the post
request:

1.  ‘telephoneNumber’,

2.  ‘accountNumber’

3.  ’siteReference’.

#### Errors

All SOA errors can be found in the SOA Master Error List \[Ref04\]. The
following are the errors that are initiated by this service:

  **Type**   **Code**   **Severity**   **Description**      **Source System**
  ---------- ---------- -------------- -------------------- -------------------
  SYSTEM     10686      CRITICAL       System Exception     Middleware
  BUSINESS   10685      ERROR          Business Exception   Middleware

#### Sample Test Cases

##### Test Case 1 – Success response

###### Purpose of Test

The purpose of this test is where a valid request for
CreateVOIPMigrationWorkOrder ‘POST’ request is passed and a success
response is received.

###### Request

###### Expected Response

Http Code: 200- OK

##### Test Case 2 – Schema Validation Exception 

###### Purpose of Test

The purpose of this test is where the request does not validate/has
schema validation error. {{Mandatory field not passed / invalid data
type}}.

###### Request

###### Expected Response

Http Code: 400- Bad Request

##### Test Case 3 – Backend Business Exception 

###### Purpose of Test

The purpose of this test is where there is a business exception while
invoking child services.

###### Request

###### Expected Response

Http Code: 500 Internal Server Error

##### Test Case 4 – Backend System Exception 

###### Purpose of Test

The purpose of this test is where there is a system exception while
invoking child services.

.

###### Request

###### Expected Response

Http Code: 400 Bad Request

##### Test Case 5 – Unexpected Exception 

###### Purpose of Test

The purpose of this test is where there is a system exception/unexpected
exception while processing the request.

###### Expected Response

Http Code: 500 Internal Server Error

Basic Sanity Checks/Tests
-------------------------

The test team/individual testing this service should ensure the below
scenarios are covered as minimum in addition to project/solution
specific test scenarios.

### Header Validation Checks

**Testing team** to perform checks to ensure the following header
elements are passed by consumer to middleware service in the Request
Header.

**This is a contractual agreement for consumers but not for development
(i.e. code doesn’t throw any exceptions) **

VMMD-activityName, VMMD-conversationID, VMMD-requestID,
VMMD-requestTimeStamp, VMMD-senderURI, VMMD-originatorURI, VMMD-userid

The below header elements could be passed when invoking this service.

VMMD-version, VMMD-service, VMMD-operation,
VMMD-priority,VMMD-senderCountry and VMMD-targetCountry

The below header elements are not used unless explicitly mentioned in
the above two points.

VMMD-replyToURI, VMMD-failureToURI, VMMD-securityType, VMMD-security,
VMMD-messageID

**Perform checks to ensure the following header elements are returned in
response Header**

VMMD-conversationId (if presented in the request), VMMD-requestId,
VMMD-requestTimeStamp, VMMD-responseTimeStamp, VMMD-responseStatus,
VMMD-messageID (if presented in the request)

### Functionality Checks

  1   Perform scenarios for mandatory and non-mandatory request elements
  --- --------------------------------------------------------------------------------------------
  2   Perform scenarios for all error codes of the service
  3   Perform scenarios to check configuration changes if any
  4   Perform scenarios to check mandatory response elements (non-mandatory where applicable)
  5   Create workorder with and without ‘Vulnerabilities details’ passed from the child service.

***NOTE:  The above scenarios are just to cover the basic features of
this service. ***

***The service test cases created should cover the above AT LEAST, but
NOT just that.***

Solution specific and Project specific scenarios are in addition to the
above and needs to be identified by the test team and created in their
test plan.

Technical Specification
-----------------------

### CreateVOIPMigrationWorkOrder – POST

#### Technical Process


**\
**

##### Perform Request Validation

Upon receiving service request, perform request validation as specified
in validation section. If request validation fails, send a failure
response to the consumer.

To build the response refer to ’To Response (Failure)’ tab in the Data
Mapping Sheet. **Operation returns to calling client.**

##### Get Workorder Data

After successful validation, create and invoke service request for
‘GetVOIPLineMigrationDetails’ to retrieve customer’s Migration workorder
data from MIDAS. Failure to retrieve Migration workorder data should
send a failure response to the consumer.

To build the response refer to ’To Response (Failure)’ tab in the Data
Mapping Sheet. **Operation returns to calling client.**

##### Create Migration Workorder

After successfully retrieving customer’s migration workorder data create
and invoke service request for ‘CreateWorkorder\_V3’ to create Migration
workorder.

In case of both success and failure update migration status (refer to
next section ‘Update Migration Status’) before sending response to the
consumer.

##### Update Migration Status

Depending upon the failure or success from the previous step, retrieve
corresponding workorder status from the configuration and update
customer’s Migration status in MIDAS using middleware service
‘UpdateVOIPLineMigration.UpdateVOIPLineMigrationStatus’.

##### MAP (Success or Failure) Response

Use the following logic to map a success or a failure response after the
migration workorder is invoked:

IF workorder is successfully created THEN

-   Where customer’s migration status is successfully updated send a
    success response with the workorder number to the consumer.
    **Operation returns to calling client.**

-   Where customer’s migration status is NOT successfully updated send a
    success response with the workorder including a fault node
    (highlighting migration status update failure) to the consumer.
    **Operation returns to calling client.**

IF workorder is NOT successfully created THEN

-   Where customer’s migration status is successfully updated send a
    Failure response including fault node (highlighting migration status
    update failure) to the consumer. **Operation returns to calling
    client.**

-   Where customer’s migration status is NOT successfully updated send a
    failure response including two faults nodes highlighting both
    (‘migration workorder failure’ and ‘migration status update
    failure’) to the consumer. **Operation returns to calling client.**

##### Data Mapping Sheet

Non-functional requirements
===========================

Security Requirements
---------------------

Follow BAU security standards, this is no service specific
requirement/standards to implement.

Configuration Requirements
--------------------------

### Timeouts

#### Child Services Timeout

Read timeout for calling the child services.

  **Time in Seconds**   **Middleware Service**
  --------------------- -------------------------------------------------------
  3                     GetVOIPLineMigrationDetails
  10                    CreateWorkOrder\_V3 (R5)
  3                     UpdateVOIPLineMigration.UpdateVOIPLineMigrationStatus

#### Configuration for Migration Status Update

  **Status Update Key**          **Status Update Key Value**   **Status Update Key Description**
  ------------------------------ ----------------------------- ---------------------------------------------
  Workorder.fail.openworkorder   Fail-Open WO                  Workorder failed due to an existing WO
  Workorder.fail.other           Fail-Others                   Workorder failed due to any other failures.
  Workorder.success              Complete                      Workorder successfully created.

Performance and Capacity Planning Requirements
----------------------------------------------

-   Expected number of service invocations per day: 1,00,000/day and
    *5000*/hr

-   Expected peak concurrent service invocations: 60 concurrent

-   95^th^ percentile response time of CreateVOIPMigrationWorkOrder
    (REST) Service: &lt; 1.0 second

-   95^th^ percentile response time of CreateVOIPMigrationWorkOrder
    (SOAP) Service: &lt; 0.75 second

The performance numbers from solution design or per consumer should also
be entered in the
[Performance](http://sharepoint/sites/support/Technology/devsupport/solutiondesign/CCMSD/SOA/Configuration%20Management/Service%20Performance%20and%20Capacity.xls)
sheet in SharePoint.

 {#section-3 .ListParagraph}

Troubleshooting
===============

Following table can be used to investigate the errors which could be
returned from this service, their root cause, potential resolution and
monitoring options.

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Symptom**                               **Cause**                                                                                                                                   **Resolution**                                             **Monitoring Method**
  ----------------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------- ---------------------------------------------------------- ------------------------------------------------------------------
  Operation is returning error code 10685   Business Exception. The backend service could have thrown business exception.                                                               Review the middleware logs and investigate error details   Watch the service log file for any instance of error code 10685.
                                                                                                                                                                                                                                                   
                                            There may be validation errors                                                                                                                                                                         

  Operation is returning error code 10686   Validation or System Exception.                                                                                                             Review the middleware logs and investigate error details   Watch the service log file for any instance of error code 10686
                                                                                                                                                                                                                                                   
                                            For Validation Exception, SOAP header or SOAP body or both have failed validation.                                                                                                                     
                                                                                                                                                                                                                                                   
                                            For System Exception, Backend service invocation has timed out. It is also possible that there is system exception in the service itself.                                                              
  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
