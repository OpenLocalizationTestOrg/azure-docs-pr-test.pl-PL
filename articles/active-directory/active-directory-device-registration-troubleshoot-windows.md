---
title: "komputery przyłączone aaaTroubleshooting hello automatyczną rejestrację domeny usługi Azure AD systemu Windows 10 i Windows Server 2016 | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z hello automatyczną rejestrację domeny usługi Azure AD komputerów przyłączonych do systemu Windows 10 i Windows Server 2016."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="30761-103">Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — Windows 10 i Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="30761-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="30761-104">Ten temat jest toohello dotyczy następujących klientów:</span><span class="sxs-lookup"><span data-stu-id="30761-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="30761-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="30761-105">Windows 10</span></span>
-   <span data-ttu-id="30761-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="30761-106">Windows Server 2016</span></span>

<span data-ttu-id="30761-107">Dla innych klientów z systemem Windows, temacie [Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD dla klientów niższych poziomów Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="30761-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="30761-108">W tym temacie założono, że skonfigurowano automatyczną rejestrację urządzeń przyłączonych do domeny jako obramowane w opisanych w [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-device-registration-get-started.md) Witaj toosupport następujące scenariusze:</span><span class="sxs-lookup"><span data-stu-id="30761-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="30761-109">Dostępu warunkowego opartego na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="30761-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="30761-110">Enterprise roaming ustawień</span><span class="sxs-lookup"><span data-stu-id="30761-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="30761-111">Windows Hello dla firm</span><span class="sxs-lookup"><span data-stu-id="30761-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="30761-112">Ten dokument zawiera wskazówki dotyczące rozwiązywania problemów w sposób tooresolve potencjalne problemy.</span><span class="sxs-lookup"><span data-stu-id="30761-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="30761-113">Witaj rejestracja jest obsługiwana w systemie Windows hello aktualizacji 10 listopada 2015 i powyżej.</span><span class="sxs-lookup"><span data-stu-id="30761-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="30761-114">Zalecamy używanie hello aktualizacji rocznicy umożliwiających hello powyższych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="30761-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="30761-115">Krok 1: Pobierz hello stan rejestracji</span><span class="sxs-lookup"><span data-stu-id="30761-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="30761-116">**Stan rejestracji hello tooretrieve:**</span><span class="sxs-lookup"><span data-stu-id="30761-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="30761-117">Witaj Otwórz wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="30761-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="30761-118">Typ **dsregcmd/status**</span><span class="sxs-lookup"><span data-stu-id="30761-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="30761-119">+----------------------------------------------------------------------+
   | Stan urządzenia |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="30761-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="30761-120">EnterpriseJoined: Nie DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 odcisk palca: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected dostawca usług kryptograficznych platformy firmy Microsoft: tak KeySignTest:: należy uruchomić z podwyższonym poziomem uprawnień tootest.</span><span class="sxs-lookup"><span data-stu-id="30761-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="30761-121">IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: tak DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="30761-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="30761-122">+----------------------------------------------------------------------+
   | Stan użytkownika |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="30761-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="30761-123">WamDefaultAuthority: organizacje WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} AzureAdPrt (AzureAd): tak</span><span class="sxs-lookup"><span data-stu-id="30761-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="30761-124">Krok 2: Ocena hello stan rejestracji</span><span class="sxs-lookup"><span data-stu-id="30761-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="30761-125">Przejrzyj hello kolejnych pól i upewnij się, że hello oczekiwanych wartości:</span><span class="sxs-lookup"><span data-stu-id="30761-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="30761-126">AzureAdJoined: tak</span><span class="sxs-lookup"><span data-stu-id="30761-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="30761-127">To pole wskazuje, czy hello urządzenie jest zarejestrowane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30761-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="30761-128">Jeśli wartość hello jest pokazywana jako "Nie", rejestracja nie została ukończona.</span><span class="sxs-lookup"><span data-stu-id="30761-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="30761-129">**Możliwe przyczyny:**</span><span class="sxs-lookup"><span data-stu-id="30761-129">**Possible causes:**</span></span>

- <span data-ttu-id="30761-130">Uwierzytelnianie komputera hello rejestracji nie powiodło się.</span><span class="sxs-lookup"><span data-stu-id="30761-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="30761-131">W organizacji hello, które nie może zostać odnalezione przez komputer hello jest serwer proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="30761-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="30761-132">Hello komputerem można nawiązać połączenia z usługi Azure AD do uwierzytelniania lub Azure usługi rejestracji urządzeń do rejestracji</span><span class="sxs-lookup"><span data-stu-id="30761-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="30761-133">Witaj komputer może nie być w sieci wewnętrznej hello organizacji lub sieci VPN z tooan bezpośredniego wiersza z procesów lokalnych kontroler domeny usługi AD.</span><span class="sxs-lookup"><span data-stu-id="30761-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="30761-134">Jeśli komputer hello ma modułu TPM, może być nieprawidłowy stan.</span><span class="sxs-lookup"><span data-stu-id="30761-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="30761-135">Może być błąd konfiguracji usług wymienionych w dokumencie hello wcześniej trzeba tooverify ponownie.</span><span class="sxs-lookup"><span data-stu-id="30761-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="30761-136">Typowe przykłady są:</span><span class="sxs-lookup"><span data-stu-id="30761-136">Common examples are:</span></span>

    - <span data-ttu-id="30761-137">Serwer federacyjny nie ma punktów końcowych protokołu WS-Trust włączone</span><span class="sxs-lookup"><span data-stu-id="30761-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="30761-138">Serwer federacyjny może uniemożliwić uwierzytelnianie ruchu przychodzącego z komputerów w sieci przy użyciu zintegrowanego uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="30761-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="30761-139">Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje tooyour zweryfikowaną nazwę domeny w usłudze Azure AD w lesie hello AD, której należy komputer hello</span><span class="sxs-lookup"><span data-stu-id="30761-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="30761-140">DomainJoined: tak</span><span class="sxs-lookup"><span data-stu-id="30761-140">DomainJoined : YES</span></span>  

<span data-ttu-id="30761-141">To pole zawiera, czy urządzenie hello jest tooan dołączonego do lokalnej usługi Active Directory.</span><span class="sxs-lookup"><span data-stu-id="30761-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="30761-142">Jeśli wartość hello jest pokazywana jako **nr**, hello urządzenia nie można automatycznie rejestru z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30761-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="30761-143">Najpierw sprawdź toohello sprzężenia urządzenie tym hello lokalnej usługi Active Directory przed zarejestrowaniem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="30761-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="30761-144">Jeśli szukasz dołączenie hello tooAzure komputer AD bezpośrednio, przejdź tooLearn o możliwości usługi Azure Active Directory Join.</span><span class="sxs-lookup"><span data-stu-id="30761-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="30761-145">WorkplaceJoined: nie</span><span class="sxs-lookup"><span data-stu-id="30761-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="30761-146">To pole wskazuje, czy hello urządzenie jest zarejestrowane w usłudze Azure AD, ale jako urządzenia osobiste (oznaczony jako dołączone do).</span><span class="sxs-lookup"><span data-stu-id="30761-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="30761-147">Czy ta wartość powinien zawierać jako "Nie" przyłączony do domeny komputera zarejestrowane w usłudze Azure AD, jednak będzie wyświetlana jako tak oznacza, że konta firmowego lub szkolnego był dodany przed toohello komputera Kończenie rejestracji.</span><span class="sxs-lookup"><span data-stu-id="30761-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="30761-148">W takim przypadku hello konto zostanie zignorowana, jeśli przy użyciu hello rocznicy zaktualizowanej wersji systemu Windows 10 (1607 po uruchomi polecenie WinVer hello w Witaj, "Uruchom" lub w oknie wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="30761-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="30761-149">WamDefaultSet: Tak i AzureADPrt: tak</span><span class="sxs-lookup"><span data-stu-id="30761-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="30761-150">Zawierają one się, że użytkownik hello został pomyślnie uwierzytelniony tooAzure AD po zarejestrowaniu się w urządzeniu toohello.</span><span class="sxs-lookup"><span data-stu-id="30761-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="30761-151">Jeśli występują "Nie" hello Oto możliwe przyczyny:</span><span class="sxs-lookup"><span data-stu-id="30761-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="30761-152">Klucz magazynu zły (STK) w moduł TPM skojarzone z urządzeniem hello rejestracji (hello wyboru KeySignTest uruchomionej z podwyższonym poziomem uprawnień).</span><span class="sxs-lookup"><span data-stu-id="30761-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="30761-153">Alternatywnego Identyfikatora logowania</span><span class="sxs-lookup"><span data-stu-id="30761-153">Alternate Login ID</span></span>

- <span data-ttu-id="30761-154">Nie można odnaleźć serwera HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="30761-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="30761-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="30761-155">Next steps</span></span>

<span data-ttu-id="30761-156">Aby uzyskać więcej informacji, zobacz hello [automatycznej rejestracji urządzeń — często zadawane pytania](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="30761-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
