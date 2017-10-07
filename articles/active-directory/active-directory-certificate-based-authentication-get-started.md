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
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Wprowadzenie do uwierzytelniania opartego na certyfikacie w usłudze Azure Active Directory

Uwierzytelnianie oparte na certyfikatach umożliwia toobe uwierzytelniony przez usługę Azure Active Directory przy użyciu certyfikatu klienta na urządzeniu z systemem Windows, Android lub iOS podczas łączenia Twoje konto programu Exchange online: 

- Aplikacje mobilne pakietu Office, takich jak Microsoft Outlook i Microsoft Word   

- Klienci programu Exchange ActiveSync (EAS) 

Konfigurowanie tej funkcji eliminuje hello potrzeby tooenter nazwę użytkownika i kombinacja hasła do niektórych poczty i aplikacje Microsoft Office na urządzeniu przenośnym. 

W tym temacie:

- Udostępnia program hello kroki tooconfigure i korzystanie z uwierzytelniania opartego na certyfikatach dla użytkowników z dzierżaw Office 365 Enterprise, Business, Education i dla instytucji rządowych USA planów. Ta funkcja jest dostępna w wersji zapoznawczej w planach Office 365 Chin, instytucji rządowych Stanów Zjednoczonych obrony i nam rządu federalnego. 

