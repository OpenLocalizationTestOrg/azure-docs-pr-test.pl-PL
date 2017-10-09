---
title: "Synchronizacja programu Azure AD Connect: opis użytkowników i kontaktów | Dokumentacja firmy Microsoft"
description: "Wyjaśnia, użytkowników i kontaktów synchronizacji Azure AD Connect."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8d204647-213a-4519-bd62-49563c421602
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi;andkjell
ms.openlocfilehash: 4d80648c53a2981eb2626338913ed2282423f183
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-users-and-contacts"></a>Synchronizacja programu Azure AD Connect: opis użytkowników i kontaktów
Istnieje kilka przyczyn dlaczego może mieć wiele lasów usługi Active Directory i istnieje kilka topologii rozmieszczania. Typowe modele zawierają wdrażania konta zasobów i lasów sync'ed usługi GAL po połączeniu & nabycia. Ale nawet w przypadku modeli czystego, modele hybrydowe wspólnej również. Hello domyślnej konfiguracji synchronizacji Azure AD Connect nie przyjmuje żadnego określonego modelu, ale w zależności od tego, jak dopasowywaniu użytkowników zostało wybrane w podręczniku instalacji hello, można zaobserwować różne zachowania.

W tym temacie firma Microsoft będzie przejście przez zachowanie hello domyślnej konfiguracji niektóre topologiami. Rozszerzana za pomocą konfiguracji hello i hello Edytor reguł synchronizacji mogą być używane toolook na powitania konfiguracji.

Istnieje kilka ogólne reguły konfiguracji hello przyjęto:

* Niezależnie od tego, który kolejności możemy zaimportować ze źródła hello usług Active Directory wynik końcowy hello powinna zawsze być hello tego samego.
* Aktywne konto zawsze przyczyniają się informacji logowania, w tym **userPrincipalName** i **sourceAnchor**.
* Wyłączonych kont przyczyniają userPrincipalName i sourceAnchor, o ile nie jest połączoną skrzynkę pocztową, jeśli nie istnieje żadne toobe aktywnego konta znaleziono.
* Konta z połączoną skrzynkę pocztową, nigdy nie będzie służyć do userPrincipalName i sourceAnchor. Zakłada się później odnaleźć aktywnego konta.
* Obiekt kontaktu może być inicjowana tooAzure AD jako kontakt lub użytkownik. Nie można ustalić naprawdę, dopóki nie zostaną przetworzone wszystkie lasów usługi Active Directory źródła.

## <a name="contacts"></a>Kontakty
Kontakty reprezentujący użytkownika w innym lesie jest posiadanie wspólnej po połączeniu & nabycia gdzie rozwiązania usługi GALSync jest mostkowanie co najmniej dwa lasy usługi programu Exchange. zawsze przyłączania do obiektu kontaktu Hello z hello łącznika miejsca przy użyciu atrybutu wiadomości powitania toohello metaverse. Jeśli istnieje już kontaktu obiekt lub obiekt użytkownika z hello sam adres e-mail, obiekty hello są połączone ze sobą. Te ustawienia zostaną skonfigurowane w regule hello **w z usługi Active Directory — kontakt Join**. Istnieje również reguły o nazwie **w z usługi Active Directory — skontaktuj się z wspólnej** z atrybutem metaverse toohello przepływu atrybutu **sourceObjectType** z stałą hello **skontaktuj się z**. Ta reguła ma pierwszeństwo bardzo niskich tak więc jeśli dowolny obiekt użytkownika jest toohello przyłączone do tego samego obiektu metaverse, a następnie reguły hello **w z usługi Active Directory — typowe użytkownika** przyczyniają się do atrybutu toothis użytkownika wartość hello. Z tą regułą ten atrybut ma wartość hello, jeśli żaden użytkownik nie został dołączony. Skontaktuj się z i hello wartość użytkownika, jeśli odnaleziono co najmniej jednego użytkownika.

