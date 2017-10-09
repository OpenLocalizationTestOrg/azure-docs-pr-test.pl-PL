---
title: "działanie aaaSign raportów w portalu usługi Azure Active Directory hello | Dokumentacja firmy Microsoft"
description: "Wprowadzenie działanie toosign raportów w portalu usługi Azure Active Directory hello"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a>Raporty aktywności logowania w portalu usługi Azure Active Directory hello

Z usługi Azure Active Directory (Azure AD) raportowania w programie hello [portalu Azure](https://portal.azure.com), można uzyskać informacji hello należy toodetermine jak robi środowiska.

Hello raportowania architektury w usłudze Azure Active Directory obejmuje hello następujące składniki:

- **Działanie** 
    - **Działania logowania** — informacje na temat użycia hello zarządzanych aplikacji i aktywności logowania użytkowników
    - **Dzienniki inspekcji** — informacje o aktywności systemu obejmujące zarządzanie użytkownikami i grupami oraz zarządzane aplikacje i działania dotyczące katalogu.
- **Bezpieczeństwo** 
    - **Ryzykowne logowania** -ryzykowne logowanie jest wskaźnik prób logowania, które mogły zostać wykonane przez osobę, która nie jest właścicielem uzasadnionych hello konta użytkownika. Aby uzyskać więcej informacji, zobacz Ryzykowne logowania.
    - **Użytkownicy oflagowani w związku z ryzykiem** — ryzykowny użytkownik jest wskaźnikiem konta użytkownika, którego bezpieczeństwo mogło zostać naruszone. Aby uzyskać więcej informacji, zobacz Użytkownicy oflagowani w związku z ryzykiem.

Ten temat zawiera omówienie hello logowania działań.

## <a name="pre-requisite"></a>Wymagania wstępne

### <a name="who-can-access-hello-data"></a>Kto ma dostęp do danych hello?
* Użytkowników w roli administratora zabezpieczeń lub czytnika zabezpieczeń hello
* Administratorzy globalni
* Dowolny użytkownik (inny niż administrator) może uzyskać dostęp do danych na temat własnych logowań 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a>Jakie licencji usługi Azure AD potrzebujesz tooaccess logowania działania?
* Dzierżawy musi mieć licencję programu Azure AD Premium, skojarzone z nim toosee hello nawet wszystkich działań logowania raportu


## <a name="signs-in-activities"></a>Działania związane z logowaniem

Informacje hello dostarczone przez użytkownika hello logowania raportu można znaleźć tooquestions odpowiedzi, takich jak:

* Co to jest hello logowania wzorzec użytkownika?
* Ilu użytkowników zalogowało się w ciągu tygodnia?
* Co to jest hello stan tych logowania?

Pierwszy wpis punktu tooall logowania działań dane są **logowania** w sekcji działania hello **usługi Azure Active**.


![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/61.png "Działania związane z logowaniem")


Dziennik inspekcji zawiera domyślny widok listy, który pokazuje:

- Witaj użytkownikowi
- Użytkownik hello aplikacji Hello jest zalogowany do
- Witaj stan logowania
- czas logowania Hello

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/41.png "Działania związane z logowaniem")

Można dostosować widok listy hello klikając **kolumn** hello w pasku narzędzi.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/19.png "Działania związane z logowaniem")

To pozwala toodisplay dodatkowe pola lub usuń pola, które są już wyświetlane.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/42.png "Działania związane z logowaniem")

Po kliknięciu elementu w widoku listy hello, otrzymasz wszystkich dostępnych informacji o nim.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/43.png "Działania związane z logowaniem")


## <a name="filtering-sign-in-activities"></a>Filtrowanie działań związanych z logowaniem

toonarrow dół hello zgłoszone poziom tooa danych czy działa dla Ciebie, dane można filtrować hello logowania przy użyciu hello następujące pola:

- Przedział czasu
- Użytkownik
- Aplikacja
- Klient
- Stan logowania

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/44.png "Działania związane z logowaniem")


Witaj **interwał czasu** filtru umożliwia tooyou toodefine przedział czasu dla hello zwróciła dane.  
Możliwe wartości:

- 1 miesiąc
- 7 dni
- 24 godziny
- Niestandardowy

