---
title: "IT usługi łącznika zarządzania w OMS | Dokumentacja firmy Microsoft"
description: "Użyj łącznika zarządzania usługi IT, aby centralnie monitorować i zarządzać nimi elementy robocze Zarządzanie usługami IT — w OMS i szybkie rozwiązywanie problemów."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 54974ef06efdae69ddbfa12b1ba9278b48b113d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>Centralne zarządzanie Zarządzanie usługami IT — elementów roboczych za pomocą łącznika zarządzania usługi IT (wersja zapoznawcza)

![Symbol łącznika usługi zarządzania IT](./media/log-analytics-itsmc/itsmc-symbol.png)

Łącznik zarządzania usługi IT (ITSMC) OMS Log Analytics umożliwia centralnie monitorować i zarządzać nimi elementy robocze między Zarządzanie usługami IT — produktów/usług.

Łącznik zarządzania usługi IT istniejących zarządzania usługi IT (zarządzanie, usługami IT —) produkty i usługi integruje się z analizy dzienników OMS.  Rozwiązanie ma dwukierunkową integrację z Zarządzanie usługami IT — produktów/usług, których zapewnia użytkownikom OMS opcję, aby utworzyć zdarzenia i alerty lub zdarzenia w rozwiązaniu Zarządzanie usługami IT —. Łącznik również importuje dane takie jak zdarzenia i żądania zmiany z Zarządzanie usługami IT — rozwiązanie do analizy dzienników OMS.

Łącznik zarządzania usługi IT możesz:

  - Centralnie monitorować i zarządzać nimi elementów roboczych dla Zarządzanie usługami IT — produktów/usług używanych w organizacji.
  - Utwórz Zarządzanie usługami IT — elementów roboczych (na przykład alert, zdarzenie, zdarzenia) w zarządzanie usługami IT — OMS alertów i za pomocą wyszukiwania dziennika.
  - Przeczytaj zdarzenia i żądania zmiany z rozwiązania Zarządzanie usługami IT — skorelowany dziennik odpowiednich danych w obszarze roboczym analizy dzienników.
  - Znajdź wszelkie nieoczekiwane i nietypowe zdarzenia i rozwiąż je, nawet przed użytkowników końcowych wywołań i raportuj je do działu pomocy technicznej.
  - Importowanie danych elementów pracy do analizy dzienników i tworzenia raportów kluczowy wskaźnik wydajności.  Korzystanie z tych raportów, możesz zidentyfikować, oceny i działają na kilka istotnych elementów, takich jak oceny złośliwego oprogramowania.
  - Wyświetlić wyselekcjonowanych pulpity nawigacyjne dla lepszy wgląd w zdarzenia, żądań zmiany i wpływ na systemy.
  - Rozwiązywanie problemów szybciej, korelując z innych rozwiązań do zarządzania w obszarze roboczym analizy dzienników.


## <a name="prerequisites"></a>Wymagania wstępne

Aby zaimportować elementy robocze Zarządzanie usługami IT — do analizy dzienników OMS, rozwiązanie wymaga połączenia między łącznika zarządzania usługi IT w OMS i IT SM produktu lub usługi z którego importowania elementów roboczych.


## <a name="configuration"></a>Konfiguracja

Dodaj rozwiązanie IT usługi zarządzania łącznika do obszaru roboczego OMS zastosowanie procesu opisanego w [rozwiązań dodać analizy dzienników z galerii rozwiązań](log-analytics-add-solutions.md).

Łącznik zarządzania usługi IT kafelka, jak widać w galerii rozwiązań:

