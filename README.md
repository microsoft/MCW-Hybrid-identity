# Hybrid identity

Contoso is a medium size financial services company with its headquarters in New York and a branch office in San Francisco. It is currently operating entirely on-premises, with the majority of its infrastructure running on the Windows platform. Contoso has recently upgraded its Active Directory environment to Windows Server 2016, and it is in the process of migrating its desktops from Windows 7 to Windows 10.
 
Contoso is facing challenges related to increased mobility of its workforce and providing access to its services to other financial partners. Contoso is looking to improve security while providing users with self-service capabilities around device, account, and password management. To drive better integration with partners, Contoso needs to provide access to some existing internal applications while maintaining a high level of security for applications hosted in the cloud and on premises while minimizing the effort required to manage customer identities.

May 2022

## Target audience

- Infrastructure Architect
- Security Architect
- IT Professional
- Cloud Solution Architect

## Abstracts

### Workshop

In this workshop, you will learn how to implement different components of a hybrid identity solution that integrates an Active Directory forest with an Azure Active Directory tenant and leverages a number of Azure Active Directory features.

At the end of this workshop, you will be able to plan, design, and deploy a hybrid identity architecture. The architecture will include a secure, available, and resilient hybrid identity infrastructure for identity and access management. 

### Whiteboard Design Session

In this whiteboard design session, you will learn how to implement different components of a hybrid identity solution that integrates an Active Directory forest with an Azure Active Directory tenant and leverages a number of Azure Active Directory features, including pass-through authentication with Seamless Single Sign-On, Multi-Factor Authentication, Self-Service Password Reset, Azure AD Password Protection for Windows Server Active Directory, Hybrid Azure AD join, Windows Hello for Business, Microsoft Intune automatic enrollment, Azure AD Conditional Access, Azure AD Application Proxy, Azure AD B2B, and Azure AD B2C.

### Hands-on Lab

In this hands-on lab you will setup and configure a number of different hybrid identity scenarios. The scenarios involve an Active Directory single-domain forest named contoso.local, which in this lab environment, consists (for simplicity reasons) of a single domain controller named DC1 and a single domain member server named APP1. The intention is to explore Azure AD-related capabilities that allow you to integrate Active Directory with Azure Active Directory, optimize hybrid authentication and authorization, and provide secure access to on-premises resources from Internet for both organizational users and users who are members of partner organizations.

### Azure services and related products

- Azure Active Directory
- Azure AD Connect
- Azure App Service
- Passthrough authentication with Seamless Single Sign-On
- Multi-Factor Authentication
- Self-Service Password Reset
- Azure AD Password Protection
- Hybrid Azure AD join
- Windows Hello for Business
- Microsoft Intune automatic enrollment
- Azure AD Conditional Access
- Azure AD Application Proxy
- Azure AD B2B
- Azure AD B2C

## Related references

- [Microsoft Cloud Workshops](https://microsoftcloudworkshop.com/index.html)
- [Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/)
- [What is hybrid identity with Azure Active Directory?](https://docs.microsoft.com/en-us/azure/active-directory/hybrid/whatis-hybrid-identity)
- [What is Conditional Access?](https://docs.microsoft.com/en-us/azure/active-directory/conditional-access/overview)
- [What is guest user access in Azure Active Directory B2B?](https://docs.microsoft.com/en-us/azure/active-directory/b2b/what-is-b2b)
- [What is Azure Active Directory B2C?](https://docs.microsoft.com/en-us/azure/active-directory-b2c/active-directory-b2c-overview)
- [What is Azure AD Connect cloud sync?](https://docs.microsoft.com/en-us/azure/active-directory/cloud-sync/what-is-cloud-sync)
- [Plan a passwordless authentication deployment in Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/authentication/howto-authentication-passwordless-deployment)

## Help & Support

We welcome feedback and comments from Microsoft SMEs & learning partners who deliver MCWs.  

***Having trouble?***
- First, verify you have followed all written lab instructions (including the Before the Hands-on lab document).
- Next, submit an issue with a detailed description of the problem.
- Do not submit pull requests. Our content authors will make all changes and submit pull requests for approval.  

If you are planning to present a workshop, *review and test the materials early*! We recommend at least two weeks prior.

### Please allow 5 - 10 business days for review and resolution of issues.
