---
title: "aaaAzure uwierzytelniania opartego na certyfikatach usługi Active Directory — wprowadzenie | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak uwierzytelnianie oparte na certyfikatach tooconfigure w środowisku"
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 3c73bdf56018c0716085c923a61e9560dbe4004c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="ac8b1-103">Wprowadzenie do uwierzytelniania opartego na certyfikacie w usłudze Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac8b1-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="ac8b1-104">Uwierzytelnianie oparte na certyfikatach umożliwia toobe uwierzytelniony przez usługę Azure Active Directory przy użyciu certyfikatu klienta na urządzeniu z systemem Windows, Android lub iOS podczas łączenia Twoje konto programu Exchange online:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-104">Certificate-based authentication enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="ac8b1-105">Aplikacje mobilne pakietu Office, takich jak Microsoft Outlook i Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="ac8b1-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="ac8b1-106">Klienci programu Exchange ActiveSync (EAS)</span><span class="sxs-lookup"><span data-stu-id="ac8b1-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="ac8b1-107">Konfigurowanie tej funkcji eliminuje hello potrzeby tooenter nazwę użytkownika i kombinacja hasła do niektórych poczty i aplikacje Microsoft Office na urządzeniu przenośnym.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="ac8b1-108">W tym temacie:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-108">This topic:</span></span>

- <span data-ttu-id="ac8b1-109">Udostępnia program hello kroki tooconfigure i korzystanie z uwierzytelniania opartego na certyfikatach dla użytkowników z dzierżaw Office 365 Enterprise, Business, Education i dla instytucji rządowych USA planów.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-109">Provides you with hello steps tooconfigure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="ac8b1-110">Ta funkcja jest dostępna w wersji zapoznawczej w planach Office 365 Chin, instytucji rządowych Stanów Zjednoczonych obrony i nam rządu federalnego.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="ac8b1-111">Przyjęto założenie, że masz już [infrastruktury kluczy publicznych (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) i [usług AD FS](connect/active-directory-aadconnectfed-whatis.md) skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="ac8b1-112">Wymagania</span><span class="sxs-lookup"><span data-stu-id="ac8b1-112">Requirements</span></span>

<span data-ttu-id="ac8b1-113">uwierzytelnianie oparte na certyfikatach tooconfigure hello musi być spełnione następujące warunki:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-113">tooconfigure certificate-based authentication, hello following must be true:</span></span>  

- <span data-ttu-id="ac8b1-114">Uwierzytelnianie oparte na certyfikatach (CBA) jest obsługiwana tylko dla środowisk federacyjnym dla aplikacji przeglądarki lub natywnego klientów korzystających z nowoczesnego uwierzytelniania (ADAL).</span><span class="sxs-lookup"><span data-stu-id="ac8b1-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="ac8b1-115">Jedynym wyjątkiem Hello jest Exchange Active Sync (EAS) dla EKSO, którego można użyć zarówno federacyjnych i zarządzanych kont.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-115">hello one exception is Exchange Active Sync (EAS) for EXO which can be used for both, federated and managed accounts.</span></span> 