![Łącznik kafelka](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Po pomyślnym dodaniu zobaczysz łącznika zarządzania usługi IT w obszarze **OMS** > **ustawienia** > **połączonych źródeł.**

![ITSMC połączone](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Domyślnie łącznika zarządzania usługi IT odświeża dane połączenia raz w co 24 godziny. Aby odświeżyć tego połączenia danych natychmiast dla wszystkich edycji lub szablonu aktualizacje, które zostaną wprowadzone, kliknij przycisk Odśwież wyświetlana obok połączenia.

 ![Odśwież ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Pakiety administracyjne
To rozwiązanie nie wymaga żadnych pakietów administracyjnych.

## <a name="connected-sources"></a>Połączone źródła

Następujące produkty Zarządzanie usługami IT — / usługi są obsługiwane przez łącznik zarządzania usługi IT:

- [Program System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [Usługi ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-the-solution"></a>Użycie rozwiązania

Po podłączeniu łącznika zarządzania OMS IT usługi z usługą Zarządzanie usługami IT — usługi analizy dzienników rozpoczyna zbieranie danych z połączonych Zarządzanie usługami IT — produktów/usług.

> [!NOTE]
> - Dane importowane przez rozwiązanie łącznika zarządzania usługi IT pojawia się w analizy dziennika jako zdarzenia o nazwie **ServiceDesk_CL**.
- Zdarzenie zawiera pole o nazwie **ServiceDeskWorkItemType_s**. które wykonać jego wartość jako zdarzenie lub żądanie, w zależności od danych elementów pracy znajdujących się na zmiany **ServiceDesk_CL** zdarzeń.

## <a name="input-data"></a>Dane wejściowe
Elementy pracy zaimportowane z Zarządzanie usługami IT — produktów/usług.

Poniższe informacje przedstawiono przykładowe dane zebrane przez łącznik zarządzania usługami IT:

> [!NOTE]
> W zależności od typu elementu roboczego zaimportowane do analizy dzienników **ServiceDesk_CL** zawiera następujące pola:

**Element pracy:** **zdarzenia**  
ServiceDeskWorkItemType_s = "Zdarzenie"

**Pola**

- ServiceDeskConnectionName
- Identyfikator technicznej usługi
- Stan
- Pilności
- Wpływ
- Priorytet
- Eskalacja
- Utworzone przez
- Rozwiązany przez
- Zamknięte przez
- Element źródłowy
- Przypisane do
- Kategoria
- Tytuł
- Opis
- Data utworzenia
- Data zamknięcia
- Data rozwiązania
- Data ostatniej modyfikacji
- Computer (Komputer)


**Element pracy:** **żądania zmiany**

ServiceDeskWorkItemType_s = "Żądanie zmiany"

**Pola**
- ServiceDeskConnectionName
- Identyfikator technicznej usługi
- Utworzone przez
- Zamknięte przez
- Element źródłowy
- Przypisane do
- Tytuł
- Typ
- Kategoria
- Stan
- Eskalacja
- Konflikt stanu
- Pilności
- Priorytet
- Ryzyko
- Wpływ
- Przypisane do
- Data utworzenia
- Data zamknięcia
- Data ostatniej modyfikacji
- Żądana data
- Planowana data rozpoczęcia
- Planowana data zakończenia
- Data rozpoczęcia pracy
- Data zakończenia pracy
- Opis
- Computer (Komputer)

## <a name="output-data-for-a-servicenow-incident"></a>Dane wyjściowe dla zdarzenia usługi ServiceNow

| Pole OMS | Zarządzanie usługami IT — pola |
|:--- |:--- |
| ServiceDeskId_s| Numer |
| IncidentState_s | Stan |
| Urgency_s |Pilności |
| Impact_s |Wpływ|
| Priority_s | Priorytet |
| CreatedBy_s | Otwarty przez |
| ResolvedBy_s | Rozwiązany przez|
| ClosedBy_s  | Zamknięte przez |
| Source_s| Skontaktuj się z typu |
| AssignedTo_s | Przypisane do  |
| Category_s | Kategoria |
| Title_s|  Krótki opis |
| Description_s|  Uwagi |
| CreatedDate_t|  Otwarte |
| ClosedDate_t| zamknięte|
| ResolvedDate_t|Rozwiązane|
| Computer (Komputer)  | element konfiguracji |

## <a name="output-data-for-a-servicenow-change-request"></a>Dane wyjściowe dla usługi ServiceNow żądania zmiany

| Pole OMS | Zarządzanie usługami IT — pola |
|:--- |:--- |
| ServiceDeskId_s| Numer |
| CreatedBy_s | Żądanie |
| ClosedBy_s | Zamknięte przez |
| AssignedTo_s | Przypisane do  |
| Title_s|  Krótki opis |
| Type_s|  Typ |
| Category_s|  Catgory |
| CRState_s|  Stan|
| Urgency_s|  Pilności |
| Priority_s| Priorytet|
| Risk_s| Ryzyko|
| Impact_s| Wpływ|
| RequestedDate_t  | Żądana według daty |
| ClosedDate_t | Data zamknięcia |
| PlannedStartDate_t  |     Planowana data rozpoczęcia |
| PlannedEndDate_t  |   Planowana data zakończenia |
| WorkStartDate_t  | Rzeczywista data rozpoczęcia |
| WorkEndDate_t | Rzeczywista data zakończenia|
| Description_s | Opis |
| Computer (Komputer)  | Element konfiguracji |

**Przykładowy ekran analizy dzienników dla danych Zarządzanie usługami IT —:**

![Ekran analiza dziennika](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a>Łącznik zarządzania usługami IT — Integracja z innych rozwiązań pakietu OMS

Łącznik zarządzania usługi IT, obecnie obsługuje integrację z rozwiązaniem mapy usługi.

Mapa usług automatycznie wykrywa składniki aplikacji w systemach Windows i Linux i mapuje komunikacji między usługami. Umożliwia ona przeglądać serwery jako traktować ich — jako połączonych systemy, które dostarczają usług krytycznych. Mapy usługi pokazuje połączeń między serwerami, procesów, i portów w dowolnej architekturze połączenia TCP z konfiguracji wymagane inne niż instalacji agenta. Więcej informacji: [mapy usługi](../operations-management-suite/operations-management-suite-service-map.md).

Dzięki tej integracji można wyświetlić elementy technicznej usług utworzone w rozwiązaniach Zarządzanie usługami IT —, jak pokazano w poniższym przykładzie:

![Zintegrowane rozwiązanie ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>Tworzenie elementów roboczych Zarządzanie usługami IT — OMS alertów

Dla alertów OMS w połączonych źródeł Zarządzanie usługami IT — można utworzyć skojarzonych elementów roboczych.  Aby to zrobić, użyj następującej procedury:

1. Z **wyszukiwania dziennika** okna, uruchom zapytania wyszukiwania dziennika, aby wyświetlić dane. Wyniki zapytania są źródłem dla elementów roboczych.
2. W **wyszukiwania dziennika**, kliknij przycisk **alertu** otworzyć **Dodaj regułę alertu** strony.

    ![Ekran analiza dziennika](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. Na **Dodaj regułę alertu** okna, podaj wymagane szczegóły dotyczące **nazwa**, **ważność**, **zapytania wyszukiwania**, i **alertu kryteria** (pomiar Metryka okno czasu).
4. Wybierz **tak** dla **akcje Zarządzanie usługami IT —**.
5. Wybierz połączenie Zarządzanie usługami IT — od **połączenia wybierz** listy.
6. Podaj szczegóły zgodnie z potrzebami.
7. Aby utworzyć element roboczy osobne dla każdego wpisu dziennika tego alertu, wybierz **utworzyć poszczególnych elementach roboczych dla każdego wpisu dziennika** wyboru.

    Lub

    Pozostaw to pole wyboru niezaznaczone można utworzyć tylko jeden element roboczy dla dowolnej liczby wpisów dziennika w ramach tego alertu.

7. Kliknij pozycję **Zapisz**.

OMS alert zostaną utworzone w obszarze **alerty**. Zarządzanie usługami IT — połączenie odpowiednich elementów roboczych są tworzone po spełnieniu warunku określony alert.

## <a name="create-itsm-work-items-from-oms-logs"></a>Tworzenie elementów roboczych Zarządzanie usługami IT — z dzienników OMS

Elementy robocze w połączonych źródeł Zarządzanie usługami IT — można utworzyć za pomocą wyszukiwania dziennika OMS. Aby to zrobić, użyj następującej procedury:

1. Z **wyszukiwania dziennika**, wyszukaj wymagane dane, wybierz szczegóły, a następnie kliknij przycisk **Utwórz element roboczy**.

    **Elementu roboczego Zarządzanie usługami IT — tworzenie** zostanie wyświetlone okno:

    ![Ekran analiza dziennika](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Dodaj następujące informacje:

  - **Tytuł elementu pracy**: tytuł dla elementu roboczego.
  - **Opis elementu roboczego**: opis nowego elementu roboczego.
  - **Wpływ na komputerze**: Nazwa komputera, na którym zostało znalezione te dane dziennika.
  - **Wybierz połączenie**: Zarządzanie usługami IT — połączenie, w którym chcesz utworzyć ten element roboczy.
  - **Element roboczy**: typ elementu roboczego.

3. Aby korzystać z istniejących szablonów elementów pracy zdarzenia, kliknij przycisk **tak** w obszarze **Generuj element pracy oparty na szablonie** opcji, a następnie kliknij przycisk **Utwórz**.

    Lub:

    Kliknij przycisk **nr** Jeśli chcesz podać dostosowanych wartości.

4. Podaj odpowiednie wartości w **typ**, **wpływ**, **pilność**, **kategorii**, i **podkategorii** pola tekstowe, a następnie kliknij przycisk **Utwórz**.

Element pracy zostanie utworzony w zarządzanie usługami IT —, które można również wyświetlić OMS.

## <a name="troubleshoot-itsm-connections-in-oms"></a>Rozwiązywanie problemów z połączeniami Zarządzanie usługami IT — w OMS
1.  Jeśli połączenie nie powiedzie się z poziomu interfejsu użytkownika połączenia źródła i możesz uzyskać **błąd podczas zapisywania połączenia** wiadomości, wykonaj następujące czynności:
 - W przypadku połączenia usługi ServiceNow, Cherwell i Provance upewnij się, że poprawnie wprowadzono hasła identyfikator/klienta nazwy użytkownika i hasła i klienta dla każdego połączenia. Jeśli błąd będzie się powtarzać, sprawdź, czy masz wystarczające uprawnienia w produktu Zarządzanie usługami IT — do nawiązania połączenia.
 - W przypadku programu Service Manager upewnij się, że aplikacji sieci Web zostanie pomyślnie wdrożona i utworzono połączenie hybrydowe. Aby sprawdzić pomyślnym nawiązaniu połączenia z komputera lokalnego programu Service Manager, odwiedź adres URL aplikacji sieci Web zgodnie z opisem w dokumentacji dotyczącej wprowadzania [połączenia hybrydowego](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  Jeśli dane z usługi ServiceNow nie jest pierwsze zsynchronizowane w OMS, upewnij się, że usługi ServiceNow, wystąpienie nie jest uśpiony. Może to nastąpić pewnego czasu w wystąpieniach deweloperów usługi ServiceNow, po bezczynności. W przeciwnym wypadku zgłosić problem.
3.  Jeśli alerty pobierania uruchomienia z pakietu OMS, ale elementy robocze nie są pobierania utworzone w zarządzanie usługami IT — elementy produktu lub konfiguracja nie otrzymują utworzone/połączone z elementów roboczych lub informacje o ogólnym, wykonaj następujące czynności:
 -  Rozwiązanie usługi zarządzania łącznika IT w portalu OMS może posłużyć do uzyskać podsumowanie połączeń/pracy elementów/komputerów itp. Kliknij komunikat o błędzie w bloku stanu, przejdź do **wyszukiwania dziennika** i wyświetlić połączenia, które zawiera błąd przy użyciu szczegóły komunikatu o błędzie.
 - bezpośrednio można wyświetlić informacje związane z/błędy w **wyszukiwania dziennika** strony *typu = ServiceDeskLog_CL*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Rozwiązywanie problemów z wdrażaniem aplikacji sieci Web programu Service Manager
1.  W przypadku problemów z wdrożeniem aplikacji sieci web upewnij się, że masz wystarczające uprawnienia w wymienionych do tworzenia/wdrożenie zasobów subskrypcji.
2.  Jeśli **obiekt odwołanie nie jest ustawione na wystąpienie obiektu** komunikat o błędzie pojawia się podczas pracy [skryptu](log-analytics-itsmc-service-manager-script.md) upewnij się, że wprowadzono prawidłowe wartości w obszarze **Konfiguracja użytkownika** sekcja.
3.  Nie można utworzyć przestrzeń nazw przekaźnik magistrali usług, upewnij się, że dostawca wymagany zasób jest zarejestrowany w subskrypcji. Jeśli nie jest zarejestrowany, ręcznie utworzyć go w portalu Azure. Można również utworzyć go podczas [Tworzenie połączenia hybrydowego](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) z portalu Azure.


## <a name="contact-us"></a>Skontaktuj się z nami

Dla zapytania lub opinii na temat łącznika zarządzania usługi IT, skontaktuj się z nami pod adresem [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Następne kroki
[Dodaj do łącznika zarządzania usługi IT zarządzanie usługami IT — produktów/usług](log-analytics-itsmc-connections.md).
