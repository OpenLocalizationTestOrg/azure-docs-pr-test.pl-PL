---
title: "aaaPublish Pulpit zdalny przy użyciu serwera Proxy aplikacji usługi Azure AD | Dokumentacja firmy Microsoft"
description: "Obejmuje hello podstaw łączniki serwera Proxy aplikacji usługi Azure AD."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a>Publikowanie pulpitu zdalnego z serwerem Proxy aplikacji usługi Azure AD

W tym artykule opisano sposób toodeploy pulpitu usługi zdalnego (RDS) z serwera Proxy aplikacji tak, aby użytkownicy zdalni nadal mogą uzyskać wydajność.

Witaj, przeznaczone odbiorcami w tym artykule są:
- Bieżącego serwera Proxy aplikacji usługi Azure AD klientów, którzy mają więcej użytkowników końcowych tootheir aplikacji toooffer przez publikowanie aplikacji lokalnych za pomocą usług pulpitu zdalnego.
- Bieżący usług pulpitu zdalnego klientów, którzy mają tooreduce hello ataku ich wdrażania za pomocą serwera Proxy aplikacji usługi Azure AD. W tym scenariuszu zapewnia ograniczony zestaw weryfikacji dwuetapowej i tooRDS kontrolę dostępu warunkowego.

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a>Jak serwer Proxy aplikacji pasuje hello standardowe wdrożenie usług pulpitu zdalnego

Standardowe wdrożenie usług pulpitu zdalnego obejmuje różnych usług ról usług pulpitu zdalnego w systemie Windows Server. Spojrzenie na powitania [architektury usług pulpitu zdalnego](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture), istnieje wiele opcji wdrażania. Witaj najbardziej znaczącej różnicy między hello [wdrożenie usług pulpitu zdalnego z serwera Proxy aplikacji usługi Azure AD](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) (wyświetlone czcionką powitania po diagram) i hello innych opcji wdrażania jest w tym scenariuszu serwer Proxy aplikacji hello stałe ruchu wychodzącego połączenie z usługą łącznika hello serwera hello. Inne wdrożenia, pozostaw otwarte połączenia przychodzące za pośrednictwem usługi równoważenia obciążenia.

