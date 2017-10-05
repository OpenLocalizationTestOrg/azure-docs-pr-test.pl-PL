---
title: "Rozwiązywanie problemów z automatyczną rejestrację domeny usługi Azure AD komputerów przyłączonych do systemu Windows 10 i Windows Server 2016 | Dokumentacja firmy Microsoft"
description: "Rozwiązywanie problemów z automatyczną rejestrację domeny usługi Azure AD komputerów przyłączonych do systemu Windows 10 i Windows Server 2016."
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
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="9141b-103">Rozwiązywanie problemów z automatyczną rejestrację domeny komputery przyłączone do usługi Azure AD — Windows 10 i Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9141b-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="9141b-104">Ten temat dotyczy następujących klientów:</span><span class="sxs-lookup"><span data-stu-id="9141b-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="9141b-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="9141b-105">Windows 10</span></span>
-   <span data-ttu-id="9141b-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9141b-106">Windows Server 2016</span></span>

<span data-ttu-id="9141b-107">Dla innych klientów z systemem Windows, temacie [Rozwiązywanie problemów z automatyczną rejestrację domeny komputery przyłączone do usługi Azure AD dla klientów niższych poziomów Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="9141b-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="9141b-108">W tym temacie założono, że skonfigurowano automatyczną rejestrację urządzeń przyłączonych do domeny jako obramowane w opisanych w [Konfigurowanie automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w usłudze Azure Active Directory](active-directory-device-registration-get-started.md) do obsługi następujących scenariuszy:</span><span class="sxs-lookup"><span data-stu-id="9141b-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="9141b-109">Dostępu warunkowego opartego na urządzeniu</span><span class="sxs-lookup"><span data-stu-id="9141b-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="9141b-110">Enterprise roaming ustawień</span><span class="sxs-lookup"><span data-stu-id="9141b-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="9141b-111">Windows Hello dla firm</span><span class="sxs-lookup"><span data-stu-id="9141b-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="9141b-112">Ten dokument zawiera wskazówki dotyczące rozwiązywania problemów na jak rozwiązać potencjalne problemy.</span><span class="sxs-lookup"><span data-stu-id="9141b-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="9141b-113">Rejestracja jest obsługiwana w systemie Windows 10 listopada 2015 aktualizacji i powyżej.</span><span class="sxs-lookup"><span data-stu-id="9141b-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="9141b-114">Zalecamy używanie aktualizacji rozliczenia dotyczące włączania powyższych scenariuszy.</span><span class="sxs-lookup"><span data-stu-id="9141b-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="9141b-115">Krok 1: Pobierz stan rejestracji</span><span class="sxs-lookup"><span data-stu-id="9141b-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="9141b-116">**Aby pobrać stan rejestracji:**</span><span class="sxs-lookup"><span data-stu-id="9141b-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="9141b-117">Otwórz wiersz polecenia jako administrator.</span><span class="sxs-lookup"><span data-stu-id="9141b-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="9141b-118">Typ **dsregcmd/status**</span><span class="sxs-lookup"><span data-stu-id="9141b-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="9141b-119">+----------------------------------------------------------------------+
   | Stan urządzenia |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="9141b-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="9141b-120">EnterpriseJoined: Nie DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 odcisk palca: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected dostawcy kryptograficznego platformy firmy Microsoft: tak KeySignTest:: należy uruchomić podniesione do testowania.</span><span class="sxs-lookup"><span data-stu-id="9141b-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="9141b-121">IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: tak DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="9141b-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="9141b-122">+----------------------------------------------------------------------+
   | Stan użytkownika |+----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="9141b-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="9141b-123">WamDefaultAuthority: organizacje WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} AzureAdPrt (AzureAd): tak</span><span class="sxs-lookup"><span data-stu-id="9141b-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="9141b-124">Krok 2: Ocena stan rejestracji</span><span class="sxs-lookup"><span data-stu-id="9141b-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="9141b-125">Przejrzyj następujące pola i upewnij się, że mają one oczekiwanych wartości:</span><span class="sxs-lookup"><span data-stu-id="9141b-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="9141b-126">AzureAdJoined: tak</span><span class="sxs-lookup"><span data-stu-id="9141b-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="9141b-127">To pole wskazuje, czy urządzenie jest zarejestrowane w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9141b-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="9141b-128">Jeśli wartość jest pokazywana jako "Nie", rejestracja nie została ukończona.</span><span class="sxs-lookup"><span data-stu-id="9141b-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="9141b-129">**Możliwe przyczyny:**</span><span class="sxs-lookup"><span data-stu-id="9141b-129">**Possible causes:**</span></span>

- <span data-ttu-id="9141b-130">Nie można przeprowadzić uwierzytelniania komputera do rejestracji.</span><span class="sxs-lookup"><span data-stu-id="9141b-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="9141b-131">W organizacji, które nie mogą zostać odnalezione przez komputer znajduje się serwer proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="9141b-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="9141b-132">Komputer można nawiązać połączenia z usługi Azure AD do uwierzytelniania lub Azure usługi rejestracji urządzeń do rejestracji</span><span class="sxs-lookup"><span data-stu-id="9141b-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="9141b-133">Komputer może nie być w wewnętrznej sieci firmy lub w sieci VPN, z bezpośredniej procesów z wiersza do lokalnego kontrolera domeny usługi AD.</span><span class="sxs-lookup"><span data-stu-id="9141b-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="9141b-134">Jeśli komputer ma modułu TPM, może być nieprawidłowy stan.</span><span class="sxs-lookup"><span data-stu-id="9141b-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="9141b-135">Może być błąd konfiguracji usług wymienionych w dokumencie wcześniej należy zweryfikować ponownie.</span><span class="sxs-lookup"><span data-stu-id="9141b-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="9141b-136">Typowe przykłady są:</span><span class="sxs-lookup"><span data-stu-id="9141b-136">Common examples are:</span></span>

    - <span data-ttu-id="9141b-137">Serwer federacyjny nie ma punktów końcowych protokołu WS-Trust włączone</span><span class="sxs-lookup"><span data-stu-id="9141b-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="9141b-138">Serwer federacyjny może uniemożliwić uwierzytelnianie ruchu przychodzącego z komputerów w sieci przy użyciu zintegrowanego uwierzytelniania systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="9141b-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="9141b-139">Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje nazwę domeny zweryfikowane w usłudze Azure AD w lesie usługi AD, w którym komputer należy do</span><span class="sxs-lookup"><span data-stu-id="9141b-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="9141b-140">DomainJoined: tak</span><span class="sxs-lookup"><span data-stu-id="9141b-140">DomainJoined : YES</span></span>  

<span data-ttu-id="9141b-141">To pole wskazuje, czy urządzenie jest dołączane do lokalnej usługi Active Directory lub nie.</span><span class="sxs-lookup"><span data-stu-id="9141b-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="9141b-142">Jeśli wartość jest pokazywana jako **nr**, urządzenie nie może automatycznie rejestru z usługą Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9141b-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="9141b-143">Najpierw należy sprawdzić, czy urządzenie łączy się w lokalnej usłudze Active Directory przed zarejestrowaniem w usłudze Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9141b-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="9141b-144">Jeśli szukasz przyłączania komputera do usługi Azure AD bezpośrednio, przejdź do Dowiedz się więcej na temat możliwości usługi Azure Active Directory Join.</span><span class="sxs-lookup"><span data-stu-id="9141b-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="9141b-145">WorkplaceJoined: nie</span><span class="sxs-lookup"><span data-stu-id="9141b-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="9141b-146">To pole wskazuje, czy urządzenie jest zarejestrowane w usłudze Azure AD, ale jako urządzenia osobiste (oznaczony jako dołączone do).</span><span class="sxs-lookup"><span data-stu-id="9141b-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="9141b-147">Jeśli ta wartość powinna wyświetlić jako "Nie" na komputerze przyłączonym do domeny zarejestrowana w usłudze Azure AD, jednak jeśli będzie wyświetlana jako tak oznacza to, że przed zakończeniem rejestracji komputera dodano konto służbowe.</span><span class="sxs-lookup"><span data-stu-id="9141b-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="9141b-148">W takim przypadku konto zostanie zignorowana, jeśli używana wersja rocznicy aktualizacji systemu Windows 10 (1607 po WinVer uruchomione polecenie w oknie "Uruchom" lub okno wiersza polecenia).</span><span class="sxs-lookup"><span data-stu-id="9141b-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="9141b-149">WamDefaultSet: Tak i AzureADPrt: tak</span><span class="sxs-lookup"><span data-stu-id="9141b-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="9141b-150">Zawierają one czy użytkownik został pomyślnie uwierzytelniony za pomocą usługi Azure AD po zalogowaniu się do urządzenia.</span><span class="sxs-lookup"><span data-stu-id="9141b-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="9141b-151">Jeśli wykazują "Nie" możliwe przyczyny są następujące:</span><span class="sxs-lookup"><span data-stu-id="9141b-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="9141b-152">Klucz magazynu zły (STK) w moduł TPM skojarzoną z tym urządzeniem rejestracji (wyboru KeySignTest uruchomionej z podwyższonym poziomem uprawnień).</span><span class="sxs-lookup"><span data-stu-id="9141b-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="9141b-153">Alternatywnego Identyfikatora logowania</span><span class="sxs-lookup"><span data-stu-id="9141b-153">Alternate Login ID</span></span>

- <span data-ttu-id="9141b-154">Nie można odnaleźć serwera HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="9141b-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="9141b-155">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9141b-155">Next steps</span></span>

<span data-ttu-id="9141b-156">Aby uzyskać więcej informacji, zobacz [automatycznej rejestracji urządzeń — często zadawane pytania](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="9141b-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 