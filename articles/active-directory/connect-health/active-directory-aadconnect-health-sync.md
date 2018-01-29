---
title: "Używanie programu Azure AD Connect Health z usługą synchronizacji | Microsoft Docs"
description: "Jest to strona programu Azure AD Connect Health, która będzie omawiać temat monitorowania synchronizacji usługi Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: mtillman
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 821d4bd7e6b526ad826caf005456edf8235291b8
ms.sourcegitcommit: e266df9f97d04acfc4a843770fadfd8edf4fa2b7
ms.translationtype: HT
ms.contentlocale: pl-PL
ms.lasthandoff: 12/11/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Monitorowanie synchronizacji usługi Azure AD Connect za pomocą programu Azure AD Connect Health
Poniższa dokumentacja dotyczy monitorowania programu Azure AD Connect (synchronizacja) przy użyciu programu Azure AD Connect Health.  Aby uzyskać informacje na temat monitorowania usług AD FS za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md). Ponadto, aby uzyskać informacje na temat monitorowania Usług domenowych Active Directory za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md).

![Program Azure AD Connect Health do celów synchronizacji](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Alerty dla programu Azure AD Connect Health do celów synchronizacji
Sekcja Alerty programu Azure AD Connect Health do celów synchronizacji zawiera listę aktywnych alertów. Każdy alert zawiera istotne informacje, kroki do rozwiązania problemu i linki do powiązanej dokumentacji. Po wybraniu aktywnego lub rozwiązanego alertu pojawi się nowy blok z dodatkowymi informacjami, kroki, jakie można podjąć, aby rozwiązać alert, oraz linki do dodatkowej dokumentacji. Można również wyświetlić dane historyczne na temat alertów, które zostały rozwiązane w przeszłości.

Po wybraniu alertu pojawią się dodatkowe informacje, kroki, jakie można podjąć, aby rozwiązać alert, oraz linki do dodatkowej dokumentacji.

![Błąd synchronizacji programu Azure AD Connect](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Ograniczona ocena alertów
Jeśli program Azure AD Connect NIE KORZYSTA z konfiguracji domyślnej (na przykład jeśli filtrowanie atrybutów zostało zmienione z konfiguracji domyślnej na konfigurację niestandardową), wtedy agent programu Azure AD Connect Health nie przekaże zdarzeń błędów powiązanych z programem Azure AD Connect.

To ogranicza ocenę alertów przez usługę. Zobaczysz baner, który wskazuje na taki stan w witrynie Azure Portal w ramach usługi.

![Program Azure AD Connect Health do celów synchronizacji](./media/active-directory-aadconnect-health-sync/banner.png)

Możesz to zmienić, klikając pozycję „Ustawienia” i pozwalając agentowi programu Azure AD Connect Health, na przekazanie wszystkich dzienników błędów.

![Program Azure AD Connect Health do celów synchronizacji](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Wgląd w szczegóły synchronizacji
Administratorzy często chcą wiedzieć, ile czasu zajmie synchronizowanie zmian z usługą Azure AD oraz ile zmian jest wprowadzanych. Ta funkcja umożliwia łatwą wizualizację tych danych za pomocą poniższych wykresów:   

* Opóźnienie operacji synchronizacji
* Trend zmiany obiektu

### <a name="sync-latency"></a>Opóźnienie synchronizacji
Ta funkcja prezentuje w sposób graficzny trend opóźnienia operacji synchronizacji (import, eksport itd.) dla łączników.  Zapewnia to szybki i łatwy sposób zrozumienia nie tylko opóźnień operacji (tym większych, im większy zestaw wprowadzanych zmian), ale także wykrycia anomalii w opóźnieniu, które mogą wymagać bliższego zbadania.

![Opóźnienie synchronizacji](./media/active-directory-aadconnect-health-sync/synclatency02.png)

Tylko opóźnienie operacji „Eksportuj” dla łącznika usługi Azure AD jest wyświetlane domyślnie.  Aby zobaczyć więcej operacji na łączniku lub aby wyświetlić operacje innych łączników, kliknij prawym przyciskiem myszy wykres i wybierz polecenie „Edytuj wykres” lub kliknij przycisk „Edytuj wykres opóźnienia”, a następnie wybierz określoną operację i łączniki.

### <a name="sync-object-changes"></a>Zmiany obiektu synchronizacji
Ta funkcja prezentuje w sposób graficzny trend liczby zmian obliczanych i eksportowanych do usługi Azure AD.  Zebranie tych informacji z dzienników synchronizacji jest obecnie trudne.  Wykres umożliwia nie tylko łatwiejszy sposób monitorowania liczby zmian, jakie zachodzą w Twoim środowisku, ale także przedstawia w sposób czytelny i obrazowy pojawiające się błędy.

![Opóźnienie synchronizacji](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Raport o błędach synchronizacji na poziomie obiektu (wersja zapoznawcza)
Ta funkcja dostarcza raport o błędach synchronizacji, które mogą wystąpić podczas synchronizowania danych tożsamości między usługami Windows Server AD i Azure AD za pomocą programu Azure AD Connect.

* Raport ten dotyczy błędów zarejestrowanych przez klienta synchronizacji (program Azure AD Connect w wersji 1.1.281.0 lub nowszej)
* Zawiera on błędy, które wystąpiły podczas ostatniej operacji synchronizacji na aparacie synchronizacji. (Pozycja „Eksportuj” w programie Azure AD Connector).
* Aby raport zawierał najnowsze dane, agent programu Azure AD Connect Health do celów synchronizacji musi mieć połączenie wychodzące z wymaganymi punktami końcowymi.
* Raport jest **aktualizowany co 30 minut** przy użyciu danych przekazanych przez agenta programu Azure AD Connect Health do celów synchronizacji. Oferuje on następujące kluczowe funkcje

  * Kategoryzacja błędów
  * Lista obiektów z błędami według kategorii
  * Wszystkie dane o błędach w jednym miejscu
  * Porównanie obiektów z błędami spowodowanymi konfliktem
  * Możliwość pobrania raportu o błędach w formie pliku CVS (wkrótce)

### <a name="categorization-of-errors"></a>Kategoryzacja błędów
W raporcie istniejące błędy synchronizacji są klasyfikowane według następujących kategorii:

| Kategoria | Opis |
| --- | --- |
| Zduplikowany atrybut |Błędy, które występują, gdy program Azure AD Connect próbuje utworzyć lub zaktualizować obiekty ze zduplikowanymi wartościami jednego lub kilku atrybutów w usłudze Azure AD, które muszą być unikatowe w dzierżawie, na przykład proxyAddresses lub UserPrincipalName. |
| Niezgodność danych |Błędy niepowodzenia miękkiego dopasowania obiektów, które powodują błędy synchronizacji. |
| Błąd weryfikacji danych |Błędy spowodowane nieprawidłowymi danymi, takimi jak nieobsługiwane znaki w atrybutach krytycznych (np. UserPrincipalName) czy błędy formatowania, które powodują niepowodzenie weryfikacji przed zapisaniem w usłudze Azure AD. |
| Duży atrybut |Błędy, które występują, gdy co najmniej jeden atrybut ma rozmiar większy niż dozwolony, długość większą niż dozwolona, lub liczbę większą niż dozwolona. |
| Inne |Wszystkie pozostałe błędy, które nie należą do powyższych kategorii. Na podstawie opinii ta kategoria zostanie podzielona na podkategorie. |

![Podsumowanie raportu o błędach synchronizacji](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Kategorie raportu o błędach synchronizacji](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Lista obiektów z błędami według kategorii
Przejście do szczegółów każdej kategorii pozwoli wyświetlić listę obiektów mających błędy z danej kategorii.
![Lista raportu o błędach synchronizacji](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Szczegóły błędu
W szczegółowym widoku dla każdego błędu są dostępne następujące dane

* Identyfikatory *obiektów usługi AD*, których dotyczy błąd
* Identyfikatory *obiektów usługi Azure AD*, których dotyczy błąd (o ile dotyczy)
* Opis błędu i sposób naprawy
* Pokrewne artykuły:

![Szczegóły raportu o błędach synchronizacji](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-the-error-report-as-csv"></a>Pobieranie raportu o błędach w formie pliku CVS
Wybierając przycisk „Eksportuj”, możesz pobrać plik CSV z pełnymi, szczegółowymi informacjami na temat wszystkich błędów.

## <a name="related-links"></a>Powiązane linki
* [Rozwiązywanie problemów z błędami występującymi podczas synchronizacji](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [Odporność względem zduplikowanych atrybutów](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Instalowanie agenta programu Azure AD Connect Health](active-directory-aadconnect-health-agent-install.md)
* [Operacje w programie Azure AD Connect Health](active-directory-aadconnect-health-operations.md)
* [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md)
* [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health — często zadawane pytania](active-directory-aadconnect-health-faq.md)
* [Historia wersji programu Azure AD Connect Health](active-directory-aadconnect-health-version-history.md)