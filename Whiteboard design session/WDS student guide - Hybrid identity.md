![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/main/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Hybrid identity
</div>

<div class="MCWHeader2">
Whiteboard design session student guide
</div>

<div class="MCWHeader3">
February 2022
</div>


Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2022 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Hybrid identity whiteboard design session student guide](#hybrid-identity-whiteboard-design-session-student-guide)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Step 1: Review the customer case study](#step-1-review-the-customer-case-study)
    - [Customer situation](#customer-situation)
    - [Customer needs](#customer-needs)
    - [Customer objections](#customer-objections)
    - [Key design considerations](#key-design-considerations)
    - [Infographic for common scenarios](#infographic-for-common-scenarios)
  - [Step 2: Design a proof of concept solution](#step-2-design-a-proof-of-concept-solution)
  - [Step 3: Present the solution](#step-3-present-the-solution)
  - [Wrap-up](#wrap-up)
  - [Additional references](#additional-references)

<!-- /TOC -->

#  Hybrid identity whiteboard design session student guide

## Abstract and learning objectives 

In this whiteboard design session, you will learn how to implement different components of a hybrid identity solution that integrates an Active Directory forest with an Azure Active Directory tenant and leverages a number of Azure Active Directory features, including pass-through authentication with Seamless Single Sign-On, Multi-Factor Authentication, Self-Service Password Reset, Azure AD Password Protection for Windows Server Active Directory, Hybrid Azure AD join, Windows Hello for Business, Microsoft Authenticator, Microsoft Intune automatic enrollment, Azure AD Conditional Access, Azure AD Application Proxy, Azure AD B2B, and Azure AD B2C.

## Step 1: Review the customer case study

**Outcome**

Analyze your customer's needs.

Timeframe: 15 minutes

Directions: With all participants in the session, the facilitator/SME presents an overview of the customer case study along with technical tips.

1. Meet your team members and trainer.

2. Read all directions for steps 1-3 in the student guide.

3. As a team, review the following customer case study.

### Customer situation

Contoso is a medium size financial services company with its headquarters in New York and a branch office in San Francisco. It is currently operating entirely on-premises, with majority of its infrastructure running on the Windows platform. 

Contoso is facing challenges related to increased mobility of its workforce. In particular, in order to drive down its office space costs, Contoso management is considering implementing a flexible work arrangement policy which would allow its employees to work on designated days from home, using either corporate- and employee-owned devices. However, the Contoso's Information Security team expressed concerns about insufficient controls that would prevent access from unauthorized or non-compliant systems. In addition, there are concerns regarding using traditional VPN technologies or DirectAccess, which tend to provide excessive access to on-premises infrastructure. 
 
**Existing Contoso Active Directory environment**

Contoso has a single domain Active Directory forest which was implemented over a decade ago. The domain was assigned a non-routable DNS name contoso.local. While the Directory Services team considered renaming the domain, this has never been implemented due to potential negative implications of such change. Contoso does own a publicly routable DNS domain name contoso.com.

Contoso has recently upgraded its Active Directory environment to Windows Server 2016, and is in the process of migrating its desktops from Windows 7 to Windows 10. The majority of their servers are running either Windows Server 2012 R2 or Windows Server 2016. 

**Customer objectives**

Contoso is exploring the option of transitioning its operations into a more internet-open model which would facilitate support for mobile workforce and integration with business partners, while, at the same time, support current security and manageability controls. Given its current environment, which is heavily dependent on Active Directory and undergoes migration to Windows 10 devices, Contoso intends to evaluate Azure Active Directory and Microsoft Intune as potential identity and management components of the target design.

The identity component of the target design should facilitate step-up authentication and per-application permissions based not only on the properties of users' accounts but also on the state of these users' devices. To maximize security, Contoso wants to minimize or even eliminate persistent assignments of privileged roles for identity management, but, at the same time, such arrangement must account for break-glass scenarios, allowing for a non-gated emergency use of privileged accounts. For obvious reasons, such accounts need to be closely monitored and audited.
 
Another Information Security concern is accidental exposure of users' passwords. Contoso would like to minimize their use in lieu of more secure authentication methods. In situations where passwords are required, users should also be able to both change and reset them without having to rely on HelpDesk services. At the same time, any on-premises Active Directory user account restrictions, such as allowed sign-in hours must be honored. Similarly, the existing Active Directory password policies must apply, although the head of Information Security would like to enhance them by preventing use of common terms within password values.
 
Besides enhancing self-service user capabilities, Contoso wants to optimize end-user experience, especially in environments where users might be using several different devices. The user-defined settings, such as accessibility or app customization should be consistent across all devices.
 
In addition, Contoso needs to expand its customer base through partnership with other financial institutions and providing direct access to its services to external clients. As part of this effort, Contoso established business relationship with Fabrikam, which manages an extensive portfolio of mortgage related products. Contoso intends to provide Fabrikam with access to its internal Windows Integrated Authentication-based web applications that could be integrated with the existing Fabrikam's products. The access methodology needs to account for the fact that in recent years, Fabrikam has modernized its technology and moved its operations almost entirely to Microsoft Azure.
 
To facilitate the expansion of their customer base, Contoso started developing a number of applications intended to be available both via web and from mobile devices. Historically, such applications were hosted in on-premises data centers, and relied on an internally developed identity management product. Going forward, Contoso wants to minimize the effort managing customer identities.

The management team of Contoso, including its CIO, Andrew Cross, emphasized the need for resiliency and Service Level Agreements associated with each of the identity-related components that are part of the target design. At the same time, they are also interested in minimizing additional infrastructure requirements to implement the design.

### Customer needs 

1.  Remote users must be able to sign into their devices using their Active Directory credentials.

2.  Existing Active Directory user sign-in hours and password policies must be preserved (although allowed password values could be further restricted). 

3.  User sign-in experience should be simplified by minimizing the number of sign-in prompts and limiting the use passwords in lieu of more secure authentication methods. 

4.  User device configuration should be simplified by leveraging a mobile device management solution and roaming user-specific settings across multiple devices.

5.  Control access of users to applications and resources by relying on a combination of multiple conditions, including users group membership, state of the users' devices, and dynamically evaluated risk based on heuristics and globally collected security related telemetry.

6.  Users must be allowed to reset their own passwords. 

7.  Designated users should be able to temporarily elevate their privileges to manage other user accounts. All elevation events must be edited.

8.  Contoso remote users must be able to access on-premises Windows Integrated Authentication-based applications.

9.  Fabrikam users must be able to access on-premises Windows Integrated Authentication-based applications.

10.  Commercial applications developed by Contoso programmers must be made available to external customers with minimum overhead associated with identity management.

11.  Resiliency must be maximized whenever possible.  Users must not lose authentication capabilities or the ability to access on-premises applications.

12.  Infrastructure requirements must be minimized.

### Customer objections 

1.  Our Active Directory domain is using a non-routable domain name. We cannot risk renaming it in order to implement single sign-on with Azure Active Directory.

2.  We have heard that it is not possible to run multiple instances of Azure AD Connect simultaneously. All identity services components in our environment must provide resiliency and support failover.

3.  If we decide to integrate our Active Directory environment with Azure Active Directory, this must be performed in stages. This is likely to be complex, considering that users in each stage would be members of different Active Directory groups and their accounts might reside in different Active Directory organizational units.

4.  Synchronizing our Active Directory accounts with Azure AD accounts makes the former vulnerable to malicious or accidental lockouts that affect the latter. This would effectively expose our on-premises environment to external attacks. 

5.  A number of critical web applications running in our on-premises environment rely on Kerberos-based Windows Integrated Authentication. Microsoft states that Azure Active Directory does not support Kerberos. Doesn't this mean that remote users authenticating to Azure Active Directory and our business partners will not be able to properly authenticate and access these applications?

### Key design considerations

1.  The choice of the authentication method supported in hybrid identity scenarios

2.  The choice of scope synchronization between Active Directory and Azure AD

3.  The choice of Azure AD edition required to satisfy Contoso's requirements

4.  The Service Level Agreements associated with the choice of the Azure AD edition 

5.  Requirements necessary to minimize dependency on passwords in lieu of more secure authentication methods

6.  The approach to allowing different authentication requirements, depending on users' group membership, state of the user devices, and dynamically evaluated risk based on heuristics and globally collected security related telemetry

7.  The approach to providing Contoso and Fabrikam users access to on-premises web applications that rely on Kerberos-based Windows Integrated Authentication

8.  The approach to providing external customers access to custom-developed applications with minimum overhead associated with identity management

9.  The method of implementing redundancy in your solution


### Infographic for common scenarios

![The diagram illustrating Azure AD Hybrid Identity with Password Hash Sync. On the left hand side, there is a cloud shape representing Public Cloud SaaS services, including Azure and Office 365, The user and the user's computer icons are positioned directly underneath. The user signs in to Azure AD represented by a circle containing the Azure AD symbol, which is pointed to by a unidirectional arrow originating from the computer icon labeled Azure AD Connect positioned on the right-hand side of the slide. This icon is connected via a unidirectional arrow to the icon representing an Active Directory domain controller, directly below it.](images/Whiteboarddesignsessiontrainerguide-HybridIdentityimages/media/azure-ad-authn-image2.png "Azure AD hybrid identity password-hash synchronization")

![The diagram illustrating Azure AD Hybrid Identity with Pass-through authentication. On the left hand side, there is a cloud shape representing Public Cloud SaaS services, including Azure and Office 365, The user and the user's computer icons are positioned directly underneath. The user signs in to Azure AD represented by a circle containing the Azure AD symbol. On the right-hand side of the slide, there are several icons within the area of the image labeled On-premises.. These icons represent an Active Directory domain controller and Azure AD Connect server that collectively perform identity sync. The domain controller also interacts with Authentication Agents that handle pass-through authentication.](images/Whiteboarddesignsessiontrainerguide-HybridIdentityimages/media/azure-ad-authn-image3.png "Azure AD hybrid identity pass-through authentication")

![The diagram illustrating Azure AD Hybrid Identity with Federated authentication. On the left hand side, there is a cloud shape representing Public Cloud SaaS services, including Azure and Office 365, The user and the user's computer icons are positioned directly underneath. The user signs in to Azure AD represented by a circle containing the Azure AD symbol. The sign-in is redirected to the area of the slide labeled Perimeter, containing two icons representing Federation Proxy servers. These servers, communicate with Federation Servers located in the area of the slide labeled On-premises. The Federation Servers communicate with an Active Directory domain controller, which, in turn, interacts with Azure AD Connect server that handles identity sync.](images/Whiteboarddesignsessiontrainerguide-HybridIdentityimages/media/azure-ad-authn-image4.png "Azure AD hybrid identity federation")

## Step 2: Design a proof of concept solution

**Outcome**

Design a solution and prepare to present the solution to the target customer audience in a 15-minute chalk-talk format.

Timeframe: 60 minutes

**Business needs**

Directions: With your team, answer the following questions and be prepared to present your solution to others:

1. Who will you present this solution to? Who is your target customer audience? Who are the decision makers?

2. What customer business needs do you need to address with your solution?

**Design**

Directions: With your team, respond to the following questions:

*Architecting a hybrid identity solution*

1.  Using the features of Azure Active Directory and the requirements from the customer, how would you design a Hybrid Identity solution?

2.  How does your design accounts for customer objectives and objections?

*Architecting a hybrid authentication solution*

1.  How does your solution address all the customer requirements in regard to authentication?

*Implementing a hybrid identity solution*

1.  What are the steps to implement a hybrid identity solution that will allow you to meet all the customer requirements?

*Assessing resiliency aspects of a hybrid identity solution*

1.  What are provisions that eliminate single points of failure in your design?

2.  What is the failover process for components that operate in the active/passive mode?

*Optimizing authentication configuration*

1.  What features will allow to optimize authentication in your solution to satisfy the following customer requirements?

*Optimizing authorization configuration*

1.  What features will allow to optimize authorization in your solution to satisfy the following customer requirements?

*Optimizing access control and management of applications and devices*

1.  What features will allow to optimize access control and management of applications and devices to satisfy the following customer requirements?

**Prepare**

Directions: As a team:

1. Identify any customer needs that are not addressed with the proposed solution.

2. Identify the benefits of your solution.

3. Determine how you will respond to the customer's objections.

Prepare a 15-minute chalk-talk style presentation to the customer.

## Step 3: Present the solution

**Outcome**

Present a solution to the target customer audience in a 15-minute chalk-talk format.

Timeframe: 30 minutes

**Presentation**

Directions:

1. Pair with another team.

2. One group is the Microsoft team, the other is the customer.

3. The Microsoft team presents their proposed solution to the customer.

4. The customer makes one of the objections from the list of objections.

5. The Microsoft team responds to the objection.

6. The customer team gives feedback to the Microsoft team.

7. Switch roles and repeat Steps 2-6.

## Wrap-up

Timeframe: 15 minutes

Directions: Reconvene with the larger group to hear the facilitator/SME share the preferred solution for the case study.

##  Additional references

|    |            |
|----------|:-------------:|
| **Description** | **Links** |
| What is hybrid identity with Azure Active Directory? | <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/whatis-hybrid-identity>  |
| Choose the right authentication method for your Azure Active Directory hybrid identity solution | <https://docs.microsoft.com/en-us/azure/security/fundamentals/choose-ad-authn>  |
| Azure AD Connect sync: Understand and customize synchronization |  <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-sync-whatis> |
| Buy a custom domain name for Azure App Service | <https://docs.microsoft.com/en-us/azure/app-service/manage-custom-dns-buy-domain>  |
| What is Conditional Access? | <https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/overview>  |
| Azure Active Directory B2B documentation | <https://docs.microsoft.com/en-us/azure/active-directory/b2b/>  |
| Azure Active Directory B2C documentation | <https://docs.microsoft.com/en-us/azure/active-directory-b2c/>  |
| Microsoft Enterprise Mobility + Security options | <https://www.microsoft.com/en-us/microsoft-365/enterprise-mobility-security/compare-plans-and-pricing>
