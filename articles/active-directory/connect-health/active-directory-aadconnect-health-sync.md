---
title: "Program Azure AD Connect Health z synchronizacją aaaUsing | Dokumentacja firmy Microsoft"
description: "Jest to strona hello Azure AD Connect Health, która będzie omawiać jak zsynchronizować toomonitor Azure AD Connect."
services: active-directory
documentationcenter: 
author: karavar
manager: femila
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/18/2017
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 56f0582be30e664026cedf15350bc23501998bfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Monitorowanie synchronizacji usługi Azure AD Connect za pomocą programu Azure AD Connect Health
powitania po dokumentacji jest szczególne toomonitoring Azure AD Connect (synchronizacja) z usługi Azure AD Connect Health.  Aby uzyskać informacje na temat monitorowania usług AD FS za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health z usługami AD FS](active-directory-aadconnect-health-adfs.md). Ponadto, aby uzyskać informacje na temat monitorowania Usług domenowych Active Directory za pomocą programu Azure AD Connect Health, zobacz [Używanie programu Azure AD Connect Health z usługami AD DS](active-directory-aadconnect-health-adds.md).

![Program Azure AD Connect Health do celów synchronizacji](./media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Alerty dla programu Azure AD Connect Health do celów synchronizacji
Hello Azure AD Connect alerty dotyczące kondycji dla sekcji synchronizacji zapewnia hello listę aktywnych alertów. Każdy alert zawiera istotne informacje, kroki rozwiązania i dokumentacji toorelated łącza. Po wybraniu aktywnego lub rozwiązanego alertu pojawi się nowy blok z dodatkowe informacje, a także czynności, które można wykonać tooresolve hello alertu i dokumentacji tooadditional łącza. Można również wyświetlić dane historyczne na temat alertów, które zostały rozwiązane w przeszłości hello.

Po wybraniu alertu, które zostaną wyświetlone dodatkowe informacje, jak również kroki można wykonać tooresolve hello alert oraz linki tooadditional dokumentacji.

![Błąd synchronizacji programu Azure AD Connect](./media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Ograniczona ocena alertów
Jeśli Azure AD Connect nie używa konfiguracji domyślnej hello (na przykład jeśli filtrowanie atrybutów zostało zmienione z konfiguracji niestandardowej konfiguracji tooa hello domyślna), następnie hello Azure AD Connect Health agent nie przekaże hello błąd zdarzeń powiązanych tooAzure AD Connect.

To ogranicza ocenę hello alertów przez usługę hello. Zobaczysz Baner, który wskazuje tego warunku w hello portalu Azure w ramach usługi.

![Program Azure AD Connect Health do celów synchronizacji](./media/active-directory-aadconnect-health-sync/banner.png)

Można to zmienić klikając pozycję "Ustawienia", dzięki czemu program Azure AD Connect Health agent tooupload wszystkich dzienników błędów.

![Program Azure AD Connect Health do celów synchronizacji](./media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Wgląd w szczegóły synchronizacji
Administratorzy często mają tooknow o hello czas toosync zmiany tooAzure AD i hello ilość zmiany zachodzące. Ta funkcja zapewnia prosty sposób toovisualize to przy użyciu hello poniżej wykresy:   

* Opóźnienie operacji synchronizacji
* Trend zmiany obiektu

### <a name="sync-latency"></a>Opóźnienie synchronizacji
Ta funkcja zapewnia graficzny trend opóźnienia hello operacji synchronizacji (import, eksport itd.) dla łączników.  Zapewnia to szybki i łatwy sposób toounderstand hello nie tylko opóźnień operacji (większe, jeśli masz dużą zestawem zachodzących zmian), ale także anomalii toodetect sposób hello opóźnienia, które mogą wymagać bliższego zbadania.

![Opóźnienie synchronizacji](./media/active-directory-aadconnect-health-sync/synclatency02.png)

Domyślnie jest wyświetlana tylko hello opóźnienie operacji "Eksportuj" hello hello łącznika usługi Azure AD.  toosee więcej operacji na łączniku hello lub tooview operacje innych łączników, kliknij prawym przyciskiem myszy na wykresie hello, wybierz pozycję Edytuj wykres lub kliknij przycisk "Edytuj wykres opóźnienia" hello i wybierz określoną operację hello i łączniki.

### <a name="sync-object-changes"></a>Zmiany obiektu synchronizacji
Ta funkcja zapewnia graficzny trend liczby hello zmian, które są oceniane i wyeksportować tooAzure AD.  Dzisiaj, w trakcie toogather tych informacji z dzienników synchronizacji hello jest trudne.  Witaj wykres umożliwia nie tylko prostszy sposób monitorowania hello liczbę zmian, które występują w danym środowisku, ale także czytelny hello błędów, które są wykonywane.

![Opóźnienie synchronizacji](./media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Raport o błędach synchronizacji na poziomie obiektu (wersja zapoznawcza)
Ta funkcja dostarcza raport o błędach synchronizacji, które mogą wystąpić podczas synchronizowania danych tożsamości między usługami Windows Server AD i Azure AD za pomocą programu Azure AD Connect.

* Raport Hello obejmuje błędów rejestrowane przez powitania klienta synchronizacji (Azure AD Connect wersji 1.1.281.0 lub nowszej)
* Obejmuje on hello błędów, które wystąpiły w ostatniej operacji synchronizacji hello na powitania aparatu synchronizacji. ("Eksport" na powitania łącznika usługi Azure AD.)
* Agent Azure AD Connect Health dla synchronizacji musi mieć łączność wychodząca toohello wymagane punkty końcowe hello raport tooinclude hello najnowsze dane.
* Raport Hello jest **zaktualizowane po co 30 minut** przy użyciu danych hello przekazany przez agenta usługi Azure AD Connect Health do celów synchronizacji. Zapewnia hello następujące kluczowe możliwości

  * Kategoryzacja błędów
  * Lista obiektów z błędami według kategorii
  * Wszystkie dane hello o błędach hello w jednym miejscu
  * Po stronie przez porównanie po stronie obiektów z powodu błędu ze względu na konflikt tooa
  * Pobierz raport o błędach hello jako CVS (wkrótce)

### <a name="categorization-of-errors"></a>Kategoryzacja błędów
Raport Hello kategoryzuje hello istniejących błędów synchronizacji w hello następujące kategorie:

| Kategoria | Opis |
| --- | --- |
| Zduplikowany atrybut |Błędy, które występują, gdy program Azure AD Connect próbuje utworzyć lub zaktualizować obiekty ze zduplikowanymi wartościami jednego lub kilku atrybutów w usłudze Azure AD, które muszą być unikatowe w dzierżawie, na przykład proxyAddresses lub UserPrincipalName. |
| Niezgodność danych |Błędy, gdy hello soft-match toomatch obiektów, które powodować błędy synchronizacji nie powiodło się. |
| Błąd weryfikacji danych |Błędy powodu tooinvalid dane, takie jak nieobsługiwane znaki w krytyczne atrybutów, takich jak UserPrincipalName, format błędy, które nie są weryfikacji przed zapisaniem w usłudze Azure AD. |
| Duży atrybut |Błędy, gdy jeden lub więcej atrybutów są większe niż hello dozwolony rozmiar, długość lub liczby. |
| Inne |Wszystkie inne błędy, które nie mieszczą się w hello powyżej kategorii. Na podstawie opinii ta kategoria zostanie podzielona na podkategorie. |

![Podsumowanie raportu o błędach synchronizacji](./media/active-directory-aadconnect-health-sync/errorreport01.png)
![Kategorie raportu o błędach synchronizacji](./media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>Lista obiektów z błędami według kategorii
Przechodzenia do poszczególnych kategorii szczegółów zawierają hello listy obiektów mających hello błędu w tej kategorii.
![Lista raportu o błędach synchronizacji](./media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Szczegóły błędu
Następujące dane są dostępne w hello szczegółowe widoku dla każdego błędu

* Identyfikatory hello *obiektu usługi Active Directory* zaangażowany
* Identyfikatory hello *obiektu usługi Active Directory Azure* zaangażowany (w razie potrzeby)
* Opis błędu i w jaki sposób toofix
* Pokrewne artykuły:

![Szczegóły raportu o błędach synchronizacji](./media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-hello-error-report-as-csv"></a>Pobierz raport o błędach hello jako woluminu CSV
Po wybraniu hello "" przycisk Eksportuj można pobrać pliku CSV ze wszystkich hello szczegółami wszystkie błędy hello.

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