Po wybraniu niestandardowego przedziału czasu możesz skonfigurować godzinę rozpoczęcia i zakończenia.

Witaj **użytkownika** filtru pozwala toospecify hello nazwy lub hello główna nazwa użytkownika (UPN) użytkownika hello są dla Ciebie ważne.

Witaj **aplikacji** filtr włącza nazwa hello toospecify aplikacji hello są dla Ciebie ważne.

Witaj **klienta** filtr włącza toospecify informacji na temat urządzeń hello są dla Ciebie ważne.

Witaj **stan logowania** filtr włącza tooselect hello następującego filtru:

- Wszystkie
- Powodzenie
- Niepowodzenie


## <a name="sign-in-activities-shortcuts"></a>Skróty działań związanych z logowaniem

Ponadto tooAzure usługi Active Directory, hello portalu Azure zapewnia dwa danych działania toosign w punkty wejścia dodatkowe:

- Użytkownicy i grupy
- Aplikacje dla przedsiębiorstw


### <a name="users-and-groups-sign-ins-activities"></a>Działania związane z logowaniem użytkowników i grup

Informacje hello dostarczone przez użytkownika hello logowania raportu można znaleźć tooquestions odpowiedzi, takich jak:

- Co to jest hello logowania wzorzec użytkownika?
- Ilu użytkowników zalogowało się w ciągu tygodnia?
- Co to jest hello stan tych logowania?



Dane toothis punktu wejścia jest wykres logowania użytkownika hello w hello **omówienie** w obszarze **użytkowników i grup**.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/45.png "Działania związane z logowaniem")

Witaj użytkownika logowania wykres przedstawia tygodniowy agregacji znaku dodatków dla wszystkich użytkowników w danym okresie. Domyślna Hello hello okres to 30 dni.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/46.png "Działania związane z logowaniem")

Po kliknięciu w dniu wykresie hello logowania otrzymasz szczegółową listę hello logowania działań w tym dniu.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/41.png "Działania związane z logowaniem")

Każdy wiersz w oferuje listę działań logowania hello hello szczegółowe informacje na temat hello wybrane logowania takich jak:

* Kto się zalogował?
* Jaka była hello powiązane UPN?
* Jakie aplikacja została docelowy hello logowania hello?
* Co to jest hello adres IP logowania hello?
* Jaki był stan hello logowania hello?

Witaj **logowania** opcja umożliwia pełny przegląd sesje logowania użytkownika.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/51.png "Działania związane z logowaniem")



## <a name="usage-of-managed-applications"></a>Użycie zarządzanych aplikacji

Dzięki widokowi skoncentrowanemu na aplikacji w ramach danych logowania można uzyskać odpowiedzi na pytania, takie jak:

* Kto korzysta z aplikacji?
* Co to jest pierwsze 3 aplikacji hello w organizacji?
* Ostatnio została wdrożona aplikacja. W jaki sposób działa?

Dane toothis punktu wejścia jest pierwsze 3 aplikacji hello w Twojej organizacji w raporcie ostatnich 30 dni hello w hello **omówienie** w obszarze **aplikacje dla przedsiębiorstw**.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/64.png "Działania związane z logowaniem")

Hello aplikacji użycia wykresu co tydzień agregacji logowania dla aplikacji 3 pierwszych w danym okresie. Domyślna Hello hello okres to 30 dni.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/47.png "Działania związane z logowaniem")

Jeśli chcesz, można ustawić fokusu hello na określonej aplikacji.


![Raportowanie](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Raportowanie")

Po kliknięciu w dniu wykresie użycia aplikacji hello otrzymasz szczegółową listę hello logowania działań.


![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/48.png "Działania związane z logowaniem")


Witaj **logowania** opcja umożliwia pełny przegląd wszystkich aplikacji tooyour zdarzenia logowania.

![Działania związane z logowaniem](./media/active-directory-reporting-activity-sign-ins/49.png "Działania związane z logowaniem")



## <a name="next-steps"></a>Następne kroki

Więcej informacji na temat aktywności logowania kody błędów tooknow, zobacz hello [logowania kody błędów raportu działania w portalu usługi Azure Active Directory hello](active-directory-reporting-activity-sign-ins-errors.md).

