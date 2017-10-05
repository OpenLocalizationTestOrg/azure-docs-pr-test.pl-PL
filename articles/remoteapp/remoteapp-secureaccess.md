---
title: "Zabezpieczanie dostępu do usługi Azure RemoteApp, a poza | Dokumentacja firmy Microsoft"
description: "Dowiedz się jak bezpieczny dostęp do usługi Azure RemoteApp przy użyciu dostępu warunkowego w usłudze Azure Active Directory"
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
ms.openlocfilehash: 28ee4698515d11964e5371628d21dbc00687c861
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="securing-access-to-azure-remoteapp-and-beyond"></a>Zabezpieczanie dostępu do usługi Azure RemoteApp, a poza
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

W tym artykule, firma Microsoft zapewni omówienie jak administrator może skonfigurować kanał bezpieczny dostęp, począwszy od użytkownika końcowego, za pośrednictwem usługi Azure RemoteApp i kończąc bezpiecznych zasobów takich jak bazy danych SQL lub innego zaplecza aplikacji. Celem jest upewnienie się, że tylko autoryzowanym użytkownikom spełniające warunki żądany dostęp do zdalnego aplikacji i że bezpiecznego zaplecza można uzyskać tylko z kontrolą środowiska usługi Azure RemoteApp, a nie z innych lokalizacji.

Istnieją 3 główne obszary, które administrator musi przyjrzeć się:

