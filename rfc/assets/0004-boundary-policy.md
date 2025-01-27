# FedRAMP Boundary Policy **Working DRAFT**

APPLICABILITY

This policy defines requirements and recommendations related to FedRAMP
boundaries for the following parties:

- **Cloud service providers (CSPs)** who participate or want to participate in
  the FedRAMP marketplace
- **Independent assessors (IAs)** who perform third-party cybersecurity
  assessments for cloud service offerings (CSOs) through their FedRAMP packages.
  IAs conduct both initial and periodic evaluations of CSOs to ensure they
  comply with federal security requirements. IAs are also known as _third-party
  assessment organizations (3PAOs)_.
- **Package reviewers from _FedRAMP designated leads_,** who are federal
  agencies responsible for sponsoring CSPs for FedRAMP authorization. A
  designated lead can be:
  - An authorizing official at a federal agency; or
  - The FedRAMP Director at GSA in the case of a program-sponsored
    authorization.
> Will this boundary guidance possibly conincide with the release of a "program-sponsored" authorization path? Since this path is being referenced in what will become official guidance, this is a great sign, however; if it's not going to be in place once this is released, I recommend removing the reference until the path is fully available. 

The purpose of this guidance is to establish greater consistency and a shared
interpretation of which systems and data fall within a FedRAMP authorized
boundary, and which do not, across all FedRAMP authorization pathways.

This guidance is normative and applies to **all** FedRAMP authorizations, and is
required to be followed by **all** cloud service providers (CSPs) and **all**
federal sponsors of FedRAMP authorizations (individual agencies, multi-agency
constructs, and FedRAMP itself in the case of program authorizations).

CSPs and IAs must adhere to this version of the policy by MONTH DD, 2025\.
Package reviewers from FedRAMP designated leads must adhere to this version of
the policy starting on MONTH DD, 2025\.

## TABLE OF CONTENTS

