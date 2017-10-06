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
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a>Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD — Windows 10 i Windows Server 2016

Ten temat jest toohello dotyczy następujących klientów:

-   Windows 10
-   Windows Server 2016

Dla innych klientów z systemem Windows, temacie [Rozwiązywanie problemów z automatyczną rejestrację domeny przyłączone tooAzure komputery AD dla klientów niższych poziomów Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).

W tym temacie założono, że skonfigurowano automatyczną rejestrację urządzeń przyłączonych do domeny jako obramowane w opisanych w [jak tooconfigure automatycznej rejestracji systemu Windows przyłączone do domeny urządzenia w usłudze Azure Active Directory](active-directory-device-registration-get-started.md) Witaj toosupport następujące scenariusze:

- [Dostępu warunkowego opartego na urządzeniu](active-directory-conditional-access-automatic-device-registration-setup.md)

- [Enterprise roaming ustawień](active-directory-windows-enterprise-state-roaming-overview.md)

- [Windows Hello dla firm](active-directory-azureadjoin-passport-deployment.md)


Ten dokument zawiera wskazówki dotyczące rozwiązywania problemów w sposób tooresolve potencjalne problemy. 

Witaj rejestracja jest obsługiwana w systemie Windows hello aktualizacji 10 listopada 2015 i powyżej.  
Zalecamy używanie hello aktualizacji rocznicy umożliwiających hello powyższych scenariuszy.

## <a name="step-1-retrieve-hello-registration-status"></a>Krok 1: Pobierz hello stan rejestracji 

**Stan rejestracji hello tooretrieve:**

1. Witaj Otwórz wiersz polecenia jako administrator.

2. Typ **dsregcmd/status**



    +----------------------------------------------------------------------+
   | Stan urządzenia |+----------------------------------------------------------------------+
    
        AzureAdJoined : YES
     EnterpriseJoined: Nie DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 odcisk palca: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected dostawca usług kryptograficznych platformy firmy Microsoft: tak KeySignTest:: należy uruchomić z podwyższonym poziomem uprawnień tootest.
                  IDP: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ == JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn: ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn: ms-drs:enterpriseregistration.windows.net DomainJoined: tak DomainName: CONTOSO
    
    +----------------------------------------------------------------------+
   | Stan użytkownika |+----------------------------------------------------------------------+
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    WamDefaultAuthority: organizacje WamDefaultId: https://login.microsoft.com WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} AzureAdPrt (AzureAd): tak



## <a name="step-2-evaluate-hello-registration-status"></a>Krok 2: Ocena hello stan rejestracji 

Przejrzyj hello kolejnych pól i upewnij się, że hello oczekiwanych wartości:

### <a name="azureadjoined--yes"></a>AzureAdJoined: tak  

To pole wskazuje, czy hello urządzenie jest zarejestrowane w usłudze Azure AD. Jeśli wartość hello jest pokazywana jako "Nie", rejestracja nie została ukończona. 

**Możliwe przyczyny:**

- Uwierzytelnianie komputera hello rejestracji nie powiodło się.

- W organizacji hello, które nie może zostać odnalezione przez komputer hello jest serwer proxy HTTP

- Hello komputerem można nawiązać połączenia z usługi Azure AD do uwierzytelniania lub Azure usługi rejestracji urządzeń do rejestracji

- Witaj komputer może nie być w sieci wewnętrznej hello organizacji lub sieci VPN z tooan bezpośredniego wiersza z procesów lokalnych kontroler domeny usługi AD.

- Jeśli komputer hello ma modułu TPM, może być nieprawidłowy stan.

- Może być błąd konfiguracji usług wymienionych w dokumencie hello wcześniej trzeba tooverify ponownie. Typowe przykłady są:

    - Serwer federacyjny nie ma punktów końcowych protokołu WS-Trust włączone

    - Serwer federacyjny może uniemożliwić uwierzytelnianie ruchu przychodzącego z komputerów w sieci przy użyciu zintegrowanego uwierzytelniania systemu Windows.

    - Nie ma żadnego obiektu punktu połączenia usługi, który wskazuje tooyour zweryfikowaną nazwę domeny w usłudze Azure AD w lesie hello AD, której należy komputer hello

---

### <a name="domainjoined--yes"></a>DomainJoined: tak  

To pole zawiera, czy urządzenie hello jest tooan dołączonego do lokalnej usługi Active Directory. Jeśli wartość hello jest pokazywana jako **nr**, hello urządzenia nie można automatycznie rejestru z usługą Azure AD. Najpierw sprawdź toohello sprzężenia urządzenie tym hello lokalnej usługi Active Directory przed zarejestrowaniem w usłudze Azure AD. Jeśli szukasz dołączenie hello tooAzure komputer AD bezpośrednio, przejdź tooLearn o możliwości usługi Azure Active Directory Join.

---

### <a name="workplacejoined--no"></a>WorkplaceJoined: nie  

To pole wskazuje, czy hello urządzenie jest zarejestrowane w usłudze Azure AD, ale jako urządzenia osobiste (oznaczony jako dołączone do). Czy ta wartość powinien zawierać jako "Nie" przyłączony do domeny komputera zarejestrowane w usłudze Azure AD, jednak będzie wyświetlana jako tak oznacza, że konta firmowego lub szkolnego był dodany przed toohello komputera Kończenie rejestracji. W takim przypadku hello konto zostanie zignorowana, jeśli przy użyciu hello rocznicy zaktualizowanej wersji systemu Windows 10 (1607 po uruchomi polecenie WinVer hello w Witaj, "Uruchom" lub w oknie wiersza polecenia).

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a>WamDefaultSet: Tak i AzureADPrt: tak
  
Zawierają one się, że użytkownik hello został pomyślnie uwierzytelniony tooAzure AD po zarejestrowaniu się w urządzeniu toohello. Jeśli występują "Nie" hello Oto możliwe przyczyny:

- Klucz magazynu zły (STK) w moduł TPM skojarzone z urządzeniem hello rejestracji (hello wyboru KeySignTest uruchomionej z podwyższonym poziomem uprawnień).

- Alternatywnego Identyfikatora logowania

- Nie można odnaleźć serwera HTTP Proxy

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji, zobacz hello [automatycznej rejestracji urządzeń — często zadawane pytania](active-directory-device-registration-faq.md) 
