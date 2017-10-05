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
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a>Rozwiązywanie problemów z automatyczną rejestrację domeny komputery przyłączone do usługi Azure AD — Windows 10 i Windows Server 2016

Ten temat dotyczy następujących klientów:

-   Windows 10
-   Windows Server 2016

Dla innych klientów z systemem Windows, temacie [Rozwiązywanie problemów z automatyczną rejestrację domeny komputery przyłączone do usługi Azure AD dla klientów niższych poziomów Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).

W tym temacie założono, że skonfigurowano automatyczną rejestrację urządzeń przyłączonych do domeny jako obramowane w opisanych w [Konfigurowanie automatycznej rejestracji urządzeń z systemem Windows przyłączonych do domeny w usłudze Azure Active Directory](active-directory-device-registration-get-started.md) do obsługi następujących scenariuszy:

- [Dostępu warunkowego opartego na urządzeniu](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Enterprise roaming ustawień](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello dla firm](active-directory-azureadjoin-passport-deployment.md)


Ten dokument zawiera wskazówki dotyczące rozwiązywania problemów na jak rozwiązać potencjalne problemy. 

Rejestracja jest obsługiwana w systemie Windows 10 listopada 2015 aktualizacji i powyżej.  
Zalecamy używanie aktualizacji rozliczenia dotyczące włączania powyższych scenariuszy.

## <a name="step-1-retrieve-the-registration-status"></a>Krok 1: Pobierz stan rejestracji 

**Aby pobrać stan rejestracji:**

1. Otwórz wiersz polecenia jako administrator.

2. Typ **dsregcmd/status**



    +----------------------------------------------------------------------+
   | Stan urządzenia |+----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Nie DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 odcisk palca: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected dostawcy kryptograficznego platformy firmy Microsoft: tak KeySignTest:: należy uruchomić podniesione do testowania.
                  IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: tak DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
   | Stan użytkownika |+----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority: organizacje WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} AzureAdPrt (AzureAd): tak



## <a name="step-2-evaluate-the-registration-status"></a>Krok 2: Ocena stan rejestracji 

Przejrzyj następujące pola i upewnij się, że mają one oczekiwanych wartości:

### <a name="azureadjoined--yes"></a>AzureAdJoined: tak  

To pole wskazuje, czy urządzenie jest zarejestrowane w usłudze Azure AD. Jeśli wartość jest pokazywana jako "Nie", rejestracja nie została ukończona. 

**Możliwe przyczyny:**

- Nie można przeprowadzić uwierzytelniania komputera do rejestracji.

- W organizacji, które nie mogą zostać odnalezione przez komputer znajduje się serwer proxy HTTP

- Komputer można nawiązać połączenia z usługi Azure AD do uwierzytelniania lub Azure usługi rejestracji urządzeń do rejestracji

- Komputer może nie być w wewnętrznej sieci firmy lub w sieci VPN, z bezpośredniej procesów z wiersza do lokalnego kontrolera domeny usługi AD.

- Jeśli komputer ma modułu TPM, może być nieprawidłowy stan.

- Może być błąd konfiguracji usług wymienionych w dokumencie wcześniej należy zweryfikować ponownie. Typowe przykłady są:

    - Serwer federacyjny nie ma punktów końcowych protokołu WS-Trust włączone

    - Serwer federacyjny może uniemożliwić uwierzytelnianie ruchu przychodzącego z komputerów w sieci przy użyciu zintegrowanego uwierzytelniania systemu Windows.

    - Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje nazwę domeny zweryfikowane w usłudze Azure AD w lesie usługi AD, w którym komputer należy do

---

### <a name="domainjoined--yes"></a>DomainJoined: tak  

To pole wskazuje, czy urządzenie jest dołączane do lokalnej usługi Active Directory lub nie. Jeśli wartość jest pokazywana jako **nr**, urządzenie nie może automatycznie rejestru z usługą Azure AD. Najpierw należy sprawdzić, czy urządzenie łączy się w lokalnej usłudze Active Directory przed zarejestrowaniem w usłudze Azure AD. Jeśli szukasz przyłączania komputera do usługi Azure AD bezpośrednio, przejdź do Dowiedz się więcej na temat możliwości usługi Azure Active Directory Join.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: nie  

To pole wskazuje, czy urządzenie jest zarejestrowane w usłudze Azure AD, ale jako urządzenia osobiste (oznaczony jako dołączone do). Jeśli ta wartość powinna wyświetlić jako "Nie" na komputerze przyłączonym do domeny zarejestrowana w usłudze Azure AD, jednak jeśli będzie wyświetlana jako tak oznacza to, że przed zakończeniem rejestracji komputera dodano konto służbowe. W takim przypadku konto zostanie zignorowana, jeśli używana wersja rocznicy aktualizacji systemu Windows 10 (1607 po WinVer uruchomione polecenie w oknie "Uruchom" lub okno wiersza polecenia).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: Tak i AzureADPrt: tak
  
Zawierają one czy użytkownik został pomyślnie uwierzytelniony za pomocą usługi Azure AD po zalogowaniu się do urządzenia. Jeśli wykazują "Nie" możliwe przyczyny są następujące:

- Klucz magazynu zły (STK) w moduł TPM skojarzoną z tym urządzeniem rejestracji (wyboru KeySignTest uruchomionej z podwyższonym poziomem uprawnień).

- Alternatywnego Identyfikatora logowania

- Nie można odnaleźć serwera HTTP Proxy

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji, zobacz [automatycznej rejestracji urządzeń — często zadawane pytania](active-directory-device-registration-faq.md) 