[1\. Policy Overview 4](#1.-policy-overview)

[1.1 Reuse of FedRAMP Authorized Cloud Service Offerings 4](#1.1-reuse-of-fedramp-authorized-cloud-service-offerings)

[1.2 Operations Outside the FedRAMP Boundary 4](#1.2-operations-outside-the-fedramp-boundary)

[2\. Requirements and Recommendations 5](#2.-requirements-and-recommendations)

[2.1 Cloud Service Providers 5](#2.1-cloud-service-providers)

[2.1.1 FedRAMP Boundary Definition 5](#2.1.1-fedramp-boundary-definition)

[2.1.2 FedRAMP Boundary Protection of Information 6](#2.1.2-fedramp-boundary-protection-of-information)

[2.1.3 FedRAMP Boundary Restrictions on Inbound and Outbound Connections 6](#2.1.3-fedramp-boundary-restrictions-on-inbound-and-outbound-connections)

[2.2 Independent Assessors (IAs) 6](<#2.2-independent-assessors-(ias)>)

## 1\. Policy Overview

The FedRAMP boundary defines the scope of a Cloud Service Offering (CSO) that
must be assessed for FedRAMP authorization.

The **_FedRAMP boundary_** includes all aspects of the CSO, including external
services, that:

1. handle[^1] federal information; and/or
2. directly impact the confidentiality, integrity, or availability of federal
   information

This includes all services to be consumed by tenants/customers and the
underlying components, infrastructure, and services (including external
services), that handle federal information as part of the CSO and the related
organizational users operating the service. It also includes privileged security
tooling, authentication systems, management/orchestration, and keying material
and secrets.

Cloud Service Providers (CSPs) and Independent Assessors (IAs) are encouraged to
engage FedRAMP when navigating complex scenarios about when services should be
inside the boundary or not. FedRAMP will create and maintain a
[knowledge base](https://help.fedramp.gov) of examples with specific guidance
where appropriate to help CSPs and IAs navigate this.

_[^1]: inclusive of any possible use of information, including creation,
collection, processing, storing, transmitting, accessing, disposing, etc._

### **1.1 Reuse of FedRAMP Authorized Cloud Service Offerings**

CSPs can leverage existing FedRAMP authorized cloud service offerings as part of
their CSO to streamline their engineering and authorization process. Reusing a
FedRAMP authorized cloud service offering will allow the CSO to inherit the
existing implementation, assessment, and testing of services from those cloud
service offerings without including the entirety of those offerings inside the
FedRAMP boundary.

The relevant inherited controls from leveraged FedRAMP authorized cloud service
providers should be reviewed during reuse or agency assessment for an
Authorization to Operate but should not be duplicated in the FedRAMP boundary or
assessment for the CSO. Documentation and assessment of leveraged FedRAMP
authorized cloud service offerings used by the CSO should be limited to the
configuration of leveraged services following guidelines in the leveraged
service’s Customer Responsibility Matrix (CRM) 
> As an advisor, I very often run into the problem that a lot of FedRAMP authorized services don't make their CRM's readily avaliable to anyone that does not have a .gov account required to request the package through the formal `package request` process. I've had a number of CSPs tell me that the CRM is `Sensitive Data` and refuse to provide to me. This makes leveraging services increasingly difficult, as we are essentially having to guess what controls can be `inherited` from the service being leveraged. There is also a difference between `leveraging` and `inheriting` that might be worth providing some clarity around. When a CSO `inherits` a control, I view that as there is nothing the CSP can do to reasonably assert any ability to impact that control's implementation and must completely rely on the FedRAMP authorized CSO being leveraged to provide for the complete control implementation. I think the best of example of this would be the ability to inherit many of the PE controls from Hyperscale providers, a CSO leveraging a hyperscale provider cannot reasonably do anything to implement a control that requires access logging at the data center, and therefore relies completely on the hyperscale provider to implement.
>
> However, 'leveraging' a CSO to implement a control is different. When I utilize a FedRAMP authorized Identity Provider as a Service (IDaaS), I am using that service to implement required controls on my CSO, however; I must configure the IDaaS in such a way that I have met the control requirements for my CSO. When I use the IDaaS to implement the requirements of IA-5 for example, I'm not `inherting` IA-5 from the IDaaS. This is a subtle but very distinct difference.
>
> I mention this because it would be great if there could be a way for FedRAMP to mandate/enforce the creation of documentation that must be made publicly available that requires CSOs to explicitly document where they can `inherit` controls and where their service can be utilized by other CSOs to for implementing control requirements. 

and remaining in compliance with
[CISA BOD 25-01: Implementation Guidance for Implementing Secure Practices for Cloud Services](https://www.cisa.gov/news-events/directives/bod-25-01-implementation-guidance-implementing-secure-practices-cloud-services).

### **1.2 Operations Outside the FedRAMP Boundary**

Ancillary services that support the CSP or CSO but pose negligible[^2] or no
direct risk to federal information should remain outside the FedRAMP boundary.
These systems may be documented in the SSP front matter and other diagrams as
appropriate to demonstrate operations of the CSO. Interactions with such systems
will be reviewed by the IA to affirm that they pose the low level of risk as
documented, but systems that pose this low risk will not be tested by the IA.

Examples of ancillary services that _may_ be outside the FedRAMP boundary
include corporate email services, development environments, and customer service
systems where a loss of confidentiality, integrity, or availability is not
likely to directly affect federal information within the CSO.

_[^2]: so small that it is not worth considering; any foreseeable risk would be
merely an inconvenience_

## 2\. Requirements and Recommendations

This section defines requirements and recommendations related to FedRAMP
boundaries for three types of stakeholders: CSPs, IAs, and package reviewers
from FedRAMP designated leads.

Each requirement and recommendation has an identifier that is unique across
FedRAMP policies. This identification approach enables referencing specific
requirements and recommendations in this and other resources.

### **2.1 Cloud Service Providers**

CSPs are responsible for defining the FedRAMP boundary for each of their CSOs,
protecting information and components within each boundary, and safeguarding the
environments of operation. The following requirements and recommendations apply
to all FedRAMP authorized CSOs unless otherwise stated.

#### **2.1.1 FedRAMP Boundary Definition**

- **FRR201:** CSPs **shall** include all CSO services and their underlying
  components, infrastructure, and services (including external services) that:

  - handle federal information; and/or

  - directly impact the confidentiality, integrity, or availability of federal
    information.

- **FRR202**: CSPs **shall** include any components required to be installed or
  run on a tenant system in order to use the CSO and may include additional
  optional components if they are included in the SSP.
> The inclusion of `may include additional optional components if they are included in the SSP` without examples is somewhat confusing. Is `optional` referring to a component that could be used based on how the agency is using the CSO, or does it mean that the component does not offer signficant risk to the CIA of `Federal Information` and is only being included for clarity? 
  

- **FRR203:** CSPs **shall** document all components, their relationships, data
  flows, types, encryption employed, access and policy enforcement points,
  security components, and ports/protocols/services used in the SSP.

- **FRR204:** CSPs **shall** address only the customer responsibilities for any
  FedRAMP authorized cloud service offerings that they wish to inherit controls
  from.
> See my comments above. These `responsibilities` are not always clearly understood by the CSO leveraging a service from an authorized CSO and getting the information is sometimes difficult, if not impossible. 

  Configurations must comply with
  [CISA BOD 25-01: Implementation Guidance for Implementing Secure Practices for Cloud Services](https://www.cisa.gov/news-events/directives/bod-25-01-implementation-guidance-implementing-secure-practices-cloud-services).

- **FRR205:** CSPs **shall** update boundary documentation as architectures
  evolve and as protections or data flows change. CSPs **shall** reflect such
  updates promptly in SSPs, continuous monitoring reports, and in the POA&M
  where they deviate from these requirements.
> Would it be good to tie this back to Change Management - I would argue that if boundary documentation requires an update, this needs to be associated with an appropriate Change Request. Maybe the way to frame it would be `CSPs shall update boundary documentation whenever there are changes to the system that impact the system architecture, boundary, protections and/or data flows. All changes shall be approved by the appropriate authority, and shall be reflected in prompt updates to the SSP, continuous monitoring reports upon implementation of the change. Any deviations from these requirements shall be documented in the POA&M and approved by the authorizing official.` 
  

#### **2.1.2 FedRAMP Boundary Protection of Information**

- **FRR206:** CSPs **shall** designate a System Owner for the CSO who has
  sufficient organizational authority to enforce all policies, procedures, and
  control implementations which affect the FedRAMP boundary, including
  contractual obligations with third parties.

- **FRR207:** CSPs **shall** **not** reuse federal information for shared
  purposes unless the government tenant specifically opts in to such sharing or
  grants access to the information. CSPs **shall** ensure that external services
  that handle federal information are configured to meet this requirement. This
  requirement applies to machine learning models trained on federal information.

- **FRR208:** CSPs **shall** ensure that security and administrative
  configuration, secrets, key material, and agents are managed within the
  FedRAMP boundary and are documented within the SSP.
> What does this mean for Infrastructure as Code (IaC)? Can IaC be managed in a developer or lower environment or does it have to be stored and managed within the FedRAMP authorization boundary? 
  

- **FRR209:** CSPs **shall** document and maintain information exchange
  agreements for all external systems within the FedRAMP boundary. This
  **shall** include the information types, encryption employed,
  ports/protocols/services used, access levels, and the requirement to meet
  FedRAMP security requirements.
> What `information types` are being referenced here? Are these the 800-60 information types? If so, what if the information being shared does not pertain to those information types? A good example of this would be utilizing a FedRAMP authorized SaaS for vulnerability scanning? That scan data would likely not be reflected in the NIST 800-60 information types.
>
> Is an `Information Exchange Agreement` going to be the only allowable format that this information can be captured in? If so, will FedRAMP be providing a template for the IEA with the requirement that every system documented in either Table 6.1 or 7.1 of the SSP is required to have a completed IEA using this template? This would different from the NIST requirements for CA-3: Information Exchange, where this information can be documented in a number of different agreements (including contracts) and is not currently mandated as an Organizationally Defined Parameter (ODP) in the FedRAMP SSP templates. 
  

- **FRR210:** CSPs **shall** ensure that federal information sent to public or
  commercial services used to support the function of a CSO is limited to
  information approved by the owner of the federal information.

#### **2.1.3 FedRAMP Boundary Restrictions on Inbound and Outbound Connections**

- **FRR211:** CSPs **shall not** permit any systems outside the FedRAMP boundary
  to directly access federal information or to make changes to the security of
  the FedRAMP boundary except when approved by the owners of the federal
  information.
> This seems to leave the door open for quite a bit of interpretation. If a system is outside the FedRAMP boundary, then it is outside the scope of an IA assessment. This requirement seems to indicate that a Federal Data Owner can approve the connection of a system that can directly access federal information or make changes to the security of the boundary based on their discretion. First, I think changing the term from `owner` to `Authorizing Official` might be best. The AO is ultimately responsible for accepting the risk of the system, and should be in charge of making decisions around such connections. There can be multiple Federal `Data Owners`in a CSO and they typically would not have the level of authority required to authorize system connections.
>
> Second, this seems to be a relatively broad ability being granted to the federal `owner`. This seems to indicate that the ability to approve connections to non-FedRAMP authorized systems, can be explicilty approved by a Federal `owner`. How does this impact a CSO's FedRAMP authorization?  
  
- **FRR212:** CSPs **shall** document all connections established between the
  FedRAMP boundary and systems in the environment of operations, including the
  data types, encryption employed, ports/protocols/services used, the level of
  access, and the service or component involved.

### **2.2 Independent Assessors (IAs)**

- **FRR216:** IAs **shall** test all components within the FedRAMP boundary and
  **shall** review and evaluate connections to systems outside the FedRAMP
  boundary as documented by the CSP following FRR201-212**.**

- **FRR217:** IAs **shall** review data flows between the FedRAMP boundary and
  the environment of operations, and **shall** validate the impact
  categorization of the data in those services, the presence of appropriate
  certifications, and ensure they have no direct security impact or privileged
  access to the federal information.

- **FRR219:** IAs **shall** document deviations from this guidance within the
  SAR, POA\&M, and other materials.