Dla udostępniania tooAzure obiektu AD, hello wychodzącą regułę **limit tooAAD — skontaktuj się z Join** spowoduje utworzenie obiektu kontaktu, jeśli hello atrybut metaverse **sourceObjectType** ustawiono zbyt**skontaktuj się z** . Jeśli ten atrybut zostanie ustawiony zbyt**użytkownika**, następnie hello reguły **się tooAAD — użytkownik przyłączyć** zamiast tego utworzyć obiektu user.
Istnieje możliwość, że obiekt jest awansowana z tooUser skontaktuj się z podczas źródła więcej usług Active Directory zostały zaimportowane i zsynchronizowane.

Na przykład w topologii usługi GALSync będzie znaleźliśmy skontaktuj się z pomocą obiektów dla każdego hello drugiego lasu możemy importowania hello pierwszy las. Spowoduje to etap nowych obiektów kontaktu w hello łącznik AAD. Gdy firma Microsoft później importuje i synchronizuje hello drugiego lasu, możemy znajdzie hello rzeczywistych użytkowników i dołącz je toohello istniejących obiektów metaverse. Firma Microsoft będą usunąć hello obiektu kontaktu w usłudze AAD i utworzyć nowy obiekt użytkownika.

Jeśli masz topologii, w których użytkownicy są reprezentowane jako kontakty, upewnij się, że Wybierz użytkowników toomatch na powitania atrybut poczty w podręczniku instalacji hello. Wybranie innej opcji będzie mieć kolejność konfiguracji zależnej. Skontaktuj się z pomocą obiektów zawsze spowoduje dołączenie na powitania atrybut poczty, ale na atrybut poczty hello tylko dołączy obiekty użytkownika, jeśli ta opcja została wybrana w podręczniku instalacji hello. Można następnie na końcu dwóch różnych obiektów w magazynie metaverse hello z hello sam atrybut poczty, jeśli obiektu kontaktu hello zaimportowano przed hello obiektu user. Podczas eksportowania tooAzure AD zostanie zgłoszony błąd. To zachowanie jest celowe i wskazuje nieprawidłowe dane lub tej topologii hello nie został poprawnie zidentyfikowane podczas instalacji hello.

## <a name="disabled-accounts"></a>Wyłączone konta
Wyłączone konta są synchronizowane również tooAzure AD. Wyłączone konta są wspólnych zasobów toorepresent w programie Exchange, na przykład sal konferencyjnych. wyjątek Hello jest użytkownikom połączoną skrzynkę pocztową; jak wcześniej wspomniano te będą nigdy nie udostępnić tooAzure konto usługi AD.

założeń Hello jest to, że jeśli zostanie znaleziony wyłączonego konta użytkownika, to firma Microsoft nie będzie zawierał inne aktywne konto później i obiekt hello jest inicjowana tooAzure AD hello userPrincipalName i znaleziono sourceAnchor. W przypadku innego konta active dołączy toohello, będzie można używać tego samego obiektu metaverse, a następnie jego userPrincipalName sourceAnchor.

## <a name="changing-sourceanchor"></a>Zmiana sourceAnchor
Po wyeksportowaniu obiektu tooAzure AD, a następnie go nie jest dozwolone toochange hello sourceAnchor już. Gdy obiekt hello został wyeksportowany hello atrybut metaverse **cloudSourceAnchor** ustawiono hello **sourceAnchor** wartość zaakceptowane przez usługę Azure AD. Jeśli **sourceAnchor** zostało zmienione i nie odpowiada **cloudSourceAnchor**, reguły hello **się tooAAD — użytkownik przyłączyć** zgłosi błąd hello **atrybutu sourceAnchor Zmieniono**. W takim przypadku należy go poprawić konfigurację hello lub danych tak samo hello sourceAnchor jest obecne w ponownie metaverse hello hello obiekt można ponownie zsynchronizować.

## <a name="additional-resources"></a>Dodatkowe zasoby
* [Azure AD Connect Sync: Dostosowywanie opcji synchronizacji](active-directory-aadconnectsync-whatis.md)
* [Integrowanie tożsamości lokalnych z usługą Azure Active Directory](active-directory-aadconnect.md)