- Przyjęto założenie, że masz już [infrastruktury kluczy publicznych (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) i [usług AD FS](connect/active-directory-aadconnectfed-whatis.md) skonfigurowany.    


## <a name="requirements"></a>Wymagania

uwierzytelnianie oparte na certyfikatach tooconfigure hello musi być spełnione następujące warunki:  

- Uwierzytelnianie oparte na certyfikatach (CBA) jest obsługiwana tylko dla środowisk federacyjnym dla aplikacji przeglądarki lub natywnego klientów korzystających z nowoczesnego uwierzytelniania (ADAL). Jedynym wyjątkiem Hello jest Exchange Active Sync (EAS) dla EKSO, którego można użyć zarówno federacyjnych i zarządzanych kont. 

- Witaj główny urząd certyfikacji i wszystkie urzędy certyfikacji pośrednich muszą być skonfigurowane w usłudze Azure Active Directory.  

- Każdego urzędu certyfikacji musi mieć listę odwołania certyfikatów (CRL), który można odwoływać się za pośrednictwem internetowy adres URL.  

- Musi mieć co najmniej jeden certyfikat urzędu skonfigurowane w usłudze Azure Active Directory. Powiązane procedurę można znaleźć w hello [Konfigurowanie urzędów certyfikacji hello](#step-2-configure-the-certificate-authorities) sekcji.  

- Dla klientów programu Exchange ActiveSync certyfikat klienta na powitania musi mieć hello routingu adres e-mail użytkownika w programie Exchange adresów online albo hello główna nazwa lub hello Nazwa RFC822 wartość z pola alternatywna nazwa podmiotu hello. Usługa Azure Active Directory mapuje atrybutu value RFC822 hello adres serwera Proxy toohello w katalogu hello.  

- Urządzenie klienta musi mieć dostęp do urzędu certyfikacji tooat co najmniej jedną, który wystawia certyfikaty klienta.  

- Certyfikat klienta na potrzeby uwierzytelniania klientów musi być wystawiony tooyour klienta.  




## <a name="step-1-select-your-device-platform"></a>Krok 1: Wybierz danej platformy urządzenia

Pierwszym krokiem hello platformy urządzeń, które są dla Ciebie ważne, należy tooreview hello poniżej:

- Obsługa aplikacji mobilnych pakietu Office Hello 
- wymagania dotyczące konkretnej implementacji Hello  

Witaj związane z istnieją informacje dotyczące hello następujące platformy urządzeń:

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-hello-certificate-authorities"></a>Krok 2: Konfigurowanie urzędów certyfikacji hello 

tooconfigure urzędów certyfikacji w usłudze Azure Active Directory, dla każdego urzędu certyfikacji, Przekaż hello następujące: 

* Witaj w część publiczną certyfikatu hello *.cer* formatu 
* Witaj internetowy adresów URL, gdzie hello list odwołania certyfikatów (CRL) znajdują się

Witaj schematu dla urzędu certyfikacji wygląda następująco: 

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

Witaj konfiguracji, można użyć hello [Azure Active Directory programu PowerShell w wersji 2](/powershell/azure/install-adv2?view=azureadps-2.0):  

1. Uruchom program Windows PowerShell z uprawnieniami administratora. 
2. Zainstaluj moduł hello Azure AD. Należy tooinstall wersji [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) lub nowszej.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

Pierwszym krokiem konfiguracji należy tooestablish połączenie z dzierżawą. Jak dzierżawcy tooyour połączenie istnieje, można przejrzeć, Dodaj, Usuń i modyfikować hello zaufanych urzędów certyfikacji, które są zdefiniowane w katalogu. 

### <a name="connect"></a>Połączenie

tooestablish połączenia z dzierżawą, użyj hello [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) polecenia cmdlet:

    Connect-AzureAD 


### <a name="retrieve"></a>Pobieranie 

urzędy certyfikacji hello zaufane tooretrieve zdefiniowanych w katalogu, użyj hello [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) polecenia cmdlet. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>Add

toocreate zaufanego urzędu certyfikacji, użyj hello [AzureADTrustedCertificateAuthority nowy](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) polecenia cmdlet i zestaw hello **crlDistributionPoint** tooa poprawną wartość atrybutu: 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF hello CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>Remove

tooremove zaufanego urzędu certyfikacji, użyj hello [AzureADTrustedCertificateAuthority Usuń](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) polecenia cmdlet:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>Modfiy

toomodify zaufanego urzędu certyfikacji, użyj hello [AzureADTrustedCertificateAuthority zestaw](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) polecenia cmdlet:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>Krok 3: Konfigurowanie odwołania

toorevoke certyfikatu klienta usługi Azure Active Directory pobiera certyfikat hello listy odwołania (CRL) z adresów URL hello przekazywane jako część informacji o certyfikacie urzędu i buforuje ją. Witaj ostatniej publikacji sygnatury czasowej (**daty wprowadzenia** właściwości) w hello listy CRL jest używana hello tooensure listy CRL jest nadal ważny. Witaj listy CRL jest toorevoke okresowo przywoływanego toocertificates dostępu, które są częścią listy hello.

Jeśli więcej błyskawicznych odwołania jest wymagana (na przykład, jeśli użytkownik utraci urządzenie), można unieważniona token autoryzacji hello hello użytkownika. tooinvalidate hello autoryzacji tokenu, ustaw hello **StsRefreshTokenValidFrom** dla tego użytkownika za pomocą środowiska Windows PowerShell. Należy zaktualizować hello **StsRefreshTokenValidFrom** dla każdego użytkownika ma dostęp toorevoke pole.

tooensure, który odwołania hello będzie się powtarzał, należy ustawić hello **daty wprowadzenia** hello listy CRL tooa data po hello wartości ustawionej przez **StsRefreshTokenValidFrom** i upewnij się, certyfikat hello zagrożona znajduje się w Witaj listy CRL.

Witaj, następujące kroki konspektu hello proces aktualizowania i unieważnia token autoryzacji hello przez ustawienie hello **StsRefreshTokenValidFrom** pola. 

**tooconfigure odwołania:** 

1. Połączenie z usługą MSOL toohello poświadczenia administratora: 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. Pobrać hello bieżącą wartość StsRefreshTokensValidFrom dla użytkownika: 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Skonfiguruj nową wartość StsRefreshTokensValidFrom bieżącą sygnaturę czasową hello użytkownika toohello równe: 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

Data Hello, ustawionych musi być w przyszłości hello. Jeśli hello data nie jest w przyszłości hello, hello **StsRefreshTokensValidFrom** nie ustawiono właściwości. Jeśli hello przypada w przyszłości, hello **StsRefreshTokensValidFrom** ustawiono toohello bieżącej godziny (nie hello Data wskazana za pomocą polecenia Set-MsolUser). 


## <a name="step-4-test-your-configuration"></a>Krok 4: Testowanie konfiguracji

### <a name="testing-your-certificate"></a>Testowanie certyfikatu

Jako pierwszego testu konfiguracji, należy spróbować toosign w zbyt[programu Outlook Web Access](https://outlook.office365.com) lub [usługi SharePoint Online](https://microsoft.sharepoint.com) przy użyciu programu **przeglądarki na urządzeniu**.

Jeśli logowanie się pomyślnie, następnie należy pamiętać, że:

- certyfikat użytkownika Hello został elastycznie tooyour urządzenie testowe
- Usługi AD FS jest poprawnie skonfigurowany.  


### <a name="testing-office-mobile-applications"></a>Testowanie aplikacji mobilnych pakietu Office

**uwierzytelnianie oparte na certyfikatach tootest na aplikację mobilną Office:** 

1. Na urządzeniu testu instalacji aplikacji mobilnych pakietu Office (np. OneDrive).
3. Uruchamianie aplikacji hello. 
4. Wprowadź nazwę użytkownika, a następnie wybierz hello certyfikat użytkownika, które chcesz toouse. 

Użytkownik powinien być pomyślnie zarejestrowany. 

### <a name="testing-exchange-activesync-client-applications"></a>Testowanie aplikacji klienta programu Exchange ActiveSync

tooaccess programu Exchange ActiveSync (EAS) przy użyciu uwierzytelniania opartego na certyfikatach, profilu EAS zawierający certyfikat klienta na powitania musi być dostępny toohello aplikacji. 

Witaj profilu EAS musi zawierać hello następujących informacji:

- Witaj toobe certyfikatu użytkownika używane do uwierzytelniania 

- punkt końcowy EAS Hello (na przykład outlook.office365.com)

Można konfigurować i umieszczona na urządzeniu hello za pośrednictwem wykorzystania hello zarządzania urządzeniami przenośnymi (MDM) jak usługa Intune lub umieszczając ręcznie certyfikat hello w hello profilu EAS urządzenia hello profilu EAS.  

### <a name="testing-eas-client-applications-on-android"></a>Testowanie aplikacji klienta EAS w systemie Android

**uwierzytelnianie certyfikatu tootest:**  

1. Konfigurowanie profilu EAS w aplikacji hello, który spełnia wymagania hello powyżej.  
2. Otwórz aplikacji hello i sprawdź, czy jest synchronizowanie poczty. 

