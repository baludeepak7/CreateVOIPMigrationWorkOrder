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

Document Information
--------------------

  ------------------------------ -----------------------------------------------------------------
  **Title**                      CreateVOIPMigrationWorkOrder (Middleware Service Specification)
  **Author / (Last saved by)**   Saleem Khan / (Khan, Saleem)
  **Status**                     Issued
  ------------------------------ -----------------------------------------------------------------

Document History
----------------

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

SOA Governance Approval
-----------------------

***The SOA Governance Authority is required to sign off this service
specification, and ensure that it adheres to SOA standards, before any
further sign off can be sought.***

  **Name**     **Title / Department**   **Approval (Y/N)**
  ------------ ------------------------ --------------------
  Steve King   SOA Governance           

Where the reviewer is not approving the document explain what changes
are needed.

For Review By
-------------

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

