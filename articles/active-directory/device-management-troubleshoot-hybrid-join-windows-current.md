---
title: "aaaTroubleshooting hybrydowe usługi Azure Active Directory przyłączone do urządzeń z systemem Windows 10 i Windows Server 2016 | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z hybrydowe usługi Azure Active Directory przyłączone do urządzeń z systemem Windows 10 i Windows Server 2016."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="03919-103">Rozwiązywanie problemów z hybrydowe usługi Azure Active Directory przyłączone do urządzeń z systemem Windows 10 i Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="03919-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="03919-104">Ten temat jest toohello dotyczy następujących klientów:</span><span class="sxs-lookup"><span data-stu-id="03919-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="03919-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="03919-105">Windows 10</span></span>
-   <span data-ttu-id="03919-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="03919-106">Windows Server 2016</span></span>

<span data-ttu-id="03919-107">Dla innych klientów z systemem Windows, temacie [niższego poziomu urządzeniach przyłączonych do rozwiązywania problemów hybrydowe usługi Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="03919-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="03919-108">W tym temacie założono, że [urządzeniach przyłączonych do skonfigurowanego hybrydowe usługi Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="03919-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="03919-109">Dostępu warunkowego opartego na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="03919-109">Device-based conditional access</span></span>

- [<span data-ttu-id="03919-110">Enterprise roaming ustawień</span><span class="sxs-lookup"><span data-stu-id="03919-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="03919-111">Windows Hello dla firm</span><span class="sxs-lookup"><span data-stu-id="03919-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="03919-112">Ten dokument zawiera wskazówki dotyczące rozwiązywania problemów w sposób tooresolve potencjalne problemy.</span><span class="sxs-lookup"><span data-stu-id="03919-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="03919-113">Dla systemu Windows 10 i Windows Server 2016 hybrydowe usługi Azure Active Directory join obsługuje hello systemu Windows 10 listopada 2015 aktualizacji i powyżej.</span><span class="sxs-lookup"><span data-stu-id="03919-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="03919-114">Firma Microsoft zaleca użycie hello rocznicy aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="03919-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="03919-115">Krok 1: Pobrać hello sprzężenia stanu</span><span class="sxs-lookup"><span data-stu-id="03919-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="03919-116">**Stan sprzężenia hello tooretrieve:**</span><span class="sxs-lookup"><span data-stu-id="03919-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="03919-117">Witaj Otwórz wiersz polecenia jako administrator</span><span class="sxs-lookup"><span data-stu-id="03919-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="03919-118">Typ **dsregcmd/status**</span><span class="sxs-lookup"><span data-stu-id="03919-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="03919-119">+----------------------------------------------------------------------+
   | Stan urządzenia |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="03919-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="03919-120">EnterpriseJoined: Nie DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 odcisk palca: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected dostawca usług kryptograficznych platformy firmy Microsoft: tak KeySignTest:: należy uruchomić z podwyższonym poziomem uprawnień tootest.</span><span class="sxs-lookup"><span data-stu-id="03919-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="03919-121">IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/ msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https:// Portal.Manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https:// enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-usługi rejestracji urządzeń: enterpriseregistration.Windows.NET DomainJoined: nazwadomeny tak: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="03919-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="03919-122">+----------------------------------------------------------------------+
   | Stan użytkownika |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="03919-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="03919-123">WamDefaultAuthority: organizacje WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} AzureAdPrt (AzureAd): tak</span><span class="sxs-lookup"><span data-stu-id="03919-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="03919-124">Krok 2: Ocena hello sprzężenia stanu</span><span class="sxs-lookup"><span data-stu-id="03919-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="03919-125">Przejrzyj hello kolejnych pól i upewnij się, że hello oczekiwanych wartości:</span><span class="sxs-lookup"><span data-stu-id="03919-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="03919-126">AzureAdJoined: tak</span><span class="sxs-lookup"><span data-stu-id="03919-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="03919-127">To pole wskazuje, czy urządzenie hello jest połączony z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03919-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="03919-128">Jeśli wartość hello jest **nr**, hello tooAzure sprzężenia AD nie została jeszcze ukończona.</span><span class="sxs-lookup"><span data-stu-id="03919-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="03919-129">**Możliwe przyczyny:**</span><span class="sxs-lookup"><span data-stu-id="03919-129">**Possible causes:**</span></span>

- <span data-ttu-id="03919-130">Nie można przeprowadzić uwierzytelniania komputera hello w celu utworzenia sprzężenia.</span><span class="sxs-lookup"><span data-stu-id="03919-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="03919-131">W organizacji hello, które nie może zostać odnalezione przez komputer hello jest serwer proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="03919-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="03919-132">Hello komputera nie można osiągnąć tooauthenticate usługi Azure AD lub Azure usługi rejestracji urządzeń do rejestracji</span><span class="sxs-lookup"><span data-stu-id="03919-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="03919-133">Witaj komputer może nie być w sieci wewnętrznej hello organizacji lub sieci VPN z tooan bezpośredniego wiersza z procesów lokalnych kontroler domeny usługi AD.</span><span class="sxs-lookup"><span data-stu-id="03919-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="03919-134">Jeśli komputer hello ma modułu TPM, może być nieprawidłowy stan.</span><span class="sxs-lookup"><span data-stu-id="03919-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="03919-135">Może być błąd konfiguracji w usługach hello zauważyć w dokumencie hello wcześniej trzeba tooverify ponownie.</span><span class="sxs-lookup"><span data-stu-id="03919-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="03919-136">Typowe przykłady są:</span><span class="sxs-lookup"><span data-stu-id="03919-136">Common examples are:</span></span>

    - <span data-ttu-id="03919-137">Serwer federacyjny nie ma punktów końcowych protokołu WS-Trust włączone</span><span class="sxs-lookup"><span data-stu-id="03919-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="03919-138">Serwerze federacyjnym nie zezwala na uwierzytelnianie ruchu przychodzącego z komputerów w sieci przy użyciu zintegrowanego uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="03919-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="03919-139">Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje tooyour zweryfikowaną nazwę domeny w usłudze Azure AD w lesie hello AD, której należy komputer hello</span><span class="sxs-lookup"><span data-stu-id="03919-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="03919-140">DomainJoined: tak</span><span class="sxs-lookup"><span data-stu-id="03919-140">DomainJoined : YES</span></span>  

<span data-ttu-id="03919-141">To pole wskazuje, czy urządzenie hello jest dołączane tooan lokalnej usługi Active Directory lub nie.</span><span class="sxs-lookup"><span data-stu-id="03919-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="03919-142">Jeśli wartość hello jest **nr**, hello urządzenia nie można wykonać sprzężenia hybrydowej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03919-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="03919-143">WorkplaceJoined: nie</span><span class="sxs-lookup"><span data-stu-id="03919-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="03919-144">To pole wskazuje, czy urządzenie hello jest zarejestrowane w usłudze Azure AD jako urządzenia osobiste (oznaczony jako *dołączonych do miejsca pracy*).</span><span class="sxs-lookup"><span data-stu-id="03919-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="03919-145">Ta wartość powinna być **nr** na komputerze przyłączonym do domeny, który jest przyłączony do hybrydowej usługi Azure AD.</span><span class="sxs-lookup"><span data-stu-id="03919-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="03919-146">Jeśli wartość hello jest **tak**, konta firmowego lub szkolnego dodano zakończenia wcześniejszych toohello hello hybrydowej usługi Azure AD join.</span><span class="sxs-lookup"><span data-stu-id="03919-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="03919-147">W takim przypadku konto hello jest ignorowane w przypadku przy użyciu hello rocznicy zaktualizowanej wersji systemu Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="03919-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="03919-148">WamDefaultSet: Tak i AzureADPrt: tak</span><span class="sxs-lookup"><span data-stu-id="03919-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="03919-149">Te pola wskazują, czy użytkownik hello został pomyślnie uwierzytelniony tooAzure AD podczas rejestrowania się w urządzeniu toohello.</span><span class="sxs-lookup"><span data-stu-id="03919-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="03919-150">Jeśli wartości hello są **nr**, może to być z powodu:</span><span class="sxs-lookup"><span data-stu-id="03919-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="03919-151">Klucz magazynu zły (STK) w moduł TPM skojarzone z urządzeniem hello rejestracji (hello wyboru KeySignTest uruchomionej z podwyższonym poziomem uprawnień).</span><span class="sxs-lookup"><span data-stu-id="03919-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="03919-152">Alternatywnego Identyfikatora logowania</span><span class="sxs-lookup"><span data-stu-id="03919-152">Alternate Login ID</span></span>

- <span data-ttu-id="03919-153">Nie można odnaleźć serwera HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="03919-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="03919-154">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="03919-154">Next steps</span></span>

<span data-ttu-id="03919-155">Odpowiedzi na pytania, zobacz hello [zarządzanie urządzeniami — często zadawane pytania](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="03919-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
