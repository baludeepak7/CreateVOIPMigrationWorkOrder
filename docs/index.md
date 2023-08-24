![](media/image1.jpeg){width="1.5104166666666667in"
height="1.0729166666666667in"}

CreateVOIPMigrationWorkOrder

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

**\
**[[[[]{#_Toc159915941 .anchor}]{#_Toc156645503 .anchor}]{#_Toc153600109
.anchor}]{#_Toc153595979 .anchor}
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

**\
**[[[[]{#_Toc159915941 .anchor}]{#_Toc156645503 .anchor}]{#_Toc153600109
.anchor}]{#_Toc153595979 .anchor}
Document Control
================

**\
**[[[[]{#_Toc159915941 .anchor}]{#_Toc156645503 .anchor}]{#_Toc153600109
.anchor}]{#_Toc153595979 .anchor}Document Information
--------------------


**\
**[[[[]{#_Toc159915941 .anchor}]{#_Toc156645503 .anchor}]{#_Toc153600109
.anchor}]{#_Toc153595979 .anchor}Document History
----------------

 
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

#### Business Process

![H:\\My Documents\\Project Folder\\\_21CV Project\\Single Customer
Migration Solution\\Activity
Diagram.bmp](media/image3.png){width="6.456944444444445in"
height="6.1030588363954505in"}

#### Request

##### Request Header

The standard HTTP request headers should contain the following values:

-   content-type: application/json; charset=utf-8

The below set of custom HTTP headers are also to be passed, as described
in the table below.

![RequestHeader.2.2\_JSON](media/image4.png){width="3.134738626421697in"
height="7.4959995625546805in"}

**\
**

##### Request Body

![H:\\My Documents\\Project Folder\\21CV Project\\Single Customer
Migration Solution\\CreateVOIPMigrationWorkOrder\\XMLSpy
Images\\REST-Request.png](media/image5.png){width="6.44799978127734in"
height="4.183999343832021in"}

#### Response

##### Response Header

**HTTP Status code**: [Please refer section
4.1.2](#_Service_Interface_Definition)

![RESTResponse](media/image6.png){width="3.509215879265092in"
height="4.395833333333333in"}

##### Response Body

![H:\\My Documents\\Project Folder\\\_21CV Project\\Single Customer
Migration
Solution\\Response.png](media/image7.png){width="6.458333333333333in"
height="3.2708333333333335in"}

##### Fault

![Fault\_2](media/image8.png){width="3.2164052930883638in"
height="8.572916666666666in"}

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

![H:\\My Documents\\Project Folder\\\_21CV Project\\Single Customer
Migration Solution\\Sequence
diagram.bmp](media/image18.png){width="6.458016185476815in"
height="7.666666666666667in"}

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
