---
title: "aaaHow tooconfigure automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny z usługą Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Konfigurowanie sieci tooregister urządzeń przyłączonych do domeny systemu Windows automatycznie i w trybie dyskretnym usłudze Azure Active Directory."
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
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="bd95e-103">Jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd95e-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="bd95e-104">toouse [dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-azure-portal.md), komputer musi być zarejestrowana w usłudze Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="bd95e-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bd95e-105">Można uzyskać listę zarejestrowanych urządzeń w Twojej organizacji za pomocą hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) polecenia cmdlet w hello [modułu programu PowerShell usługi Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="bd95e-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="bd95e-106">Ten artykuł zawiera kroki hello konfigurowania hello automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny z usługą Azure AD w organizacji.</span><span class="sxs-lookup"><span data-stu-id="bd95e-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="bd95e-107">Aby uzyskać więcej informacji na temat:</span><span class="sxs-lookup"><span data-stu-id="bd95e-107">For more information about:</span></span>

- <span data-ttu-id="bd95e-108">Funkcja dostępu warunkowego, zobacz [dostępu warunkowego opartego na urządzenia usługi Azure Active Directory](active-directory-conditional-access-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="bd95e-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="bd95e-109">Urządzenia Windows 10 w pracy hello i doświadczeń hello rozszerzone po zarejestrowaniu w usłudze Azure AD, zobacz [systemu Windows 10 dla przedsiębiorstw hello: używanie urządzeń do pracy](active-directory-azureadjoin-windows10-devices-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bd95e-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="bd95e-110">Windows 10 Enterprise E3 w dostawcy usług Kryptograficznych, zobacz hello [systemu Windows 10 Enterprise E3 w dostawcy usług Kryptograficznych — omówienie](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span><span class="sxs-lookup"><span data-stu-id="bd95e-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="bd95e-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="bd95e-111">Before you begin</span></span>

<span data-ttu-id="bd95e-112">Przed rozpoczęciem konfigurowania hello automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w danym środowisku, należy zapoznać się z hello obsługiwane scenariusze i hello ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="bd95e-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="bd95e-113">czytelność hello tooimprove opisy hello, w tym temacie używa powitania po termin:</span><span class="sxs-lookup"><span data-stu-id="bd95e-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="bd95e-114">**Urządzenia z systemem Windows bieżącego** -określenie to odnosi się toodomain przyłączone do urządzeń z systemem Windows 10 lub Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bd95e-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="bd95e-115">**Urządzenia z systemem Windows niższego poziomu** -określenie to odnosi się tooall **obsługiwane** przyłączonych do domeny urządzenia z systemem Windows, które nie są uruchomione systemu Windows 10 ani Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="bd95e-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="bd95e-116">Bieżący urządzeń z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="bd95e-116">Windows current devices</span></span>

- <span data-ttu-id="bd95e-117">Dla urządzeń z systemem Windows hello pulpitu systemu operacyjnego, zaleca się użycie systemu Windows 10 Anniversary aktualizacji (w wersji 1607) lub nowszym.</span><span class="sxs-lookup"><span data-stu-id="bd95e-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="bd95e-118">Witaj rejestracji urządzeń z systemem Windows bieżącego **jest** obsługiwane w niefederacyjnych środowiskach, takich jak konfiguracje synchronizacji skrótu hasła.</span><span class="sxs-lookup"><span data-stu-id="bd95e-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="bd95e-119">Urządzenia z systemem Windows niższego poziomu</span><span class="sxs-lookup"><span data-stu-id="bd95e-119">Windows down-level devices</span></span>

- <span data-ttu-id="bd95e-120">obsługiwane są następujące urządzenia z systemem Windows niższego poziomu Hello:</span><span class="sxs-lookup"><span data-stu-id="bd95e-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="bd95e-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="bd95e-121">Windows 8.1</span></span>
    - <span data-ttu-id="bd95e-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="bd95e-122">Windows 7</span></span>
    - <span data-ttu-id="bd95e-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bd95e-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="bd95e-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="bd95e-124">Windows Server 2012</span></span>
    - <span data-ttu-id="bd95e-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="bd95e-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="bd95e-126">Witaj rejestracji urządzeń z systemem Windows niższego poziomu **jest** obsługiwane w środowiskach niefederacyjnych za pośrednictwem bezproblemowe rejestracji jednokrotnej [Azure Active Directory bezproblemowe logowanie jednokrotne](https://aka.ms/hybrid/sso).</span><span class="sxs-lookup"><span data-stu-id="bd95e-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="bd95e-127">Witaj rejestracji urządzeń z systemem Windows niższego poziomu **nie jest** obsługiwane na urządzeniach przy użyciu profilów mobilnych.</span><span class="sxs-lookup"><span data-stu-id="bd95e-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="bd95e-128">Jeśli używasz mobilnego profile i ustawienia, należy użyć systemu Windows 10.</span><span class="sxs-lookup"><span data-stu-id="bd95e-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="bd95e-129">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="bd95e-129">Prerequisites</span></span>

<span data-ttu-id="bd95e-130">Przed rozpoczęciem włączenie hello automatyczną rejestrację urządzeń przyłączonych do domeny w organizacji, należy toomake się, że są uruchomione zaktualizowanej wersji programu Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="bd95e-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="bd95e-131">Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="bd95e-131">Azure AD Connect:</span></span>

- <span data-ttu-id="bd95e-132">Przechowuje hello skojarzenie hello konta komputera w sieci lokalnej Active Directory (AD) i hello obiekt urządzenia w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd95e-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="bd95e-133">Umożliwia urządzeniu innych powiązanych funkcji, takich jak Windows Hello dla firm.</span><span class="sxs-lookup"><span data-stu-id="bd95e-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="bd95e-134">Kroki konfiguracji</span><span class="sxs-lookup"><span data-stu-id="bd95e-134">Configuration steps</span></span>

<span data-ttu-id="bd95e-135">Ten temat zawiera kroki hello wymagane we wszystkich scenariuszach typowej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="bd95e-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="bd95e-136">Użyj powitania po tooget tabeli omówienie hello kroki, które są wymagane dla danego scenariusza:</span><span class="sxs-lookup"><span data-stu-id="bd95e-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="bd95e-137">Kroki</span><span class="sxs-lookup"><span data-stu-id="bd95e-137">Steps</span></span>                                      | <span data-ttu-id="bd95e-138">Synchronizacja skrótów bieżące i hasło systemu Windows</span><span class="sxs-lookup"><span data-stu-id="bd95e-138">Windows current and password hash sync</span></span> | <span data-ttu-id="bd95e-139">Bieżącego systemu Windows i Federacji</span><span class="sxs-lookup"><span data-stu-id="bd95e-139">Windows current and federation</span></span> | <span data-ttu-id="bd95e-140">Niższego poziomu z systemem Windows</span><span class="sxs-lookup"><span data-stu-id="bd95e-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="bd95e-141">Krok 1: Konfigurowanie punktu połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="bd95e-141">Step 1: Configure service connection point</span></span> | ![Zaznacz][1]                            | ![Zaznacz][1]                    | ![Zaznacz][1]        |
| <span data-ttu-id="bd95e-145">Krok 2: Skonfiguruj wystawiania oświadczeń</span><span class="sxs-lookup"><span data-stu-id="bd95e-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![Zaznacz][1]                    | ![Zaznacz][1]        |
| <span data-ttu-id="bd95e-148">Krok 3: Włącz urządzenia z systemem innym niż Windows 10</span><span class="sxs-lookup"><span data-stu-id="bd95e-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![Zaznacz][1]        |
| <span data-ttu-id="bd95e-150">Krok 4: Wdrażanie formantu i wdrożenia</span><span class="sxs-lookup"><span data-stu-id="bd95e-150">Step 4: Control deployment and rollout</span></span>     | ![Zaznacz][1]                            | ![Zaznacz][1]                    | ![Zaznacz][1]        |
| <span data-ttu-id="bd95e-154">Krok 5: Sprawdzanie zarejestrowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="bd95e-154">Step 5: Verify registered devices</span></span>          | ![Zaznacz][1]                            | ![Zaznacz][1]                    | ![Zaznacz][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="bd95e-158">Krok 1: Konfigurowanie punktu połączenia usługi</span><span class="sxs-lookup"><span data-stu-id="bd95e-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="bd95e-159">obiekt (SCP) punktu połączenia usługi Hello jest używany przez urządzenia podczas hello rejestracji toodiscover informacje o dzierżawy usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd95e-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="bd95e-160">W lokalnej usługi Active Directory (AD) obiekt SCP hello hello automatyczną rejestrację urządzeń przyłączonych do domeny muszą istnieć w hello nazewnictwa kontekstu partycji konfiguracji komputera hello lasu.</span><span class="sxs-lookup"><span data-stu-id="bd95e-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="bd95e-161">Istnieje tylko jeden kontekście nazewnictwa konfiguracji w każdym lesie.</span><span class="sxs-lookup"><span data-stu-id="bd95e-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="bd95e-162">W konfiguracji obejmującego wiele lasów usługi Active Directory punkt połączenia z usługą hello musi istnieć we wszystkich lasach środowiska zawierającego komputery przyłączone do domeny.</span><span class="sxs-lookup"><span data-stu-id="bd95e-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="bd95e-163">Można użyć hello [ **Get-ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) polecenia cmdlet tooretrieve hello kontekście nazewnictwa konfiguracji w lesie.</span><span class="sxs-lookup"><span data-stu-id="bd95e-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="bd95e-164">Dla lasu z nazwą domeny usługi Active Directory hello *fabrikam.com*, jest w kontekście nazewnictwa konfiguracji hello:</span><span class="sxs-lookup"><span data-stu-id="bd95e-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="bd95e-165">W lesie obiekt hello punkt połączenia usługi dla rejestracji automatycznej hello urządzeń przyłączonych do domeny znajduje się na:</span><span class="sxs-lookup"><span data-stu-id="bd95e-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="bd95e-166">W zależności od tego, jak zostały wdrożone usługi Azure AD Connect obiektu SCP hello może zostały już skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="bd95e-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="bd95e-167">Można sprawdzić istnienia obiektu hello hello i pobrać wartości odnajdywania hello przy użyciu hello następującego skryptu programu Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="bd95e-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="bd95e-168">Witaj **$scp. Słowa kluczowe** dane wyjściowe zawierają informacje o dzierżawy hello Azure AD, na przykład:</span><span class="sxs-lookup"><span data-stu-id="bd95e-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="bd95e-169">Jeśli punkt połączenia usługi hello nie istnieje, można go utworzyć, uruchamiając hello `Initialize-ADSyncDomainJoinedComputerSync` polecenia cmdlet na serwerze programu Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="bd95e-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="bd95e-170">Poświadczenia administratora przedsiębiorstwa jest wymagana toorun tego polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd95e-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="bd95e-171">polecenia cmdlet Hello:</span><span class="sxs-lookup"><span data-stu-id="bd95e-171">hello cmdlet:</span></span>

- <span data-ttu-id="bd95e-172">Tworzy punkt połączenia z usługą hello w lesie usługi Active Directory hello Azure AD Connect jest połączona z.</span><span class="sxs-lookup"><span data-stu-id="bd95e-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="bd95e-173">Wymaga toospecify hello `AdConnectorAccount` parametru.</span><span class="sxs-lookup"><span data-stu-id="bd95e-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="bd95e-174">To jest konto hello, która jest skonfigurowana jako usługi Active Directory connector konta w usłudze Azure AD connect.</span><span class="sxs-lookup"><span data-stu-id="bd95e-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="bd95e-175">Witaj poniższy skrypt pokazuje przykład za pomocą polecenia cmdlet hello.</span><span class="sxs-lookup"><span data-stu-id="bd95e-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="bd95e-176">W tym skrypcie `$aadAdminCred = Get-Credential` wymaga tootype nazwę użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd95e-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="bd95e-177">Potrzebna jest nazwa użytkownika hello tooprovide format nazwy podmiotu zabezpieczeń (UPN) użytkownika hello (`user@example.com`).</span><span class="sxs-lookup"><span data-stu-id="bd95e-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="bd95e-178">Witaj `Initialize-ADSyncDomainJoinedComputerSync` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bd95e-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="bd95e-179">Używa hello moduł środowiska PowerShell usługi Active Directory, który korzysta z usługi Active Directory w sieci Web uruchomiony na kontrolerze domeny.</span><span class="sxs-lookup"><span data-stu-id="bd95e-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="bd95e-180">Usługi sieci Web w usłudze Active Directory jest obsługiwana na kontrolerach domeny z systemem Windows Server 2008 R2 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bd95e-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="bd95e-181">Jest obsługiwana tylko przez hello **MSOnline PowerShell w wersji modułu 1.1.166.0**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="bd95e-182">toodownload ten moduł służy [łącze](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span><span class="sxs-lookup"><span data-stu-id="bd95e-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="bd95e-183">Dla kontrolerów domeny z systemem Windows Server 2008 lub starszej wersji należy użyć skryptu hello poniżej punktu połączenia usługi hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="bd95e-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="bd95e-184">W konfiguracji wielu lasów należy użyć hello następującego skryptu toocreate hello punkt połączenia z usługą w każdym lesie, w którym istnieje komputerów:</span><span class="sxs-lookup"><span data-stu-id="bd95e-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="bd95e-185">Krok 2: Skonfiguruj wystawiania oświadczeń</span><span class="sxs-lookup"><span data-stu-id="bd95e-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="bd95e-186">W federacyjnych Azure konfiguracji AD urządzeń zależą od usługi Active Directory Federation Services (AD FS) lub 3 strona tooAzure tooauthenticate usługi federacyjnej AD lokalnymi.</span><span class="sxs-lookup"><span data-stu-id="bd95e-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="bd95e-187">Urządzenia uwierzytelniania tooget tooregister tokenu dostępu przed hello usługi Azure Active Directory urządzenia rejestracji (urządzeń DRS Azure).</span><span class="sxs-lookup"><span data-stu-id="bd95e-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="bd95e-188">Systemu Windows, które urządzenia bieżące uwierzytelniania przy użyciu zintegrowanego uwierzytelniania systemu Windows tooan active WS-Trust punktu końcowego (w wersji 1.3 lub 2005) obsługiwanych przez usługę federacyjną lokalne powitania.</span><span class="sxs-lookup"><span data-stu-id="bd95e-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="bd95e-189">Korzystając z usług AD FS, albo **adfs/services/zaufania/13/windowstransport** lub **adfs/services/zaufania/2005/windowstransport** musi być włączona.</span><span class="sxs-lookup"><span data-stu-id="bd95e-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="bd95e-190">Jeśli używasz powitania serwera Proxy sieci Web uwierzytelniania, również upewnić się, czy ten punkt końcowy został opublikowany za pośrednictwem serwera proxy hello.</span><span class="sxs-lookup"><span data-stu-id="bd95e-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="bd95e-191">Widać, jakie punkty końcowe są włączane za pośrednictwem konsoli zarządzania usług AD FS hello w obszarze **usługi > punkty końcowe**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="bd95e-192">Jeśli nie masz jako lokalnej usługi federacyjnej usług AD FS, wykonaj hello instrukcje użytkownika czy obsługę protokołu WS-Trust 1.3 lub punkty końcowe 2005, a te są publikowane za pomocą pliku wymiany metadanych (MEX) hello toomake dostawcy.</span><span class="sxs-lookup"><span data-stu-id="bd95e-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="bd95e-193">Hello następujące oświadczeń musi istnieć w tokenie hello odebrane przez usługi rejestracji urządzeń usługi Azure dla toocomplete rejestracji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bd95e-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="bd95e-194">Usługi rejestracji urządzeń usługi Azure utworzy obiekt urządzenia w usłudze Azure AD, niektóre z tych informacji, która jest następnie używane przez obiekt urządzenia hello nowo utworzony tooassociate Azure AD Connect z hello komputera konta lokalnego.</span><span class="sxs-lookup"><span data-stu-id="bd95e-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="bd95e-195">Jeśli masz więcej niż jedną nazwę zweryfikowanej domeny należy hello tooprovide następujące oświadczenie dla komputerów:</span><span class="sxs-lookup"><span data-stu-id="bd95e-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="bd95e-196">Jeśli są już wystawiania oświadczeń nazwę ImmutableID (np. alternatywnego Identyfikatora logowania) należy tooprovide jedno oświadczenie odpowiednie dla komputerów:</span><span class="sxs-lookup"><span data-stu-id="bd95e-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="bd95e-197">Następujące sekcje hello można znaleźć informacje o:</span><span class="sxs-lookup"><span data-stu-id="bd95e-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="bd95e-198">wartości Hello Każde oświadczenie ma</span><span class="sxs-lookup"><span data-stu-id="bd95e-198">hello values each claim should have</span></span>
- <span data-ttu-id="bd95e-199">Jak definicji będzie wyglądać w usługach AD FS</span><span class="sxs-lookup"><span data-stu-id="bd95e-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="bd95e-200">Definicja Hello pomaga tooverify czy wartości hello są obecne, lub jeśli potrzebujesz toocreate je.</span><span class="sxs-lookup"><span data-stu-id="bd95e-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="bd95e-201">Jeśli nie używasz usług AD FS dla lokalnego serwera federacyjnego, postępuj zgodnie z dostawcą instrukcje toocreate hello odpowiednia konfiguracja tooissue tych oświadczeń.</span><span class="sxs-lookup"><span data-stu-id="bd95e-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="bd95e-202">Problem konta typu oświadczenia</span><span class="sxs-lookup"><span data-stu-id="bd95e-202">Issue account type claim</span></span>

<span data-ttu-id="bd95e-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**— To oświadczenie musi zawierać wartość **DJ**, które identyfikują urządzenie hello jako komputer przyłączony do domeny.</span><span class="sxs-lookup"><span data-stu-id="bd95e-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="bd95e-204">W usługach AD FS można dodawać reguł przekształcania wystawiania, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="bd95e-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="bd95e-205">Wystawiać objectGUID hello komputera konta lokalnego</span><span class="sxs-lookup"><span data-stu-id="bd95e-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="bd95e-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**— To oświadczenie musi zawierać hello **objectGUID** wartość hello lokalnego konta komputera.</span><span class="sxs-lookup"><span data-stu-id="bd95e-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="bd95e-207">W usługach AD FS można dodawać reguł przekształcania wystawiania, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="bd95e-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="bd95e-208">Wystawiać objectSID hello komputera konta lokalnego</span><span class="sxs-lookup"><span data-stu-id="bd95e-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="bd95e-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**— To oświadczenie musi zawierać hello hello **objectSid** wartość hello lokalnego konta komputera.</span><span class="sxs-lookup"><span data-stu-id="bd95e-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="bd95e-210">W usługach AD FS można dodawać reguł przekształcania wystawiania, która wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="bd95e-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="bd95e-211">Wystawiać issuerID dla komputera, gdy wiele zweryfikować nazwy domeny w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd95e-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="bd95e-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**— To oświadczenie musi zawierać hello URI Uniform Resource Identifier () dowolnego hello zweryfikować nazwy domeny, które uzyskuj hello lokalnej wystawiania tokenu hello Federacji (AD FS lub strona 3).</span><span class="sxs-lookup"><span data-stu-id="bd95e-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="bd95e-213">W usługach AD FS można dodać reguły przekształcania wystawiania, które wyglądają jak hello tych poniżej w tej kolejności po hello tych powyżej.</span><span class="sxs-lookup"><span data-stu-id="bd95e-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="bd95e-214">Należy pamiętać reguły hello problem tooexplicitly jedną regułę dla użytkowników jest konieczne.</span><span class="sxs-lookup"><span data-stu-id="bd95e-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="bd95e-215">W poniższych reguł hello dodawany jest pierwsza reguła identyfikacji użytkownika, a uwierzytelnianie komputera.</span><span class="sxs-lookup"><span data-stu-id="bd95e-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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


<span data-ttu-id="bd95e-216">W powyższym oświadczeń hello</span><span class="sxs-lookup"><span data-stu-id="bd95e-216">In hello claim above,</span></span>

- <span data-ttu-id="bd95e-217">`$<domain>`jest adres URL hello AD FS usługi</span><span class="sxs-lookup"><span data-stu-id="bd95e-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="bd95e-218">`<verified-domain-name>`jest to symbol zastępczy należy tooreplace z jednym z nazwy domeny zweryfikowane w usłudze Azure AD</span><span class="sxs-lookup"><span data-stu-id="bd95e-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="bd95e-219">Aby uzyskać więcej informacji o nazwach zweryfikowanej domeny, zobacz [tooAzure nazwy domeny niestandardowej usługi Active Directory dodać](active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="bd95e-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="bd95e-220">tooget listę domeny zweryfikowane firmy, można użyć hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="bd95e-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="bd95e-222">Wystawiać nazwę ImmutableID dla komputera, gdy istnieje jeden dla użytkowników (np. alternatywny logowania identyfikatora)</span><span class="sxs-lookup"><span data-stu-id="bd95e-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="bd95e-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`**— To oświadczenie musi zawierać prawidłową wartość dla komputerów.</span><span class="sxs-lookup"><span data-stu-id="bd95e-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="bd95e-224">W usługach AD FS można utworzyć reguły przekształcania wystawiania w następujący sposób:</span><span class="sxs-lookup"><span data-stu-id="bd95e-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="bd95e-225">Reguły przekształcania wystawiania pomocnika skryptu toocreate hello AD FS</span><span class="sxs-lookup"><span data-stu-id="bd95e-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="bd95e-226">Hello poniższy skrypt pomaga z hello tworzenie wystawiania hello przekształcenie reguł opisanych powyżej.</span><span class="sxs-lookup"><span data-stu-id="bd95e-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="bd95e-227">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bd95e-227">Remarks</span></span> 

- <span data-ttu-id="bd95e-228">Ten skrypt dołącza hello zasady toohello istniejących zasad.</span><span class="sxs-lookup"><span data-stu-id="bd95e-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="bd95e-229">Nie uruchamiaj skryptu hello dwukrotnie ponieważ hello zestaw reguł zostanie dodany dwa razy.</span><span class="sxs-lookup"><span data-stu-id="bd95e-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="bd95e-230">Upewnij się, że odpowiednie nie istnieją żadne reguły tych oświadczeń (warunkach hello odpowiedniego) przed ponownym uruchomieniem hello skryptu.</span><span class="sxs-lookup"><span data-stu-id="bd95e-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="bd95e-231">Jeśli masz wiele zweryfikowanej domeny nazw (jak pokazano w portalu usługi Azure AD hello lub przy użyciu polecenia cmdlet Get-MsolDomains hello), należy ustawić wartość hello **$multipleVerifiedDomainNames** w hello skryptu zbyt**$true**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="bd95e-232">Upewnij się również usunięcie istniejących oświadczenie issuerid został utworzony przez program Azure AD Connect lub za pomocą innych środków.</span><span class="sxs-lookup"><span data-stu-id="bd95e-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="bd95e-233">Oto przykład dla tej reguły:</span><span class="sxs-lookup"><span data-stu-id="bd95e-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="bd95e-234">Jeśli już wystawiły **nazwę ImmutableID** oświadczenia dla kont użytkowników, należy ustawić wartość hello **$immutableIDAlreadyIssuedforUsers** w hello skryptu zbyt**$true**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="bd95e-235">Krok 3: Włącz urządzeń z systemem Windows niższego poziomu</span><span class="sxs-lookup"><span data-stu-id="bd95e-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="bd95e-236">Jeśli niektóre urządzenia przyłączone do domeny z systemem Windows niższego poziomu urządzeń, należy:</span><span class="sxs-lookup"><span data-stu-id="bd95e-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="bd95e-237">Skonfigurować zasadę usługi Azure AD tooenable urządzenia tooregister użytkowników.</span><span class="sxs-lookup"><span data-stu-id="bd95e-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="bd95e-238">Konfigurowanie sieci lokalnej federacyjnych usługi tooissue oświadczeń toosupport **zintegrowane uwierzytelnianie systemu Windows (IWA)** w czasie rejestracji urządzenia.</span><span class="sxs-lookup"><span data-stu-id="bd95e-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="bd95e-239">Dodaj hello Azure AD urządzenia uwierzytelniania punktu końcowego toohello lokalnego intranetu stref, które monituje tooavoid certyfikatu podczas uwierzytelniania urządzenia hello.</span><span class="sxs-lookup"><span data-stu-id="bd95e-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="bd95e-240">Ustawienie zasad w usłudze Azure AD tooenable urządzenia tooregister użytkowników</span><span class="sxs-lookup"><span data-stu-id="bd95e-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="bd95e-241">tooregister urządzeń niższego poziomu z systemem Windows, należy upewnić się, że hello ustawienie użytkowników tooallow tooregister urządzeń w usłudze Azure AD jest ustawiony toomake.</span><span class="sxs-lookup"><span data-stu-id="bd95e-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="bd95e-242">W portalu Azure hello możesz znaleźć tego ustawienia:</span><span class="sxs-lookup"><span data-stu-id="bd95e-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="bd95e-243">Witaj następujące zasady muszą mieć wartość zbyt**wszystkie**: **użytkownicy mogą zarejestrować swoje urządzenia w usłudze Azure AD**</span><span class="sxs-lookup"><span data-stu-id="bd95e-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![Rejestrowanie urządzeń](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="bd95e-245">Konfigurowanie usługi federacyjnej lokalnej</span><span class="sxs-lookup"><span data-stu-id="bd95e-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="bd95e-246">Lokalne usługi federacyjnej musi obsługiwać wystawiającego hello **authenticationmehod** i **wiaormultiauthn** toohello usługi Azure AD jednostki uzależnionej zawierający żądania oświadczeń podczas odbierania uwierzytelniania resouce_params parametr o wartości zakodowanej, jak pokazano poniżej:</span><span class="sxs-lookup"><span data-stu-id="bd95e-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="bd95e-247">Jeśli takie żądanie pochodzi, usługa federacyjna lokalne powitania musi uwierzytelnić użytkownika hello przy użyciu zintegrowanego uwierzytelniania systemu Windows i na sukces, należy wygenerować hello następujące dwa oświadczenia:</span><span class="sxs-lookup"><span data-stu-id="bd95e-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="bd95e-248">W usługach AD FS należy dodać tej metody uwierzytelniania hello przekazuje do reguł przekształcania wystawiania.</span><span class="sxs-lookup"><span data-stu-id="bd95e-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="bd95e-249">**tooadd tej reguły:**</span><span class="sxs-lookup"><span data-stu-id="bd95e-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="bd95e-250">W konsoli zarządzania hello AD FS Przejdź zbyt`AD FS > Trust Relationships > Relying Party Trusts`.</span><span class="sxs-lookup"><span data-stu-id="bd95e-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="bd95e-251">Kliknij prawym przyciskiem myszy hello platformą tożsamości programu Microsoft Office 365 obiekt jednostki uzależnionej zaufania, a następnie wybierz **Edycja reguł oświadczeń**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="bd95e-252">Na powitania **reguły przekształcania wystawiania** wybierz opcję **Dodaj regułę**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="bd95e-253">W hello **reguły oświadczeń** szablon z listy wybierz **wysyłanie oświadczeń przy użyciu reguły niestandardowej**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="bd95e-254">Wybierz **dalej**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-254">Select **Next**.</span></span>
6. <span data-ttu-id="bd95e-255">W hello **nazwy reguły oświadczeń** wpisz **reguły oświadczeń metody uwierzytelniania**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="bd95e-256">W hello **reguły oświadczeń** okno, hello typu następujące reguły:</span><span class="sxs-lookup"><span data-stu-id="bd95e-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="bd95e-257">Na serwerze federacyjnym, wpisz polecenie programu PowerShell hello poniżej po zastąpieniu  **\<RPObjectName\>**  z nazwą hello do obiektu jednostki uzależnionej strony dla obiekt zaufania jednostki uzależnionej strony usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd95e-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="bd95e-258">Ten obiekt zwykle nosi nazwę **Microsoft Office 365 tożsamość platformy**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="bd95e-259">Dodaj hello Azure AD urządzenia uwierzytelniania punktu końcowego toohello lokalny Intranet strefy</span><span class="sxs-lookup"><span data-stu-id="bd95e-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="bd95e-260">certyfikat tooavoid monity podczas tooAzure AD, możesz wypchnąć tooyour zasady urządzeń przyłączonych do domeny hello tooadd następującego adresu URL toohello lokalny intranet w programie Internet Explorer uwierzytelniania użytkowników w rejestrze urządzeń:</span><span class="sxs-lookup"><span data-stu-id="bd95e-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="bd95e-261">Krok 4: Wdrażanie formantu i wdrożenia</span><span class="sxs-lookup"><span data-stu-id="bd95e-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="bd95e-262">Po zakończeniu kroków hello wymagane urządzeń przyłączonych do domeny są gotowe tooautomatically rejestru z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd95e-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="bd95e-263">Wszystkich przyłączonych do domeny urządzeń z systemem Windows 10 Anniversary Update i Windows Server 2016 automatycznie zarejestrować w usłudze Azure AD na urządzeniu ponownego uruchomienia lub logowania użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd95e-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="bd95e-264">Zarejestrować nowe urządzenia z usługą Azure AD, gdy hello urządzenie zostanie uruchomione ponownie, po zakończeniu operacji przyłączania do domeny hello.</span><span class="sxs-lookup"><span data-stu-id="bd95e-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="bd95e-265">Urządzenia, które zostały wcześniej dołączone tooAzure AD (na przykład w usłudze Intune) przejścia zbyt"*przyłączonych do domeny, zarejestrowane w usłudze AAD*"; jednak zajmuje trochę czasu, zanim ten proces toocomplete dla wszystkich urządzeń powodu normalny toohello Przepływ działania domeny i użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd95e-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="bd95e-266">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bd95e-266">Remarks</span></span>

- <span data-ttu-id="bd95e-267">Można użyć zasad grupy obiektu toocontrol hello wdrażanie automatycznej rejestracji systemu Windows 10 i Windows Server 2016 komputerów przyłączonych do domeny.</span><span class="sxs-lookup"><span data-stu-id="bd95e-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="bd95e-268">Aktualizacja systemu Windows 10 listopada 2015 automatycznie rejestruje z usługą Azure AD **tylko** Jeśli obiekt zasad grupy hello wdrożenia jest ustawiona.</span><span class="sxs-lookup"><span data-stu-id="bd95e-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="bd95e-269">toorollout hello automatyczną rejestrację komputerów z systemem Windows niższego poziomu, można wdrożyć [pakiet Instalatora Windows](#windows-installer-packages-for-non-windows-10-computers) toocomputers wybrany.</span><span class="sxs-lookup"><span data-stu-id="bd95e-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="bd95e-270">Jeśli wypychanych urządzeń przyłączonych do domeny tooWindows 8.1 obiektu zasad grupy hello rejestracji zostanie podjęta próba; jednak zaleca się, że używasz hello [pakiet Instalatora Windows](#windows-installer-packages-for-non-windows-10-computers) tooregister wszystkich urządzeń z systemem Windows niższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="bd95e-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="bd95e-271">Utwórz obiekt zasad grupy</span><span class="sxs-lookup"><span data-stu-id="bd95e-271">Create a Group Policy object</span></span> 

<span data-ttu-id="bd95e-272">Wdrażanie hello toocontrol automatycznej rejestracji bieżącego komputerów z systemem Windows, należy wdrożyć hello **rejestrować komputery przyłączone do domeny jako urządzenia** urządzeń toohello obiektu zasad grupy ma tooregister.</span><span class="sxs-lookup"><span data-stu-id="bd95e-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="bd95e-273">Na przykład można wdrożyć jednostki organizacyjnej tooan zasad hello lub tooa grupy zabezpieczeń.</span><span class="sxs-lookup"><span data-stu-id="bd95e-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="bd95e-274">**tooset hello zasad:**</span><span class="sxs-lookup"><span data-stu-id="bd95e-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="bd95e-275">Otwórz **Menedżera serwera**, a następnie przejdź zbyt`Tools > Group Policy Management`.</span><span class="sxs-lookup"><span data-stu-id="bd95e-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="bd95e-276">Przejdź toohello domeny węzła, który odpowiada toohello domenie rejestracji automatycznej tooactivate bieżącego komputerów z systemem Windows.</span><span class="sxs-lookup"><span data-stu-id="bd95e-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="bd95e-277">Kliknij prawym przyciskiem myszy **obiektów zasad grupy**, a następnie wybierz **nowy**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="bd95e-278">Wpisz nazwę obiektu zasad grupy.</span><span class="sxs-lookup"><span data-stu-id="bd95e-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="bd95e-279">Na przykład *tooAzure automatycznej rejestracji AD*.</span><span class="sxs-lookup"><span data-stu-id="bd95e-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="bd95e-280">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-280">Select **OK**.</span></span>
5. <span data-ttu-id="bd95e-281">Kliknij prawym przyciskiem myszy nowy obiekt zasad grupy, a następnie wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="bd95e-282">Przejdź za**Konfiguracja komputera** > **zasady** > **Szablony administracyjne** > **systemu Windows Składniki** > **Rejestracja urządzenia**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="bd95e-283">Kliknij prawym przyciskiem myszy **rejestrować komputery przyłączone do domeny jako urządzenia**, a następnie wybierz **Edytuj**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bd95e-284">Ten szablon zasad grupy została zmieniona z wcześniejszych wersji hello konsoli zarządzania zasadami grupy.</span><span class="sxs-lookup"><span data-stu-id="bd95e-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="bd95e-285">Jeśli używasz starszej wersji konsoli hello Przejdź zbyt`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span><span class="sxs-lookup"><span data-stu-id="bd95e-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="bd95e-286">Wybierz **włączone**, a następnie wybierz **Zastosuj**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="bd95e-287">Kliknij przycisk **OK**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-287">Select **OK**.</span></span>
9. <span data-ttu-id="bd95e-288">Łącze hello lokalizacji tooa obiektu zasad grupy wybranych przez użytkownika.</span><span class="sxs-lookup"><span data-stu-id="bd95e-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="bd95e-289">Na przykład można je połączyć tooa określonej jednostce organizacyjnej.</span><span class="sxs-lookup"><span data-stu-id="bd95e-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="bd95e-290">Możesz również można połączyć go tooa określonej grupy zabezpieczeń komputerów, które automatycznie zarejestrować w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd95e-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="bd95e-291">tooset te zasady dla wszystkich przyłączonych do domeny systemu Windows 10 i Windows Server 2016 komputerów w organizacji link hello zasad grupy obiektu toohello domeny.</span><span class="sxs-lookup"><span data-stu-id="bd95e-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="bd95e-292">Pakietów Instalatora Windows na komputerach z systemem innym niż Windows 10</span><span class="sxs-lookup"><span data-stu-id="bd95e-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="bd95e-293">tooregister przyłączonych do domeny z systemem Windows niższego poziomu komputerów w środowisku federacyjnym można pobrać i zainstalować te pakiet Instalatora Windows (msi) z Centrum pobierania w hello [firmy Microsoft dla komputerów z systemem innym niż Windows 10Dołączdomiejscapracy](https://www.microsoft.com/en-us/download/details.aspx?id=53554) strony.</span><span class="sxs-lookup"><span data-stu-id="bd95e-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="bd95e-294">Można wdrożyć pakiet hello przy użyciu system dystrybucji oprogramowania, takich jak System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="bd95e-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="bd95e-295">Witaj pakietu obsługuje hello standardowej instalacji dyskretnej opcje z hello *quiet* parametru.</span><span class="sxs-lookup"><span data-stu-id="bd95e-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="bd95e-296">System Center Configuration Manager Current Branch oferuje dodatkowe korzyści z wcześniejszych wersji, takich jak hello możliwości tootrack ukończyć rejestracji.</span><span class="sxs-lookup"><span data-stu-id="bd95e-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="bd95e-297">Aby uzyskać więcej informacji, zobacz [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="bd95e-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="bd95e-298">Instalator Hello utworzenie zaplanowanego zadania, w systemie hello, który jest uruchamiany w kontekście użytkownika hello.</span><span class="sxs-lookup"><span data-stu-id="bd95e-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="bd95e-299">zadanie Hello jest wyzwalane, gdy hello użytkownik loguje się tooWindows.</span><span class="sxs-lookup"><span data-stu-id="bd95e-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="bd95e-300">zadanie Hello dyskretnie rejestruje hello urządzenia z usługą Azure AD przy użyciu poświadczeń użytkownika powitania po uwierzytelnieniu przy użyciu zintegrowanego uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="bd95e-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="bd95e-301">toosee hello zaplanowanego zadania, w urządzeniu hello przejść za**Microsoft** > **dołączania**, a następnie przejdź toohello Biblioteka Harmonogramu zadań.</span><span class="sxs-lookup"><span data-stu-id="bd95e-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="bd95e-302">Krok 5: Sprawdzanie zarejestrowanych urządzeń</span><span class="sxs-lookup"><span data-stu-id="bd95e-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="bd95e-303">Pomyślnie zarejestrowanych urządzeń w Twojej organizacji można sprawdzić za pomocą hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) polecenia cmdlet w hello [modułu programu PowerShell usługi Azure Active Directory](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span><span class="sxs-lookup"><span data-stu-id="bd95e-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="bd95e-304">dane wyjściowe tego polecenia cmdlet Hello zawiera urządzenia zarejestrowane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bd95e-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="bd95e-305">tooget wszystkie urządzenia, użyj hello **— wszystkie** parametr, a następnie filtr ich przy użyciu hello **deviceTrustType** właściwości.</span><span class="sxs-lookup"><span data-stu-id="bd95e-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="bd95e-306">Przyłączony do domeny urządzenia mają wartość **przyłączonych do domeny**.</span><span class="sxs-lookup"><span data-stu-id="bd95e-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd95e-307">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bd95e-307">Next steps</span></span>

* [<span data-ttu-id="bd95e-308">Automatycznej rejestracji urządzeń — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="bd95e-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="bd95e-309">Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — Windows 10 i Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bd95e-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="bd95e-310">Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — z systemem innym niż Windows 10</span><span class="sxs-lookup"><span data-stu-id="bd95e-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="bd95e-311">Dostęp warunkowy do usługi Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bd95e-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
