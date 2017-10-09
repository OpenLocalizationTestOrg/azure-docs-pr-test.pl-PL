---
title: "działanie aaaAudit raportów w portalu usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "Raporty dotyczące działań w portalu usługi Azure Active Directory hello inspekcji toohello wprowadzenie"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a>Raporty dotyczące działań w portalu usługi Azure Active Directory hello inspekcji 

Z raportowaniem w usłudze Azure Active Directory (Azure AD), można uzyskać informacji hello potrzebne toodetermine jak robi środowiska.

Witaj raportowania architektury w usłudze Azure AD składa się z hello następujące składniki:

- **Działanie** 
    - **Działania logowania** — informacje na temat użycia hello zarządzanych aplikacji i aktywności logowania użytkowników
    - **Dzienniki inspekcji** — informacje o aktywności systemu obejmujące zarządzanie użytkownikami i grupami oraz zarządzane aplikacje i działania dotyczące katalogu.
- **Bezpieczeństwo** 
    - **Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika. Aby uzyskać więcej informacji, zobacz Ryzykowne logowania.
    - **Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone. Aby uzyskać więcej informacji, zobacz Użytkownicy oflagowani w związku z ryzykiem.

Ten temat zawiera omówienie hello inspekcji działań.
 
## <a name="who-can-access-hello-data"></a>Kto ma dostęp do danych hello?
* Użytkowników w roli administratora zabezpieczeń lub czytnika zabezpieczeń hello
* Administratorzy globalni
* Poszczególni użytkownicy (inni niż administratorzy) mogą wyświetlać dane na temat własnych działań


## <a name="audit-logs"></a>Dzienniki inspekcji

Hello dzienników inspekcji w usłudze Azure Active Directory zawierają rekordy działania systemu dla zgodności.  
Pierwszy tooall w punkcie wejścia inspekcja danych jest **dzienniki inspekcji** w hello **działania** sekcji **usługi Azure Active Directory**.

![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/61.png "Dzienniki inspekcji")

Dziennik inspekcji zawiera domyślny widok listy, który pokazuje:

- Witaj Data i godzina wystąpienia hello
- Witaj inicjatora / aktora (*kto*) działania 
- Witaj działania (*co*) 
- docelowy Hello

![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/18.png "Dzienniki inspekcji")

Można dostosować widok listy hello klikając **kolumn** hello w pasku narzędzi.

![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/19.png "Dzienniki inspekcji")

To pozwala toodisplay dodatkowe pola lub usuń pola, które są już wyświetlane.

![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/21.png "Dzienniki inspekcji")


Po kliknięciu elementu w widoku listy hello, otrzymasz wszystkich dostępnych informacji o nim.

![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/22.png "Dzienniki inspekcji")


## <a name="filtering-audit-logs"></a>Dzienniki inspekcji filtrowania

toonarrow dół hello zgłoszone poziom tooa danych czy działa dla Ciebie, dane można filtrować hello inspekcji przy użyciu hello następujące pola:

- Zakres dat
- Zainicjowane przez (aktor)
- Kategoria
- Typ zasobu działania
- Działanie

![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/23.png "Dzienniki inspekcji")


Witaj **zakresu dat** filtru umożliwia tooyou toodefine przedział czasu dla hello zwróciła dane.  
Możliwe wartości:

- 1 miesiąc
- 7 dni
- 24 godziny
- Niestandardowy

Po wybraniu niestandardowego przedziału czasu możesz skonfigurować godzinę rozpoczęcia i zakończenia.

Witaj **inicjowane przez** filtr włącza toodefine możesz aktora nazwy lub jej uniwersalnych głównej nazwy (UPN).

Witaj **kategorii** filtr włącza tooselect hello następującego filtru:

- Wszystkie
- Kategoria podstawowa
- Katalog podstawowy
- Samoobsługowe zarządzanie hasłami
- Samoobsługowe zarządzanie grupami
- Aprowizacja kont — automatyczne przerzucanie haseł
- Zaproszeni użytkownicy
- Usługa MIM
- Identity Protection
- B2C

