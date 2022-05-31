![Microsoft Cloud Workshops](https://github.com/Microsoft/MCW-Template-Cloud-Workshop/raw/main/Media/ms-cloud-workshop.png "Microsoft Cloud Workshops")

<div class="MCWHeader1">
Hybrid identity
</div>

<div class="MCWHeader2">
Hands-on lab step-by-step
</div>

<div class="MCWHeader3">
May 2022
</div>


Information in this document, including URL and other Internet Web site references, is subject to change without notice. Unless otherwise noted, the example companies, organizations, products, domain names, e-mail addresses, logos, people, places, and events depicted herein are fictitious, and no association with any real company, organization, product, domain name, e-mail address, logo, person, place or event is intended or should be inferred. Complying with all applicable copyright laws is the responsibility of the user. Without limiting the rights under copyright, no part of this document may be reproduced, stored in or introduced into a retrieval system, or transmitted in any form or by any means (electronic, mechanical, photocopying, recording, or otherwise), or for any purpose, without the express written permission of Microsoft Corporation.

Microsoft may have patents, patent applications, trademarks, copyrights, or other intellectual property rights covering subject matter in this document. Except as expressly provided in any written license agreement from Microsoft, the furnishing of this document does not give you any license to these patents, trademarks, copyrights, or other intellectual property.

The names of manufacturers, products, or URLs are provided for informational purposes only and Microsoft makes no representations and warranties, either expressed, implied, or statutory, regarding these manufacturers or the use of the products with any Microsoft technologies. The inclusion of a manufacturer or product does not imply endorsement of Microsoft of the manufacturer or product. Links may be provided to third party sites. Such sites are not under the control of Microsoft and Microsoft is not responsible for the contents of any linked site or any link contained in a linked site, or any changes or updates to such sites. Microsoft is not responsible for webcasting or any other form of transmission received from any linked site. Microsoft is providing these links to you only as a convenience, and the inclusion of any link does not imply endorsement of Microsoft of the site or the products contained therein.

© 2022 Microsoft Corporation. All rights reserved.

Microsoft and the trademarks listed at <https://www.microsoft.com/en-us/legal/intellectualproperty/Trademarks/Usage/General.aspx> are trademarks of the Microsoft group of companies. All other trademarks are property of their respective owners.

**Contents**

<!-- TOC -->

- [Hybrid identity hands-on lab step-by-step](#hybrid-identity-hands-on-lab-step-by-step)
  - [Abstract and learning objectives](#abstract-and-learning-objectives)
  - [Overview](#overview)
  - [Solution architecture](#solution-architecture)
  - [Exercise 1: Integrate an Active Directory forest with an Azure Active Directory tenant](#exercise-1-integrate-an-active-directory-forest-with-an-azure-active-directory-tenant)
    - [Task 1: Create an Azure Active Directory tenant and activate an EMS E5 trial](#task-1-create-an-azure-active-directory-tenant-and-activate-an-ems-e5-trial)
    - [Task 2: Create and configure Azure AD users](#task-2-create-and-configure-azure-ad-users)
    - [Task 3: Purchase a custom domain name](#task-3-purchase-a-custom-domain-name)
    - [Task 4: Assign a custom domain name to the Contoso Azure AD tenant](#task-4-assign-a-custom-domain-name-to-the-contoso-azure-ad-tenant)
    - [Task 5: Configure DNS suffix in the Contoso Active Directory forest](#task-5-configure-dns-suffix-in-the-contoso-active-directory-forest)
    - [Task 6: Install Azure AD Connect](#task-6-install-azure-ad-connect)
    - [Task 7: Enable Active Directory Recycle Bin](#task-7-enable-active-directory-recycle-bin)
    - [Task 8: Configure Azure AD Connect attribute-level filtering](#task-8-configure-azure-ad-connect-attribute-level-filtering)
    - [Task 9: Initiate and verify directory synchronization](#task-9-initiate-and-verify-directory-synchronization)
    - [Task 10: Configure Hybrid Azure AD join](#task-10-configure-hybrid-azure-ad-join)
    - [Task 11: Perform Hybrid Azure AD join](#task-11-perform-hybrid-azure-ad-join)
  - [Exercise 2: Manage Authentication, Authorization, and Access Control in Hybrid Scenarios](#exercise-2-manage-authentication-authorization-and-access-control-in-hybrid-scenarios)
    - [Task 1: Create Active Directory groups](#task-1-create-active-directory-groups)
    - [Task 2: Assign EMS E5 licenses to Azure AD users](#task-2-assign-ems-e5-licenses-to-azure-ad-users)
    - [Task 3: Enable password writeback and Self-Service Password Reset](#task-3-enable-password-writeback-and-self-service-password-reset)
    - [Task 4: Implement Azure AD Password Protection for Windows Server Active Directory](#task-4-implement-azure-ad-password-protection-for-windows-server-active-directory)
    - [Task 5: Enable Azure Active Directory Identity Protection](#task-5-enable-azure-active-directory-identity-protection)
    - [Task 6: Enable Automatic Intune Enrollment](#task-6-enable-automatic-intune-enrollment)
    - [Task 7: Enable Enterprise-State-Roaming](#task-7-enable-enterprise-state-roaming)
    - [Task 8: Implement Azure AD Conditional Access Policies](#task-8-implement-azure-ad-conditional-access-policies)
    - [Task 9: Implement Azure AD Privileged Identity Management](#task-9-implement-azure-ad-privileged-identity-management)
  - [Exercise 3: Configure application access in hybrid scenarios](#exercise-3-configure-application-access-in-hybrid-scenarios)
    - [Task 1: Install and configure Azure AD Application Proxy](#task-1-install-and-configure-azure-ad-application-proxy)
    - [Task 2: Configure an Azure AD Application Proxy application](#task-2-configure-an-azure-ad-application-proxy-application)
    - [Task 3: Test an Azure AD Application Proxy application](#task-3-test-an-azure-ad-application-proxy-application)
    - [Task 4: Create an Azure Active Directory tenant and activate an EMS E5 trial](#task-4-create-an-azure-active-directory-tenant-and-activate-an-ems-e5-trial)
    - [Task 5: Create and configure Azure AD users](#task-5-create-and-configure-azure-ad-users)
    - [Task 6: Create and configure Azure AD guest user and group accounts](#task-6-create-and-configure-azure-ad-guest-user-and-group-accounts)
    - [Task 7: Configure an Azure AD Application Proxy application for B2B access](#task-7-configure-an-azure-ad-application-proxy-application-for-b2b-access)
    - [Task 8: Test an Azure AD Application Proxy application](#task-8-test-an-azure-ad-application-proxy-application)
  - [Exercise 4: Create resiliency within the Hybrid Identity infrastructure](#exercise-4-create-resiliency-within-the-hybrid-identity-infrastructure)
    - [Task 1: Create a VM for the secondary domain controller](#task-1-create-a-vm-for-the-secondary-domain-controller)
    - [Task 2: Promote the VM to a domain controller](#task-2-promote-the-vm-to-a-domain-controller)
    - [Task 3: Install Azure AD Connect in standby mode](#task-3-install-azure-ad-connect-in-standby-mode)
    - [Task 4: Install pass through agent](#task-4-install-pass-through-agent)
    - [Task 5: Configure Azure AD Application Proxy for BDC-1 VM](#task-5-configure-azure-ad-application-proxy-for-bdc-1-vm)
  - [Exercise 5: Configure Password-less Authentication methods](#exercise-5-configure-password-less-authentication-methods)
    - [Task 1: Configure Authentication methods](#task-1-configure-authentication-methods)
  - [After the hands-on lab](#after-the-hands-on-lab)
    - [Task 1: Delete resources](#task-1-delete-resources)

<!-- /TOC -->

# Hybrid identity hands-on lab step-by-step 

## Abstract and learning objectives 

In this hands-on lab you will setup and configure a number of different hybrid identity scenarios. The scenarios involve an Active Directory single-domain forest named corp.contoso.com, which in this lab environment, consists (for simplicity reasons) of a single domain controller named DC1 and a single domain member server named APP1. The intention is to explore Azure AD-related capabilities that allow you to integrate Active Directory with Azure Active Directory, optimize hybrid authentication and authorization, and provide secure access to on-premises resources from Internet for both organizational users and users who are members of partner organizations. 

## Overview

Contoso has asked you to integrate their on-premises Active Directory single-domain forest named corp.contoso.com with Azure AD and implement all necessary prerequisites to allow them to benefit from such Azure AD features as single sign-on to cloud and on-premises applications, enhanced sign-in security with Multi-Factor Authentication and Windows Hello for Business, Hybrid Azure AD join, Self-Service Password Reset and Password Protection, automatic enrollment of Windows 10 devices into Microsoft Intune, and Azure AD Privileged Identity Protection. They want to also provide secure access to their on-premises, Windows Integrated Authentication-based applications from Internet for both organizational users and users who are members of partner organizations, although they also want to be able to loosen restrictions when access originates from Hybrid Azure AD joined computers residing in their on-premises data centers. The same applications also need to be made available to Contoso's business partners. 

## Solution architecture

From the architectural standpoint, the deployment will consist of the following components:

-   On-premises Active Directory environment consisting of a single domain controller (DC1) and one domain member server (APP1), running Windows Server 2016 operating system. 

-   Contoso Azure AD tenant

-   Fabrikam Azure AD tenant

    ![High level architecture consisting of the on-premises environment represented by a rectangle on the left-hand side, two cloud outlines representing the Azure AD tenant of Contoso and Fabrikam on the right-hand side, and the Microsoft Intune icon in the middle. The on-premises environment contains an icon representing Active Directory domain controllers, providing such functionality as Azure AD Connect-based synchronization with attribute level filtering and password writeback, Azure AD Application Proxy with its on-premises connector, Service Connection Point for Hybrid Azure AD join, and Password Protection DC Agent. There is also a web server icon, representing the hybrid Azure AD joined server hosting the APP1 application, used also as the Password Application Proxy. The Contoso Azure AD tenant provides such functionality as Azure AD application proxy, My Apps portal, Automatic Intune enrollment, Enterprise State Roaming, Conditional Access, Azure AD Identity Protection, Azure AD Privileged Identity Management, Azure AD MFA, and Self-Service Password Reset.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/HOL_Architecture_Overview.png "Architecture Overview")

## Exercise 1: Integrate an Active Directory forest with an Azure Active Directory tenant

Duration: 150 minutes

**Overview**

In this exercise, you will integrate an Active Directory forest with an Azure Active Directory tenant by creating an Azure Active Directory tenant and activating an Enterprise Mobility + Security E5 trial, creating and configuring an Azure AD user, purchasing a custom domain name, assigning a custom domain name to the Contoso Azure AD tenant, configuring DNS suffix in the Contoso Active Directory forest, installing Azure AD Connect, enable Active Directory Recycle Bin, configuring Azure AD Connect attribute-level filtering, initiating and verifying directory synchronization, configuring Hybrid Azure AD join, and performing Hybrid Azure AD join of a Windows Server 2016 VM.

### Task 1: Create an Azure Active Directory tenant and activate an EMS E5 trial

In this task, you will create an Azure Active Directory tenant with the following settings: 

-   Organization name: **Contoso**

-   Initial domain name: Any valid, unique domain name.

-   Country or region: **United States**

1. From the lab computer, start a new Web browser window and navigate to the Azure portal at <https://portal.azure.com> if you haven't already.

2. When prompted, sign into the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises.

3. On the lab computer, in the Azure portal, select **+ Create a resource**.

4. On the **New** blade, in the **Search the Marketplace** text box, type **Azure Active Directory** and, in the list of results, select **Azure Active Directory**.

    ![A screenshot that depicts the New blade. In the New blade, Azure Active Directory is searched for in the Search the Marketplace text box and selected from the search results.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SearchAD.png "Search for and select Azure Active Directory")

5. Select **Create**.

6. On the **Basics** tab, leave Azure Active Directory selected and select **Next: Configuration >**

    ![A screenshot that shows Azure Active Directory select with the Next: Configuration > button called out.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/aad-basics.png "Select Azure Active Directory and click Next")

7. On the **Configuration** tab, specify the following settings and select **Review + create**. Then select **Create**.

    -   Organization name: **Contoso**

    -   Initial domain name: Any valid, unique domain name.

    -   Country or region: **United States**

8. Once it's created, follow the link to navigate to your new tenant. navigate to your subscription blade. Select **Change directory**.

    ![A screenshot that depicts the link to click to navigate to the new Azure Active Directory tenant.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ChangeDirectory.png "Select the link to navigate to your new tenant")

9.  On the **Contoso - Overview** blade, select **Licenses** under **Manage** on the left navigation.

10. On the **Contoso - Licenses**, blade, select **All Products** and select **+ Try/Buy**.

11. On the **Activate** blade, in the **ENTERPRISE MOBILITY + SECURITY E5** section, select **Free trial** and then select **Activate**.

    ![A screenshot that depicts the Licenses - All products blade with the Active blade open. On the Active blade, under 'Enterprise Mobility + Security E5 free trial', then Activate button is selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ActivateTrial.png "Activate Enterprise Mobility + Security E5 free trial")

   > **Note**: Activation typically takes about 5 minutes. Refresh the page to see the license added.

### Task 2: Create and configure Azure AD users

In this task, you will configure Azure AD user accounts in the newly created Azure AD tenant with the following settings. This will include assigning EM+S E5 licenses to the user account you are using for this lab as well as creating a new Azure AD user account with the following settings and assigning to it the Global Administrator role as well as the EM+S E5 license.

- Name: **john.doe**

- First name: **John**

- Last name: **Doe**
    
- Password: **Auto-generate password**
    
- Show Password: **Enabled**

- Groups: **0 group selected**
    
- Roles: **Global Administrator**
    
- Block sign in: **No**
    
- Usage location: **United States**
    
- Job title: **Leave blank**
    
- Department: **Leave blank**

1. From the lab computer, in the Azure portal, navigate back to the **Contoso - Overview** blade.

2. On the **Contoso - Overview** blade, select **Users** under **Manage** in the left navigation.

3. On the **Users - All users** blade, select the entry representing your user account.

4. On the **Profile** blade of your user account, select **Edit**.

    ![Screenshot that depicts the Profile blade with the Edit button select](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SelectEdit.png "Select Edit on the user account Profile blade")

5. In the **Settings** section, in the **Usage location** drop-down list, select the **United States** entry and select **Save**.

    ![Screenshot that depicts United States being selected in the Usage location dropdown menu of the Profile blade](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SettingsUsageLocation.png "Select United States for the Usage location")

6. On the **Profile** blade of your user account, select **Licenses** under **Manage** on the left. 

7. On the **Licenses** blade, select **+ Assignments**.

8. On the **Update license assignments** blade, enable the **Enterprise Mobility + Security E5** checkbox, ensure that all the corresponding license options are enabled, and select **Save**.

    ![Screenshot that depicts the Update license assignments blade with Enterprise Mobility + Security E5 and it's subsequent license options selected. The Save button is also selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/UpdateLicenseAssignments.png "Update license assignments")

9. On the **Users - All users** blade, select **+ New user**.

10. On the **New user** blade, ensure that the **Create user** option is selected, specify the following settings, and select **Create**:

    - User name: **john.doe\@*your Azure AD tenant domain name*** where ***your Azure AD tenant domain name*** is the domain name you specified when creating the Contoso Azure AD tenant.

    - Name: **john.doe**

    - First name: **John**

    - Last name: **Doe**
    
    - Password: **Auto-generate password**
    
    - Show Password: **Enabled**

    - Groups: **0 group selected**
    
    - Roles: **Global Administrator**
    
    - Block sign in: **No**
    
    - Usage location: **United States**
    
    - Job title: **Leave blank**
    
    - Department: **Leave blank**

    ![Screenshot that depicts the New user blade with all the specified settings selected and the Create button selected](images/Hands-onlabstep-bystep-HybridIdentityImages/media/NewUser.png "Add a new user with the listed settings")

    > **Note**: Copy the **User name** and **Password** values into Notepad. You will need them later in this lab.

11. On the **Users - All users** blade, select the entry representing the newly created user account.

12. On the **john.doe - Profile** blade, select **Licenses** under **Manage** on the left.

13. On the **john.doe - Licenses** blade, select **+ Assignments**.

14. On the **Update license assignments** blade, enable the **Enterprise Mobility + Security E5** checkbox, ensure that all the corresponding license options are enabled, and select **Save**.

    ![Screenshot that depicts the Update license assignments blade with Enterprise Mobility + Security E5 and it's subsequent license options selected. The Save button is also selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/UpdateLicenseAssignments2.png "Update license assignments")

### Task 3: Purchase a custom domain name

In this task, you will purchase a custom DNS domain name by leveraging the functionality described at <https://docs.microsoft.com/en-us/azure/app-service/manage-custom-dns-buy-domain>.

1. On the lab computer, in the browser displaying the Azure portal, navigate to your subscription blade and select **Change directory**. In the **Change the directory** blade on the right, select **Default Directory** in the dropdown and select **Change**. 
   
2. Return to the **Azure Active Directory** overview blade. Select **Switch tenant** and select the **Default Directory** associated with the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises then select **Switch**. 

3. In the Azure portal's left navigation, select **+ Create a resource**.

4. Search for **web app** and select **Create** within **Web App**.

    ![Screenshot that depicts the New blade with 'Web App' selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SelectWebApp1.png "Select create web app resource")

5. On the **Basics** tab of the **Web App** blade, specify the following settings and select **Next: Deployment**:

    - Subscription: The name of the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises.

    - Resource Group: **(Create new) contosohilab-RG**.

    - Name: Any valid, globally unique name.
    
    - Publish: **Code**

    - Runtime stack: **.NET Core 3.1 (LTS)**

    - Operating system: **Windows**

    - Region: Any Azure region in which you can create Azure Web Apps in the target subscription.

    - App Service plan: Accept the default.

    - SKU and size: **Shared D1** (If necessary, select **Change size**, select Dev/Test, select **D1** and select **Apply**)

    ![Screenshot that depicts the Basics tab of the Web App blade with the above listed settings selected and the Next: Monitoring button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/16febupdate2.png "Web app basics information")

6. Select **Next: Networking** and then **Next: Monitoring**
  
7. On the **Monitoring** tab of the **Web App** blade, specify the following setting and select **Review + create** then **Create**:

    - Enable Application Insights: **No**

8. In the Azure portal, search for and select **App Service Domains** on the top search bar.

    ![Screenshot that depicts the Azure portal with App Service Domains searched for and selected at the top of the search bar.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ASD.png "Select App Service Domains service")

9.  On the **App Service Domains** blade, select **Create App Service Domain**.

10. On the **Basics** tab, select your subscription, the **contosohilab-RG** Resource Group, search for unique domain, and select the one you want to use. Then select **Next: Contact Information**.

    ![Screenshot showing all of the settings above to select a custom domain to purchase.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/asd-selectdomain.png "Select a custom domain to purchase")

11. Enter in the required contact information and select **Next: Advanced**

12. Ensure that **Enable privacy protection** is Enabled. Select **Review + create** then **Create**.

    ![Screenshot showing domain privacy enabled.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/asd-domainprivacy.png "Domain privacy enabled")

### Task 4: Assign a custom domain name to the Contoso Azure AD tenant

In this task, you will assign a newly purchased custom DNS domain name to the Contoso Azure AD tenant. 

1. On the lab computer, in the Azure portal, select the **Directory + Subscription** icon in the toolbar of the Azure portal (to the right of the **Cloud Shell** icon) and switch to the Contoso Azure AD tenant. 
   
   ![In this screenshot, the Directory + Subscription blade is depicted with the Contoso directory selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ContosoSwitch.png "Contoso directory switch")

2. In the Azure portal, navigate to **Azure Active Directory** to navigate to the **Contoso - Overview** blade.

3. On the **Contoso - Overview** blade, select **Custom domain names** under **Manage** on the left.

4. On the **Contoso - Custom domain names** blade, select **+ Add custom domain**.

5. On the **Add custom domain** blade that appears on the right, in the **Custom domain name** text box, type the domain name you purchased in the previous task and select **Add domain**. You will be redirected to a new blade displaying your custom domain name settings.

6. Identify the value of the **TXT** record on the custom domain name blade. 

7. On the lab computer, start another browser tab and navigate to the Azure portal.

8. In the Azure portal, select the **Directory + Subscription** icon in the toolbar of the Azure portal (to the right of the **Cloud Shell** icon) to switch to the Azure AD tenant associated with the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises (the **Default Directory**). 

9.  In the Azure portal, select **All services** in the portal's left navigation. In the **Search All** textbox, type **DNS zones**, and then select the **DNS zones** entry in the listing of search results.

    ![In this screenshot, the All services blade is depicted with DNS zones searched for in the search box and selected in the search results.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SearchDNSZones.png "DNS Zones search and select")

10. On the **DNS zones** blade, select the entry with the name matching the custom domain name you purchased in the previous task.

11. On the DNS zone blade, select **+ Record set**. 

12. On the **Add record set** blade, specify the following settings and select **OK**:

    - Name: **\@**

    - Type: **TXT**

    - TTL: **1**

    - TTL unit: **Hours**

    - Value: The value of **DESTINATION OR POINTS TO ADDRESS** entry you identified on the **Custom domain name** blade.

13. Switch back to the browser window displaying the custom domain name blade and select **Verify**. Ensure that the verification was successful. 

14. Select **Make primary** and confirm the change when prompted. 

    ![In this screenshot, the Custom domain name blade is depicted with the Make primary button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/MakePrimary.png "Select Make primary on Custom domain name blade")

### Task 5: Configure DNS suffix in the Contoso Active Directory forest

In this task, you will configure the DNS suffix of the Contoso Active Directory forest to match the newly verified Azure AD custom domain name.

1. On the lab computer, in the Azure portal, verify that you are signed into the Azure AD tenant associated with the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises (the **Default Directory**). If not, select the **Directory + Subscription** icon in the toolbar of the Azure portal (to the right of the **Cloud Shell** icon) to switch to that Azure AD tenant. 

2. In the Azure portal, navigate to the blade of the **DC1** virtual machine.

3. On the **DC1** virtual machine blade, connect to **DC1** via Remote Desktop. When prompted to sign in, use the **demouser** name and the **demo\@pass123** password. 

4. Within the Remote Desktop session to **DC1**, on the **Server Manager** window, start the **Active Directory Domains and Trusts** console under **Tools**. 

    ![In this screenshot, Server Manager is depicted with the Active Directory Domains and Trusts console selected on the Tools dropdown menu.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ADDTConsole.png "Stare Active Directory Domains and trusts console on Server Manager window")

5. In the **Active Directory Domains and Trusts** console, right-click **Active Directory Domains and Trusts [DC1.corp.contoso.com]** on the left and select **Properties**.

    ![In this screenshot, the Active Directory Domains and Trusts console is depicted with 'Active Directory Domains and Trusts' right-clicked on the left with the Properties button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/NodeProperties.png "Open Active Directory Domains and Trusts Properties")

6. On the **UPN Suffixes** tab of the **Active Directory Domains and Trusts [DC1.corp.contoso.com]** window, in the **Alternative UPN suffixes** textbox, type the name of the custom domain you verified in the previous task, select **Add**, and then select **OK**.

    ![In this screenshot, the Active Directory Domains and Trusts [DC1.corp.contoso.com] window is depicted with the custom domain verified in the previous task added to the Alternative UPN suffixes selected. The OK button is then selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/UPNSuffix.png "Add UPN suffix")

7. Within the Remote Desktop session to **DC1**, on the **Server Manager** window, start the **Active Directory Users and Computers** console under **Tools**. 

    ![In this screenshot, Server Manager is depicted with the Active Directory Users and Computers console selected on the Tools dropdown menu.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ADUCConsole.png "Start Active Directory Users and Computers console on Server Manager window")

8. In the **Active Directory Users and Computers** console, expand **corp.contoso.com** on the left and examine the organizational unit hierarchy of the domain and the group membership of the domain groups. 

    ![In this screenshot, on the Active Directory Users and Computers console, constoso.local under Active Directory Users and Computers on the left is expanded. The Domain and group hierarchy an now be viewed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/NodeHierarchy1.png "Domain and group hierarchy")

9.  Within the Remote Desktop session to **DC1**, start Windows Visual Studio Code and, update and run the following script to replace the UPN suffix of all users who are members of the **Engineering** group with the one matching the custom verified domain name of the Contoso Azure AD tenant (replace the placeholder `<custom_domain_name>` with the actual name of the custom verified domain name you assigned to the Contoso Azure AD tenant). 

    ```pwsh
    $domainName = '<custom_domain_name>'
    $users = Get-ADGroupMember -Identity 'Engineering' -Recursive | Where-Object {$_.objectClass -eq 'user'}

    foreach ($user in $users) {
        $user = Get-ADUser -Identity $User.SamAccountName
        $userName = $user.UserPrincipalName.Split('@')[0] 
        $upn = $userName + "@" + $domainName 
        $user | Set-ADUser -UserPrincipalName $upn
    }
    ```

### Task 6: Install Azure AD Connect

In this task, you will install Azure AD Connect.

1. Within the Remote Desktop session to **DC1**, start the Edge browser and navigate to the Azure portal at <https://portal.azure.com>.

2. When prompted to sign in, enter the credentials of the **john.doe** Azure AD user account, which you copied into Notepad earlier in this exercise.

3. When prompted, change the password for the **john.doe** user account. 
  
    > **Note**: If you receive the message **We've seen that password too many times before. Choose something harder to guess**, you'll need to modify the password until it is unique enough to be accepted.

4. If prompted whether to **Stay signed in?"** select **No**. You will be redirected to the Azure portal interface. 

5. If presented with the **Welcome to Microsoft Azure** dialog box, select **Maybe later**. 

6. In the Azure portal, navigate to **Azure Active Directory** in the Azure portal. Then navigate to the **Contoso - Overview** blade.

7. On the **Contoso - Overview** blade, select **Azure AD Connect** under **Manage** on the left.

8.  On the **Azure AD Connect** blade, select the **Download Azure AD Connect** link.

    ![In this screenshot, the Azure AD Connect blade is depicted with the Download Azure AD Connect link selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/DownloadADC.png "Download Azure AD Connect")

9.  On the **Microsoft Azure Active Directory Connect** web page of the Microsoft Downloads site, select **Download**.

10. Select **Open file** once the **AzureADConnect.msi** and finished downloading. Select **Run** to start the **Microsoft Azure Active Directory Connect** installation wizard. 

11. On the **Welcome to Azure AD Connect** page, check the **I agree to the license terms and privacy notice** box and select **Continue**.

    ![In this screenshot, the Welcome to Azure AD Connect page is depicted with the 'I agree to the license terms and privacy notice' box checked and the Continue button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ADCWelcomeWizard.png "Agree to terms and select Next")

12. On the **Express Settings** page, select the **Customize** button.

13. On the **Install required components** page, leave all optional configuration options deselected and select **Install**.

14. On the **User sign-in** page, select the **Pass-through authentication** option and the **Enable single sign-on** checkboxes, and select **Next**.

    ![In this screenshot, the User sign-in page of the Microsoft Azure AD Connect wizard is depicted with the Pass-through authentication option and the Enable single sign-on checkboxes selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_UserSign-in.png "Select sign-in options and select Next")

15. On the **Connect to Azure AD** page, sign in by using the credentials of the **john.doe** account and select **Next**.

16. On the **Connect your directories** page, ensure that the **corp.contoso.com** entry appears in the **FOREST** drop-down list and select **Add Directory**. In the **AD forest account**, ensure that the **Create new AD account** option is selected, in the **ENTERPRISE ADMIN USERNAME** textbox, type **CORP.CONTOSO.COM\\demouser**, in the **PASSWORD** textbox, type **demo\@pass123**, and select **OK**.

    ![In this screenshot, the Connect your directories page of the Microsoft Azure AD Connect wizard is depicted with corp.contoso.com having been added.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_ConnectyourDirectories1.png "Connect your Contoso directory")

17. Back on the **Connect your directories** page, select **Next**.

18. On the **Azure AD sign-in configuration** page, ensure that your custom domain name is listed as the verified **Active Directory UPN Suffix**, and that the **userPrincipalName** entry appears in the **USER PRINCIPAL NAME** drop-down list. Note the warning stating **Users will not be able to sign into Azure AD with on-premises credentials if the UPN suffix does not match a verified domain name**. Check the **Continue without matching all UPN suffixes to verified domain** box and select **Next**. 

    >**Note**: This is expected, since some users are still configured with the **contoso.local** UPN suffix, which is not routable and cannot be configured as a verified custom domain name of an Azure AD tenant.

    ![In this screenshot, the Azure AD sign-in configuration page of the Microsoft Azure AD Connect wizard is depicted with the custom domain name listed as verified, and the userPrincipalName is listed as the attribute to use as the AzureAD username. The Next button is then selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_AzureADsign-inconfiguration.png "Configure sign-in and select Next")

19. On the **Domain and OU filtering** page, ensure that only the **DemoAccounts** OU and all its children OUs are selected and select **Next**. 

    ![In this screenshot, on the Domain and OU filtering page of the Microsoft Azure AD Connect wizard, the Demo Accounts OU and all its child OUs are selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_DomainandOUFiltering.png "Select Demo Accounts and Child OUs then select Next")

20. On the **Uniquely identifying your users** page, accept the default settings and select **Next**. 

    ![In this screenshot, on the Uniquely identifying your users page of the Microsoft Azure AD Connect wizard, the default settings are displayed. The Next button is then selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_UniquelyIdentifyingyourusers.png "Uniquely Identifying your Users")

21. On the **Filter users and devices** page, accept the default settings and select **Next**. 

    ![In this screenshot, on the Filter users and devices page of Microsoft Azure AD Connect wizard, the default settings are displayed. The Next button is then selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_FilterUsersandDevices.png "Filter Users and Devices")

22. On the **Optional features** page, accept the default settings and select **Next**.

    ![In this screenshot, on the Optional features page of the Microsoft Azure AD Connect wizard, the default settings are displayed. The Next button is then selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_OptionalFeatures.png "Optional Features")

23. On the **Enable single sign-on** page, select **Enter credentials**, in the **Forest credentials** dialog box, sign in with the **CORP\\demouser** username and **demo\@pass123** password, and select **Next**.

    ![In this screenshot, on the Enable single sign-on page of the Microsoft Azure AD Connect wizard, the prompt for forest credentials is displayed with the credentials listed above entered.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_EnableSingleSign-on.png "Enable Single Sign-on")

24. On the **Ready to configure** page, ensure that the **Start the synchronization process when configuration completes** checkbox is **NOT** selected and select **Install**.

    ![In this screenshot, on the Enable single sign-on page of the Microsoft Azure AD Connect wizard, the Start the synchronization process when configuration completes is not selected and the Install button is selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_ReadytoConfigure.png "Ready to Configure")

   > **Note**: You will configure attribute-level filtering before enabling the synchronization process.

   > **Note**: Installation should take about 2 minutes.

26. On the **Configuration complete** page, select **Exit**.

    ![In this screenshot, on the Configuration complete page of the Microsoft Azure AD Connect wizard, the status of the installation is displayed as Complete and the Exit button is selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConnect_ConfigurationComplete.png "Configuration Complete")


### Task 7: Enable Active Directory Recycle Bin

In this task, you will enable Recycle Bin in the Contoso Active Directory domain. 

1. Within the Remote Desktop session to **DC1**, on the Tools menu in the Server Manager console, start **Active Directory Administrative Center**.

    ![In this screenshot, the Server Manager console is depicted with the Tools menu open and the Start Active Directory Administrative Center console selected in the Tools menu dropdown.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/StartADAC.png "Start Active Directory Administrative Center")

2. In the **Active Directory Administrative Center** console, right-click **corp (local)** on the left and select **Enable Recycle Bin**. When prompted to confirm, select **OK**.

    ![In this screenshot, the Active Directory Administrative Center console is depicted with 'corp (local)' right-clicked and the Enable Recycle Bin option selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AD_EnableRecycleBin.png "Select Enable Recycle Bin for the local domain")

3. When prompted to refresh AD Administrative Center, select **OK**.

   > **Note**: For information regarding benefits of the Recycle Bin in hybrid scenarios, refer to <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-sync-recycle-bin>

### Task 8: Configure Azure AD Connect attribute-level filtering

In this task, you will configure Azure AD Connect attribute level filtering that will limit synchronization of user accounts to those with the UPN suffix matching the custom domain name of the target Azure AD tenant.

   > **Note**: The positive filtering option requires at least two sync rules. One of them determines the correct scope of objects to synchronize. The second catch-all sync rule filters out all objects that have not yet been identified as an object that should be synchronized.

1. Within the Remote Desktop session to **DC1**, start **Synchronization Rules Editor** under **Azure AD Connect** in the Start menu.

    ![In this screenshot, the Start menu is open within the Remote Desktop session to DC1 and under Azure AD Connect, Synchronization Rules Editor is selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/StartSRE.png "Open Synchronization Rules Editor")

2. In the Synchronization Rules Editor window, on the **View and manage your synchronization rules** page, ensure that **Inbound** appears in the **Direction** drop-down list and select **Add new rule**. This will launch the **Create inbound synchronization rule** wizard.

    ![In this screenshot, the Synchronization Rules Editor window is depicted with the Inbound rules displayed, Inbound selected on the Direction dropdown menu, and the 'Add new rule' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SynchronizationRulesEditor_AddNewRule.png "Add New Inbound Rule")

3. On the **Create inbound synchronization rule - Description** page, specify the following settings and select **Next**:

    - Name: **Custom In from AD - UPN Filter**

    - Description: **Custom Inbound Rule - includes users with UPN set to match the Azure AD custom domain**

    - Connected System: **corp.contoso.com**

    - Connected System Object Type: **user**

    - Metaverse Object Type: **person**

    - Link Type: **join**

    - Precedence: **50**

    - Tag: **Leave empty**

    - Enable Password Sync: **Leave empty**

    - Disabled: **Leave empty**

    ![In this screenshot, the description page of the Create inbound synchronization rule wizard is depicted with the required configuration settings and the Next button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_Description.png "Enter Sync Rule Description information")

4. On the **Create inbound scoping filter** page, select **Add Group**, select **Add clause** specify the following, and select **Next**:

    - Attribute: **userPrincipalName**

    - Operator: **ENDSWITH**

    - Value: **\@\<your custom domain name>**

    ![In this screenshot, the scoping filter page of the Create inbound synchronization rule wizard is depicted with the require the configuration settings and the Next button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_ScopingFilter.png "Create inbound scoping filter")

5. On the **Join Rules** page, select **Next**.

6. On the **Transformations** page, select **Add transformation** specify the following and select **Add**:

    - FlowType: **Constant**

    - Target Attribute: **cloudFiltered**

    - Source: **False**

    ![In this screenshot, the Transformations page of the Create inbound synchronization rule wizard is depicted with the required configuration settings selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_Transformations.png "Add transformation")

7. When presented with a **Warning** dialog box displaying that message stating that **A full import and full synchronization will be run on 'corp.contoso.com' during your next synchronization cycle**, select **OK**.

   > **Note**: This should bring you back to the View and manage your synchronization rules interface, with the new rule listed at the top of the rule list. 

    ![In this screenshot, the synchronization rules editor with the newly created Custom in from AD - UPN Filter rule is highlighted.](images/2020-04-27-23-44-31.png "View new rule")

8. Back in the **Synchronization Rules Editor** window, on the **View and manage your synchronization rules** page, ensure that **Inbound** appears in the **Direction** drop-down list and select **Add new rule** again. This will launch the **Create inbound synchronization rule** wizard.

9. On the **Description** page, specify the following settings and select **Next**:

    - Name: **Custom In from AD - Catch-all Filter**

    - Description: **Custom Inbound Rule - excludes all users with UPN not set to match the Azure AD custom domain**

    - Connected System: **corp.contoso.com**

    - Connected System Object Type: **user**

    - Metaverse Object Type: **person**

    - Link Type: **join**

    - Precedence: **51**

    - Tag: **Leave empty**

    - Enable Password Sync: **Leave empty**

    - Disabled: **Leave empty**

    ![In this screenshot, the description page of the Create inbound synchronization rule wizard is depicted, with the configuration settings selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_DescriptionCatchAll.png "Create Catch All Description inbound sync rule")

10. On the **Scoping filer** page, select **Next**.

11. On the **Join Rules** page, select **Next**.

12. On the **Transformations** page, select **Add transformation** specify the following and select **Add**:

    - FlowType: **Constant**

    - Target Attribute: **cloudFiltered**

    - Source: **True**

    ![In this screenshot, the Transformations page of the Create inbound synchronization rule wizard is depicted with the required configuration settings selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateInboundSynchronizationRule_TransformationsCatchAll.png "Add transformation to rule")

13. When presented with a **Warning** dialog box displaying a message stating that **A full import and full synchronization will be run on 'corp.contoso.com' during your next synchronization cycle**, select **OK**.

    >**Note**: This should bring you back to the **View and manage your synchronization rules** interface, with the new rules listed at the top of the rule list. 

    ![In this screenshot, the Synchronization Rules Editor is depicted displaying Inbound rules, including the two newly created inbound rules.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SynchronizationRulesEditor_AddNewRule_withRules.png "Displayed rules")

### Task 9: Initiate and verify directory synchronization

1. Within the Remote Desktop session to **DC1**, double-click the **Azure AD Connect** desktop shortcut.

2. On the **Welcome to Azure AD Connect** page, select **Configure**. 

3. On the **Additional tasks** page, select **Customize synchronization options** and select **Next**.

    ![In this screenshot, the 'Additional tasks' page of the Azure AD Connect wizard is depicted with the 'Customize synchronization options' option and Next button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CustomizeSyncOptions.png "Customize synchronization options task")

4. On the **Connect to Azure AD** page, sign in by using the credentials of the **john.doe** account and select **Next**.

5. On the **Connect your directories** page, select **Next**.

6. On the **Domain and OU filtering** page, select **Next**. 

7. On the **Optional features** page, accept the default settings and select **Next**.

8. On the **Enable single sign-on** page, select **Next**.

9. On the **Ready to configure** page, select the **Start the synchronization process when configuration completes** checkbox and select **Configure**.

    ![In this screenshot, the 'Ready to configure' page of the Azure AD Connect wizard is depicted with the 'Start the synchronization process when configuration completes' checkbox and the Configure button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ReadyConfigurePage.png "Ready to configure page")

10. On the **Configuration complete** page, select **Exit**.

11. Within the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal, navigate to the **Users - All users** blade of the Contoso Azure AD tenant.

12. On the **Users - All users** blade, note that the list of user objects includes all user accounts with the UPN suffix matching the custom domain name of the Azure AD tenant. You may need to refresh the page or wait a few minutes to see the change.

    ![In this screenshot, the 'Users - All users' blade of the Azure portal is depicted with all the user objects with the custom domain UPN suffixes listed.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/UserObjects.png "User objects shown with custom domain UPN suffixes")

13. In the Azure portal, navigate to the **Groups - All groups** blade of the Contoso Azure AD tenant and note that all the corp.contoso.com domain groups have been synchronized as well. 

14. In the Azure portal, navigate to the **Contoso - Azure AD Connect** blade and select **Azure AD Connect** on the left. Verify that the following settings are set: 

    - Azure AD Connect Sync Status: **Enabled** 
  
    - Last Sync: **This should be a timestamp of some sort**. 
  
    - Password Hash Sync: **Disabled** 
  
    - Federation: **Disabled**
   
    - Seamless single sign-on: **Enabled for 1 domain** 
  
    - Pass-through authentication: **Enabled with 1 agent**

   > **Note**: In a production environment, you would install additional agents for redundancy. For more information, refer to <https://docs.microsoft.com/en-us/azure/active-directory/hybrid/how-to-connect-pta-quick-start>.

### Task 10: Configure Hybrid Azure AD join

In this task, you will configure Azure AD Connect device synchronization options.

1. Within the Remote Desktop session to **DC1**, double-click the **Azure AD Connect** desktop shortcut.

2. On the **Welcome to Azure AD Connect** page, select **Configure**. 

3. On the **Additional tasks** page, select **Configure device options** and select **Next**.

4. On the **Overview** page, review the information regarding **Hybrid Azure AD join** and **Device writeback**, and select **Next**.

5. On the **Connect to Azure AD** page, sign in by using the credentials of the **john.doe** account and select **Next**.

6. On the **Device options** page, ensure that the **Configure Hybrid Azure AD join** option is selected and select **Next**. 

    ![In this screenshot, the 'Device options' page of the Azure AD Connect configuration wizard is depicted with the 'Configure Hybrid Azure AD join' option and the Next button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ConfigureHybridAzureADJoin.png "Configure Hybrid Azure AD join option is selected")

7. On the **Device operating system** page, select the **Windows 10 or later domain-joined devices** and **Supported Windows down-level domain-joined devices** checkboxes, and select **Next**. 

   > **Note**: Windows down-level devices are supported only if you are using Seamless SSO for managed domains or a federation service such as AD FS for federated domains.

8. On the **SCP configuration** page, check the **corp.contoso.com** Active Directory forest box, select the **Azure Active Directory** entry in the **Authentication Service** dropdown list, and select **Add**.

    ![In this screenshot, the 'SCP configuration' page of the Azure AD Connect configuration wizard is depicted with the required settings and the Add button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SCPConfig.png "SCP configuration page with proper selections")

9. When prompted for Enterprise Admin Credentials for corp.contoso.com, in the **Windows Security** dialog box, sign in with the **CORP\\demouser** user name and **demo\@pass123** password.

10. Back on the **SCP configuration** page, select **Next**.

11. On the **Ready to configure** page, select **Configure**.

12. On the **Configuration complete** page verify that the task completed successfully and select **Exit**.

   > **Note**: For more information regarding configuring hybrid Azure Active Directory join for managed domains, refer to <https://docs.microsoft.com/en-us/azure/active-directory/devices/hybrid-azuread-join-managed-domains#configure-hybrid-azure-ad-join>.


### Task 11: Perform Hybrid Azure AD join

1. On the lab computer, in the Azure portal, verify that you are signed into the Azure AD tenant associated with the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises (the **Default directory**). If not, select the **Directory + Subscription** icon in the toolbar of the Azure portal (to the right of the **Cloud Shell** icon) to switch to that Azure AD tenant. 

2. In the Azure portal, navigate to the blade of the **APP1** virtual machine.

3. On the **APP1** virtual machine blade, connect to **APP1** via Remote Desktop. When prompted to sign in, use the **AGAyers\@<custom_domain_name>** user name with the **demo@pass123** password (where **<custom_domain_name>** placeholder represents the custom DNS domain name you assigned to the Contoso Azure AD tenant earlier in this exercise.

4. Within the Remote Desktop session to **APP1**, on the **Server Manager** window, start **Task Scheduler** under **Tools**. 

    ![In this screenshot, the Server Manager window on the Remote Desktop connection to APP1 is depicted with the Tools menu open and the Task Scheduler option selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/TaskScheduler.png "Star Task scheduler via Server Manager")

5. In the **Task Scheduler** console, navigate to **Task Scheduler Library** > **Microsoft** > **Windows** > **Workplace Join**. From there, enable then run the **Automatic-Device-Join** task. 

    ![In this screenshot, the Task Scheduler console window is depicted with the Workplace Join node selected on the left and the 'Start device join' task and the Enable button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/StartDeviceJoin.png "Start device join task in Task Scheduler")

6. Switch to the Remote Desktop session to **DC1** and, open a Windows PowerShell console, start Azure AD Connect delta synchronization by running the following:

   ```pwsh
   Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. Switch back to the Remote Desktop session to **APP1** and start a **Command Prompt**.

8. From the Command Prompt window, check the Azure AD registration status of APP1 by running the following: 

   ```
   dsregcmd /status
   ```

9. Verify that the output of the command resembles the following:

   ```
   +----------------------------------------------------------------------+
   | Device State                                                         |
   +----------------------------------------------------------------------+

        AzureAdJoined : YES
     EnterpriseJoined : NO
             DeviceId : 61eea2b8-efbe-43d9-b267-126433c8ee34
           Thumbprint : BBAAA0FB4A55E880388851BED955A2669A961A96
       KeyContainerId : 2eb75eb8-0a1d-437b-99d9-9dd161ca0d90
          KeyProvider : Microsoft Software Key Storage Provider
         TpmProtected : NO
         KeySignTest: : PASSED
                  Idp : login.windows.net
             TenantId : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
           TenantName : xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx
          AuthCodeUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/authorize
       AccessTokenUrl : https://login.microsoftonline.com/xxxxxxx-xxxx-xxx-xxxx-xxxxxxxxxx/oauth2/token
               MdmUrl :
            MdmTouUrl :
     MdmComplianceUrl :
          SettingsUrl :
       JoinSrvVersion : 1.0
           JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/
            JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net
        KeySrvVersion : 1.0
            KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/
             KeySrvId : urn:ms-drs:enterpriseregistration.windows.net
         DomainJoined : YES
           DomainName : CORP

   +----------------------------------------------------------------------+
   | User State                                                           |
   +----------------------------------------------------------------------+

               NgcSet : NO
      WorkplaceJoined : NO
        WamDefaultSet : NO
           AzureAdPrt : NO

   +----------------------------------------------------------------------+
   | Ngc Prerequisite Check                                               |
   +----------------------------------------------------------------------+

        IsUserAzureAD : NO
        PolicyEnabled : NO
       DeviceEligible : YES
   SessionIsNotRemote : NO
     X509CertRequired : NO
         PreReqResult : WillNotProvision

   ```
11. Switch back to the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal, navigate to the **Devices - All devices** blade of the Contoso Azure AD tenant and verify that there is an entry representing the APP1 server, with the **Join Type** set to **Hybrid Azure AD joined**.

   > **Note**: You might need to wait until the Azure AD registration status is correctly reported and its Azure AD object appears in the Azure portal.

   ![In this screenshot, the 'Devices - All devices' blade of the Azure portal is depicted with an entry representing the APP1 server with the 'Join Type' set to 'Hybrid Azure AD joined'](images/Hands-onlabstep-bystep-HybridIdentityImages/media/APP1_HybridAzureADjoined.png "APP1 server entry is shown")


**Summary**

In this exercise, you integrated an Active Directory forest with an Azure Active Directory tenant by creating an Azure Active Directory tenant and activating an Enterprise Mobility + Security E5 trial, creating and configuring an Azure AD user, purchasing a custom domain name, assigning a custom domain name to the Contoso Azure AD tenant, configuring DNS suffix in the Contoso Active Directory forest, installing Azure AD Connect, enable Active Directory Recycle Bin, configuring Azure AD Connect attribute-level filtering, initiating and verifying directory synchronization, configuring Hybrid Azure AD join, and performing Hybrid Azure AD join of a Windows Server 2016 VM.


## Exercise 2: Manage Authentication, Authorization, and Access Control in Hybrid Scenarios

Duration: 150 minutes

**Overview**

In this exercise, you will optimize authentication, authorization, and access control for Contoso Active Directory environment integrated with the Contoso Azure AD tenant by enabling Azure AD Multi-Factor Authentication, enabling Azure AD password writeback and Self-Service Password Reset, implementing, Azure AD Password Protection, enabling Azure Active Directory Identity Protection, enabling Automatic Intune Enrollment, as well as implementing Azure AD Privileged Identity Management and Azure AD Conditional Access Policies.


### Task 1: Create Active Directory groups

In this task, you will create and configure Active Directory groups that will be used to control authentication, authorization, and access control and synchronize them to the Contoso Azure AD tenant. 

1. Within the Remote Desktop session to **DC1**, on the **Server Manager** window, under **Tools** start the **Active Directory Users and Computers** console. 

2. In the **Active Directory Users and Computers** console, expand **corp.contoso.com** on the left and navigate to **Demo Accounts > Groups**. 

    ![In this screenshot, the Active Directory Users and Computers console is depicted with the left navigation expanded to 'corp.contoso.com' > 'Demo Accounts' > 'Groups' with 'Groups' selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/NodeNavigation.png "Navigate to DemoAccounts > Groups in Active Directory Users and Computers")

3. In the **Groups** directory, right-click then select **New** then select **Group**. Create a new group with the following settings and select **OK**:

    - Group name: **Engineering - Mandatory MFA**

    - Group name (pre-Windows 2000): **Engineering - Mandatory MFA**

    - Group scope: **Global**

    - Group type: **Security**

    ![In this screenshot, the 'New Object - Group' dialog is depicted with the required settings selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateGroupDirectory.png "Create new group in directory")

4. Open the **Properties** window of the **Engineering - Mandatory MFA** group, in the **Description** text box, type **Engineering users with user state-based MFA enforcement (without Conditional Access)** then select **Apply** then **OK**.

5. Within the Remote Desktop session to **DC1**, open Visual Studio Code and run the following to add designated users to the newly created group (replace the placeholder `<custom_domain_name>` with the actual name of the custom verified domain name you assigned to the Contoso Azure AD tenant).

    ```pwsh
    $domainName = '<custom_domain_name>'
    $users = Get-ADGroupMember -Identity 'Engineering' -Recursive | Where-Object {($_.objectClass -eq 'user') -and ($_.distinguishedName -like "*OU=NY,OU=US,OU=Users,OU=Demo Accounts,DC=corp,DC=contoso,DC=com")}
    foreach ($user in $users) {
        $user = Get-ADUser -Identity $User.SamAccountName
        Add-ADGroupMember -Identity 'Engineering - Mandatory MFA' -Members $user
    }
    ```

6. Open a Windows PowerShell console, start Azure AD Connect delta synchronization by running the following:

   ```pwsh
    Start-ADSyncSyncCycle -PolicyType Delta
   ```

7. In the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant and select **Groups** on the left.

8. On the **Groups - All groups** blade, verify that there is an entry representing the **Engineering - Mandatory MFA** group containing the Azure AD user accounts matching Active Directory user accounts which are members of the Active Directory **Engineering - Mandatory MFA** group.


### Task 2: Assign EMS E5 licenses to Azure AD users

In this task, you assign a value to the **UsageLocation** attribute of each user account and assign an Azure AD Premium license to each user. This is necessary in order to implement Azure AD-based Multi-Factor Authentication for these users.

1. Within the Remote Desktop session to **DC1**, open a Windows PowerShell console, run the following to install Azure AD Graph PowerShell module for Graph (select **Yes to All** when prompted whether to proceed with the installation):

    ```pwsh
    Install-Module -Name Microsoft.Graph
    ```

2. Find the permissions you'll need to 

3. Open a Windows PowerShell console, run the following to sign into the Contoso Azure AD tenant. When prompted, sign in with the **john.doe** Azure AD user account, which you created in the previous exercise. Accept any Permissions requests that pop up when logging in.

    ```pwsh
    Connect-MgGraph -Scope "Directory.ReadWrite.All"
    ```

4. On the Script pane of the Windows PowerShell ISE window, run the following to set the **Location** attribute to **United States** for all Azure AD user accounts with the UPN suffix matching the custom verified domain name of the Contoso Azure AD tenant. 

    ```pwsh
    $domainName = (Get-MgDomain | Where-Object IsDefault -eq 'True').Id
    Get-MgUser | Where-Object {$_.UserPrincipalName -like "*@$domainName"} | ForEach-Object {Update-MgUser -UserId $_.UserPrincipalName -UsageLocation 'US'}
    ```
5. On the Script pane of the Windows PowerShell ISE window, run the following to assign the EM+S E5 trial licenses to all Azure AD user accounts with the UPN suffix matching the custom verified domain name of the Contoso Azure AD tenant. 

    ```pwsh
    $skuID = (Get-MgSubscribedSku | Where-Object {$_.SkuPartNumber -eq 'EMSPREMIUM'}).SkuId
    $users =  Get-MgUser | Where-Object {$_.UserPrincipalName -like "*@$domainName"}
    foreach($user in $users) { 
        Set-MgUserLicense -UserId $user.UserPrincipalName -AddLicenses @{SkuId = $skuID} -RemoveLicenses @()
    }
    ```
### Task 3: Enable password writeback and Self-Service Password Reset

In this task, you will enable password writeback and Self-Service Password Reset (SSPR) for Contoso users that had their accounts synchronized to the Contoso Azure AD tenant.

1. Within the Remote Desktop session to **DC1**, double-click the **Azure AD Connect** desktop shortcut.

2. On the **Welcome to Azure AD Connect** page, select **Configure**. 

3. On the **Additional tasks** page, select **Customize synchronization options** and select **Next**.

4. On the **Connect to Azure AD** page, sign in by using the credentials of the **john.doe** account and select **Next**.

5. On the **Connect your directories** page, select **Next**.

6. On the **Domain and OU filtering** page, select **Next**. 

7. On the **Optional features** page, check the **Password writeback** box and select **Next**.

8. On the **Enable single sign-on** page, select **Next**.

9.  On the **Ready to configure** page, ensure that the **Start the synchronization process when configuration completes** checkbox is selected and select **Configure**.

10. On the **Configuration complete** page, select **Exit**.

11. Within the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

12. On the **Contoso - Overview** blade, select **Password reset** on the left under **Manage**. 

13. On the **Password reset - Properties** blade, set **Self-service password reset enabled** to **Selected**, choose **No groups selected**. On the **Default password reset policy** blade that appears on the right, select **Engineering**, choose **Select**, and select **Save**.

14. On the **Password reset - Properties** blade, select **Authentication methods** on the left under **Manage**.

15. On the **Password reset - Authentication methods** blade, set **Number of methods required to reset** to **2**, enable all **Methods available to users**, including **Mobile app notification**, **Mobile app code**, **Email**, **Mobile phone (SMS only)**, and **Security questions**. 

    ![In this screenshot, the 'Password reset - Authentication methods' blade of the Azure portal is depicted with the required authentication method settings listed above are selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SettingAuthenticationMethods.png "Setting authentication methods and requirements")

   > **Note**: The **Office phone** method is not available in trial subscriptions.

16. Set **Number of security questions required to register** and **Number of questions required to reset** to **3**. 

    ![In this screenshot, the 'Password reset - Authentication methods' blade of the Azure portal is depicted with the required authentication method settings listed above are selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SetSecurityQuestions.png "Set security questions and requirements")

17. Choose **No security questions configured**. On the **Select security questions** blade that appears, select **+ Predefined**. On the **Add predefined security questions** blade that appears on the right, select any 5 questions, select **OK** twice, and, back on the **Password reset - Authentication methods** blade, select **Save**.

    ![In this screenshot, the 'Select security questions' blade of the Azure portal is depicted with the '+ Predefined' button selected with the required predefined security questions selected on the 'Add predefined security questions' blade on the right.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SelectSecurityQuestions.png "Select security questions")

18. On the **Password reset - Authentication methods** blade, select **Registration** on the left and ensure that **Require users to register when signing in** is set to **Yes** and that **Number of days before users are asked to re-confirm their authentication information** is set to **180**.

19. On the **Password reset** blade, select **On-premises integration** on the left and verify that the **Write back passwords to your on-premises directory** setting is set to **Yes**. Note that you have the option to **Allow users to unlock accounts without resetting their passwords**.


### Task 4: Implement Azure AD Password Protection for Windows Server Active Directory

In this task, you will implement Azure AD password Protection for Windows Server Active Directory.

1. Within the Remote Desktop session to **DC1**, on the **Server Manager** window, under **Tools** start **Group Policy Management** console. 

2. In the **Group Policy Management** console, navigate to **Forest: corp.contoso.com > Domains > corp.contoso.com** on the left, right-click **Default Domain Policy** and select **Edit**. 

    ![In this screenshot, the Group Policy Management console window is depicted with 'Forest: corp.contoso.com' > 'Domains' > 'corp.contoso.com' expanded on the left navigation and 'Default Domain Policy' right-clicked with the Edit option selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/EditDefaultDomainPolicy.png "Edit default domain policy")

3. In the **Group Policy Management Editor**, navigate to **Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy**. 

4. Set the value of the **Account lockout threshold** to **10** and select **OK** and accept the settings in the **Suggested Value Changes**. 

    ![In this screenshot, the Group Policy Management Editor is depicted with the 'Account lockout threshold properties' dialog open with the required settings selected and the 'Suggested Value Changes' dialog open with the OK button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADPasswordProtectionPolicy_ADLockout.png "Group policy management")

5. Within the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

6. On the **Contoso - Overview** page, select **Security** under **Manage** on the left.

7. On the **Security - Getting started** page, select **Authentication methods** under **Manage** on the left.

8. On the **Authentication methods - Policies** page, select **Password protection** under **Manage** on the left.

9.  On the **Authentication methods - Password protection** page, specify the following settings and select **Save**:

    - Lockout threshold: **5**

    - Lockout duration in seconds: **3600**

    - Enforce custom list: **Yes**

    - Custom banned password list: **Contoso**, **password**, **pass** (type each word on a separate line without commas).

    - Enable password protection on Windows Server Active Directory: **Yes**

    - Mode: **Audit**

    ![In this screenshot, the 'Authentication methods - Password protection' blade in the Azure portal is depicted with the required settings and the Save button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SetPasswordProtection.png "Set password protection")

10. Switch to the Remote Desktop session to **APP1** virtual machine, where you are signed in as the user **AGAyers** with the **demo@pass123** password.

11. Launch **Internet Explorer** Select the cog wheel, and then **Internet Options**

    ![Screenshot showing selecting the cog wheel and then internet options in Internet Explorer.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/app1-installedge-internetoptions.png "Selecting Internet Option")

12. Select the **Security** tab, leave **Internet** selected, then select **Custom level...**

    ![Depict selecting the security tab, and setting the custom level for the internet security settings](images/Hands-onlabstep-bystep-HybridIdentityImages/media/app1-installedge-customsecurity.png "Selecting custom level for internet security options")

13. Scroll almost half-way down and enable File download. Select OK, confirm changing the settings, select OK.

    ![Show the File download setting being enabled in the security settings in the internet zone](images/Hands-onlabstep-bystep-HybridIdentityImages/media/app1-installedge-allowdownloads.png "Allow file downloads")

14. Now that file downloads are allowed on **APP1**, us Internet Explorer to download and install Edge for **Windows 64-bit** from the following URL.

    ```https://www.microsoft.com/en-us/edge/business/download```

15. Start the Edge browser once it's installed, navigate to the **Azure AD Password Protection for Windows Server Active Directory** page at the below listed URL. Select **Download** under **Azure AD Password Protection for Windows Server Active Directory**. Download and install **AzureADPasswordProtectionProxySetup.exe** with the default options.

    ```
    https://www.microsoft.com/download/details.aspx?id=57071
    ```

16.  Within the Remote Desktop session to **APP1**, start a Windows PowerShell console as Administrator, run the following to register the proxy (replace the `<domain_name>` placeholder with the name of the default domain name associated with the Contoso Azure AD tenant). When prompted, sign into the Contoso Azure AD tenant using the credentials of the **john.doe** user account.
  
    ```pwsh
    Import-Module AzureADPasswordProtection
    Register-AzureADPasswordProtectionProxy -AccountUpn 'john.doe@<domain_name>.onmicrosoft.com'
    ```

18. In the same Windows PowerShell console session, run the following to register the Active Directory forest (replace the `<domain_name>` placeholder with the name of the default domain name associated with the Contoso Azure AD tenant). If you get a login prompt, use **john.doe** account again:

    ```pwsh
    Register-AzureADPasswordProtectionForest -AccountUpn 'john.doe@<domain_name>.onmicrosoft.com'
    ```

19. Switch to the Remote Desktop session to **DC1** virtual machine, where you are signed in as the user **CORP\demouser** with the **demo@pass123** password. 

20. Within the Remote Desktop session to **DC1**, start the Edge browser, navigate to the **Azure AD Password Protection for Windows Server Active Directory** page at the below listed URL. Select **Download** under **Azure AD Password Protection for Windows Server Active Directory**. Download and install **AzureADPasswordProtectionProxySetup.exe** with the default options.

    ```
    https://www.microsoft.com/download/details.aspx?id=57071
    ```

21. Restart DC1 once the setup completes.

### Task 5: Enable Azure Active Directory Identity Protection

In this task, you will enable Azure AD Identity Protection

1. After **DC1** reboots, connect to **DC1** via Remote Desktop. When prompted to sign in, use the **demouser** name with the **demo\@pass123** password. 

3. Within the Remote Desktop session to **DC1**, start the Edge browser and navigate to the Azure portal at the URL below:

    ```
    portal.azure.com
    ```

4. When prompted to sign in, enter the credentials of the **john.doe** Azure AD user account, which you copied into Notepad earlier in this exercise.

5. In the Azure portal, search for and select **Azure AD Identity Protection** in the search bar at the top of the page.

6. On the **Azure AD Identity Protection** blade, select **MFA registration policy** on the left under **Protect**.

7. On the **Azure AD Identity Protection - MFA registration policy** blade, in the **Assignments** section, select **All users**. 

    ![In this screenshot, the 'Azure AD Identity Protection - MFA registration policy' blade of the Azure portal is depicted with the 'All users' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SelectUsers.png "Select All users")

8. On the **Include** tab that opens on the right, choose **Select individual users and groups**. On the **Select users** blade, in the **Select** text box, type **Engineering**, in the list of results, select **Engineering** and choose **Select**.

    ![In this screenshot, the 'Azure AD Identity Protection - MFA registration policy' blade of the Azure portal is depicted with the Include tab of the Users blade selected with the 'Select individual users and groups' option selected and the 'Select users' blade open with the 'Engineering' group and 'Select' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/IdentityProtection_MFAregistrationpolicy_UsersInclude.png "Include Engineering group")

9. On the **Exclude** tab, choose **0 users and groups selected**. On the **Select users** blade, in the **Select** text box, type **Engineering - Mandatory MFA**, in the list of results, select **Engineering - Mandatory MFA**, choose **Select**.

    ![In this screenshot, the 'Azure AD Identity Protection - MFA registration policy' blade of the Azure portal is depicted with the Exclude tab of the Users blade selected with the '0 users and groups selected' button selected and the 'Select users' blade open with the 'Engineering - Mandatory MFA' group and 'Select' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/IdentityProtection_MFAregistrationpolicy_UsersExclude.png "Exclude groups settings")

10. Back on the **Azure AD Identity Protection - MFA registration policy** blade, in the **Controls** section, ensure that the **Require Azure MFA registration** checkbox is selected. Set **Enforce Policy** to **On** and select **Save**.

    ![In this screenshot, the 'Azure AD Identity Protection - MFA registration policy' blade of the Azure portal is depicted with the 'Require Azure MFA registration' checkbox selected and the 'Enforce Policy' set to On.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/IdentityProtection_MFAregistrationpolicy_EnforcePolicy.png "Enforce policy and require MFA registration")

11. On the **Azure AD Identity Protection** blade, select **User risk policy** on the left under **Protect**.

12. On the **Azure AD Identity Protection - User risk policy** blade, configure the **User risk remediation policy** with the following settings and save your configuration:

    - Assignments: 

        - Users: **All users**

        - User risk: **Low and above**

    - Controls:

        - Access: **Allow access** and **Require password change**

    - Enforce Policy: **On**

    ![In this screenshot, the 'Azure AD Identity Protection - User risk policy' blade of the Azure portal is depicted with the required settings and the Save button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/IdentityProtection_UserRiskPolicy.png "Set the user risk policy")

### Task 6: Enable Automatic Intune Enrollment

In this task, you will enable automatic enrollment of hybrid Azure AD devices into Intune. 

1. Within the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal, navigate to the following URL in a tab. 

    ```
    https://endpoint.microsoft.com
    ```
2. On the **Microsoft Endpoint Manager admin center** page, select **Devices** on the left navigation.

3. On the **Devices** blade, select **Enrolled devices** under **Device enrollment** on the left.

4. On the **Windows enrollment** blade, select **Automatic Enrollment**.

5. On the **Configure** blade, set **MDM user scope** to **All** and select **Save**.

    ![In this screenshot, the Configure blade of the Azure portal is depicted with the 'MDM user scope" setting set to all and the Save button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SetMDMUserScope.png "Set MDM user scope on Configure blade")

### Task 7: Enable Enterprise-State-Roaming

1. Within the Remote Desktop session to **DC1**, in the Edge browser tab displaying the Azure portal, navigate to the blade of the Contoso Azure AD tenant.

2. On the **Contoso - Overview** page, select **Devices** under **Manage** on the left.

3. On the **Devices - All devices** page, select **Enterprise State Roaming** on the left.

4. On the **Devices - Enterprise State Roaming** blade, for **Users may sync settings and app data across devices**, select **Selected**. Choose **No member selected** below. Select **+ Add** then select the **Engineering** group from the list of Azure AD tenant users and groups that appears on the right. Choose **Select**, then **Ok**, then **Save**. 

    ![In this screenshot, the 'Members allowed to sync settings and app data' blade is depicted with the '+ Add' button selected and the 'Add members' blade open with the Engineering group searched for and selected along with the Select button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SelectEngineering.png "Select Engineering group")

### Task 8: Implement Azure AD Conditional Access Policies

In this task, you will implement Azure AD Conditional Access Policies.

1. Within the Remote Desktop sessizon to **DC1**, in the Edge browser tab displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

2. On the **Contoso - Overview** blade, select **Properties** under **Manage** on the left. Select **Manage Security defaults**. On the **Enable security defaults** blade that appears on the right, select **No** under **Enable security defaults** then check **My organization is using Conditional Access**. Then select **Save**. Return to the **Contoso - Overview** blade.

    ![In this screenshot, the 'Contoso - Overview' blade is depicted with the Properties and 'Manage security defaults' buttons selected and with the 'Enable security defaults' blade open on the right with the required configuration listed above selected along with the Save button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/DisableSD.png "Disabling the security defaults")

3. On the **Contoso - Overview** page, select **Security** under **Manage** on the left.

4. On the **Security - Getting started** page, select **Named locations** under **Manage** on the left.

5. On the **Security - Named locations** page, select **+ IP ranges location**.

6. On the **New location (IP ranges)** blade, specify the name **Contoso Headquarters**.

7. Select the **Mark as trusted location** checkbox, then select **+**.

    ![Showing entering the name, selecting the checkbox for trusted location and then the + to add a new IP range.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ca-newlocation.png "Adding a new trusted IP location")

8. Add the public IP address of the APP1 Azure VM (this can be found on its page in the portal) in the CIDR notation (i.e., x.x.x.x/32). Then select **Create**

    ![In this screenshot, adding the public IP address of the App1 server is show.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ca-addipaddress.png "Adding a new IP address")

9. Select **Conditional Access** under **Protect** on the left.

10. On the **Conditional Access - Policies** page, select **+ New policy** and **Create new policy from templates**. The first policy created will enforce MFA for the **Engineering - Mandatory MFA** group.

11. Leave **Identities** selected and select **Next**

    ![Leaving Identities selected, the Next button to select is highlighted.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ca-template-identities.png "Identities selected in customize your build")

12. Select **Require multi-factor authentication for all users**, Name your policy **Require multi-factor authentication for Enginerering  Mandatory MFA**, set the **Policy state** to **On**, select **Next** and then **Create Policy**

    ![This screenshot highlights selecting require multi-factor authentication for all users, the policy name and setting the policy state to On.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ca-template-selectmfa.png "Require multi-factor authentication for all users")

13. Once the policy is created select it to make an update.

14. Select **All users included and specific users excluded** under **Users or workload identities**. Change from **All users** to **Select users and groups**, **Users and groups**, and select the group **Engineering - Mandatory MFA**

    ![Screenshot showing the change from All users to select users and group with engineering - mandatory mfa selected](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ca-template-changeassignment.png "Engineering - Mandatory MFA group selected")

15. Select the **Exclude** tab and notice that when we create a conditional access policy from a template, the user creating the policy (in this case john.doe) is automatically added to the exclude list to ensure the user isn't locked out of their own Azure AD tenant. Select **Save**

16. Select **+ New policy** then **Create new policy**. Now a second policy will be created for the rest of the engineering users.

16. On the **New** blade, in the **Name** text box, type **Contoso Engineering On-Premises Conditional Access Policy**.

17. On the **New** blade, in the **Assignments** section, select **0 users or workload identities selected**.

18. On the **Include** tab, choose the **Select users and groups** option, select the **Users and groups** checkbox. On the **Select** blade, type **Engineering**, in the list of results, select **Engineering**, and choose **Select**.

    ![In this screenshot, the New blade is depicted with the Include tab selected along with the 'Select users and groups' and 'Users and groups' options and the Select blade is open with the Engineering group searched for and selected along with the Select button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_UsersandGroupsInclude.png "Include Configuration Settings")

19. On the **Exclude** tab, select the **Users and groups** checkbox. On the **Select excluded users** blade, type **Engineering**. In the list of results, select **Engineering - Mandatory MFA**, and choose **Select**.

    ![In this screenshot, the New blade is depicted with the Exclude tab selected along with the 'Users and groups' option and the Select blade is open with the 'Engineering - Mandatory MFA' group searched for and selected along with the Select button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_UsersandGroupsExclude.png "Exclude configuration settings and selections")

20. On the **New** blade, in the **Assignments** section, select **No cloud apps, actions, or authentication contexts selected**.

21. On the **Include** tab that appears, choose the **Select apps** option. On the **Select** blade, select the **Microsoft Azure Management** checkbox, choose **Select**.

    ![In this screenshot, the Include tab is depicted with the 'Select apps' option selected and the Select blade is open with the 'Microsoft Azure Management' a[[]] searched for and selected along with the Select button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_CloudppsandActionsInclude.png "Select the Microsoft Azure Management app")

   > **Note**: Review the warning stating **Don't lock yourself out! This policy impacts the Azure portal. Before you continue, ensure that you or someone else will be able to get back into the portal**. Disregard this warning if you are configuring persistent browser session policy that works correctly only if "All cloud apps" are selected.

17. On the **New** blade, in the **Conditions** section, select **0 conditions selected**.

18. Select **Not configured** under **Sign-in risk**. In the **Sign-in risk** blade, set **Configure** to **Yes**, check the **No risk** box, and choose **Done**.

    ![In this screenshot, 'Not configured' under 'Sign-in risk' is selected and the 'Sign-in risk' blade is open with the Configure and 'No risk' options selected along with the Select button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_SigninRisk.png "Configure sign-in risk settings")

19. Select **Not configured** under **Device platforms**. On the **Device platforms** blade, set **Configure** to **Yes**, on the **Include** tab, choose **Select device platforms**. Check the **Windows** box, and select **Done**.

    ![In this screenshot, 'Not configured' under 'Device platforms' is selected and the 'Device platforms' blade is open with the Configure, 'Select device platform', and 'Windows' options selected under the Include tab along with the Done button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_DevicePlatforms.png "Device platform settings")

20. Select **Not configured** under **Locations**. On the blade that appears, set **Configure** to **Yes**. On the **Include** tab, choose **Selected locations**. On the **Select** blade, check the **Contoso Headquarters** box, choose **Select**.
    
    ![In this screenshot, the Select blade of the Azure portal is depicted with the Contoso Headquarters box checked and the Select button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_Locations.png "Select conditional access locations")

21. Select **Not configured** under **Client apps**, on the **Client apps** blade, set **Configure** to **Yes**. Check the **Browser**, **Mobile apps and desktop clients**, **Exchange ActiveSync clients**, and **Other clients** boxes, and select **Done**.

    ![In this screenshot, 'Not configured' under 'Client apps' is selected and the 'Client apps' blade is open on the right with Configure set to Yes and the options listed above selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_Clientapps.png "Conditional access client apps selections")

22. Back on the **New** blade, in the **Access controls** section, select **0 controls selected** under **Grant**.

23. On the **Grant** blade, ensure that the **Grant access** option is selected. Check the **Require Hybrid Azure AD joined device** box, accept the default choice of **Require all the selected controls** under **For multiple controls** and choose **Select**.

    > **Note**: Review the warning **Don't lock yourself out! Make sure that your device is Hybrid Azure AD Joined**.

    ![In this screenshot, the New blade of the Azure portal is depicted with the '0 controls selected' button selected and the Grant blade open with the required options listed above selected along with the Select button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_AccesscontrolsGrant.png "Access controls Grant settings")

24. Back on the **New** blade, in the **Access controls** section, select **0 controls selected** under **Session**. 

25. Review the **Session** blade settings but do not modify them. Close it when you are finished.

26. On the **New** blade, set **Enable policy** to **On** and select **Create**.

    ![In this screenshot, the New blade of the Azure portal is depicted with 'Enable policy' set to On and the Create button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_Final.png "Conditional access enable policy and create")

27. Back on the **Conditional Access - Policies** blade, select **What If**.

28. On the **What If** blade, specify the following settings and select **What If**:

    - User: **Teresa F. Bell**

    - Cloud apps or actions: **Microsoft Azure Management**

    - IP address: **The public IP address of the APP1 Azure VM**

    - Country or region: **United States**

    - Device platform: **Windows**

    - Client apps: **Browser**

    - Sign-in risk: **No risk**

29. Review the evaluation results and note the policy and the grant controls that will apply.

    ![In this screenshot, within the Azure portal the What If settings and the evaluation results of the newly created conditional access policy are depicted.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADConditionalAccess_WhatIf_parameters.png "What if settings and results")

30. Re-run the evaluation but first change the **Sign-in risk** to **Low** and review the evaluation results.


### Task 9: Implement Azure AD Privileged Identity Management

In this task, you will implement Azure AD Privileged Identity Management.

1. Within the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal, navigate to the **All services** blade.

2. In the search text box, type **Privileged Identity Management** and, in the list of results, select **Azure AD Privileged Identity Management**.

3. On the **Privileged Identity Management** page, select **Azure AD roles** under **Manage** on the left.

4. On the **Contoso - Quick start** page, select **Assign eligibility**.

5. On the **Contoso - Roles** page, select **+ Add assignments**.

6. On the **Add assignments** blade, specify the following settings to designate **Ann G. Ayers** as an eligible member of the **Authentication Administrator** role then select **Next** then **Assign**. 

    - Select role: **Authentication Administrator**

    - Select members: **Ann G. Ayers**

   > **Note**: **Authentication Administrator** role grants privileges to set or reset non-password credentials and update passwords for all users. Authentication Administrators can require users to re-register against existing non-password credential (for example, MFA or FIDO) and revoke remember MFA on the device, which prompts for MFA on the next sign-in.

   ![In this screenshot, the 'Add assignments' blade of the Azure portal is depicted with the required settings listed above configured and the Next button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AddAAAssignment.png "Adding the Authentication Administrator role assignment")

7. On the **Contoso - Roles** blade, select **Assignments** under **Manage** on the left and note that **Ann G. Ayers** is listed as eligible for the **Authentication Administrator** role.

8. Switch to the Remote Desktop session to **APP1**, start the Edge browser, and browse to the Azure portal at [**http://portal.azure.com**](http://portal.azure.com). From here sign-in as Ann G. Ayers. The username can be found on the **Users - All users** page in the Azure portal window on the lab computer. The password will be **demo@pass123**.

    > Note: If you prompted that you have 14 days to add additional information, you can still choose skip. Even if you choose skip here, on the next screen you'll be required to enter additional MFA information.

9.  When prompted to provide additional information, select **Next**, on the **Keep your account secure** page, select **I want to set up a different method**. At the **Choose a different method** dialog, select **Phone** on the dropdown then select **Confirm**. 

    - On the **Phone** page, enter your phone number and select **Next**.

    - Enter the code in the email you received, select **Next**.

10. When prompted again to provide additional information, select **Next**, on the **Keep your account secure** page, select **I want to set up a different method**. At the **Choose a different method** dialog, select **Email** on the dropdown then select **Confirm**. 

    - On the **Email** page, enter an email address you can access and select **Next**.

    - Enter the code in the text message you received, select **Next**.

11. Back on the **Keep your account secured** page, select **Done**. You will now be able to use Azure portal. 

12. In the Azure portal, navigate to the **Privileged Identity Management - Quick start** page. 

13. On the **Privileged Identity Management - Quick start** page, select **My roles** under **Tasks** on the left.

14. On the **My roles - Azure AD roles** page, on the **Eligible assignments** tab, select **Activate** next to the **Authentication Administrator** role entry. 

15. On the **Activate - Authentication Administrator** blade, enter some random next in the **Reason** box then select **Activate**. Wait for the role to activate and the page to refresh.

16. Switch to the **Active assignments** tab, note that the role assignment has been activated.

    ![In this screenshot, the 'My roles - Azure AD roles' blade of the Azure portal is depicted with the 'Active assignments' tab selected and the Activated state of the role assignment highlighted.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ActiveAssignment.png "The role assignment is active")

**Summary**

In this exercise, you optimized authentication, authorization, and access protection for Contoso Active Directory environment integrated with the Contoso Azure AD tenant by enabling Azure AD Multi-Factor Authentication, enabling Azure AD password writeback and Self-Service Password Reset, implementing, Azure AD Password Protection, enabling Azure Active Directory Identity Protection, enabling Automatic Intune Enrollment, as well as implementing Azure AD Privileged Identity Management and Azure AD Conditional Access Policies.


## Exercise 3: Configure application access in hybrid scenarios

Duration: 90 minutes

**Overview**

In this exercise, you will configure access to on-premises Integrated Windows Authentication app (implemented as the default IIS web site) from the internet by installing and configuring Azure AD Application Proxy. You will test access to this application by using a Contoso Azure AD tenant user account as well as by using a Fabrikam Azure AD tenant user account configured as a guest account in the Contoso Azure AD tenant. 


### Task 1: Install and configure Azure AD Application Proxy

In this task, you will install and configure Azure AD Application Proxy.

1. Within the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

2. On the **Contoso - Overview** blade of the Contoso Azure AD tenant, select **Application proxy** under **Manage** on the left.

3. On the **Contoso - Application proxy** blade, select **Download connector service**.

4. On the **Application Proxy Connector Download** blade on the right, review the system requirements and select **Accept terms & Download**.

5. When prompted whether to save or run **AADApplicationProxyConnectorInstaller.exe**, select **Run**.

   > **Note**: In a production environment, you would install the connector on a domain member server. We are using a domain controller strictly for simplicity.

6. Install Microsoft Azure Active Directory Application Proxy Connector with default settings. When prompted to sign in, enter the credentials of the **john.doe** Azure AD user account, which you created in the first exercise of this lab.

7. Once the installation completes, refresh the Edge browser page displaying the **Contoso - Application proxy** blade and verify that it includes the **DC1.corp.contoso.com** entry in the **Default** connector group.

8. On the **Contoso - Application proxy** blade, select **Enable application proxy** and, when prompted for confirmation, select **Yes**.

    ![In this screenshot, the 'Contoso - Application proxy' blade of the Azure portal is depicted with the 'DC1.corp.contoso.com' entry listed under the Default connector group.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/VerifyConnector.png "Verify that the connector is present")

### Task 2: Configure an Azure AD Application Proxy application

In this task, you will configure an Azure AD Application Proxy application.

1. On the **Contoso - Application proxy** blade, select **+ Configure an app**.

2. On the **Add your own on-premises application** blade, specify the following settings and select **+ Add**.

    - Name: **APP1 Default Web Site**

    - Internal URL: **http://app1.corp.contoso.com**

    - External URL: **Accept the default value**.

    - Pre Authentication: **Azure Active Directory**

    - Connector Group: **Default**

    - Backend Application Timeout: **Default**

    - Use HTTP-Only Cookie: **No**

    - Use Secure Cookie: **Yes**

    - Use Persistent Cookie: **No**

    - Translate URLs in Headers: **Yes**

    - Translate URLs in Application Body: **No**

    ![In this screenshot, the 'Add your own on-premises application' blade of the Azure portal is depicted with the required settings listed above and the '+ Add' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/OnPremAppSettings.png "Enter On-prem app settings")

3. In the search bar at the top of the Azure portal, search for and select **Enterprise applications**. In the list of applications, select **APP1 Default Web Site**.

4. On the **APP1 Default Web Site - Overview** blade, in the **Getting Started** section, select **Assign users and groups**.

    ![In this screenshot, the 'APP1 Default Web Site - Overview' blade of the Azure portal is depicted with the 'Assign users and groups' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SelectAssignUsersGroups.png "Select Assign users and groups")

5. On the **APP1 Default Web Site - Users and groups** blade, select **+ Add user/group**.

6. On the **Add Assignment** blade, specify the following settings and select **Assign**:

    - Users and groups: **Engineering**

    - Select Role: **User**

    ![In this screenshot, the 'Add Assignment' blade of the Azure portal is depicted with the required settings listed above and the Assign button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AddAssignment.png "Add assignment blade and group selection")

7. On the **APP1 Default Web Site - Users and groups** blade, select **Single sign-on** under **Manage** on the left.

8. On the **APP1 Default Web Site - Single sign-on** blade, select **Windows Integrated Authentication**.

9. Within the Remote Desktop session to **DC1**, start a **Command Prompt**. On the **Command Prompt**, run the following to identify Service Principal Names associated with the APP1 computer account.

    ```
    setspn -L APP1
    ```

10. Review the output, switch back to the Edge browser window displaying the Azure portal, and, on the **APP1 Default Web Site - Configure Integrated Windows Authentication (IWA)** blade, specify the following settings and select **Save**.

    - Internal Application SPN: **HTTP/APP1.corp.contoso.com**

    - Delegated Login Identity: **User principal name**

    ![In this screenshot, the 'APP1 Default Web Site - Configure Integrated Windows Authentication (IWA)' blade is depicted with the settings listed above specified and the 'Save' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ConfigureIWA.png "Configure IWA")

   > **Note**: The HTTP service class is one of the built-in services that act as an alias to the HOST SPN. For more information, refer to **How to use SPNs when you configure Web applications that are hosted on Internet Information Services** at <https://support.microsoft.com/en-us/help/929650/how-to-use-spns-when-you-configure-web-applications-that-are-hosted-on>

12. Within the Remote Desktop session to **DC1**, in the Server Manager console, select **Tools** and then select **Active Directory Users and Computers**. 

13. In the **Active Directory Users and Computers** console, select **View** and, in the **View** menu, enable **Advanced Features**.

    ![In this screenshot, the 'Active Directory Users and Computers' console is depicted with the View menu open and the Advanced Features button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/EnableAdvancedFeatures.png "Enable Advanced Features in the console")

14. In the **Active Directory Users and Computers** console, locate the computer account hosting the Azure AD Application Proxy connector (**DC1** in our case) under **Domain Controllers** within **corp.contoso.com** and display its **Properties** window.

    ![In this screenshot, the 'Active Directory Users and Computers' console is depicted with the Domain Controllers node selected on the left and the DC1 computer account right-clicked with the Properties menu option selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/DisplayComputerProperties.png "Display computer properties")

15. In the **DC1 Properties** window, switch to the **Delegation** tab and select the option **Trust this computer for delegation to specified services only**.

16. Select the option **Use any authentication protocol**, select **Add**, in the **Add Services** window, select **Users or Computers**, in the **Select Users or Computers** dialog box, in the **Enter the object names to select** text box, type **APP1**, select **Check Names** to verify the name resolves, and select **OK**. 

    ![In this screenshot, the 'DC1 Properties' window is depicted with the Delegation tab selected with the 'Trust this computer for delegation to specified services only' and 'Use any authentication protocol' options and the 'Add' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/DelegationConfiguration.png "Delegation configuration")

17. Back in the **Add Services** window, select the **http** entry and select **OK**. 

    ![In this screenshot, 'Add Services' window is depicted with the 'http' entry selected along with the OK button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADApplicationProxy_Delegation_http.png "Delegation http")

18. Back in the **DC1 Properties** window, select **OK**.

### Task 3: Test an Azure AD Application Proxy application

1. From the lab computer, start a browser in Private mode and browse to the URL below. When prompted to sign in, use the **AGAyers\@<custom_domain_name>** user name with the **demo@pass123** password (where **<custom_domain_name>** placeholder represents the custom DNS domain name you assigned to the Contoso Azure AD tenant in the first exercise of this lab.

    ```
    https://myapps.microsoft.com
    ```

2. If prompted for MFA to enter a code, use either the phone number or email that you entered in the previous exercise to complete the MFA prompt.

3. On the **Apps** page of the **Application Access Panel**, select the **APP1 Default Web Site** icon. This will automatically open a new browser tab displaying the Default Web Site page on APP1.


### Task 4: Create an Azure Active Directory tenant and activate an EMS E5 trial

In this task, you will create another Azure Active Directory tenant representing the Fabrikam organization, with the following settings: 

-   Organization name: **Fabrikam**

-   Initial domain name: Any valid, unique domain name.

-   Country or region: **United States**

1. From the lab computer, start a new Web browser window and navigate to the Azure portal at <https://portal.azure.com>.

2. When prompted, sign into the Azure subscription into which you deployed resources in the Before Hands-On Lab exercises (the **Default Directory**).

3. On the lab computer, in the Azure portal, expand the left navigation and select **+ Create a resource**.

4. On the **New** blade, in the **Search the Marketplace** text box, type **Azure Active Directory** and, in the list of results, select **Azure Active Directory**.

5. On the **Azure Active Directory** blade, select **Create** and **Azure Active Directory**.

6. On the **Basics** tab, leave **Azure Active Dirtory** selected, and then select **Next: Configuration**.
c
7. On the **Configuration** tab, enter the following settings. The select **Review + create** and then **Create**.

    -   Organization name: **Fabrikam**

    -   Initial domain name: Any valid, unique domain name.

    -   Country or region: **United States**

    ![In this screenshot, the 'Create tenant' blade of the Azure portal is depicted with the required settings listed above and the Create button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateDirectoryConfiguration.png "Create tenant configuration form")

7. After the tenant has created, select **Fabrikam** to navigate to the newly created tenant.

    ![Screenshot showing the link to the Fabrikam tenant.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/fabrikam-newtenant.png "Link to the Fabrikam tenant")

8. On the **Fabrikam - Overview** page, select **Licenses** on the left.

9.  On the **Licenses - Overview**, page, select **All Products** under **Manage** on the left. Then select **+ Try/Buy**.

10. On the **Activate** page, in the **ENTERPRISE MOBILITY + SECURITY E5** section, select **Free trial** and then select **Activate**.

    ![In this screenshot, the Activate blade of the Azure portal is selected with the 'ENTERPRISE MOBILITY + SECURITY E5' section open with 'Free trial' selected along with the Activate button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/ActivateFreeTrial.png "Active free trial")


### Task 5: Create and configure Azure AD users

In this task, you will configure Azure AD user accounts in the newly created Azure AD tenant with the following settings. This will include assigning EM+S E5 licenses to the user account you are using for this lab as well as creating a new Azure AD user account with the following settings and assigning to it the Global Administrator role as well as the EM+S E5 license.

- Name: **jane.doe**

- First name: **Jane**

- Last name: **Doe**
    
- Password: **Auto-generate password**
    
- Show Password: **Enabled**

- Groups: **0 group selected**
    
- Roles: **Global Administrator**
    
- Block sign in: **No**
    
- Usage location: **United States**
    
- Job title: **Leave blank**
    
- Department: **Leave blank**

1. From the lab computer, in the Azure portal, navigate back to the **Fabrikam - Overview** page.

2. On the **Fabrikam - Overview** page, select **Users** under **Manage**.

3. On the **Users - All users** page, select the entry representing your user account.

4. On the **Profile** page of your user account, in the **Settings** section, select **Edit**.

    ![In this screenshot, the user Profile blade in the Azure portal is depicted with the Edit button selected in the Settings section.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/EditProfileSettings.png "Editing Settings")

5. In the **Settings** section, in the **Usage location** drop-down list, select the **United States** entry and select **Save**.

    ![In this screenshot, the user Profile blade in the Azure portal is depicted with United States selected in the 'Usage location' dropdown of the Settings section and the Save button is selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/UsageLocationDropdown.png "Usage location dropdown selection")

6. On the **Profile** page of your user account, select **Licenses** under **Manage** on the left.

7. On the **Licenses** page, select **+ Assignments**.

8. On the **Update license assignments** page, check the **Enterprise Mobility + Security E5** box, ensure that all the corresponding license options are enabled, and select **Save**.

9. On the **Users - All users** page, select **+ New user**.

10. On the **New user** page, ensure that the **Create user** option is selected, specify the following settings, and select **Create**:

    > **Note**: Copy the **User name** and **Password** values into Notepad. You will need them later in this lab.

    - User name: **jane.doe\@*your Azure AD tenant domain name*** where ***your Azure AD tenant domain name*** is the domain name you specified when creating the Fabrikam Azure AD tenant in the previous task.

    - Name: **jane.doe**

    - First name: **Jane**

    - Last name: **Doe**
    
    - Password: **Auto-generate password**
    
    - Show Password: **Enabled**

    - Groups: **0 group selected**
    
    - Roles: **Global Administrator**
    
    - Block sign in: **No**
    
    - Usage location: **United States**
    
    - Job title: **Leave blank**
    
    - Department: **Leave blank**
    

    ![In this screenshot, the 'New user' blade of the Azure portal is depicted with the 'Create user' option selected along with the required settings listed above and the Create button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateNewUser.png "New user blade with selected configuration")

11. On the **Users - All users** page, select the entry representing the newly created user account.

12. On the **jane.doe - Profile** page, select **Licenses** under **Manage** on the left.

13. On the **jane.doe - Licenses** page, select **+ Assignments**.

14. On the **Update license assignments** page, check the **Enterprise Mobility + Security E5** box, ensure that all the corresponding license options are enabled, and select **Save**.

### Task 6: Create and configure Azure AD guest user and group accounts

In this task, you will create and configure Azure AD guest accounts in the Contoso Azure AD tenant representing users in the Fabrikam Azure AD tenant.

1. Switch to the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal at <https://portal.azure.com> into which you are signed in with the **john.doe** credentials, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

2. On the **Contoso - Overview** page, select **Users** under **Manage** on the left.

3. On the **Users - All users** page, select **+ New guest user**.

4. On the **New user** page, ensure that the **Invite user** option is selected, specify the following settings, and select **Invite**:

    -  Name: **fabrikam-jane.doe**

    -  Email address: **The email address of the jane.doe user you created earlier**.

    -  First name: **Jane**

    -  Last name: **Doe**

    -  Personal message: **Welcome to the Contoso Azure AD tenant**

    -  Groups: **0 groups selected**

    -  Roles: **User**

    -  Block sign in: **No**

    -  Usage location: **United States**

    -  Job title : **Not set**

    -  Department : **Not set**

    ![In this screenshot, the 'New user' blade of the Azure portal is depicted with the 'Invite user' option selected along with the required settings listed above and the Invite button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/InviteNewUser.png "Invite new user settings")

5. In the Azure portal navigate back to the **Contoso - Overview** blade of the Contoso Azure AD tenant and select **Groups** under **Manage** on the left.

6. On the **Groups - All groups** page, select **New group**. 

7. On the **New group** page, specify the following settings, and select **Create**:

    -  Group type: **Security**

    -  Group name: **Fabrikam B2B users**

    -  Group description: **Fabrikam B2B users**

    - Azure AD roles can be assigned to the group: **No**

    -  Membership type: **Assigned**

    -  Owners: **No owners selected**

    -  Members: **fabrikam-jane.doe**

    ![In this screenshot, the 'New group' blade is depicted with the required settings listed above selected along with the Create button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateGroup.png "Create new group")

8. On the **Groups - All groups** blade, select the newly created group and, on the **Fabrikam B2B users** group, copy its **Object id** value and paste it into Notepad. You will need it later in this exercise.

9. Switch to the lab computer, start a web browser using in private/incognito mode and browse to https://portal.azure.com/<yourcontosotenant>.onmicrosoft.com. Where <yourcontosotenant> is the name you chose for your contoso tenant.

10. When prompted, sign in by using the credentials of the **jane.doe** Fabrikam Azure AD user account.

11. When prompted, grant the Contoso Azure AD tenant requested permissions by selecting **Accept**. 

12. When prompted, change the password for the **jane.doe** Fabrikam Azure AD user account. 
  
    > **Note**: If you receive the message **We've seen that password too many times before. Choose something harder to guess**, you'll need to modify the password until it is unique enough to be accepted.

13. In the Azure portal, sign out from the Contoso Azure AD tenant and close the window of the web browser in private/incognito mode.

### Task 7: Configure an Azure AD Application Proxy application for B2B access

In this task, you will configure an Azure AD Application Proxy application for B2B access.

1. Within the Remote Desktop session to **DC1**, in the Edge browser window displaying the Azure portal, navigate to the **Contoso - Overview** page of the Contoso Azure AD tenant.

2. On the **Contoso - Overview** page of the Contoso Azure AD tenant, select **Enterprise applications** under **Manage** on the left.

3. On the **Enterprise applications - All applications** page, select **APP1 Default Web Site**.

4. On the **APP1 Default Web Site - Overview** page, select **Users and groups** under **Manage** on the left.

5. On the **APP1 Default Web Site - Users and groups** page, select **+ Add user/group**.

6. On the **Add Assignment** page, specify the following settings and select **Assign**:

    - Users and groups: **jane.doe**

    - Select Role: **User**

7. Within the Remote Desktop session to **DC1**, in the Azure portal, navigate back to the **Contoso - Overview** blade of the Contoso Azure AD tenant.

8. On the **Contoso - Overview** page, select **App registrations** under **Manage** on the left.

9.  On the **Contoso - App registrations** page, select **+ New registration**.

10. On the **Register an application** page, specify the following information and select **Register**:

    - Name: **Sync B2B users**

    - Supported account types: **Accounts in this organizational directory only (Contoso only - Single tenant)**

    - Redirect URI (Optional): **Web** and **https://loopback**

    ![In this screenshot, the 'Register an application' blade of the Azure portal is depicted with the required settings listed above selected along with the Register button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/RegisterApplication.png "Register an application")

11. You will be automatically redirected to the **Sync B2B users** page.

12. On the **Sync B2B users** page, select **API permissions** under **Manage** on the left. 

13. On the **Sync B2B users - API permissions** page, in the **Configured permissions** section, select **+ Add a permission**.

14. On the **Request API permission** blade that appears on the right, switch to the **APIs my organization uses** tab, in the search text box, type **Windows Azure Active Directory**, in the list of results, select **Windows Azure Active Directory**, and then select **Application permissions**.

    ![In this screenshot, the 'Request API permission' blade of the Azure portal is depicted with the 'APIs my organization uses' tab selected with 'Windows Azure Active Directory' searched for and selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/RequestAPIPermissions.png "Request API permissions blade")

15. On the **Request API permissions** blade, in the **Select permissions** section, expand the **Directory** subsection, check the **Directory.Read.All** box, and select **Add permissions**.

    ![In this screenshot, the 'Request API permissions' blade of the Azure portal is depicted with the Directory.Read.All permission under the Directory subsection checked and the 'Add permissions' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/SyncB2BUsers_RequestAPIpermissions.png "API permission request settings")

16. Back on the **Sync B2B users - API permissions** page, in the **Configured permissions** section, select **Grant admin consent for Contoso**. Select **Yes** when prompted.

17. If prompted, sign in with the credentials of the **john.doe** Contoso Azure AD user account and, on the **Permissions requested Accept for your organization** page, select **Accept**.

18. Review the status of the permissions listed in the **Configured permissions** section on the **Sync B2B users - API permissions** blade and ensure that they are listed as **Granted for Contoso**.

    ![In this screenshot, the 'Sync B2B users - API permissions' blade of the Azure portal is depicted with the configured permissions listed with a status of 'Granted for Contoso'.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/GrantedForContoso.png "Permissions granted for Contoso")

19. On the **Sync B2B users - API permission** page, select **Certificates & secrets** under **Manage** on the left.

20. On the **Sync B2B users - Certificates & secrets** page, select **+ New client secret**.

21. On the **Add a client secret** page, specify the following information and select **Add**.

    - Description: **Sync B2B users secret 1**

    - Expires: **12 months**

22. Copy the resulting secret value. You will need it later in this task.

    > **Note**: This value will not be displayed again and cannot be retrieved once you navigate away from the current page. If you lose it, you will have to delete the secret and create another one.

23. On the **Sync B2B users** blade, select **Overview** on the left.

24. On the **Sync B2B users - Overview** blade, note the values of the **Application (client) ID** and **Directory (tenant) ID**. You will need them later in this task.

25. Within the Remote Desktop session to **DC1**, switch to the **Active Directory Users and Computers** console. 

26. In the **Active Directory Users and Computers** console, expand **corp.contoso.com** on the left, create an organizational unit named **Demo B2B Accounts** directly in the root of the domain with two child organizational units named **Enabled** and **Disabled**.

    ![In this screenshot, the 'Active Directory Users and Computers' console is depicted with the 'corp.contoso.com' node right-clicked with New then Organizational Unit selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/CreateOU.png "Create an organizational unit")

    > **Note**: These OUs must NOT be synchronized back to the Azure AD tenant using Azure AD Connect. Make sure not to include the guest user objects in the synchronization scope.

27. Within the Remote Desktop session to **DC1**, open a Windows PowerShell console and run the following to add a suffix matching the default DNS name of the Contoso Azure AD tenant (replace the `<domain_name>` placeholder with the name of the default domain name associated with the Contoso Azure AD tenant):

    ```pwsh
    Get-ADForest | Set-ADForest -UPNSuffixes @{Add="<domain_name>.onmicrosoft.com"}
    ```

28. Within the Remote Desktop session to **DC1**, start the Edge browser and browse to the following URL.

    ```
    https://www.microsoft.com/en-us/download/details.aspx?id=51495
    ```

29. On the **Connectors for Microsoft Identity Manager 2016 SP1 and Forefront Identity Manager 2010 R2 SP1** page, download **Script and Readme to pull Azure AD B2B users on-prem_v1.0.3.zip** and extract its content. You'll have to scroll down to find it.

30. Once the files are extracted, right click on the PowerShell script, open the file properties, and **Unblock** the script.

30. Within the Remote Desktop session to **DC1**, in Visual Studio Code, open the newly extracted PowerShell script **AppProxy-GuestAccountCreation-v1.0.3.ps1** and modify its content by updating it to match the following:

    > Note: If for some reason you can't open the file, you can use the **Open folder** option in Visual Studio Code to open the folder containing the script.

    ```pwsh
    $B2BGroupSid = "TODO" #Fabrikam B2B users Azure AD group's ObjectID that you identified earlier in this exercise.
    $ShadowAccountOU = "OU=Enabled,OU=Demo B2B Accounts,DC=corp,DC=contoso,DC=com" #Organizational Unit for placing shadow accounts
    $ShadowAccountOUArchive = "OU=Disabled,OU=Demo B2B Accounts,DC=corp,DC=contoso,DC=com" #Organizational Unit for moving disabled shadows

    # Requires Azure AD configuration - refer to documentation
    $appID = "TODO" #The value of Client ID parameter of the Sync B2B user application you identified earlier in this exercise
    $appSecret = "TODO" #The value of the secret of the Sync B2B user application you identified earlier in this exercise
    $tenantdomain   = "TODO" #The name of the default domain name associated with the Contoso Azure AD tenant
    $tenantID = "TODO" #The value of Azure AD tenant ID parameter of the Sync B2B user application you identified earlier in this exercise
    ```
    > **Note**: For more information regarding the script and its implementation, refer to the **Readme - Script to pull Azure AD B2B users on-prem_v1.0.3.pdf** file, included in the **1.1.953.0\Script and Readme to pull Azure AD B2B users on-prem_v1.0.3.zip** file you downloaded earlier in this task.

31. Install the AzureAD PowerShell Module using the script below. Confirm any prompts while installing it.

    ```
    Install-Module AzureAD
    ```

1.  Execute the script and ensure that it did not return any error messages. 

    > **Note**: You can schedule script execution in regular intervals by using Windows Scheduled Tasks. For details, refer to the **Readme - Script to pull Azure AD B2B users on-prem_v1.0.3.pdf** file.

2.  Switch back to the Azure Active Directory Users and Computers console and verify that a user account of **jane.doe** is listed in the **Demo B2B Accounts\\Enabled** organizational unit. You may have to refresh the console. 

    > **Note**: In a production environment, you could provide access to Integrated Windows Authentication apps by leveraging Microsoft Identity Manager. You can also provide access to on-premises apps that support SAML-based authentication directly from the Azure portal. For more information, refer to Grant B2B users in Azure AD access to your on-premises applications at <https://docs.microsoft.com/en-us/azure/active-directory/b2b/hybrid-cloud-to-on-premises>.

    ![In this screenshot, the 'Active Directory Users and Computers' console is depicted with the 'jane.doe' user account listed in the 'Demo B2B Accounts\Enabled' organizational unit.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/UserAccountVerification.png "User account verification")


### Task 8: Test an Azure AD Application Proxy application

1. On the lab computer, start a browser in Private mode and go to the URL below:

    ```
    https://myapps.microsoft.com
    ```

2. When prompted, sign in by using the **jane.doe** Fabrikam Azure AD user account. 

3. Once signed in, select the **Jane Fabrikam** icon in the upper right corner of the Application Access Panel page and, in the drop-down menu, select **Switch organization**.

4. Select the **Contoso** Organization.

4. On the **Apps** page of the **Application Access Panel**, select the **APP1 Default Web Site** icon. This will automatically open a new browser tab displaying the Default Web Site page on APP1.


**Summary**

In this exercise, you configured access to on-premises Integrated Windows Authentication app (implemented as the default IIS web site) from the internet by installing and configuring Azure AD Application Proxy. You also tested access to this application by using a Contoso Azure AD tenant user account as well as by using a Fabrikam Azure AD tenant user account configured as a guest account in the Contoso Azure AD tenant. 

## Exercise 4: Create resiliency within the Hybrid Identity infrastructure

Duration: 90 minutes

**Overview**

In this exercise, you will configure a secondary domain controller and install Azure AD Connect in standby mode for fail-over. You will also configure a second pass-through agent and application proxy on the secondary domain controller. 


### Task 1: Create a VM for the secondary domain controller

In this task, you will create a VM that will become the backup domain controller within the hybrid infrastructure.

1. From within the Azure portal, select **+ Create a resource**, select **Compute**, and select **Create** under **Virtual machines**.

    ![In this screenshot, you are selecting to create a Virtual machine as a compute resource.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/createvm.png "Create a Virtual machine")

2. Complete the following information for the Virtual machine and select **Next: Disks**:
   
    - Resource group: **hybrididentity-RG** 
  
    - Virtual machine name: **BDC-1**
  
    - Image: **Windows Server 2016 Datacenter - Gen 1** 
  
    - Size: **Standard_D2s_v3**
   
    - Username: **demouser** 
  
    - Password: **demo@pass123**
  
    - Public inbound ports: **Allow selected ports**
  
    - Select inbound ports: **RDP (3389)**

    ![This screenshot is showing the basic configuration details for the virtual machine.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/createvmdetails.png "Virtual machine basic configuration")

3. Select **Create and attach a new disk**.

4. On the **Create a new disk** tile, select **Change size** and change the disk size to 32 GB.

5. Select **OK** to continue.

    ![This screenshot is showing where to change the disk size before creating a new managed disk for the virtual machine.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/adddisk.png "Change disk size")

6. Select **Next: Networking** and verify the Virtual network is **TlgBaseConfig-01-VNET** and Subnet is **subnet-01**.  This will make sure that the new Virtual machine is on the same network as the primary domain controller, **DC-1**. Keep the default values for the remaining fields.  Select **Review + create**.
   
    ![In this screenshot, the networking tile is being configured and we are choosing the existing virtual network and subnet.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/vmnetwork.png "Virtual machine networking")

7. Select **Create** to create the Virtual machine.

### Task 2: Promote the VM to a domain controller

In this task, you will promote the newly created VM to a domain controller and configure it to be the backup to DC1.

1. Navigate to the **hybrididentity-RG** Resource group and select the **BDC-1** Virtual machine.
   
2. Select **Connect** and choose **RDP**.
    
    ![This screenshot is showing how to connect to the virtual machine using RDP.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/connectrdp.png  "Connect with RDP")

3. Connect to the Virtual machine with the username and password used in the previous task.
   
4. From the **Server Manager** dashboard, select **Add roles and features**.

    ![After connecting into the virtual machine, you will configure the server role in server manager as shown in this screenshot.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/addroles.png "Add Server roles and features")

5. Select **Next** in the **Add Roles and Features Wizard**, at the **Server selection** tab, verify that **BDC-1** is selected, then select **Next** for the **Server Roles** tab.

6. Select the **Active Directory Domain Services** checkbox under **Roles**.

    ![In this screenshot, you will select the role of Active Directory Domain Service in the server roles wizard.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/addaddsrole.png "Select server roles")

7. When the **Add features** tile opens, uncheck the box for **Include management tools (if applicable)** and select **Add Features** to continue.

    ![In this screenshot, you unselect the include management tools checkbox and add features.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/addsaddfeatures.png "Add roles and features wizard")

8. Select **Next** through **Features** and **AD DS**.  At the **Confirmation** tile, select **Install**.

    ![This screenshot shows the configurations being complete and ready to install.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/addsinstall.png "Install server roles")

9. Select **Close** when installation completes.

10. Right-click the network connection icon on the taskbar to open the **Network and sharing center**.
    
11. Select **Ethernet** next to **Connections**.
    
12. When the **Ethernet Status** tile opens, select **Properties**.
    
13. On the **Ethernet Properties** tile, select **Internet Protocol Version 4 (TCP/IPv4)**, and select **Properties**.
    
14. On the **Internet Protocol Version 4 (TCP/IPv4)** tile, select the radio button for **Use the following DNS server addresses** and enter the IP address of **DC-1**. Select **OK** to save the changes. 
        
    ![This screenshot shows the steps to follow to add a DNS server to the device network configuration.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/dc1dns.png "Add DNS to Network properties")

15. Restart the **BDC-1** Virtual machine.

16. When **BDC-1** restarts, RDP back into it.  There will be a flag with a notification on the top right of the **Server Manager Dashboard**.  Select this flag for the **Post-deployment Configuration**, and select **Promote this server to a domain controller**.

    ![After the virtual machine restarts, select to promote the server by selecting the flag in the Server Manager, as shown in this screenshot.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/promotedc.png "Promote the server to a DC")

17. Select **Add a domain controller to an existing domain**, select **Select**. 

    ![This screenshot shows the deployment configuration to add an existing domain by selecting select.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/existingdomain.png "Add DC to existing domain")

18. Enter **corp.contoso.com\demouser** for the server username and password **demo@pass123** to authenticate to the domain.

    ![This screenshot shows how to login to the existing domain.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/addcontosodomain.png "Login to existing domain")

1.  Select **corp.contoso.com** and **OK**.

    ![This screenshot shows that you can now select the existing domain for the new backup domain controller.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/contosodomain.png "Select existing domain")

19. Select **Next**.

    ![The existing domain is now populated in the deployment configuration along with the administrator credentials.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/domainconfignext1.png "Existing domain credentials")

20. On **Domain Controller options**, keep **Domain Name System (DNS) server** and **Global Catalog (GC)** checked.  Enter the password **demo@pass123** for the **Directory Services Restore Mode (DSRM)** password.  Select **Next**.

    ![As the screenshot shows, you will need to create a password for directory services restore mode.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/dcoptions.png "DC options")

21. For **DNS options**, select **Next**.

22. On **Additional options**, select **DC1.corp.contoso.com** on the **Replicate from** drop-down and select **Next**.

    ![In this screenshot, you will choose the drop-down arrow and select the primary domain controller to replicate from.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/dc1replica.png "Select primary domain controller")

23. Leave **Paths** the default value and select **Next**.

    ![This screenshot shows the default paths that will remain unchanged.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/dcpaths.png "Default file paths")

24. **Review options** and select **Next**.

    ![This screenshot shows the configuration settings prior to installing the new role.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/dcreviewoptions.png "Review options")

25. Verify that **All prerequisite checks passed successfully** and select **Install**.

    ![This screenshot shows what you should see when the server has passed the prerequisite checks prior to installing the domain controller role.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/checkspassed.png "Pre-requisite check")

26. After installation, the VM will restart, and the **BDC-1** will be configured as your **Backup domain controller**.

27. In order for clients to fail-over to **BDC-1** when **DC-1** is off-line, the IP address of **BDC-1** will need to be added as the **Alternate DNS server** within **Internet Protocol Version 4 (TCP/IPv4) Properties** on all domain joined devices.  On each device, repeat steps 10-15 in this task, but enter the internal IP address of **BDC-1** as the **Alternate DNS server** address.

    ![After the backup domain controller role is installed, device network IP settings must have the IP address added as the Alternate DNS server.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/alternatedns.png "Alternate DNS server IP address")


### Task 3: Install Azure AD Connect in standby mode

In this task, you will install and configure Azure AD Connect in standby mode.  This will allow **BDC-1** to take over identity synchronization if **DC1** goes offline.

1. Since **Azure AD Connect** has already been downloaded and installed from the portal, on **BDC-1** you need to navigate to the **Microsoft Download Center** to download **Azure AD Connect** for **BDC-1**.

    ```
    https://www.microsoft.com/en-us/download/confirmation.aspx?id=47594
    ```

2. Scroll down to find **Microsoft Azure Active Directory Connect** and select **Download**.

    ![In this screenshot, we are navigating to the Microsoft Download Center to download Azure AD Connect.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/azureadconnectdownload.png "Download Azure AD Connect")

3. Download the **AzureADConnect.msi** file by selecting **Click here** under **Download link**.

    ![In this screenshot, we are selecting the link to download the Azure AD Connect msi file.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/azureadconnectdownloadlink.png "Azure AD Connect msi file")

4. When prompted, select the drop-down arrow and choose **Save as** to save the **AzureADConnect.msi** file to the **Downloads** folder.

    ![In this screenshot, we are selecting the save location for the Azure AD Connect msi file.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/azureadconnectsaveas.png "Save file to Download folder")

5. After the download is complete, go to the **Downloads** folder in **File Explorer** and run the **AzureADConnect** installation.

    ![After the download is complete, you will navigate to the downloads folder to select the file to install, as shown in this screenshot.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/azureadconnectfile.png "Run Azure AD Connect installation")

6. After installation, the **Microsoft Azure Active Directory Connect** configuration wizard will start automatically.  Accept the license terms to continue.

    ![This screenshot shows that you are required to agree to the license terms before installing Azure AD Connect.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/azureadconnectterms.png "Agree to license terms")

7. To configure the **BDC-1** backup domain controller as a staging server, select **Customize**.

    ![This screenshot shows that you will not be using Express settings but will need to customize the settings.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/customizesettings.png "Customize settings")

8. Select **Install**.

    ![Install the required components and do not select any of the optional components before selecting install, as shown in this screenshot.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/installazureadconnect.png "Install Azure AD Connect")

9.  Follow the same steps as Exercise 1, Task 6, Steps 15-24.  On the final **Configure** step, un-check the **Start the synchronization process when configuration completes** checkbox, and select the **Enable staging mode** checkbox. Select **Install** to complete the installation of the configuration.

    ![Once Azure AD Connect has been installed and all credentials have been provided, unselect the checkbox for starting synchronization and check the box for enable staging mode as shown in this screenshot.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/readytoconfigure.png "Configure in staging mode")

10. Navigate to the **Windows Start menu** and open **Synchronization Service Manager**.

    ![This screenshot shows the Synchronization service application within the Windows Start menu.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/syncservice.png "Open Synchronization service")
    
11. Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**. Select **Run**, select **Full import**, and **OK**. Do these steps for all Connectors of this type.

    ![After the Synchronization service manager opens, select Connectors on the menu as shown in this screenshot.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/syncconnectors.png "Select Connectors")

12. Select the Connector with type **Azure Active Directory (Microsoft)**. Select **Run**, select **Full import**, and **OK**.
    
13. Make sure the tab Connectors is still selected. For each Connector with type **Active Directory Domain Services**, select **Run**, select **Delta Synchronization**, and **OK**.
    
14. Select the Connector with type **Azure Active Directory (Microsoft)**. Select **Run**, select **Delta Synchronization**, and **OK**.


### Task 4: Install pass through agent 

In this task, you will install and configure the Azure AD Connect pass through agent.

1. Within the Remote Desktop session to **BDC-1**, in the Edge browser window displaying the Azure portal, navigate to the **Contoso - Overview** blade of the Contoso Azure AD tenant.
   
2. To download the latest version of the Authentication Agent (version 1.5.193.0 or later), sign in to the Azure Active Directory admin center with your tenant's global administrator credentials.
   
3. Select Azure Active Directory in the left pane.
   
4. Select Azure AD Connect, select Pass-through authentication, and then select Download Agent.
   
5. Select the Accept terms & download button.
   
6. Run the downloaded Authentication Agent executable and providing your tenant's global administrator credentials when prompted.
   

### Task 5: Configure Azure AD Application Proxy for BDC-1 VM

In this task, you will configure Azure AD Application Proxy for the BDC-1 VM.

1. Within the Remote Desktop session to **DC1**, in the Server Manager console, select **Tools** and then select **Active Directory Users and Computers**. 

2.  In the **Active Directory Users and Computers** console, select **View** and, in the **View** menu, enable **Advanced Features**.

    ![In this screenshot, the 'Active Directory Users and Computers' console is depicted with the View menu open and the Advanced Features button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/EnableAdvancedFeatures.png "Enable Advanced Features in the console")

3.  In the **Active Directory Users and Computers** console, locate the computer account hosting the Azure AD Application Proxy connector (**DC1** in our case) under **Domain Controllers** within **corp.contoso.com** and display its **Properties** window.

    ![In this screenshot, the 'Active Directory Users and Computers' console is depicted with the Domain Controllers node selected on the left and the DC1 computer account right-clicked with the Properties menu option selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/DisplayComputerProperties.png "Display computer properties")

4.  In the **DC1 Properties** window, switch to the **Delegation** tab and select the option **Trust this computer for delegation to specified services only**.

5.  Select the option **Use any authentication protocol**, select **Add**, in the **Add Services** window, select **Users or Computers**, in the **Select Users or Computers** dialog box, in the **Enter the object names to select** text box, type **APP1** and select **OK**. 

    ![In this screenshot, the 'DC1 Properties' window is depicted with the Delegation tab selected with the 'Trust this computer for delegation to specified services only' and 'Use any authentication protocol' options and the 'Add' button selected.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/DelegationConfiguration.png "Delegation configuration")

6.  Back in the **Add Services** window, select the **http** entry and select **OK**. 

    ![In this screenshot, 'Add Services' window is depicted with the 'http' entry selected along with the OK button.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/AzureADApplicationProxy_Delegation_http.png "Delegation http")

7.  Back in the **DC1 Properties** window, select **OK**.

**Summary** 

In this exercise, you installed and configured a backup domain controller, set it up for Azure AD Connect standby synchronization, and added redundancy with the Azure AD Connect pass through agents and Application proxy.  You have now configured a resilient and available hybrid identity architecture.

## Exercise 5: Configure Password-less Authentication methods

### Task 1: Configure Authentication methods

1. Navigate to Azure Active Directory within the Azure portal.  In the Azure Active Directory menu, select **Security**.

    ![In this screenshot, we navigate to Azure Active Directory and choose Security in the tile menu.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/azureadsecurity.png "Azure AD Security")

2. In the **Security | Getting Started** tile, select **Authentication methods** under the **Manage** section of the left tile menu.

    ![In this screenshot, we are selecting authentication methods under the manage menu.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/authmethods.png "Authentication methods")

3. Under **Method**, select **Microsoft Authenticator**.

4. The details will populate below, select **Yes** for **Enable**, select **Select users** for **Target**.  

5. Select **Add users and groups** and select **Ann G. Ayers** under users.  Select **Save** to add the user.  

6. Select **Save** under **Details** to save the configuration.

    ![In this screenshot, we are configuring the authentication method of Microsoft Authenticator for one of the users in Azure AD.](images/Hands-onlabstep-bystep-HybridIdentityImages/media/configmsftauthenticator.png "Configure Microsoft Authenticator")

7. The next time that **Ann G. Ayers** attempts to login, they will be prompted to configure the **Microsoft Authenticator** app to complete authentication.

**Lab summary**

In this hands-on lab, you setup and configured a number of different hybrid identity scenarios. The scenarios involved an Active Directory single-domain forest named corp.contoso.com, which in this lab environment, consisted (for simplicity reasons) of a single domain controller named DC1 and a single domain member server named APP1. You explored Azure AD-related capabilities that allowed you to integrate Active Directory with Azure Active Directory, optimized hybrid authentication and authorization, and provided secure access to on-premises resources from Internet for both organizational users and users who are members of partner organizations. 

## After the hands-on lab

Duration: 20 Minutes

### Task 1: Delete resources

1. Now that the HOL is complete, go ahead and delete all of the Resource Groups created for this HOL. You will no longer need those resources, and it will be beneficial to clean up your Azure Subscription. In addition, remove the verified domain from the Contoso Azure AD tenant.

You should follow all steps provided *after* attending the Hands-on lab.

