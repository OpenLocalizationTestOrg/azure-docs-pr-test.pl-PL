---
title: "Raporty dotyczące inicjowania obsługi aplikacji tooSaaS konta użytkowników usługi Azure Active Directory | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocheck hello stan inicjowania obsługi zadania konta użytkowników i jak tootroubleshoot hello inicjowania obsługi administracyjnej poszczególnych użytkowników."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: asmalser-msft
ms.openlocfilehash: 5dcf9e5dbaacf3a2c81183c5d81e331858671b86
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-reporting-on-automatic-user-account-provisioning"></a>Samouczek: Raportowania na inicjowanie obsługi konta użytkowników


Usługa Azure Active Directory obejmuje [konta użytkownika usługi inicjowania obsługi administracyjnej](active-directory-saas-app-provisioning.md) który ułatwia automatyzację hello inicjowania obsługi administracyjnej do inicjowania obsługi administracyjnej kont użytkowników w aplikacji SaaS i innych systemów w celu hello życia tożsamości end-to-end Zarządzanie. Usługi Azure AD obsługuje wstępnie zintegrowanych użytkownika inicjowania obsługi administracyjnej łączników dla wszystkich aplikacji hello i systemów w sekcji "Proponowanym" hello hello [galerii aplikacji Azure AD](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/azure-active-directory-apps?page=1&subcategories=featured).

W tym artykule opisano, jak toocheck hello stan inicjowania obsługi administracyjnej zadania po ich górę i w jaki sposób tootroubleshoot hello inicjowania obsługi poszczególnych użytkowników i grup.

## <a name="overview"></a>Omówienie

