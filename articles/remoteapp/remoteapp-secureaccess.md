---
title: "aaaSecuring dostępu tooAzure RemoteApp i | Dokumentacja firmy Microsoft"
description: "Dowiedz się jak bezpieczny dostęp tooAzure RemoteApp przy użyciu dostępu warunkowego w usłudze Azure Active Directory"
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 98dfe69e2f5fa5014b6eb3157e01f131c287134d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-remoteapp-and-beyond"></a>Zabezpieczanie dostępu tooAzure RemoteApp i nowszych
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

W tym artykule, firma Microsoft zapewni omówienie jak administrator może skonfigurować kanał bezpieczny dostęp, począwszy od użytkownika końcowego hello, za pośrednictwem usługi Azure RemoteApp i kończąc bezpiecznych zasobów takich jak bazy danych SQL lub innego zaplecza aplikacji. Celem Hello jest toomake się upewnić, że tylko autoryzowanym użytkownikom, który hello spotkania potrzeby warunki mają dostęp do zdalnego aplikacji i który hello bezpiecznego zaplecza można uzyskać tylko z hello pod kontrolą środowiska usługi Azure RemoteApp, a nie z innych lokalizacji.

Istnieją 3 głównych obszarów Witaj, Administratorze musi toolook na:

![Zagadnienia dostępu warunkowego w usłudze Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

Poniżej pytania toothese informacji i odpowiedzi.

## <a name="who-can-access-hello-collection"></a>Kto ma dostęp do kolekcji hello?
Hello administrator wybiera hello użytkowników, którzy mogą uzyskiwać dostęp do aplikacji zdalnego w kolekcji hello. Możesz użyć roboczych usługi Azure Active Directory (Azure AD) lub kont służbowych (wcześniej nazywane, "konta organizacyjne") lub konta Microsoft (np. @outlook.com). Większość scenariuszy przedsiębiorstwa za pomocą kont usługi Azure AD; pozwala korzystać z funkcji dostępu warunkowego, omówiono w dalszej części, a są również hello wybór tylko dla kolekcji przyłączonych do domeny. Witaj dalszej części artykułu hello przyjęto założenie, że używasz konta usługi Azure AD z usługą Azure RemoteApp.

**Co mamy osiągnąć:**

Przy użyciu tooAzure dostępu toocontrol kont usługi Azure AD, które RemoteApp daje dwie czynności:

1. Zawsze wiedzieć, kto ma dostęp do powitalne połączyć się z aplikacji, które firma Microsoft został opublikowany i dostęp do wszelkich zapleczy tych aplikacji.
2. Sterować hello podstawowej usługi Azure AD, można utworzyć i usuwania kont użytkowników, zestaw zasad haseł, użyć uwierzytelniania wieloskładnikowego, itd. 

## <a name="how-is-hello-collection-accessed-from-where"></a>Jak kolekcji hello jest dostępny? Gdzie?
Często Administratorzy mają toodefine zasady do uzyskiwania dostępu do środowisku publiczny internetowy, takich jak usługi Azure RemoteApp. Na przykład mają tooensure, że użytkownicy uzyskujący dostęp do środowiska hello poza siecią firmową hello mają dostęp toogain uwierzytelnianie wieloskładnikowe (MFA) toouse; lub prawdopodobnie powinien zostać całkowicie zablokowany.

Administratorzy usługi Azure RemoteApp używać funkcji hello dostępne za pośrednictwem zasad dostępu warunkowego tooset Azure AD Premium do środowiska usługi Azure RemoteApp. Można również użyć sformatowanego raportowania i alertów toomonitor funkcje jak środowisko hello jest dostępny.

### <a name="how-tooset-up-conditional-access-for-azure-remoteapp"></a>Jak tooset dostępu warunkowego dla usługi Azure RemoteApp
Możemy toowalk będzie za pośrednictwem przykładowy scenariusz — hello Azure RemoteApp administrator chce tooblock dostępu toohello środowiska, gdy użytkownicy znajdują się poza siecią firmową hello.

> [!NOTE]
> Przyjęto założenie, uaktualniono usługi Azure AD toohello warstwy Premium i utworzeniu co najmniej jedną kolekcję usługi Azure RemoteApp.
> 
> 

1. W portalu Azure kliknij hello **usługi Active Directory** kartę. Następnie kliknij przycisk hello katalogu będzie tooconfigure.
   
   Pamiętaj: Dostęp warunkowy jest właściwością katalogu, a nie usługi Azure RemoteApp, więc cała konfiguracja odbywa się na poziomie katalogu hello. Oznacza to również potrzebne toobe hello katalogu administratora toomake tych zmian.
2. Kliknij przycisk **aplikacji**, a następnie kliknij przycisk **funkcji RemoteApp systemu Microsoft Azure** tooset dostępu warunkowego. Należy pamiętać, że można skonfigurować dostęp warunkowy dla każdej aplikacji "oprogramowanie jako usługa" w katalogu oddzielnie.
   ![Konfigurowanie dostępu warunkowego dla usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. Na powitania **Konfiguruj** ustaw **Włącz zasady dostępu** tooON.
   ![Włącz zasady dostępu do usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. Teraz można skonfigurować różne zasady i określ, kto tooapply ich do:
   
   1. Wybierz **blokowanie dostępu, gdy nie w pracy** toocompletely uniemożliwić użytkownikom dostęp do usługi Azure RemoteApp poza hello środowiska sieciowego możesz określić.
   2. Kliknij opcję hello poniżej toodefine hello zakresów adresów IP stanowią "zaufanej sieci." Wszystko poza te zostaną odrzucone.
5. Przetestować konfigurację przez uruchamianie powitania klienta usługi Azure RemoteApp z adresu IP poza zakres hello. Po zalogowaniu się przy użyciu poświadczeń usługi Azure AD powinien zostać wyświetlony komunikat podobny do tego:

![Odmowa dostępu tooAzure programów RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>Funkcje późniejszego dostępu warunkowego
Zespół usługi Azure Active Directory Hello pracuje nad nowych funkcji dostępu warunkowego. Administratorzy będą mogli toocreate nowych typów reguł poza reguły na podstawie lokalizacji sieciowej. Publicznej wersji zapoznawczej funkcji hello powinna być wkrótce dostępna.

### <a name="how-toomonitor-access-tooazure-remoteapp"></a>Jak toomonitor dostępu tooAzure programów RemoteApp
Toouse wspaniałych funkcji równolegle z dostępu warunkowego jest funkcja raportowania hello Azure Active Directory Premium. Można użyć toomonitor raportów, który uzyskuje dostęp do środowiska i wykrywać wszelkie podejrzane działania.

Na przykład można wyświetlić nazwy hello hello użytkowników, którzy dostęp do usługi Azure RemoteApp, ile razy go jak i kiedy.

1. W portalu Azure kliknij **usługi Active Directory**, a następnie kliknij przycisk katalogu.
2. Przejdź toohello **raporty** kartę.
3. Wybierz z listy hello raportów **użycia aplikacji** w obszarze **zintegrowanych aplikacji**.
   
   Zobaczysz niektórych zagregowanych danych statystycznych dla usługi Azure RemoteApp. 
   ![Zagregowane Statystyka dostępu do usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Kliknij przycisk informacje o tooreveal aplikacji hello o użytkowników uzyskujących dostęp do usługi Azure RemoteApp.
   ![Statystyka dostępu użytkownika usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>Podsumowanie
Z usługi Azure Active Directory Premium można skonfigurować reguły tooAzure RemoteApp dostępu (i innego oprogramowania jako aplikacje usługi dostępne za pośrednictwem usługi Azure AD). Reguły są obecnie ograniczone toonetwork zasady na podstawie lokalizacji, ale zostaną w przyszłości hello rozszerzone tooother aspekty zarządzania przedsiębiorstwem.

Usługi Azure AD Premium oferuje również raportowania i monitorowania możliwości, które dalsze rozszerzanie kontroli Witaj, Administratorze hello ma w swoim środowisku usługi Azure RemoteApp.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>Jak utworzyć się, że moje bezpiecznego zasób jest dostępny tylko w mojej środowiska usługi Azure RemoteApp?
W poprzednich sekcjach tego artykułu firma Microsoft skupia się na zabezpieczania środowiska usługi Azure RemoteApp toohello dostępu. Firma Microsoft ma osiągnąć który, wybierając hello użytkowników, którzy mają prawa dostępu i konfigurowanie kontroli toofurther reguły dostępu jak wykorzystują hello usługi.

Typowy scenariusz w przypadku wdrożeń usługi Azure RemoteApp jest, zdalnych aplikacji hello potrzeby toocommunicate z zasobem zaplecza, na przykład bazy danych SQL. Ten zasób jest obsługiwana lokalnie (np. w sieci firmowej) lub w chmurze hello (np. w usłudze Azure IaaS). Administratorzy często mają toomake się upewnić, że hello zaplecza zasobów można uzyskać tylko przez aplikacje wdrażane za pomocą usługi Azure RemoteApp, a nie na przykład przez aplikację do uruchamiania bezpośrednio na komputerze użytkownika i uzyskiwanie dostępu za pośrednictwem publicznej sieci Internet. Usługa Azure RemoteApp występuje często hello centralnie zarządzanych i zabezpieczonym środowisku i w związku z tym hello ścieżki tylko za pomocą którego użytkownicy powinna interakcji z hello zasobów wewnętrznych.

rozwiązanie Hello jest tooplace zarówno hello środowiska usługi Azure RemoteApp i hello bezpiecznych zasobów w hello sieci wirtualnych tego samego Azure (VNET). Jeśli zasób hello jest w innej lokacji, może nawiązać połączenie sieci VPN typu lokacja lokacja, na przykład toocreate centrum danych Azure hello rozszerzania sieci wirtualnej i powitania klienta w środowisku lokalnym.

Usługa Azure RemoteApp obsługuje dwa typy wdrożeń kolekcji, w którym można podać własne sieci Wirtualnej:

* Non przyłączonych do domeny: aplikacji hello będzie mieć "procesów w wierszu" z hello inne zasoby w hello sieci Wirtualnej. Na przykład może to być tooconnect używane aplikacje tooa SQL bazy danych, która używa uwierzytelniania programu SQL (aplikacje uwierzytelniania użytkownika hello bezpośrednio hello bazy danych)
* Przyłączonych do domeny: hello maszyn wirtualnych używanej przez usługę Azure RemoteApp są tooa dołączonego do kontrolera domeny w hello sieci Wirtualnej. Jest to przydatne, gdy aplikacje hello muszą tooauthenticate na kontrolerze domeny systemu Windows w kolejności tooget dostępu tooa zaplecza zasobów.
  ![Kolekcja przyłączonych do domeny w usłudze Azure RemoteApp](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-toocreate-a-secure-connection-between-azure-and-my-on-premises-environment"></a>Jak toocreate bezpiecznego połączenia między Azure i Moje w środowisku lokalnym
Dostępnych jest kilka opcji konfiguracji podłączania środowiska Azure i lokalnymi. Omówienie opcji hello jest dostępnych tutaj.

Z usługą Azure RemoteApp muszą tooconfigure najpierw sieci wirtualnej, a następnie użyć podczas procesu tworzenia hello kolekcji. 

## <a name="hello-complete-solution"></a>Witaj kompletnego rozwiązania
Poniższy diagram Hello zawiera hello kompletnego rozwiązania, gdzie nawiązaliśmy kanał bezpieczny dostęp z hello użytkownika końcowego, za pomocą usługi Azure RemoteApp (usługa ARA), do hello wewnętrznej bazy danych zasobów.
![Zabezpieczanie usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png) w etapie 1 możemy wybranych użytkowników hello i utworzyć reguły dostępu, które kontrolują, jak można uzyskać dostępu do ARA. W poniższym przykładzie hello możemy tylko Zezwól na dostęp dla użytkowników pracujących w sieci firmowej hello. Niezgodne użytkownicy nie będą w stanie tooaccess hello ARA środowiska.
Na etapie 2 Firma Microsoft ma uwidoczniony hello zasobów w wewnętrznej bazie danych tylko za pośrednictwem hello konfigurację sieci wirtualnej lub sieć VPN, która sterować. Usługa Azure RemoteApp została umieszczona w hello sam sieci wirtualnej. wynik końcowy Hello jest, że hello zasobów można uzyskać tylko za pośrednictwem środowiska ARA hello.