- <span data-ttu-id="ac8b1-116">Witaj główny urząd certyfikacji i wszystkie urzędy certyfikacji pośrednich muszą być skonfigurowane w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-116">hello root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="ac8b1-117">Każdego urzędu certyfikacji musi mieć listę odwołania certyfikatów (CRL), który można odwoływać się za pośrednictwem internetowy adres URL.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="ac8b1-118">Musi mieć co najmniej jeden certyfikat urzędu skonfigurowane w usłudze Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="ac8b1-119">Powiązane procedurę można znaleźć w hello [Konfigurowanie urzędów certyfikacji hello](#step-2-configure-the-certificate-authorities) sekcji.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-119">You can find related steps in hello [Configure hello certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="ac8b1-120">Dla klientów programu Exchange ActiveSync certyfikat klienta na powitania musi mieć hello routingu adres e-mail użytkownika w programie Exchange adresów online albo hello główna nazwa lub hello Nazwa RFC822 wartość z pola alternatywna nazwa podmiotu hello.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-120">For Exchange ActiveSync clients, hello client certificate must have hello user’s routable email address in Exchange online in either hello Principal Name or hello RFC822 Name value of hello Subject Alternative Name field.</span></span> <span data-ttu-id="ac8b1-121">Usługa Azure Active Directory mapuje atrybutu value RFC822 hello adres serwera Proxy toohello w katalogu hello.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-121">Azure Active Directory maps hello RFC822 value toohello Proxy Address attribute in hello directory.</span></span>  

- <span data-ttu-id="ac8b1-122">Urządzenie klienta musi mieć dostęp do urzędu certyfikacji tooat co najmniej jedną, który wystawia certyfikaty klienta.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-122">Your client device must have access tooat least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="ac8b1-123">Certyfikat klienta na potrzeby uwierzytelniania klientów musi być wystawiony tooyour klienta.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-123">A client certificate for client authentication must have been issued tooyour client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="ac8b1-124">Krok 1: Wybierz danej platformy urządzenia</span><span class="sxs-lookup"><span data-stu-id="ac8b1-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="ac8b1-125">Pierwszym krokiem hello platformy urządzeń, które są dla Ciebie ważne, należy tooreview hello poniżej:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-125">As a first step, for hello device platform you care about, you need tooreview hello following:</span></span>

- <span data-ttu-id="ac8b1-126">Obsługa aplikacji mobilnych pakietu Office Hello</span><span class="sxs-lookup"><span data-stu-id="ac8b1-126">hello Office mobile applications support</span></span> 
- <span data-ttu-id="ac8b1-127">wymagania dotyczące konkretnej implementacji Hello</span><span class="sxs-lookup"><span data-stu-id="ac8b1-127">hello specific implementation requirements</span></span>  

<span data-ttu-id="ac8b1-128">Witaj związane z istnieją informacje dotyczące hello następujące platformy urządzeń:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-128">hello related information exists for hello following device platforms:</span></span>

- [<span data-ttu-id="ac8b1-129">Android</span><span class="sxs-lookup"><span data-stu-id="ac8b1-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="ac8b1-130">iOS</span><span class="sxs-lookup"><span data-stu-id="ac8b1-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a><span data-ttu-id="ac8b1-131">Krok 2: Konfigurowanie urzędów certyfikacji hello</span><span class="sxs-lookup"><span data-stu-id="ac8b1-131">Step 2: Configure hello certificate authorities</span></span> 

<span data-ttu-id="ac8b1-132">tooconfigure urzędów certyfikacji w usłudze Azure Active Directory, dla każdego urzędu certyfikacji, Przekaż hello następujące:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-132">tooconfigure your certificate authorities in Azure Active Directory, for each certificate authority, upload hello following:</span></span> 

* <span data-ttu-id="ac8b1-133">Witaj w część publiczną certyfikatu hello *.cer* formatu</span><span class="sxs-lookup"><span data-stu-id="ac8b1-133">hello public portion of hello certificate, in *.cer* format</span></span> 
* <span data-ttu-id="ac8b1-134">Witaj internetowy adresów URL, gdzie hello list odwołania certyfikatów (CRL) znajdują się</span><span class="sxs-lookup"><span data-stu-id="ac8b1-134">hello Internet facing URLs where hello Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="ac8b1-135">Witaj schematu dla urzędu certyfikacji wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-135">hello schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="ac8b1-136">Witaj konfiguracji, można użyć hello [Azure Active Directory programu PowerShell w wersji 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="ac8b1-136">For hello configuration, you can use hello [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>  

1. <span data-ttu-id="ac8b1-137">Uruchom program Windows PowerShell z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-137">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="ac8b1-138">Zainstaluj moduł hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-138">Install hello Azure AD module.</span></span> <span data-ttu-id="ac8b1-139">Należy tooinstall wersji [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-139">You need tooinstall Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="ac8b1-140">Pierwszym krokiem konfiguracji należy tooestablish połączenie z dzierżawą.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-140">As a first configuration step, you need tooestablish a connection with your tenant.</span></span> <span data-ttu-id="ac8b1-141">Jak dzierżawcy tooyour połączenie istnieje, można przejrzeć, Dodaj, Usuń i modyfikować hello zaufanych urzędów certyfikacji, które są zdefiniowane w katalogu.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-141">As soon as a connection tooyour tenant exists, you can review, add, delete and modify hello trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="ac8b1-142">Połączenie</span><span class="sxs-lookup"><span data-stu-id="ac8b1-142">Connect</span></span>

<span data-ttu-id="ac8b1-143">tooestablish połączenia z dzierżawą, użyj hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-143">tooestablish a connection with your tenant, use hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="ac8b1-144">Pobieranie</span><span class="sxs-lookup"><span data-stu-id="ac8b1-144">Retrieve</span></span> 

<span data-ttu-id="ac8b1-145">urzędy certyfikacji hello zaufane tooretrieve zdefiniowanych w katalogu, użyj hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-145">tooretrieve hello trusted certificate authorities that are defined in your directory, use hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="ac8b1-146">Add</span><span class="sxs-lookup"><span data-stu-id="ac8b1-146">Add</span></span>

<span data-ttu-id="ac8b1-147">toocreate zaufanego urzędu certyfikacji, użyj hello [AzureADTrustedCertificateAuthority nowy](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) polecenia cmdlet i zestaw hello **crlDistributionPoint** tooa poprawną wartość atrybutu:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-147">toocreate a trusted certificate authority, use hello [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set hello **crlDistributionPoint** attribute tooa correct value:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="ac8b1-148">Remove</span><span class="sxs-lookup"><span data-stu-id="ac8b1-148">Remove</span></span>

<span data-ttu-id="ac8b1-149">tooremove zaufanego urzędu certyfikacji, użyj hello [AzureADTrustedCertificateAuthority Usuń](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-149">tooremove a trusted certificate authority, use hello [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="ac8b1-150">Modfiy</span><span class="sxs-lookup"><span data-stu-id="ac8b1-150">Modfiy</span></span>

<span data-ttu-id="ac8b1-151">toomodify zaufanego urzędu certyfikacji, użyj hello [AzureADTrustedCertificateAuthority zestaw](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-151">toomodify a trusted certificate authority, use hello [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="ac8b1-152">Krok 3: Konfigurowanie odwołania</span><span class="sxs-lookup"><span data-stu-id="ac8b1-152">Step 3: Configure revocation</span></span>

<span data-ttu-id="ac8b1-153">toorevoke certyfikatu klienta usługi Azure Active Directory pobiera certyfikat hello listy odwołania (CRL) z adresów URL hello przekazywane jako część informacji o certyfikacie urzędu i buforuje ją.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-153">toorevoke a client certificate, Azure Active Directory fetches hello certificate revocation list (CRL) from hello URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="ac8b1-154">Witaj ostatniej publikacji sygnatury czasowej (**daty wprowadzenia** właściwości) w hello listy CRL jest używana hello tooensure listy CRL jest nadal ważny.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-154">hello last publish timestamp (**Effective Date** property) in hello CRL is used tooensure hello CRL is still valid.</span></span> <span data-ttu-id="ac8b1-155">Witaj listy CRL jest toorevoke okresowo przywoływanego toocertificates dostępu, które są częścią listy hello.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-155">hello CRL is periodically referenced toorevoke access toocertificates that are a part of hello list.</span></span>

<span data-ttu-id="ac8b1-156">Jeśli więcej błyskawicznych odwołania jest wymagana (na przykład, jeśli użytkownik utraci urządzenie), można unieważniona token autoryzacji hello hello użytkownika.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-156">If a more instant revocation is required (for example, if a user loses a device), hello authorization token of hello user can be invalidated.</span></span> <span data-ttu-id="ac8b1-157">tooinvalidate hello autoryzacji tokenu, ustaw hello **StsRefreshTokenValidFrom** dla tego użytkownika za pomocą środowiska Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-157">tooinvalidate hello authorization token, set hello **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="ac8b1-158">Należy zaktualizować hello **StsRefreshTokenValidFrom** dla każdego użytkownika ma dostęp toorevoke pole.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-158">You must update hello **StsRefreshTokenValidFrom** field for each user you want toorevoke access for.</span></span>

<span data-ttu-id="ac8b1-159">tooensure, który odwołania hello będzie się powtarzał, należy ustawić hello **daty wprowadzenia** hello listy CRL tooa data po hello wartości ustawionej przez **StsRefreshTokenValidFrom** i upewnij się, certyfikat hello zagrożona znajduje się w Witaj listy CRL.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-159">tooensure that hello revocation persists, you must set hello **Effective Date** of hello CRL tooa date after hello value set by **StsRefreshTokenValidFrom** and ensure hello certificate in question is in hello CRL.</span></span>

<span data-ttu-id="ac8b1-160">Witaj, następujące kroki konspektu hello proces aktualizowania i unieważnia token autoryzacji hello przez ustawienie hello **StsRefreshTokenValidFrom** pola.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-160">hello following steps outline hello process for updating and invalidating hello authorization token by setting hello **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="ac8b1-161">**tooconfigure odwołania:**</span><span class="sxs-lookup"><span data-stu-id="ac8b1-161">**tooconfigure revocation:**</span></span> 

1. <span data-ttu-id="ac8b1-162">Połączenie z usługą MSOL toohello poświadczenia administratora:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-162">Connect with admin credentials toohello MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="ac8b1-163">Pobrać hello bieżącą wartość StsRefreshTokensValidFrom dla użytkownika:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-163">Retrieve hello current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="ac8b1-164">Skonfiguruj nową wartość StsRefreshTokensValidFrom bieżącą sygnaturę czasową hello użytkownika toohello równe:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-164">Configure a new StsRefreshTokensValidFrom value for hello user equal toohello current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="ac8b1-165">Data Hello, ustawionych musi być w przyszłości hello.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-165">hello date you set must be in hello future.</span></span> <span data-ttu-id="ac8b1-166">Jeśli hello data nie jest w przyszłości hello, hello **StsRefreshTokensValidFrom** nie ustawiono właściwości.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-166">If hello date is not in hello future, hello **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="ac8b1-167">Jeśli hello przypada w przyszłości, hello **StsRefreshTokensValidFrom** ustawiono toohello bieżącej godziny (nie hello Data wskazana za pomocą polecenia Set-MsolUser).</span><span class="sxs-lookup"><span data-stu-id="ac8b1-167">If hello date is in hello future, **StsRefreshTokensValidFrom** is set toohello current time (not hello date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="ac8b1-168">Krok 4: Testowanie konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ac8b1-168">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="ac8b1-169">Testowanie certyfikatu</span><span class="sxs-lookup"><span data-stu-id="ac8b1-169">Testing your certificate</span></span>

<span data-ttu-id="ac8b1-170">Jako pierwszego testu konfiguracji, należy spróbować toosign w zbyt[programu Outlook Web Access](https://outlook.office365.com) lub [usługi SharePoint Online](https://microsoft.sharepoint.com) przy użyciu programu **przeglądarki na urządzeniu**.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-170">As a first configuration test, you should try toosign in too[Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="ac8b1-171">Jeśli logowanie się pomyślnie, następnie należy pamiętać, że:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-171">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="ac8b1-172">certyfikat użytkownika Hello został elastycznie tooyour urządzenie testowe</span><span class="sxs-lookup"><span data-stu-id="ac8b1-172">hello user certificate has been provisioned tooyour test device</span></span>
- <span data-ttu-id="ac8b1-173">Usługi AD FS jest poprawnie skonfigurowany.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-173">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="ac8b1-174">Testowanie aplikacji mobilnych pakietu Office</span><span class="sxs-lookup"><span data-stu-id="ac8b1-174">Testing Office mobile applications</span></span>

<span data-ttu-id="ac8b1-175">**uwierzytelnianie oparte na certyfikatach tootest na aplikację mobilną Office:**</span><span class="sxs-lookup"><span data-stu-id="ac8b1-175">**tootest certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="ac8b1-176">Na urządzeniu testu instalacji aplikacji mobilnych pakietu Office (np. OneDrive).</span><span class="sxs-lookup"><span data-stu-id="ac8b1-176">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="ac8b1-177">Uruchamianie aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-177">Launch hello application.</span></span> 
4. <span data-ttu-id="ac8b1-178">Wprowadź nazwę użytkownika, a następnie wybierz hello certyfikat użytkownika, które chcesz toouse.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-178">Enter your user name, and then select hello user certificate you want toouse.</span></span> 

<span data-ttu-id="ac8b1-179">Użytkownik powinien być pomyślnie zarejestrowany.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-179">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="ac8b1-180">Testowanie aplikacji klienta programu Exchange ActiveSync</span><span class="sxs-lookup"><span data-stu-id="ac8b1-180">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="ac8b1-181">tooaccess programu Exchange ActiveSync (EAS) przy użyciu uwierzytelniania opartego na certyfikatach, profilu EAS zawierający certyfikat klienta na powitania musi być dostępny toohello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-181">tooaccess Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing hello client certificate must be available toohello application.</span></span> 

<span data-ttu-id="ac8b1-182">Witaj profilu EAS musi zawierać hello następujących informacji:</span><span class="sxs-lookup"><span data-stu-id="ac8b1-182">hello EAS profile must contain hello following information:</span></span>

- <span data-ttu-id="ac8b1-183">Witaj toobe certyfikatu użytkownika używane do uwierzytelniania</span><span class="sxs-lookup"><span data-stu-id="ac8b1-183">hello user certificate toobe used for authentication</span></span> 

- <span data-ttu-id="ac8b1-184">punkt końcowy EAS Hello (na przykład outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="ac8b1-184">hello EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="ac8b1-185">Można konfigurować i umieszczona na urządzeniu hello za pośrednictwem wykorzystania hello zarządzania urządzeniami przenośnymi (MDM) jak usługa Intune lub umieszczając ręcznie certyfikat hello w hello profilu EAS urządzenia hello profilu EAS.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-185">An EAS profile can be configured and placed on hello device through hello utilization of Mobile device management (MDM) such as Intune or by manually placing hello certificate in hello EAS profile on hello device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="ac8b1-186">Testowanie aplikacji klienta EAS w systemie Android</span><span class="sxs-lookup"><span data-stu-id="ac8b1-186">Testing EAS client applications on Android</span></span>

<span data-ttu-id="ac8b1-187">**uwierzytelnianie certyfikatu tootest:**</span><span class="sxs-lookup"><span data-stu-id="ac8b1-187">**tootest certificate authentication:**</span></span>  

1. <span data-ttu-id="ac8b1-188">Konfigurowanie profilu EAS w aplikacji hello, który spełnia wymagania hello powyżej.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-188">Configure an EAS profile in hello application that satisfies hello requirements above.</span></span>  
2. <span data-ttu-id="ac8b1-189">Otwórz aplikacji hello i sprawdź, czy jest synchronizowanie poczty.</span><span class="sxs-lookup"><span data-stu-id="ac8b1-189">Open hello application, and verify that mail is synchronizing.</span></span> 