Łączniki inicjowania obsługi administracyjnej są głównie Konfigurowanie i skonfigurować za pomocą hello [portalu zarządzania Azure](https://portal.azure.com), przez następujące hello [podane dokumentacji](active-directory-saas-tutorial-list.md) dla aplikacji hello gdzie inicjowania obsługi administracyjnej kont użytkowników Żądana. Gdy skonfigurowana i uruchomiona, inicjowania obsługi administracyjnej zadania dla aplikacji mogą być zgłaszane przy użyciu jednej z dwóch metod:

* **Portal zarządzania Azure** — w tym artykule opisano głównie podczas pobierania informacji w raporcie z hello [portalu zarządzania Azure](https://portal.azure.com), zapewniające zarówno inicjowania obsługi administracyjnej raport z podsumowaniem jak i szczegółowe inicjowania obsługi administracyjnej Inspekcja dzienników dla danej aplikacji.

* **Interfejs API inspekcji** — Azure Active Directory oferuje również inspekcji interfejsu API umożliwia szczegółowe programowe pobieranie hello inicjowania obsługi administracyjnej dzienniki inspekcji. Zobacz [inspekcji usługi Azure Active Directory dokumentacja interfejsu API](active-directory-reporting-api-audit-reference.md) dla określonych toousing dokumentacji tego interfejsu API. Gdy w tym artykule nie szczegółowo opisano jak toouse hello interfejsu API, jego szczegóły hello typy obsługi zdarzeń, które są rejestrowane w dzienniku inspekcji hello.

### <a name="definitions"></a>Definicje

W tym artykule wykorzystano hello następujące warunki określonych poniżej:

* **Źródłowy System** -synchronizuje się z repozytorium hello użytkowników, którzy hello inicjowania obsługi usługi Azure AD. Azure Active Directory jest hello systemu źródłowego dla większości hello wstępnie zintegrowanych łączników udostępniania, jednak istnieje kilka wyjątków (przykład: produktu Workday synchronizacji ruchu przychodzącego).

* **Docelowy System** -synchronizuje repozytorium hello użytkowników, którzy hello inicjowania obsługi usługi Azure AD do. Jest to zazwyczaj aplikacji SaaS (przykłady: Salesforce, usługi ServiceNow, Google Apps, Dropbox dla firm), jednak w niektórych przypadkach może być systemu lokalnego, takie jak Active Directory (przykład: tooActive synchronizacji ruchu przychodzącego dla produktu Workday katalogu).


## <a name="getting-provisioning-reports-from-hello-azure-management-portal"></a>Pobieranie inicjowania obsługi administracyjnej raporty z portalu zarządzania Azure hello

tooget udostępniania informacji w raporcie dla danej aplikacji, start uruchamiając hello [portalu zarządzania Azure](https://portal.azure.com) i przeglądanie toohello przedsiębiorstwa aplikacji, dla której skonfigurowano usługę inicjowania obsługi administracyjnej. Na przykład w przypadku udostępniania użytkownikom tooLinkedIn podniesienie uprawnień, szczegóły aplikacji hello nawigacji ścieżki toohello to:

**Usługa Azure Active Directory > aplikacje dla przedsiębiorstw > wszystkie aplikacje > LinkedIn podniesienia uprawnień**

W tym miejscu są dostępne raport z podsumowaniem hello inicjowania obsługi administracyjnej i inicjowania obsługi administracyjnej dzienników inspekcji hello, oba opisane poniżej.


### <a name="provisioning-summary-report"></a>Raport z podsumowaniem inicjowania obsługi administracyjnej

Hello inicjowania obsługi administracyjnej raport z podsumowaniem jest widoczna w hello **inicjowania obsługi administracyjnej** karcie daną aplikację. Znajduje się w sekcji szczegółów synchronizacji hello poniżej **ustawienia**i udostępnia hello następujących informacji:

* Witaj łącznej liczby użytkowników i / grupy które zostały zsynchronizowane i znajdują się w zakresie udostępniania między systemem źródłowym hello i hello system docelowy.

* Ostatnia synchronizacja czasu hello Hello zostało uruchomione. Synchronizacja odbyła zazwyczaj co 20 40 minut, po zakończeniu pełnej synchronizacji.

* Określa, czy początkowa Pełna synchronizacja została ukończona.

* Czy hello procesu udostępniania zostały umieszczone w kwarantannie, i jakie hello przyczyny stanu kwarantanny hello jest np. (błąd toocommunicate z systemu docelowego powodu tooinvalid poświadczenia administratora)

Hello inicjowania obsługi administracyjnej raport z podsumowaniem powinna być hello pierwszym miejscu Administratorzy wygląd toocheck na kondycję operacyjną hello hello zadanie inicjowania obsługi administracyjnej.

 ![Raport z podsumowaniem](./media/active-directory-saas-provisioning-reporting/summary_report.PNG)

### <a name="provisioning-audit-logs"></a>Dzienniki inspekcji inicjowania obsługi administracyjnej
Wszystkie działania wykonywane przez hello świadczenie usługi są rejestrowane w dziennikach inspekcji hello Azure AD, które można wyświetlić w hello **dzienniki inspekcji** kartę w obszarze hello **Inicjowanie obsługi konta** kategorii. Typy zdarzeń rejestrowane działania:

* **Importowanie zdarzeń** — "import" zdarzenie jest rejestrowane zawsze hello Azure AD service inicjowania obsługi administracyjnej pobiera informacje o poszczególnych użytkowników i grup z systemu źródłowego lub systemu docelowego. Podczas synchronizacji użytkownicy są pobierane z systemu źródłowego hello najpierw z wynikami hello rejestrowane jako "przycisk Importuj, zdarzenia. Witaj zgodnymi identyfikatorami hello pobrać użytkowników są następnie zapytanie względem toocheck systemu docelowego hello, jeśli istnieją, z wynikami hello zarejestrowany jako "przycisk Importuj, zdarzenia. Te zdarzenia rejestrować wszystkie atrybuty zamapowane użytkownika i ich wartości, które zarejestrowanych przez usługi inicjowania obsługi administracyjnej hello Azure AD w czasie hello hello zdarzenia. 

* **Zdarzenia reguły synchronizacji** — te zdarzenia raportu dotyczącego wyników hello hello atrybutu mapowania reguł i dowolne skonfigurowane filtry zakresu po dane użytkownika zostały zaimportowane i obliczone z systemów źródłowych i docelowych hello. Na przykład jeśli użytkownik w systemie źródłowym jest uznany za toobe w zakresie obsługi i zakładany toonot istnieje w systemie docelowym hello, następnie to zdarzenie rejestruje hello użytkownika będą udostępniane w systemie docelowym hello. 

* **Eksportowanie zdarzeń** — "export" zdarzenie jest rejestrowane zawsze hello Azure AD inicjowania obsługi usługi zapisuje użytkownika konta lub grupy, obiekt tooa systemu docelowego. Te zdarzenia rejestrować wszystkie atrybuty użytkowników i ich wartości, które zostały napisane przez hello inicjowania obsługi usługi Azure AD w czasie hello hello zdarzenia. Jeśli wystąpił błąd podczas zapisywania hello użytkownika konta lub grupy, obiekt toohello systemu docelowego, będzie wyświetlana w tym miejscu.

* **Przetwarzanie zdarzeń depozytu** -Escrow — proces wystąpić, gdy hello świadczenie usługi napotka błąd podczas próby wykonania operacji i rozpoczyna się operacja hello tooretry wycofania interwał czasu. Zdarzenie "depozytu" rejestrowany jest zawsze, gdy operacji inicjowania obsługi administracyjnej została wycofana.

Podczas przeglądania inicjowania obsługi zdarzeń dla poszczególnych użytkowników, zdarzenia hello normalnie występuje w następującej kolejności:

1. Importowanie zdarzeń: użytkownika są pobierane z systemu źródłowego hello.

2. Importowanie zdarzeń: system docelowy jest toocheck, którego dotyczy kwerenda istnienie hello hello pobrać użytkownika.

3. Zdarzenia reguły synchronizacji: dane użytkownika z systemów źródłowych i docelowych są sprawdzane dla atrybutu hello skonfigurowane reguły mapowania i określania zakresu toodetermine filtrów, jaką akcję, należy wykonać.

4. Eksportowanie zdarzeń: Jeśli zdarzenia reguły synchronizacji hello definiowane, że akcja powinna być wykonana (np. Add, Update, Delete), a następnie hello wyniki akcji hello są rejestrowane w przypadku eksportowania.

![Tworzenie użytkownika testowego usługi Azure AD](./media/active-directory-saas-provisioning-reporting/audit_logs.PNG)


### <a name="looking-up-provisioning-events-for-a-specific-user"></a>Wyszukiwanie inicjowania obsługi zdarzeń dla określonego użytkownika

Hello najczęściej przypadek użycia dla inicjowania obsługi dzienników inspekcji hello jest hello toocheck stanu indywidualne konto udostępniania. toolook hello ostatniego inicjowania obsługi zdarzeń dla określonego użytkownika:

1. Przejdź toohello **dzienniki inspekcji** sekcji.

2. Z hello **kategorii** menu, wybierz opcję **Inicjowanie obsługi konta**.

3. W hello **zakres dat** menu, wybierz hello zakresu dat toosearch,

4. W hello **wyszukiwania** pasek, wprowadź identyfikator użytkownika hello mają toosearch dla użytkownika hello. format Hello wartość Identyfikatora powinna odpowiadać, niezależnie od wybranego jako hello podstawowy identyfikator dopasowania w hello atrybutu mapowania konfiguracji (np. userPrincipalName lub pracowników numer identyfikacyjny). wartość Identyfikatora Hello wymagane będzie widoczny w kolumnie docelowych hello.

5. Naciśnij klawisz Enter toosearch. najpierw zostanie zwrócony Hello najnowszych inicjowania obsługi zdarzeń.

6. Zdarzenia są zwracane, należy pamiętać hello typów działań i czy powodzeniem lub niepowodzeniem. Jeśli żadne wyniki nie są zwracane, następnie oznacza hello użytkownika nie istnieje albo nie ma jeszcze wykryto hello w procesie inicjowania obsługi, jeśli pełnej synchronizacji nie zostało jeszcze zakończone.

7. Polecenie pojedynczych zdarzeń szczegóły tooview rozszerzony, w tym wszystkie właściwości użytkownika, które zostały pobrane, obliczone lub zapisywane jako część hello zdarzeń.


### <a name="tips-for-viewing-hello-provisioning-audit-logs"></a>Porady dotyczące wyświetlania hello inicjowania obsługi dzienników inspekcji

Najlepsze czytelności w hello portalu Azure, wybierz hello **kolumn** przycisk i wybierz następujące kolumny:

* **Data** -pokazuje hello Data hello zdarzenie wystąpiło.
* **Docelowych** — przedstawia hello aplikacji nazwy i Identyfikatora użytkownika będące tematów hello hello zdarzenia.
* **Działanie** — Witaj typ działania, jak opisano wcześniej.
* **Stan** — czy zdarzenie hello zakończyło się powodzeniem, czy nie.
* **Przyczyna stanu** — podsumowanie co się stało w hello inicjowania obsługi zdarzeń.


## <a name="troubleshooting"></a>Rozwiązywanie problemów

Witaj inicjowania obsługi administracyjnej podsumowania dzienniki raportu i inspekcji odgrywają kluczową rolę ułatwienia Administratorzy Rozwiązywanie problemów z różnych inicjowania obsługi problemów z konta użytkownika.

Oparta na scenariuszu wskazówki na temat tootroubleshoot automatycznej aprowizacji użytkowników, zobacz [problemów, konfigurowanie i Inicjowanie obsługi administracyjnej użytkowników aplikacji tooan](active-directory-application-provisioning-content-map.md).


## <a name="additional-resources"></a>Dodatkowe zasoby

* [Zarządzanie aprowizacja konta użytkowników dla aplikacji przedsiębiorstwa](active-directory-enterprise-apps-manage-provisioning.md)
* [Co to jest dostęp do aplikacji i logowanie jednokrotne z usługą Azure Active Directory?](active-directory-appssoaccess-whatis.md)
