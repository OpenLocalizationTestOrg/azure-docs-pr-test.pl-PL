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
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a>Rozwiązywanie problemów z hybrydowe usługi Azure Active Directory przyłączone do urządzeń z systemem Windows 10 i Windows Server 2016 

Ten temat jest toohello dotyczy następujących klientów:

-   Windows 10
-   Windows Server 2016

Dla innych klientów z systemem Windows, temacie [niższego poziomu urządzeniach przyłączonych do rozwiązywania problemów hybrydowe usługi Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-legacy.md).

W tym temacie założono, że [urządzeniach przyłączonych do skonfigurowanego hybrydowe usługi Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport następujące scenariusze:

- Dostępu warunkowego opartego na urządzeniu

- [Enterprise roaming ustawień](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello dla firm](active-directory-azureadjoin-passport-deployment.md)


Ten dokument zawiera wskazówki dotyczące rozwiązywania problemów w sposób tooresolve potencjalne problemy. 


Dla systemu Windows 10 i Windows Server 2016 hybrydowe usługi Azure Active Directory join obsługuje hello systemu Windows 10 listopada 2015 aktualizacji i powyżej. Firma Microsoft zaleca użycie hello rocznicy aktualizacji.

## <a name="step-1-retrieve-hello-join-status"></a>Krok 1: Pobrać hello sprzężenia stanu 

**Stan sprzężenia hello tooretrieve:**

1. Witaj Otwórz wiersz polecenia jako administrator

2. Typ **dsregcmd/status**



    +----------------------------------------------------------------------+
   | Stan urządzenia |+----------------------------------------------------------------------+
    
        AzureAdJoined: YES
     EnterpriseJoined: Nie DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 odcisk palca: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected dostawca usług kryptograficznych platformy firmy Microsoft: tak KeySignTest:: należy uruchomić z podwyższonym poziomem uprawnień tootest.
                  IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/ msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https:// Portal.Manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https:// enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-usługi rejestracji urządzeń: enterpriseregistration.Windows.NET DomainJoined: nazwadomeny tak: CONTOSO
    
    +----------------------------------------------------------------------+
   | Stan użytkownika |+----------------------------------------------------------------------+
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    WamDefaultAuthority: organizacje WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} AzureAdPrt (AzureAd): tak



## <a name="step-2-evaluate-hello-join-status"></a>Krok 2: Ocena hello sprzężenia stanu 

Przejrzyj hello kolejnych pól i upewnij się, że hello oczekiwanych wartości:

### <a name="azureadjoined--yes"></a>AzureAdJoined: tak  

To pole wskazuje, czy urządzenie hello jest połączony z usługą Azure AD. Jeśli wartość hello jest **nr**, hello tooAzure sprzężenia AD nie została jeszcze ukończona. 

**Możliwe przyczyny:**

- Nie można przeprowadzić uwierzytelniania komputera hello w celu utworzenia sprzężenia.

- W organizacji hello, które nie może zostać odnalezione przez komputer hello jest serwer proxy HTTP

- Hello komputera nie można osiągnąć tooauthenticate usługi Azure AD lub Azure usługi rejestracji urządzeń do rejestracji

- Witaj komputer może nie być w sieci wewnętrznej hello organizacji lub sieci VPN z tooan bezpośredniego wiersza z procesów lokalnych kontroler domeny usługi AD.

- Jeśli komputer hello ma modułu TPM, może być nieprawidłowy stan.

- Może być błąd konfiguracji w usługach hello zauważyć w dokumencie hello wcześniej trzeba tooverify ponownie. Typowe przykłady są:

    - Serwer federacyjny nie ma punktów końcowych protokołu WS-Trust włączone

    - Serwerze federacyjnym nie zezwala na uwierzytelnianie ruchu przychodzącego z komputerów w sieci przy użyciu zintegrowanego uwierzytelniania systemu Windows.

    - Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje tooyour zweryfikowaną nazwę domeny w usłudze Azure AD w lesie hello AD, której należy komputer hello

---

### <a name="domainjoined--yes"></a>DomainJoined: tak  

To pole wskazuje, czy urządzenie hello jest dołączane tooan lokalnej usługi Active Directory lub nie. Jeśli wartość hello jest **nr**, hello urządzenia nie można wykonać sprzężenia hybrydowej usługi Azure AD.  

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: nie  

To pole wskazuje, czy urządzenie hello jest zarejestrowane w usłudze Azure AD jako urządzenia osobiste (oznaczony jako *dołączonych do miejsca pracy*). Ta wartość powinna być **nr** na komputerze przyłączonym do domeny, który jest przyłączony do hybrydowej usługi Azure AD. Jeśli wartość hello jest **tak**, konta firmowego lub szkolnego dodano zakończenia wcześniejszych toohello hello hybrydowej usługi Azure AD join. W takim przypadku konto hello jest ignorowane w przypadku przy użyciu hello rocznicy zaktualizowanej wersji systemu Windows 10 (1607).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: Tak i AzureADPrt: tak
  
Te pola wskazują, czy użytkownik hello został pomyślnie uwierzytelniony tooAzure AD podczas rejestrowania się w urządzeniu toohello. Jeśli wartości hello są **nr**, może to być z powodu:

- Klucz magazynu zły (STK) w moduł TPM skojarzone z urządzeniem hello rejestracji (hello wyboru KeySignTest uruchomionej z podwyższonym poziomem uprawnień).

- Alternatywnego Identyfikatora logowania

- Nie można odnaleźć serwera HTTP Proxy

## <a name="next-steps"></a>Następne kroki

Odpowiedzi na pytania, zobacz hello [zarządzanie urządzeniami — często zadawane pytania](device-management-faq.md) 
