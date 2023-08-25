CreateVOIPMigrationWorkOrder

Service Description
===================

The CreateVOIPMigrationWorkOrder service is part of the integration flow
“Service Problem Management”. This is a technical service used to
facilitate the Migration process (by creating a workorder) for the
customers from ‘TDM’ telephony service to the Voice over Cable (VoC)
service. It also updates the Customer Migration status in MIDAS after
attempting to create the Migration Workorder.

*Note: Please be aware that this service doesn’t check customer
eligibility for migration before creating a ‘Migration Workorder’. It is
therefore consumer’s responsibility to check the customer migration
eligibility before calling this service to create a ‘Migration
Workorder’.*[[]{#_Toc256000916 .anchor}]{#scroll-bookmark-2064 .anchor}

### CreateVOIPMigrationWorkOrder – POST


  telephoneNumber        (String) -     String e.g. 447874384949
  
  accountIdentification       (Object)  
  
  AccountIdentification.accountNumber   (String)  
  
  AccountIdentification.siteReference   (Numeric int)

Response
--------

  **Parameter**                                      **Data Type**
  -------------------------------------------------- ---------------
  CreateVOIPMigrationWorkOrder                       Object
  CreateVOIPMigrationWorkOrder.failure               Object
  CreateVOIPMigrationWorkOrder.failure.fault         Array
  CreateVOIPMigrationWorkOrder.success               Object
  CreateVOIPMigrationWorkOrder.success.fault         Array
  CreateVOIPMigrationWorkOrder.success.orderNumber   String

Following parameters should NOT be ‘NULL’ or ‘BLANK’ in the post
request:

-   ‘telephoneNumber’,

-   ‘accountNumber’

-   ’siteReference’.

Error response
--------------

  **Type**   **Code**   **Description**      **Severity**   **Source System**
  ---------- ---------- -------------------- -------------- -------------------
  SYSTEM     10686      System Exception     CRITICAL       Middleware
  BUSINESS   10685      Business Exception   ERROR          Middleware
