---
title: "Konfigurowanie automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w usłudze Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Konfigurowanie urządzeń przyłączonych do domeny systemu Windows zarejestrować automatycznie i w trybie dyskretnym za pomocą usługi Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: dccd7df6a5f85df4179c7ea7cfc476cfb57f48c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="a0500-103">Konfigurowanie automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0500-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="a0500-104">Aby użyć [dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-azure-portal.md), komputer musi być zarejestrowana w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a0500-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="a0500-105">Można uzyskać listę zarejestrowanych urządzeń w Twojej organizacji za pomocą [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) polecenia cmdlet w [modułu programu PowerShell usługi Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="a0500-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="a0500-106">Ten artykuł zawiera kroki związane z konfigurowaniem automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny z usługą Azure AD w organizacji.</span><span class="sxs-lookup"><span data-stu-id="a0500-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="a0500-107">Aby uzyskać więcej informacji na temat:</span><span class="sxs-lookup"><span data-stu-id="a0500-107">For more information about:</span></span>

- <span data-ttu-id="a0500-108">Funkcja dostępu warunkowego, zobacz [dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a0500-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="a0500-109">Urządzenia z systemem Windows 10 w miejscu pracy i rozszerzonych środowisk po zarejestrowaniu w usłudze Azure AD, zobacz [systemu Windows 10 dla przedsiębiorstw: używanie urządzeń do pracy](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a0500-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="a0500-110">Windows 10 Enterprise E3 w dostawcy usług Kryptograficznych, zobacz [systemu Windows 10 Enterprise E3 w dostawcy usług Kryptograficznych — omówienie](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="a0500-110">Windows 10 Enterprise E3 in CSP, see the [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="a0500-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="a0500-111">Before you begin</span></span>

<span data-ttu-id="a0500-112">Przed rozpoczęciem konfigurowania automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w danym środowisku, należy zapoznać się z obsługiwanych scenariuszach i ograniczeniach.</span><span class="sxs-lookup"><span data-stu-id="a0500-112">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="a0500-113">Aby zwiększyć czytelność opisy, w tym temacie używa następujących termin:</span><span class="sxs-lookup"><span data-stu-id="a0500-113">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="a0500-114">**Urządzenia z systemem Windows bieżącego** -określenie to odnosi się do urządzeń przyłączonych do domeny z systemem Windows 10 lub Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a0500-114">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="a0500-115">**Urządzenia z systemem Windows niższego poziomu** -określenie to odnosi się do wszystkich **obsługiwane** przyłączonych do domeny urządzenia z systemem Windows, które nie są uruchomione systemu Windows 10 ani Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a0500-115">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="a0500-116">Bieżący urządzeń z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="a0500-116">Windows current devices</span></span>

- <span data-ttu-id="a0500-117">W przypadku urządzeń z pulpitu systemu operacyjnego Windows, zaleca się użycie systemu Windows 10 Anniversary aktualizacji (w wersji 1607) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="a0500-117">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="a0500-118">Rejestracja urządzeń z systemem Windows bieżącego **jest** obsługiwane w niefederacyjnych środowiskach, takich jak konfiguracje synchronizacji skrótu hasła.</span><span class="sxs-lookup"><span data-stu-id="a0500-118">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="a0500-119">Urządzenia z systemem Windows niższego poziomu</span><span class="sxs-lookup"><span data-stu-id="a0500-119">Windows down-level devices</span></span>

- <span data-ttu-id="a0500-120">Obsługiwane są następujące urządzeń z systemem Windows niższego poziomu:</span><span class="sxs-lookup"><span data-stu-id="a0500-120">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="a0500-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="a0500-121">Windows 8.1</span></span>
    - <span data-ttu-id="a0500-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="a0500-122">Windows 7</span></span>
    - <span data-ttu-id="a0500-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="a0500-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="a0500-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="a0500-124">Windows Server 2012</span></span>
    - <span data-ttu-id="a0500-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="a0500-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="a0500-126">Rejestracja urządzeń z systemem Windows niższego poziomu **jest** obsługiwane w środowiskach niefederacyjnych za pośrednictwem bezproblemowe rejestracji jednokrotnej [Azure Active Directory bezproblemowe logowanie jednokrotne](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="a0500-126">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="a0500-127">Rejestracja urządzeń z systemem Windows niższego poziomu **nie jest** obsługiwane na urządzeniach przy użyciu profilów mobilnych.</span><span class="sxs-lookup"><span data-stu-id="a0500-127">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="a0500-128">Jeśli używasz mobilnego profile i ustawienia, należy użyć systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="a0500-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="a0500-129">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="a0500-129">Prerequisites</span></span>

<span data-ttu-id="a0500-130">Przed rozpoczęciem Włączenie automatycznej rejestracji urządzeń przyłączonych do domeny w swojej organizacji, musisz upewnij się, że uruchamiasz zaktualizowanej wersji programu Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="a0500-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="a0500-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="a0500-131">Azure AD Connect:</span></span>

- <span data-ttu-id="a0500-132">Umożliwia zachowanie skojarzenia między konta komputera w lokalnej usłudze Active Directory (AD) i obiekt urządzenia w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0500-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="a0500-133">Umożliwia urządzeniu innych powiązanych funkcji, takich jak Windows Hello dla firm.</span><span class="sxs-lookup"><span data-stu-id="a0500-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="a0500-134">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a0500-134">Configuration steps</span></span>

<span data-ttu-id="a0500-135">Ten temat zawiera kroki wymagane w przypadku wszystkich scenariuszy typowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a0500-135">This topic includes the required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="a0500-136">Skorzystaj z poniższej tabeli, aby uzyskać przegląd kroków, które są wymagane dla danego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="a0500-136">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="a0500-137">Kroki</span><span class="sxs-lookup"><span data-stu-id="a0500-137">Steps</span></span>                                      | <span data-ttu-id="a0500-138">Synchronizacja skrótów bieżące i hasło systemu Windows</span><span class="sxs-lookup"><span data-stu-id="a0500-138">Windows current and password hash sync</span></span> | <span data-ttu-id="a0500-139">Bieżącego systemu Windows i Federacji</span><span class="sxs-lookup"><span data-stu-id="a0500-139">Windows current and federation</span></span> | <span data-ttu-id="a0500-140">Niższego poziomu z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="a0500-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="a0500-141">Krok 1: Konfigurowanie punktu połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="a0500-141">Step 1: Configure service connection point</span></span> | ![Zaznacz][1]                            | ![Zaznacz][1]                    | ![Zaznacz][1]        |
| <span data-ttu-id="a0500-145">Krok 2: Skonfiguruj wystawiania oświadczeń</span><span class="sxs-lookup"><span data-stu-id="a0500-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Zaznacz][1]                    | ![Zaznacz][1]        |
| <span data-ttu-id="a0500-148">Krok 3: Włącz urządzenia z systemem innym niż Windows 10</span><span class="sxs-lookup"><span data-stu-id="a0500-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Zaznacz][1]        |
| <span data-ttu-id="a0500-150">Krok 4: Wdrażanie formantu i wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a0500-150">Step 4: Control deployment and rollout</span></span>     | ![Zaznacz][1]                            | ![Zaznacz][1]                    | ![Zaznacz][1]        |
| <span data-ttu-id="a0500-154">Krok 5: Sprawdzanie zarejestrowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="a0500-154">Step 5: Verify registered devices</span></span>          | ![Zaznacz][1]                            | ![Zaznacz][1]                    | ![Zaznacz][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="a0500-158">Krok 1: Konfigurowanie punktu połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="a0500-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="a0500-159">Obiekt (SCP) punkt połączenia usługi jest używany przez urządzenia podczas rejestrowania informacji dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0500-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="a0500-160">W lokalnej usługi Active Directory (AD) obiektu SCP automatycznej rejestracji urządzeń przyłączonych do domeny muszą istnieć w kontekście partycji komputera lesie nazw konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="a0500-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="a0500-161">Istnieje tylko jeden kontekście nazewnictwa konfiguracji w każdym lesie.</span><span class="sxs-lookup"><span data-stu-id="a0500-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="a0500-162">W konfiguracji obejmującego wiele lasów usługi Active Directory punkt połączenia z usługą musi istnieć we wszystkich lasach środowiska zawierającego komputery przyłączone do domeny.</span><span class="sxs-lookup"><span data-stu-id="a0500-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="a0500-163">Można użyć [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) polecenia cmdlet, aby pobrać kontekście nazewnictwa konfiguracji w lesie.</span><span class="sxs-lookup"><span data-stu-id="a0500-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="a0500-164">Dla lasu o nazwie domeny usługi Active Directory *fabrikam.com*, jest w kontekście nazewnictwa konfiguracji:</span><span class="sxs-lookup"><span data-stu-id="a0500-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="a0500-165">W lesie obiektu SCP automatycznej rejestracji urządzeń przyłączonych do domeny znajduje się na:</span><span class="sxs-lookup"><span data-stu-id="a0500-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="a0500-166">W zależności od tego, jak zostały wdrożone usługi Azure AD Connect obiektu SCP może zostały już skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="a0500-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="a0500-167">Można sprawdzić istnienia obiektu i pobierania wartości odnajdywania przy użyciu następujący skrypt programu Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a0500-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="a0500-168">**$Scp. Słowa kluczowe** dane wyjściowe zawierają informacje o dzierżawy usługi Azure AD, na przykład:</span><span class="sxs-lookup"><span data-stu-id="a0500-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="a0500-169">Jeśli punkt połączenia usługi nie istnieje, należy go utworzyć, uruchamiając `Initialize-ADSyncDomainJoinedComputerSync` polecenia cmdlet na serwerze programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a0500-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="a0500-170">Poświadczenia administratora przedsiębiorstwa jest wymagana do uruchamiania tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0500-170">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="a0500-171">Polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a0500-171">The cmdlet:</span></span>

- <span data-ttu-id="a0500-172">Tworzy punkt połączenia z usługą w lesie usługi Active Directory, którą połączony jest Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="a0500-172">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="a0500-173">Wymaga podania `AdConnectorAccount` parametru.</span><span class="sxs-lookup"><span data-stu-id="a0500-173">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="a0500-174">Jest to konto, która jest skonfigurowana jako usługi Active Directory connector konta w usłudze Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="a0500-174">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="a0500-175">Poniższy skrypt pokazuje przykład za pomocą polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0500-175">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="a0500-176">W tym skrypcie `$aadAdminCred = Get-Credential` wymaga nazwy użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a0500-176">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="a0500-177">Należy podać nazwę użytkownika w formacie (UPN) Nazwa główna użytkownika (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="a0500-177">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="a0500-178">`Initialize-ADSyncDomainJoinedComputerSync` Polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="a0500-178">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="a0500-179">Używa modułu środowiska PowerShell usługi Active Directory, która zależy od usługi Active Directory w sieci Web uruchomiony na kontrolerze domeny.</span><span class="sxs-lookup"><span data-stu-id="a0500-179">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="a0500-180">Usługi sieci Web w usłudze Active Directory jest obsługiwana na kontrolerach domeny z systemem Windows Server 2008 R2 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a0500-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="a0500-181">Jest obsługiwana tylko przez **MSOnline PowerShell w wersji modułu 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="a0500-181">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="a0500-182">Aby pobrać ten moduł, użyj [łącze](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="a0500-182">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="a0500-183">Dla kontrolerów domeny z systemem Windows Server 2008 lub starszej wersji Użyj poniższego skryptu, aby utworzyć punkt połączenia usługi.</span><span class="sxs-lookup"><span data-stu-id="a0500-183">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="a0500-184">W konfiguracji wielu lasów należy użyć następującego skryptu można utworzyć punktu połączenia z usługą w każdym lesie, w którym istnieje komputerów:</span><span class="sxs-lookup"><span data-stu-id="a0500-184">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="a0500-185">Krok 2: Skonfiguruj wystawiania oświadczeń</span><span class="sxs-lookup"><span data-stu-id="a0500-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="a0500-186">W federacyjnych Azure konfiguracji AD urządzeń zależą od usługi Active Directory Federation Services (AD FS) lub 3 strona lokalnej usługi federacyjnej do uwierzytelniania usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0500-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="a0500-187">Uwierzytelnianie urządzeń do uzyskania tokenu dostępu, aby zarejestrować przed Azure Active Directory usługi rejestracji urządzeń (Azure DRS).</span><span class="sxs-lookup"><span data-stu-id="a0500-187">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="a0500-188">Systemu Windows, które urządzenia bieżące uwierzytelniania przy użyciu zintegrowanego uwierzytelniania systemu Windows do aktywnego punktu końcowego usługi WS-Trust (w wersji 1.3 lub 2005) obsługiwanych przez usługę federacyjną lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="a0500-188">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="a0500-189">Korzystając z usług AD FS, albo **adfs/services/zaufania/13/windowstransport** lub **adfs/services/zaufania/2005/windowstransport** musi być włączona.</span><span class="sxs-lookup"><span data-stu-id="a0500-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="a0500-190">Jeśli korzystasz z uwierzytelniania serwera Proxy sieci Web, również upewnić się, czy ten punkt końcowy został opublikowany przez serwer proxy.</span><span class="sxs-lookup"><span data-stu-id="a0500-190">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="a0500-191">Widać, jakie punkty końcowe są włączane za pośrednictwem konsoli zarządzania usług AD FS, w obszarze **usługi > punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="a0500-191">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="a0500-192">Jeśli nie masz jako lokalnej usługi federacyjnej usług AD FS, postępuj zgodnie z instrukcjami dostawcy, aby upewnić się na obsługę protokołu WS-Trust 1.3 lub punkty końcowe 2005, a te są publikowane za pomocą pliku wymiany metadanych (MEX).</span><span class="sxs-lookup"><span data-stu-id="a0500-192">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="a0500-193">Następujące oświadczeń musi istnieć w tokenie odebranych przez Azure usługi rejestracji urządzeń w czasie rejestracji urządzenia do ukończenia.</span><span class="sxs-lookup"><span data-stu-id="a0500-193">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="a0500-194">Usługi rejestracji urządzeń usługi Azure utworzy obiekt urządzenia w usłudze Azure AD, niektóre z tych informacji, która jest następnie używany przez program Azure AD Connect do skojarzenia obiektu urządzenia nowo utworzony z komputera konta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="a0500-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="a0500-195">Jeśli masz więcej niż jedną nazwę zweryfikowanej domeny, musisz podać następujące oświadczenie dla komputerów:</span><span class="sxs-lookup"><span data-stu-id="a0500-195">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="a0500-196">Jeśli są już wystawiania oświadczeń nazwę ImmutableID (np. alternatywnego Identyfikatora logowania) musisz podać jedno oświadczenie odpowiednie dla komputerów:</span><span class="sxs-lookup"><span data-stu-id="a0500-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="a0500-197">W poniższych sekcjach można znaleźć informacje o:</span><span class="sxs-lookup"><span data-stu-id="a0500-197">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="a0500-198">Wartości Każde oświadczenie ma</span><span class="sxs-lookup"><span data-stu-id="a0500-198">The values each claim should have</span></span>
- <span data-ttu-id="a0500-199">Jak definicji będzie wyglądać w usługach AD FS</span><span class="sxs-lookup"><span data-stu-id="a0500-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="a0500-200">Definicja pomaga Sprawdź, czy wartości są obecne lub należy je utworzyć.</span><span class="sxs-lookup"><span data-stu-id="a0500-200">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="a0500-201">Jeśli nie używasz usług AD FS dla lokalnego serwera federacyjnego, wykonaj instrukcje z dostawcą, aby utworzyć odpowiednią konfigurację wystawiać te oświadczenia.</span><span class="sxs-lookup"><span data-stu-id="a0500-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="a0500-202">Problem konta typu oświadczenia</span><span class="sxs-lookup"><span data-stu-id="a0500-202">Issue account type claim</span></span>

<span data-ttu-id="a0500-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**— To oświadczenie musi zawierać wartość **DJ**, które identyfikują urządzenie jako komputer przyłączony do domeny.</span><span class="sxs-lookup"><span data-stu-id="a0500-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="a0500-204">W usługach AD FS można dodawać reguł przekształcania wystawiania, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="a0500-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="a0500-205">Wystawiać objectGUID komputera konta lokalnego</span><span class="sxs-lookup"><span data-stu-id="a0500-205">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="a0500-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**— To oświadczenie musi zawierać **objectGUID** wartość Konto komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="a0500-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="a0500-207">W usługach AD FS można dodawać reguł przekształcania wystawiania, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="a0500-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="a0500-208">Wystawiać objectSID komputera konta lokalnego</span><span class="sxs-lookup"><span data-stu-id="a0500-208">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="a0500-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**— To oświadczenie musi zawierać **objectSid** wartość Konto komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="a0500-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="a0500-210">W usługach AD FS można dodawać reguł przekształcania wystawiania, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="a0500-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="a0500-211">Wystawiać issuerID dla komputera, gdy wiele zweryfikować nazwy domeny w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0500-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="a0500-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**— To oświadczenie musi zawierać jednolity identyfikator zasobów (URI) dowolnej nazwy domeny zweryfikowane, łączących się z usługą federacyjną lokalnego (AD FS lub strona 3) wystawiania tokenu.</span><span class="sxs-lookup"><span data-stu-id="a0500-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="a0500-213">W usługach AD FS można dodać reguły przekształcania wystawiania przypominających widocznych poniżej w tej kolejności, po nich powyżej.</span><span class="sxs-lookup"><span data-stu-id="a0500-213">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="a0500-214">Należy pamiętać, że konieczne jest tym co najmniej jedna reguła jawnie wystawiania reguły dla użytkowników.</span><span class="sxs-lookup"><span data-stu-id="a0500-214">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="a0500-215">W poniższych reguł dodawany jest pierwsza reguła identyfikacji użytkownika, a uwierzytelnianie komputera.</span><span class="sxs-lookup"><span data-stu-id="a0500-215">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="a0500-216">W powyższym oświadczeń</span><span class="sxs-lookup"><span data-stu-id="a0500-216">In the claim above,</span></span>

- <span data-ttu-id="a0500-217">`$<domain>`jest to adres URL usługi AD FS</span><span class="sxs-lookup"><span data-stu-id="a0500-217">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="a0500-218">`<verified-domain-name>`jest to symbol zastępczy, który należy zastąpić nazwy domeny zweryfikowane w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="a0500-218">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="a0500-219">Aby uzyskać więcej informacji o nazwach zweryfikowanej domeny, zobacz [Dodawanie niestandardowej nazwy domeny do usługi Azure Active Directory](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="a0500-219">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="a0500-220">Aby uzyskać listę domeny zweryfikowane firmy, można użyć [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a0500-220">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="a0500-222">Wystawiać nazwę ImmutableID dla komputera, gdy istnieje jeden dla użytkowników (np. alternatywny logowania identyfikatora)</span><span class="sxs-lookup"><span data-stu-id="a0500-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="a0500-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**— To oświadczenie musi zawierać prawidłową wartość dla komputerów.</span><span class="sxs-lookup"><span data-stu-id="a0500-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="a0500-224">W usługach AD FS można utworzyć reguły przekształcania wystawiania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="a0500-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="a0500-225">Skrypt pomocnika do tworzenia reguł przekształcania wystawiania usług AD FS</span><span class="sxs-lookup"><span data-stu-id="a0500-225">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="a0500-226">Poniższy skrypt pomaga z tworzeniem wystawiania przekształcenie reguł opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="a0500-226">The following script helps you with the creation of the issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="a0500-227">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a0500-227">Remarks</span></span> 

- <span data-ttu-id="a0500-228">Ten skrypt dołącza reguły do istniejących reguł.</span><span class="sxs-lookup"><span data-stu-id="a0500-228">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="a0500-229">Nie uruchamiaj skryptu dwa razy, ponieważ zestaw reguł zostanie dodany dwa razy.</span><span class="sxs-lookup"><span data-stu-id="a0500-229">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="a0500-230">Upewnij się, że odpowiednie nie istnieją żadne reguły dla tych oświadczeń (zgodnie z warunkami odpowiedniego) przed ponownym uruchomieniem skryptu.</span><span class="sxs-lookup"><span data-stu-id="a0500-230">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="a0500-231">Jeśli masz wiele nazw zweryfikowanej domeny (jak pokazano w portalu usługi Azure AD lub przy użyciu polecenia cmdlet Get-MsolDomains), ustaw wartość **$multipleVerifiedDomainNames** w skrypcie **$true**.</span><span class="sxs-lookup"><span data-stu-id="a0500-231">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="a0500-232">Upewnij się również usunięcie istniejących oświadczenie issuerid został utworzony przez program Azure AD Connect lub za pomocą innych środków.</span><span class="sxs-lookup"><span data-stu-id="a0500-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="a0500-233">Oto przykład dla tej reguły:</span><span class="sxs-lookup"><span data-stu-id="a0500-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="a0500-234">Jeśli już wystawiły **nazwę ImmutableID** oświadczenia dla kont użytkowników, ustaw wartość **$immutableIDAlreadyIssuedforUsers** w skrypcie **$true**.</span><span class="sxs-lookup"><span data-stu-id="a0500-234">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="a0500-235">Krok 3: Włącz urządzeń z systemem Windows niższego poziomu</span><span class="sxs-lookup"><span data-stu-id="a0500-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="a0500-236">Jeśli niektóre urządzenia przyłączone do domeny z systemem Windows niższego poziomu urządzeń, należy:</span><span class="sxs-lookup"><span data-stu-id="a0500-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="a0500-237">Ustawienie zasad w usłudze Azure AD, aby umożliwić użytkownikom rejestrowanie urządzeń.</span><span class="sxs-lookup"><span data-stu-id="a0500-237">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="a0500-238">Skonfiguruj lokalną usługę federacyjną wystawiać oświadczenia do obsługi **zintegrowane uwierzytelnianie systemu Windows (IWA)** w czasie rejestracji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a0500-238">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="a0500-239">Dodawanie punktu końcowego uwierzytelniania urządzenia usługi Azure AD do lokalnej strefy intranetowej do monity certyfikatu podczas uwierzytelniania urządzenia.</span><span class="sxs-lookup"><span data-stu-id="a0500-239">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="a0500-240">Ustawienie zasad w usłudze Azure AD, aby umożliwić użytkownikom rejestrowanie urządzeń</span><span class="sxs-lookup"><span data-stu-id="a0500-240">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="a0500-241">Aby zarejestrować urządzenia z systemem Windows niższego poziomu, musisz upewnij się, że ustawiony jest ustawienie, aby umożliwić użytkownikom rejestrowanie urządzeń w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0500-241">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="a0500-242">To ustawienie, w obszarze można znaleźć w portalu Azure:</span><span class="sxs-lookup"><span data-stu-id="a0500-242">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="a0500-243">Następująca zasada musi mieć ustawioną **wszystkie**: **użytkownicy mogą zarejestrować swoje urządzenia w usłudze Azure AD**</span><span class="sxs-lookup"><span data-stu-id="a0500-243">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![Rejestrowanie urządzeń](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="a0500-245">Konfigurowanie usługi federacyjnej lokalnej</span><span class="sxs-lookup"><span data-stu-id="a0500-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="a0500-246">Lokalne usługi federacyjnej musi obsługiwać wystawianie **authenticationmehod** i **wiaormultiauthn** oświadczeń, gdy odbiera żądanie uwierzytelnienia do jednostki uzależnionej usługi Azure AD zawierający resouce_params parametr o wartości zakodowanej, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="a0500-246">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="a0500-247">Jeśli takie żądanie pochodzi, lokalną usługę federacyjną musi uwierzytelnić użytkownika przy użyciu zintegrowanego uwierzytelniania systemu Windows i na sukces, należy wydać następujące dwa oświadczenia:</span><span class="sxs-lookup"><span data-stu-id="a0500-247">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="a0500-248">W usługach AD FS należy dodać reguły przekształcania wystawiania, który przechodzi przez metodę uwierzytelniania.</span><span class="sxs-lookup"><span data-stu-id="a0500-248">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="a0500-249">**Aby dodać tę regułę:**</span><span class="sxs-lookup"><span data-stu-id="a0500-249">**To add this rule:**</span></span>

1. <span data-ttu-id="a0500-250">W konsoli zarządzania usług AD FS przejdź do `AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="a0500-250">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="a0500-251">Kliknij prawym przyciskiem myszy obiekt zaufania jednostki uzależnionej strony platformy tożsamości pakietu Microsoft Office 365, a następnie wybierz **Edycja reguł oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="a0500-251">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="a0500-252">Na **reguły przekształcania wystawiania** wybierz opcję **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="a0500-252">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="a0500-253">W **reguły oświadczeń** szablon z listy wybierz **wysyłanie oświadczeń przy użyciu reguły niestandardowej**.</span><span class="sxs-lookup"><span data-stu-id="a0500-253">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="a0500-254">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="a0500-254">Select **Next**.</span></span>
6. <span data-ttu-id="a0500-255">W **nazwy reguły oświadczeń** wpisz **reguły oświadczeń metody uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="a0500-255">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="a0500-256">W **reguły oświadczeń** wpisz następującą regułę:</span><span class="sxs-lookup"><span data-stu-id="a0500-256">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="a0500-257">Na serwerze federacyjnym, wpisz poniższe polecenie programu PowerShell po zastąpieniu  **\<RPObjectName\>**  nazwą jednostki uzależnionej strony obiektu dla obiekt zaufania jednostki uzależnionej strony usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0500-257">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="a0500-258">Ten obiekt zwykle nosi nazwę **Microsoft Office 365 tożsamość platformy**.</span><span class="sxs-lookup"><span data-stu-id="a0500-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="a0500-259">Dodawanie punktu końcowego uwierzytelniania urządzenia usługi Azure AD do strefy Lokalny Intranet</span><span class="sxs-lookup"><span data-stu-id="a0500-259">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="a0500-260">Aby uniknąć certyfikatu monity podczas uwierzytelniania użytkowników w rejestrze urządzeń do usługi Azure AD, możesz wypchnąć zasad na urządzeniach przyłączonych do domeny, aby dodać następujący adres URL do strefy Lokalny Intranet w programie Internet Explorer:</span><span class="sxs-lookup"><span data-stu-id="a0500-260">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="a0500-261">Krok 4: Wdrażanie formantu i wdrożenia</span><span class="sxs-lookup"><span data-stu-id="a0500-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="a0500-262">Po wykonaniu kroków, które urządzenia przyłączone do domeny są gotowe do automatycznego rejestrowania w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0500-262">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span></span> <span data-ttu-id="a0500-263">Wszystkich przyłączonych do domeny urządzeń z systemem Windows 10 Anniversary Update i Windows Server 2016 automatycznie zarejestrować w usłudze Azure AD na urządzeniu ponownego uruchomienia lub logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a0500-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="a0500-264">Zarejestrować nowe urządzenia z usługą Azure AD po ponownym uruchomieniu urządzenia po zakończeniu operacji przyłączania do domeny.</span><span class="sxs-lookup"><span data-stu-id="a0500-264">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

<span data-ttu-id="a0500-265">Urządzenia, które zostały wcześniej dołączone do usługi Azure AD (na przykład w usłudze Intune) przechodzenia do "*przyłączonych do domeny, zarejestrowane w usłudze AAD*"; jednak zajmuje trochę czasu, zanim ten proces, aby ukończyć dla wszystkich urządzeń z powodu przepływu działanie domeny i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a0500-265">Devices that were previously workplace-joined to Azure AD (for example for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="a0500-266">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a0500-266">Remarks</span></span>

- <span data-ttu-id="a0500-267">Obiekt zasad grupy umożliwia kontrolować dystrybucję automatycznej rejestracji systemu Windows 10 i komputerów przyłączonych do domeny systemu Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a0500-267">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="a0500-268">Aktualizacja systemu Windows 10 listopada 2015 automatycznie rejestruje z usługą Azure AD **tylko** Jeśli obiekt zasad grupy wdrożenia jest ustawiony.</span><span class="sxs-lookup"><span data-stu-id="a0500-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="a0500-269">Aby wdrażanie automatycznej rejestracji komputerów z systemem Windows niższego poziomu, można wdrożyć [pakiet Instalatora Windows](#windows-installer-packages-for-non-windows-10-computers) na komputerach, które można wybrać.</span><span class="sxs-lookup"><span data-stu-id="a0500-269">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="a0500-270">Jeśli obiekt zasad grupy jest wypchnąć urządzeniom Windows 8.1 przyłączonych do domeny, będą podejmowane rejestracji; jednak zaleca się, że używasz [pakiet Instalatora Windows](#windows-installer-packages-for-non-windows-10-computers) do rejestrowania wszystkich urządzeń z systemem Windows niższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="a0500-270">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="a0500-271">Utwórz obiekt zasad grupy</span><span class="sxs-lookup"><span data-stu-id="a0500-271">Create a Group Policy object</span></span> 

<span data-ttu-id="a0500-272">Aby kontrolować dystrybucję automatycznej rejestracji bieżącego komputerów z systemem Windows, należy wdrożyć **rejestrować komputery przyłączone do domeny jako urządzenia** obiektu zasad grupy dla urządzeń, które chcesz zarejestrować.</span><span class="sxs-lookup"><span data-stu-id="a0500-272">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="a0500-273">Na przykład można wdrożyć zasady, do jednostki organizacyjnej lub grupie zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="a0500-273">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="a0500-274">**Aby ustawić zasady:**</span><span class="sxs-lookup"><span data-stu-id="a0500-274">**To set the policy:**</span></span>

1. <span data-ttu-id="a0500-275">Otwórz **Menedżera serwera**, a następnie przejdź do `Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="a0500-275">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="a0500-276">Przejdź do węzła domeny, która odnosi się do domeny, w której chcesz aktywować rejestracji automatycznej bieżącego komputerów z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="a0500-276">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="a0500-277">Kliknij prawym przyciskiem myszy **obiektów zasad grupy**, a następnie wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="a0500-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="a0500-278">Wpisz nazwę obiektu zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="a0500-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="a0500-279">Na przykład *automatycznej rejestracji w usłudze Azure AD*.</span><span class="sxs-lookup"><span data-stu-id="a0500-279">For example, *Automatic Registration to Azure AD*.</span></span> <span data-ttu-id="a0500-280">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0500-280">Select **OK**.</span></span>
5. <span data-ttu-id="a0500-281">Kliknij prawym przyciskiem myszy nowy obiekt zasad grupy, a następnie wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="a0500-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="a0500-282">Przejdź do **Konfiguracja komputera** > **zasady** > **Szablony administracyjne** > **systemu Windows Składniki** > **Rejestracja urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="a0500-282">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="a0500-283">Kliknij prawym przyciskiem myszy **rejestrować komputery przyłączone do domeny jako urządzenia**, a następnie wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="a0500-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a0500-284">Ten szablon zasad grupy została zmieniona z wcześniejszych wersji konsoli zarządzania zasadami grupy.</span><span class="sxs-lookup"><span data-stu-id="a0500-284">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="a0500-285">Jeśli używasz starszej wersji konsoli przejdź do `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="a0500-285">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="a0500-286">Wybierz **włączone**, a następnie wybierz **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="a0500-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="a0500-287">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0500-287">Select **OK**.</span></span>
9. <span data-ttu-id="a0500-288">Połącz obiekt zasad grupy z wybraną lokalizację.</span><span class="sxs-lookup"><span data-stu-id="a0500-288">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="a0500-289">Na przykład można je połączyć do określonej jednostki organizacyjnej.</span><span class="sxs-lookup"><span data-stu-id="a0500-289">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="a0500-290">Możesz również można połączyć go do grupy zabezpieczeń określonych komputerów, które automatycznie zarejestrować w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0500-290">You also could link it to a specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="a0500-291">Aby ustawić te zasady dla wszystkich przyłączonych do domeny systemu Windows 10 i Windows Server 2016 komputerów w organizacji, należy połączyć obiekt zasad grupy do domeny.</span><span class="sxs-lookup"><span data-stu-id="a0500-291">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="a0500-292">Pakietów Instalatora Windows na komputerach z systemem innym niż Windows 10</span><span class="sxs-lookup"><span data-stu-id="a0500-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="a0500-293">Aby zarejestrować przyłączonych do domeny komputerów z systemem Windows niższego poziomu w środowisku federacyjnym, można pobrać i zainstalować te pakiet Instalatora Windows (msi) z Centrum pobierania [Microsoft dołączania dla komputerów z systemem innym niż Windows 10](https://www.microsoft.com/en-us/download/details.aspx?id=53554)strony.</span><span class="sxs-lookup"><span data-stu-id="a0500-293">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="a0500-294">Pakiet można wdrożyć przy użyciu system dystrybucji oprogramowania, takich jak System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="a0500-294">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="a0500-295">Pakiet obsługuje opcje standardowa Instalacja dyskretna z *quiet* parametru.</span><span class="sxs-lookup"><span data-stu-id="a0500-295">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="a0500-296">System Center Configuration Manager Current Branch oferuje dodatkowe korzyści z wcześniejszych wersji, takich jak możliwość śledzenia rejestracji ukończone.</span><span class="sxs-lookup"><span data-stu-id="a0500-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="a0500-297">Aby uzyskać więcej informacji, zobacz [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="a0500-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="a0500-298">Instalator tworzy zaplanowane zadanie w systemie, który jest uruchamiany w kontekście użytkownika.</span><span class="sxs-lookup"><span data-stu-id="a0500-298">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="a0500-299">Zadanie jest wyzwalane, gdy użytkownik loguje się do systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a0500-299">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="a0500-300">Zadanie dyskretnie zarejestrowanie urządzenia w usłudze Azure AD przy użyciu poświadczeń użytkownika po uwierzytelnieniu przy użyciu zintegrowanego uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="a0500-300">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="a0500-301">Aby wyświetlić zaplanowane zadanie, na urządzeniu, przejdź do **Microsoft** > **dołączania**, a następnie przejdź do biblioteki harmonogramu zadań.</span><span class="sxs-lookup"><span data-stu-id="a0500-301">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="a0500-302">Krok 5: Sprawdzanie zarejestrowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="a0500-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="a0500-303">Pomyślnie zarejestrowanych urządzeń w swojej organizacji można sprawdzić za pomocą [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) polecenia cmdlet w [modułu programu PowerShell usługi Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="a0500-303">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="a0500-304">Dane wyjściowe tego polecenia cmdlet zawierają urządzeń zarejestrowanych w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a0500-304">The output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="a0500-305">Aby uzyskać wszystkie urządzenia, należy użyć **— wszystkie** parametr, a następnie przeprowadź filtrowanie ich przy użyciu **deviceTrustType** właściwości.</span><span class="sxs-lookup"><span data-stu-id="a0500-305">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="a0500-306">Przyłączony do domeny urządzenia mają wartość **przyłączonych do domeny**.</span><span class="sxs-lookup"><span data-stu-id="a0500-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0500-307">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a0500-307">Next steps</span></span>

* [<span data-ttu-id="a0500-308">Automatycznej rejestracji urządzeń — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="a0500-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="a0500-309">Rozwiązywanie problemów z automatyczną rejestrację domeny komputery przyłączone do usługi Azure AD — Windows 10 i Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="a0500-309">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="a0500-310">Rozwiązywanie problemów z automatyczną rejestrację domeny komputery przyłączone do usługi Azure AD — z systemem innym niż Windows 10</span><span class="sxs-lookup"><span data-stu-id="a0500-310">Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="a0500-311">Dostęp warunkowy do usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a0500-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