![Aplikacja serwera Proxy znajduje się między hello wirtualna usług pulpitu zdalnego i hello publicznej sieci internet](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

We wdrożeniu usług pulpitu zdalnego hello roli usług pulpitu zdalnego w sieci Web i roli bramy usług pulpitu zdalnego hello uruchamiać na maszynach skierowane do Internetu. Te punkty końcowe są widoczne dla hello z następujących powodów:
- Usług pulpitu zdalnego w sieci Web zapewnia użytkownikowi hello toosign publiczny punkt końcowy w i widoku hello różnych aplikacji lokalnych i komputery stacjonarne, które mogą uzyskiwać dostęp do. Po wybraniu zasobu, połączenie RDP jest tworzony za pomocą natywnej aplikacji hello na powitania systemu operacyjnego.
- Brama usług pulpitu zdalnego wejścia obraz powitania, gdy użytkownik uruchamia połączenie RDP hello. Hello bramy usług pulpitu zdalnego obsługuje ruch RDP hello szyfrowane przechodzących przez hello Internet i tłumaczy go toohello, który lokalnego serwera, który hello użytkownik nawiązuje połączenie. W tym scenariuszu hello hello ruchu, który odbiera bramy usług pulpitu zdalnego, pochodzi z powitania serwera Proxy aplikacji usługi Azure AD.

>[!TIP]
>Jeśli nie zostało to jeszcze wdrożone RDS przed lub chcesz uzyskać więcej informacji, aby rozpocząć, Dowiedz się, jak za[bezproblemowo wdrożenia usług pulpitu zdalnego z usługi Azure Resource Manager i portalu Azure Marketplace](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure).

## <a name="requirements"></a>Wymagania

- Zarówno hello sieci Web usług pulpitu zdalnego i Brama usług pulpitu zdalnego punkty końcowe muszą znajdować się na hello sam komputera i z typowy katalog główny. Sieci Web usług pulpitu zdalnego i Brama usług pulpitu zdalnego zostanie opublikowany jako pojedynczą aplikacją, może mieć pojedynczy jednokrotnego między aplikacjami hello dwa.

- Ma już [wdrożone RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure), i [włączono serwer Proxy aplikacji](active-directory-application-proxy-enable.md).

- W tym scenariuszu przyjęto go użytkownikom końcowym za pomocą programu Internet Explorer na pulpitach systemu Windows 7 lub Windows 10, które łączenie się za pośrednictwem strony sieci Web usług pulpitu zdalnego hello. Jeśli potrzebujesz toosupport innych systemów operacyjnych, zobacz [obsługę innych konfiguracji klienta](#support-for-other-client-configurations).

  >[!NOTE]
  >Aktualizacja systemu Windows 10 twórca nie jest obecnie obsługiwane.

- W programie Internet Explorer Włącz hello dodatek ActiveX usług pulpitu zdalnego.

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a>Wdrażanie hello wspólnego scenariusza usług pulpitu zdalnego i serwera Proxy aplikacji

Po skonfigurowaniu usługi pulpitu zdalnego i aplikacji serwera Proxy Azure AD dla danego środowiska, należy wykonać hello kroki toocombine hello dwa rozwiązania. Te kroki przeprowadzenie publikowania aplikacji hello dwa udostępnianych w sieci web usług pulpitu zdalnego punkty końcowe (sieci Web usług pulpitu zdalnego i Brama usług pulpitu zdalnego), a następnie kierowanie ruchu w sieci toogo usług pulpitu zdalnego za pośrednictwem serwera Proxy aplikacji.

### <a name="publish-hello-rd-host-endpoint"></a>Publikowanie hello usług pulpitu zdalnego hosta z punktu końcowego

1. [Opublikuj nową aplikację serwera Proxy aplikacji](application-proxy-publish-azure-portal.md) z hello następujące wartości:
   - Wewnętrzny adres URL: https://\<rdhost\>.com /, gdzie \<rdhost\> jest hello typowy katalog główny, który sieci Web usług pulpitu zdalnego i Brama usług pulpitu zdalnego udziału.
   - Zewnętrzny adres URL: To pole jest wypełniane automatycznie na podstawie nazwy hello aplikacji hello, ale można go zmodyfikować. Użytkownicy przechodzą toothis URL przy uzyskiwaniu dostępu do usług pulpitu zdalnego.
   - Metoda uwierzytelniania wstępnego: Azure Active Directory
   - Tłumaczenie nagłówków adresu URL: nie
2. Przypisywanie użytkowników toohello opublikowana aplikacja usług pulpitu zdalnego. Upewnij się, że wszystkie mają tooRDS dostępu zbyt.
3. Pozostaw hello pojedynczej logowania jednokrotnego metody dla aplikacji hello jako **usługi Azure AD rejestracji jednokrotnej wyłączone**. Użytkownicy są proszeni tooauthenticate po tooAzure AD i raz tooRD sieci Web, ale ma pojedynczego logowania jednokrotnego tooRD bramy.
4. Przejdź za**usługi Azure Active Directory** > **rejestracji aplikacji** > *aplikacji* > **ustawienia**.
5. Wybierz **właściwości** i hello aktualizacji **adres URL strony głównej** pola toopoint tooyour sieci Web usług pulpitu zdalnego w punkcie końcowym (takich jak https://\<rdhost\>.com/RDWeb).

### <a name="direct-rds-traffic-tooapplication-proxy"></a>Bezpośrednie RDS tooApplication ruch serwera Proxy

Połącz toohello wdrożenie usług pulpitu zdalnego jako administrator i Zmień nazwę serwera bramy usług pulpitu zdalnego hello hello wdrożenia. Dzięki temu, że połączenia przechodzą przez powitania serwera Proxy aplikacji usługi Azure AD.

1. Połącz serwer RDS toohello hello roli Broker połączeń usług pulpitu zdalnego.
2. Uruchom **Menedżera serwera**.
3. Wybierz **usług pulpitu zdalnego** z okienka hello powitania po lewej stronie.
4. Wybierz **omówienie**.
5. W sekcji Przegląd wdrożenia hello, zaznacz hello menu rozwijane i wybierz polecenie **Edytuj właściwości wdrożenia**.
6. Na karcie bramy usług pulpitu zdalnego hello, zmień hello **nazwy serwera** toohello pola zewnętrznego adresu URL dla punktu końcowego hosta hello usług pulpitu zdalnego na serwerze Proxy aplikacji.
7. Zmień hello **logowania — metoda** pola zbyt**uwierzytelniania hasła**.

  ![Ekran właściwości wdrożenia na usługi pulpitu zdalnego](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. Dla każdej kolekcji uruchom następujące polecenie hello. Zastąp  *\<yourcollectionname\>*  i  *\<proxyfrontendurl\>*  odpowiednimi informacjami. To polecenie umożliwia logowanie jednokrotne między sieci Web usług pulpitu zdalnego i Brama usług pulpitu zdalnego oraz optymalizację wydajności:

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   **Na przykład:**
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. Modyfikacja hello tooverify hello niestandardowe właściwości protokołu RDP, a także zawartość pliku RDP hello widoku, które zostaną pobrane z RDWeb dla tej kolekcji, uruchom następujące polecenie hello:
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

Teraz, gdy skonfigurowano pulpitu zdalnego, serwer Proxy aplikacji usługi Azure AD przejmuje jako składnik internetowy hello usług pulpitu zdalnego. Możesz usunąć hello innych publiczne punkty końcowe skierowane do Internetu na maszynach w sieci Web usług pulpitu zdalnego i Brama usług pulpitu zdalnego.

## <a name="test-hello-scenario"></a>Scenariusz hello testów

Przetestuj hello scenariusza z programu Internet Explorer na komputerze 10 lub Windows 7.

1. Zewnętrzny adres URL toohello skonfigurowaniu go lub Znajdź aplikacji hello [panelu MyApps](https://myapps.microsoft.com).
2. Zostanie wyświetlona prośba tooAzure tooauthenticate usługi Active Directory. Użyj konta przypisania toohello aplikacji.
3. Zostanie wyświetlona prośba tooRD tooauthenticate sieci Web.
4. Po pomyślnym uwierzytelniania usług pulpitu zdalnego, możesz wybrać hello pulpitu lub aplikacji i rozpocząć pracę.

## <a name="support-for-other-client-configurations"></a>Obsługę innych konfiguracji klienta

Konfiguracja Hello opisane w tym artykule jest przeznaczony dla użytkowników na Windows 7 lub Windows 10, w przypadku programu Internet Explorer oraz hello dodatek ActiveX usług pulpitu zdalnego. Jeśli potrzebujesz, jednak można obsługiwać innych systemów operacyjnych i przeglądarek. Różnica Hello jest hello metodę uwierzytelniania, którego używasz.

| Metoda uwierzytelniania | Obsługiwany klient konfiguracji |
| --------------------- | ------------------------------ |
| Wstępne uwierzytelnianie    | Windows 7/10 przy użyciu programu Internet Explorer + dodatek ActiveX usług pulpitu zdalnego |
| Przekazywanie | Inne obsługującego aplikacji pulpitu zdalnego firmy Microsoft hello systemu operacyjnego |

Przepływ uwierzytelniania wstępnego Hello oferuje więcej korzyści w zakresie zabezpieczeń niż hello passthrough przepływu. Przy użyciu wstępnego uwierzytelniania można wykorzystać funkcje uwierzytelniania usługi Azure AD, takie jak logowanie jednokrotne dostępu warunkowego i weryfikację dwuetapową dla zasobów lokalnych. Można również upewnij się, że tylko uwierzytelnianego osiągnie ruchu w sieci.

uwierzytelnianie przechodnie toouse, są tylko dwie zmiany toohello czynności opisane w tym artykule:
1. W [publikowania hello usług pulpitu zdalnego hosta z punktu końcowego](#publish-the-rd-host-endpoint) kroku 1, ustaw hello metoda uwierzytelniania wstępnego za**Passthrough**.
2. W [bezpośredniego RDS ruchu tooApplication Proxy](#direct-rds-traffic-to-application-proxy), całkowicie pominąć krok 8.

## <a name="next-steps"></a>Następne kroki

[Włącz tooSharePoint dostępu zdalnego z serwera Proxy aplikacji usługi Azure AD](application-proxy-enable-remote-access-sharepoint.md)  
[Zagadnienia dotyczące zabezpieczeń do uzyskiwania dostępu do aplikacji zdalnie przy użyciu serwera Proxy aplikacji usługi Azure AD](application-proxy-security-considerations.md)
