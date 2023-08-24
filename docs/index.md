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

Document Control
================

**\
**[[[[]{#_Toc159915941 .anchor}]{#_Toc156645503 .anchor}]{#_Toc153600109
.anchor}]{#_Toc153595979 .anchor}DOCUMENT INFORMATION

  -------------------------- ----------------------------
  **Document Author:**       Saleem Khan
  **Title:**                 <CreateVOIPMigrationWorkOrder>
  **Status:**                Issued
  -------------------------- ----------------------------

[[[[[]{#_Toc143240777 .anchor}]{#_Toc159915942 .anchor}]{#_Toc156645504
.anchor}]{#_Toc153600110 .anchor}]{#_Toc153595980 .anchor}CHANGE HISTORY