![Zagadnienia dostępu warunkowego w usłudze Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

Odczytywanie informacji oraz odpowiedzi na te pytania.

## <a name="who-can-access-the-collection"></a>Kto ma dostęp do kolekcji?
Administrator wybiera użytkowników, którzy mogą uzyskiwać dostęp do aplikacji zdalnego w kolekcji. Możesz użyć roboczych usługi Azure Active Directory (Azure AD) lub kont służbowych (wcześniej nazywane, "konta organizacyjne") lub konta Microsoft (np. @outlook.com). Większość scenariuszy przedsiębiorstwa za pomocą kont usługi Azure AD; umożliwiają one korzystanie z dostępu warunkowego funkcji omówiono w dalszej części i są również jedyną dostępną dla kolekcji przyłączonych do domeny. Pozostałej części tego artykułu przyjęto założenie, że używasz konta usługi Azure AD z usługą Azure RemoteApp.

**Co mamy osiągnąć:**

Aby kontrolować dostęp do usługi Azure RemoteApp przy użyciu konta usługi Azure AD zapewnia nam dwie czynności:

1. Zawsze wiemy, kto ma dostęp do aplikacji, firma Microsoft został opublikowany i uzyskać dostępu do żadnego zapleczy nawiązać tych aplikacji.
2. Można utworzyć i usuwania kont użytkowników, zestaw zasad haseł, użyć uwierzytelniania wieloskładnikowego itp sterować podstawowej usługi Azure AD. 

## <a name="how-is-the-collection-accessed-from-where"></a>Jak kolekcji jest dostępny? Gdzie?
Często Administratorzy chcesz zdefiniować zasady do uzyskiwania dostępu do środowisku publiczny internetowy, takich jak usługi Azure RemoteApp. Na przykład chcą upewnić się, że użytkownicy uzyskujący dostęp do środowiska spoza sieci firmowej muszą używać uwierzytelniania wieloskładnikowego (MFA) w celu uzyskania dostępu; lub prawdopodobnie powinien zostać całkowicie zablokowany.

Administratorzy usługi Azure RemoteApp można użyć funkcji dostępnych za pośrednictwem usługi Azure AD Premium można ustawić zasady dostępu warunkowego dla swojego środowiska usługi Azure RemoteApp. Raportowanie i alerty funkcji zaawansowanych mogą również wykorzystać do monitorowania, jak jest uzyskiwany środowiska.

### <a name="how-to-set-up-conditional-access-for-azure-remoteapp"></a>Jak skonfigurować dostęp warunkowy dla usługi Azure RemoteApp
Zamierzamy przeprowadzenie przykładowy scenariusz — usługi Azure RemoteApp, administrator chce zablokować dostęp do środowiska, jeśli użytkownicy znajdują się poza siecią firmową.

> [!NOTE]
> Przyjęto założenie, uaktualniono do warstwy Premium usługi Azure AD i utworzeniu co najmniej jedną kolekcję usługi Azure RemoteApp.
> 
> 

1. W portalu Azure, kliknij **usługi Active Directory** kartę. Następnie kliknij katalog, który chcesz skonfigurować.
   
   Pamiętaj: Dostęp warunkowy jest właściwością katalogu, a nie usługi Azure RemoteApp, więc cała konfiguracja odbywa się na poziomie katalogu. Oznacza to również, że, musisz być administratorem katalogu, aby wprowadzić te zmiany.
2. Kliknij przycisk **aplikacji**, a następnie kliknij przycisk **funkcji RemoteApp systemu Microsoft Azure** do skonfigurowania dostępu warunkowego. Należy pamiętać, że można skonfigurować dostęp warunkowy dla każdej aplikacji "oprogramowanie jako usługa" w katalogu oddzielnie.
   ![Konfigurowanie dostępu warunkowego dla usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. Na **Konfiguruj** ustaw **Włącz zasady dostępu** na wartość on.
   ![Włącz zasady dostępu do usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. Teraz możesz skonfigurować różne zasady i określ, kto zastosować je do:
   
   1. Wybierz **blokowanie dostępu, gdy nie w pracy** Aby całkowicie uniemożliwić użytkownikom dostęp do usługi Azure RemoteApp poza środowisko sieciowe, należy określić.
   2. Kliknij opcję poniżej, aby zdefiniować zakresów adresów IP, które stanowią "zaufanej sieci." Wszystko poza te zostaną odrzucone.
5. Aby przetestować konfigurację, uruchamiania klienta usługi Azure RemoteApp z adresu IP spoza zakresu określona. Po zalogowaniu się przy użyciu poświadczeń usługi Azure AD powinien zostać wyświetlony komunikat podobny do tego:

![Odmowa dostępu do usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>Funkcje późniejszego dostępu warunkowego
Zespół usługi Azure Active Directory działa na nowych funkcji dostępu warunkowego. Administratorzy będą mogli tworzyć reguły na podstawie lokalizacji nowych typów reguł znajdujących się poza siecią. Publicznej wersji zapoznawczej nowych funkcji powinna być wkrótce dostępna.

### <a name="how-to-monitor-access-to-azure-remoteapp"></a>Jak monitorować dostęp do usługi Azure RemoteApp
Wspaniałych funkcji można używać równolegle z dostępu warunkowego jest funkcja raportowania usługi Azure Active Directory — wersja Premium. Możesz używać raportów do monitorowania, który uzyskuje dostęp do środowiska i wykrywać wszelkie podejrzane działania.

Na przykład widać nazwy użytkowników, którzy dostęp do usługi Azure RemoteApp, ile razy go jak i kiedy.

1. W portalu Azure kliknij **usługi Active Directory**, a następnie kliknij przycisk katalogu.
2. Przejdź do **raporty** kartę.
3. Wybierz z listy raportów **użycia aplikacji** w obszarze **zintegrowanych aplikacji**.
   
   Zobaczysz niektórych zagregowanych danych statystycznych dla usługi Azure RemoteApp. 
   ![Zagregowane Statystyka dostępu do usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Kliknij aplikację, aby wyświetlić informacje o użytkownikach, uzyskiwanie dostępu do usługi Azure RemoteApp.
   ![Statystyka dostępu użytkownika usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>Podsumowanie
Z usługi Azure Active Directory Premium można skonfigurować reguł dostępu do usługi Azure RemoteApp (i inne oprogramowanie jako usługa aplikacje dostępne za pośrednictwem usługi Azure AD). Reguły są obecnie ograniczone do zasad na podstawie lokalizacji sieciowej, ale w przyszłości będzie dotyczyć innych aspektów zarządzania przedsiębiorstwem.

Azure AD Premium oferuje również raportowania i monitorowania możliwości, które dalsze rozszerzanie kontroli administratora ma w swoim środowisku usługi Azure RemoteApp.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>Jak utworzyć się, że moje bezpiecznego zasób jest dostępny tylko w mojej środowiska usługi Azure RemoteApp?
W poprzednich sekcjach tego artykułu firma Microsoft skupia się na zabezpieczanie dostępu do środowiska usługi Azure RemoteApp. Firma Microsoft ma osiągnąć, który Wybieranie użytkowników, którzy mają prawa dostępu i konfigurując reguły dostępu, aby ściślej kontrolować sposób może korzystać z usługi.

Typowy scenariusz w przypadku wdrożeń usługi Azure RemoteApp jest zdalne aplikacje muszą komunikować się z zasobem zaplecza, na przykład bazy danych SQL. Ten zasób jest obsługiwana lokalnie (np. w sieci firmowej) lub w chmurze (np. w usłudze Azure IaaS). Administratorzy często chce mieć pewność, że zasób zaplecza można uzyskać tylko przez aplikacje wdrażane za pomocą usługi Azure RemoteApp, a nie na przykład przez aplikację do uruchamiania bezpośrednio na komputerze użytkownika i uzyskiwanie dostępu za pośrednictwem publicznej sieci Internet. Usługa Azure RemoteApp jest często postrzegane jako zabezpieczonych i centralnie zarządzanego środowiska i w związku z tym ścieżkę tylko za pomocą którego użytkownicy powinna korzystają z zasobów wewnętrznych.

Rozwiązaniem jest umieszczenie środowiska usługi Azure RemoteApp i bezpiecznych zasobów w tej samej Azure wirtualnych sieci (VNET). Jeśli zasób znajduje się w innej lokacji, można ustanowić połączenia sieci VPN lokacja lokacja, na przykład aby utworzyć sieć wirtualną spanning centrum danych platformy Azure i klienta w środowisku lokalnym.

Usługa Azure RemoteApp obsługuje dwa typy wdrożeń kolekcji, w którym można podać własne sieci Wirtualnej:

* Non przyłączonych do domeny: aplikacje mają "procesów w wierszu" innych zasobów w sieci Wirtualnej. Na przykład, to może służyć do połączenia aplikacji korzystającej z uwierzytelniania SQL bazy danych SQL (aplikacje uwierzytelnić użytkownika bezpośrednio w bazie danych)
* Przyłączonych do domeny: maszyn wirtualnych używanych przez usługę Azure RemoteApp są łączone z kontrolerem domeny w sieci Wirtualnej. Jest to przydatne, gdy potrzebne do uwierzytelnienia kontrolera domeny systemu Windows, aby można było uzyskać dostęp do zasobów wewnętrznych.
  ![Kolekcja przyłączonych do domeny w usłudze Azure RemoteApp](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-to-create-a-secure-connection-between-azure-and-my-on-premises-environment"></a>Jak utworzyć bezpiecznego połączenia między Azure i Moje w środowisku lokalnym
Dostępnych jest kilka opcji konfiguracji podłączania środowiska Azure i lokalnymi. Omówienie opcji jest dostępnych tutaj.

Z usługą Azure RemoteApp należy najpierw skonfigurować sieci wirtualnej, a następnie użyć go w trakcie procesu tworzenia Twojej kolekcji. 

## <a name="the-complete-solution"></a>Kompletne rozwiązanie
Na poniższym diagramie pokazano kompletnego rozwiązania, w którym nawiązaliśmy kanału bezpiecznego dostępu użytkownika końcowego za pośrednictwem usługi Azure RemoteApp (usługa ARA), do zasobów w wewnętrznej bazie danych.
![Zabezpieczanie usługi Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png) w etapie 1 możemy wybranych użytkowników i utworzyć reguły dostępu, które kontrolują, jak można uzyskać dostępu do ARA. W poniższym przykładzie mamy tylko Zezwalaj na dostęp dla użytkowników pracujących w sieci firmowej. Niezgodne użytkownicy nie będą mogli uzyskiwać dostęp do środowiska ARA na wszystkich.
Na etapie 2 Firma Microsoft ma uwidoczniony zasobów w wewnętrznej bazie danych tylko za pośrednictwem konfiguracji sieci wirtualnej lub sieć VPN, które sterować. Usługa Azure RemoteApp została umieszczona w tej samej sieci wirtualnej. W rezultacie to, czy zasób jest dostępny tylko za pośrednictwem środowiska ARA.