Witaj **typu zasobu działania** filtr włącza tooselect jedną z następujących hello filtry:

- Wszystkie 
- Grupa
- Katalog
- Użytkownik
- Aplikacja
- Zasady
- Urządzenie
- Inne

Po wybraniu **grupy** jako **typu zasobu działania**, Pobierz kategorii dodatkowy filtr, który umożliwia tooalso podaj **źródła**:

- Azure AD
- O365


Witaj **działania** filtru jest oparta na powitania kategorii i wybór typów zasobów działania podejmowane. Można wybrać określonego mają toosee lub wybierz wszystkie działania. 

Można pobrać listy hello wszystkich działań inspekcji przy użyciu interfejsu API programu Graph https://graph.windows.net/$ hello tenantdomain/działań/auditActivityTypes? api-version = beta, gdzie $tenantdomain = nazwę domeny, lub zobacz artykuł toohello [inspekcji raportu zdarzenia](active-directory-reporting-audit-events.md).


## <a name="audit-logs-shortcuts"></a>Skróty dzienników inspekcji

Ponadto zbyt**usługi Azure Active Directory**, hello Azure portal udostępnia dwa dodatkowe punkty wejścia tooaudit danych:

- Użytkownicy i grupy
- Aplikacje dla przedsiębiorstw

### <a name="users-and-groups-audit-logs"></a>Dzienniki inspekcji użytkowników i grup

Z użytkownika i raporty dotyczące inspekcji na podstawie grupy można uzyskać odpowiedzi tooquestions, takich jak:

- Jakie rodzaje aktualizacje zostały zastosowane hello użytkowników?

- Ilu użytkowników zostało zmienionych?

- Ile haseł zostało zmienionych?

- Jakich zmian dokonał administrator w katalogu?

- Co to są hello grup, które zostały dodane?

- Czy istnieją grupy, w których dokonano zmiany członkostwa?

- Zostały zmienione hello właścicieli grupy?

- Jakie licencje zostały przypisane tooa grupy lub użytkownika?

Jeśli chcesz tooreview inspekcji dane, które są powiązane toousers i grup, można znaleźć widok filtrowany w obszarze **dzienniki inspekcji** w hello **działania** sekcji hello **użytkowników i grup**. Ten punkt wejścia ma wartość **Użytkownicy i grupy** wstępnie wybraną dla opcji **Typ zasobu działania**.

![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/93.png "Dzienniki inspekcji")

### <a name="enterprise-applications-audit-logs"></a>Dzienniki inspekcji aplikacji dla przedsiębiorstw

Raporty dotyczące inspekcji, z aplikacji, możesz uzyskać tooquestions odpowiedzi, takich jak:

* Co to są aplikacje hello, które zostały dodane lub zaktualizowane?
* Co to są aplikacje hello, które zostały usunięte?
* Czy usługa w ramach aplikacji została zmieniona?
* Zostały zmienione nazwy aplikacji hello?
* Kto udzielił zgody tooan aplikacji?

Jeśli chcesz tooreview inspekcji dane, które są powiązane tooyour aplikacji, można znaleźć widok filtrowany w obszarze **dzienniki inspekcji** w hello **działania** sekcji hello **aplikacje dla przedsiębiorstw**  bloku. Ten punkt wejścia ma wartość **Aplikacje dla przedsiębiorstw** wstępnie wybraną dla opcji **Typ zasobu działania**.

![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/134.png "Dzienniki inspekcji")

Można filtrować tego widoku dalsze dół toojust **grup** lub po prostu **użytkowników**.

![Dzienniki inspekcji](./media/active-directory-reporting-activity-audit-logs/25.png "Dzienniki inspekcji")


## <a name="next-steps"></a>Następne kroki

Omówienie raportowania patrz hello [raportowania usługi Azure Active Directory](active-directory-reporting-azure-portal.md).

