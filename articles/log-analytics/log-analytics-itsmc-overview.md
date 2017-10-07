---
title: "Łącznik usługi zarządzania w OMS aaaIT | Dokumentacja firmy Microsoft"
description: "Użyj monitora toocentrally łącznika zarządzania usługi IT hello zarządzania elementami pracy Zarządzanie usługami IT — Witaj w OMS i szybkie rozwiązywanie problemów."
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
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a>Centralne zarządzanie Zarządzanie usługami IT — elementów roboczych za pomocą łącznika zarządzania usługi IT (wersja zapoznawcza)

![Symbol łącznika usługi zarządzania IT](./media/log-analytics-itsmc/itsmc-symbol.png)

Można użyć hello IT usługi zarządzania łącznika (ITSMC) w monitorze toocentrally analizy dzienników OMS i zarządzania elementami pracy przez Zarządzanie usługami IT — produktów/usług.

Hello IT usługi zarządzania łącznika usług i produktach zarządzania usługi IT (zarządzanie, usługami IT —) integruje się z analizy dzienników OMS.  rozwiązanie Hello ma dwukierunkową integrację z Zarządzanie usługami IT — produktów/usług, w przypadku, gdy zapewnia hello OMS użytkowników opcji toocreate zdarzenia, alerty lub zdarzenia w rozwiązaniu Zarządzanie usługami IT —. Łącznik Hello również importuje dane takie jak zdarzenia i żądania zmiany z Zarządzanie usługami IT — rozwiązanie do analizy dzienników OMS.

Łącznik zarządzania usługi IT możesz:

  - Centralnie monitorować i zarządzać nimi elementów roboczych dla Zarządzanie usługami IT — produktów/usług używanych w organizacji.
  - Utwórz Zarządzanie usługami IT — elementów roboczych (na przykład alert, zdarzenie, zdarzenia) w zarządzanie usługami IT — OMS alertów i za pomocą wyszukiwania dziennika.
  - Przeczytaj zdarzenia i żądania zmiany z rozwiązania Zarządzanie usługami IT — skorelowany dziennik odpowiednich danych w obszarze roboczym analizy dzienników.
  - Znajdź wszelkie nieoczekiwane i nietypowe zdarzenia i rozwiązać je, nawet przed użytkownikom końcowym hello wywołań i raportuj je toohello pracy działu pomocy technicznej.
  - Importowanie danych elementów pracy do analizy dzienników i tworzenia raportów kluczowy wskaźnik wydajności.  Korzystanie z tych raportów, możesz zidentyfikować, oceny i działają na kilka istotnych elementów, takich jak oceny złośliwego oprogramowania.
  - Wyświetlić wyselekcjonowanych pulpity nawigacyjne dla lepszy wgląd w zdarzenia, żądań zmiany i wpływ na systemy.
  - Rozwiązywanie problemów szybciej, korelując z innych rozwiązań do zarządzania w obszarze roboczym analizy dzienników hello.


## <a name="prerequisites"></a>Wymagania wstępne

tooimport hello Zarządzanie usługami IT — elementów pracy do analizy dzienników OMS, hello rozwiązanie wymaga połączenia między hello łącznika zarządzania usługi IT w hello OMS i IT SM hello produktu lub usługi, z których importować hello elementów roboczych.


## <a name="configuration"></a>Konfiguracja

Dodaj hello obszar roboczy łącznika zarządzania usługi IT rozwiązania tooyour OMS, za pomocą hello procesu opisanego w [rozwiązań analizy dzienników dodać hello galerii rozwiązań](log-analytics-add-solutions.md).

Łącznik zarządzania usługi IT kafelka, jak widać w galerii rozwiązań hello:

![Łącznik kafelka](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

Po pomyślnym dodaniu zobaczysz hello łącznika zarządzania usługi IT w obszarze **OMS** > **ustawienia** > **połączonych źródeł.**

![ITSMC połączone](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> Domyślnie hello łącznika zarządzania usługi IT odświeża dane połączenia hello raz w co 24 godziny. toorefresh tego połączenia danych natychmiast dla wszystkich edycji lub szablon aktualizacji, które zostaną wprowadzone, kliknij przycisk hello odświeżania wyświetlany przycisk następnej tooyour połączenie.

 ![Odśwież ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a>Pakiety administracyjne
To rozwiązanie nie wymaga żadnych pakietów administracyjnych.

## <a name="connected-sources"></a>Połączone źródła

Witaj następujących produktów/usług Zarządzanie usługami IT — są obsługiwane przez hello łącznika zarządzania usługi IT:

- [Program System Center Service Manager (SCSM)](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [Usługi ServiceNow](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [Provance](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [Cherwell](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a>Za pomocą rozwiązania hello

Po podłączeniu hello OMS IT usługi zarządzania łącznika z usługą Zarządzanie usługami IT — usługi analizy dzienników hello rozpoczyna zbieranie danych hello z Zarządzanie usługami IT — hello połączone produktów/usług.

> [!NOTE]
> - Dane importowane przez rozwiązanie łącznika zarządzania usługi IT pojawia się w analizy dziennika jako zdarzenia o nazwie **ServiceDesk_CL**.
- Zdarzenie zawiera pole o nazwie **ServiceDeskWorkItemType_s**. które wykonać jego wartość, jak zdarzenia lub żądania zmiany, w zależności od hello elementu roboczego dane zawarte w hello **ServiceDesk_CL** zdarzeń.

## <a name="input-data"></a>Dane wejściowe
Elementy robocze zaimportowane z hello Zarządzanie usługami IT — produktów/usług.

Witaj następujące informacje znajdują się przykładowe dane zebrane przez łącznik zarządzania usługami INFORMATYCZNYMI hello:

> [!NOTE]
> W zależności od hello typu elementu roboczego zaimportowane do analizy dzienników **ServiceDesk_CL** zawiera hello następujące pola:

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
| ServiceDeskId_s| Liczba |
| IncidentState_s | Stan |
| Urgency_s |Pilności |
| Impact_s |Wpływ|
| Priority_s | Priorytet |
| CreatedBy_s | Otwarty przez |
| ResolvedBy_s | Rozwiązany przez|
| ClosedBy_s  | Zamknięte przez |
| Source_s| Skontaktuj się z typu |
| AssignedTo_s | Zbyt przypisany |
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
| ServiceDeskId_s| Liczba |
| CreatedBy_s | Żądanie |
| ClosedBy_s | Zamknięte przez |
| AssignedTo_s | Zbyt przypisany |
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

Łącznik zarządzania usługi IT, obecnie obsługuje integrację z hello rozwiązania mapy usługi.

Mapa usług automatycznie odnajduje hello składniki aplikacji w systemie Windows i systemów Linux i map hello komunikacji między usługami. Pozwala ona tooview serwerów jako należy wziąć pod uwagę z nich — jako połączonych systemy, które dostarczają usług krytycznych. Mapy usługi pokazuje połączeń między serwerami, procesów, i portów w dowolnej architekturze połączenia TCP z konfiguracji wymagane inne niż instalacji agenta. Więcej informacji: [mapy usługi](../operations-management-suite/operations-management-suite-service-map.md).

Z tej integracji można wyświetlać elementy technicznej usług hello utworzone w hello Zarządzanie usługami IT — rozwiązania, jak pokazano w hello poniższy przykład:

![Zintegrowane rozwiązanie ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a>Tworzenie elementów roboczych Zarządzanie usługami IT — OMS alertów

Hello OMS alertów można utworzyć skojarzonych elementów roboczych w źródłach Zarządzanie usługami IT — Witaj połączony.  toodo tego hello użyj następującej procedury:

1. Z **wyszukiwania dziennika** okna danych tooview zapytania wyszukiwania dziennika jest uruchamiane. Wyniki zapytania są źródłem powitania dla elementów roboczych.
2. W **wyszukiwania dziennika**, kliknij przycisk **alertu** tooopen hello **Dodaj regułę alertu** strony.

    ![Ekran analiza dziennika](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. Na powitania **Dodaj regułę alertu** okna, podaj szczegóły hello wymagane **nazwa**, **ważność**, **zapytania wyszukiwania**, i  **Kryteria alertu** (pomiar Metryka okno czasu).
4. Wybierz **tak** dla **akcje Zarządzanie usługami IT —**.
5. Wybierz połączenie Zarządzanie usługami IT — od hello **połączenia wybierz** listy.
6. Podaj szczegóły hello zgodnie z potrzebami.
7. toocreate elementu roboczego osobne dla każdego wpisu dziennika z tym hello alertów, wybierz pozycję **utworzyć poszczególnych elementach roboczych dla każdego wpisu dziennika** wyboru.

    Lub

    Pozostaw to pole wyboru niezaznaczone toocreate tylko jednego elementu roboczego dla dowolnej liczby wpisów dziennika w ramach tego alertu.

7. Kliknij pozycję **Zapisz**.

Hello OMS alert zostaną utworzone w obszarze **alerty**. Witaj pracy odpowiedniego połączenia Zarządzanie usługami IT — elementy są tworzone po spełnieniu warunku hello określony alert.

## <a name="create-itsm-work-items-from-oms-logs"></a>Tworzenie elementów roboczych Zarządzanie usługami IT — z dzienników OMS

Można utworzyć elementów roboczych w źródłach Zarządzanie usługami IT — Witaj połączone za pomocą wyszukiwania dziennika OMS. toodo tego hello użyj następującej procedury:

1. Z **wyszukiwania dziennika**, wyszukiwanie danych hello wymagane, wybierz hello szczegółów, a następnie kliknij przycisk **Utwórz element roboczy**.

    Witaj **elementu roboczego Zarządzanie usługami IT — tworzenie** zostanie wyświetlone okno:

    ![Ekran analiza dziennika](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   Dodaj hello poniższe informacje:

  - **Tytuł elementu pracy**: tytuł dla elementu roboczego hello.
  - **Opis elementu roboczego**: opis hello nowego elementu roboczego.
  - **Wpływ na komputerze**: Nazwa komputera hello, gdzie te dane dziennika został znaleziony.
  - **Wybierz połączenie**: Zarządzanie usługami IT — połączenie, w którym chcesz toocreate tego elementu roboczego.
  - **Element roboczy**: typ elementu roboczego.

3. toouse istniejącego szablonu elementu pracy zdarzenia, kliknij przycisk **tak** w obszarze **Generuj element pracy oparty na szablonie hello** opcji, a następnie kliknij przycisk **Utwórz**.

    Lub:

    Kliknij przycisk **nr** Jeśli chcesz tooprovide dostosowanych wartości.

4. Podaj odpowiednie wartości hello w hello **typ**, **wpływ**, **pilność**, **kategorii**, i **podkategorii**  pola tekstowe, a następnie kliknij przycisk **Utwórz**.

element roboczy Hello zostaną utworzone w hello Zarządzanie usługami IT —, które można również wyświetlić OMS.

## <a name="troubleshoot-itsm-connections-in-oms"></a>Rozwiązywanie problemów z połączeniami Zarządzanie usługami IT — w OMS
1.  Jeśli połączenie nie powiedzie się z połączonych źródła interfejsu użytkownika i pobrać hello **błąd podczas zapisywania połączenia** komunikatów, hello następujące:
 - W przypadku połączenia usługi ServiceNow, Cherwell i Provance upewnij się, możesz hello prawidłowo wprowadzić nazwę użytkownika/hasło i klienta identyfikator/klucz tajny klienta dla każdego połączenia hello. Jeśli hello błąd będzie się powtarzał, sprawdź, czy masz wystarczające uprawnienia w hello odpowiednie zarządzanie usługami IT — produktu toomake hello połączenia.
 - W przypadku programu Service Manager, sprawdź, czy aplikacja sieci Web powitania po pomyślnym wdrożeniu i utworzono połączenie hybrydowe. pomyślnie jest nawiązywane połączenie hello tooverify z hello lokalnego programu Service Manager maszyny, odwiedź adres URL aplikacji sieci Web hello zgodnie z opisem w dokumentacji hello dokonywania hello [połączenia hybrydowego](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).

2.  Jeśli dane z usługi ServiceNow nie jest pierwsze zsynchronizowane w OMS, upewnij się, że to wystąpienie usługi ServiceNow hello nie jest uśpiony. Taka sytuacja może chwilę wystąpić w hello wystąpień usługi ServiceNow deweloperów, po bezczynności. Else, zgłoś problem hello.
3.  Jeśli alerty pobierania uruchomienia z pakietu OMS, ale nie pobierania utworzonych elementów roboczych w zarządzanie usługami IT — produktu lub elementy konfiguracji nie otrzymują toowork utworzone połączone elementy lub wszelkie informacje ogólne, hello następujące:
 -  Rozwiązanie usługi zarządzania łącznika IT w portalu OMS może być używane tooget podsumowanie połączeń/pracy elementów/komputerów itp. Komunikat o błędzie hello w bloku stanu powitania kliknij kolejno zbyt**wyszukiwania dziennika** i wyświetlić hello połączenie, które zawiera błąd hello przy użyciu okna Szczegóły hello w komunikacie o błędzie hello.
 - informacje związane z/błędy hello bezpośrednio można wyświetlić w hello **wyszukiwania dziennika** strony *typu = ServiceDeskLog_CL*.

## <a name="troubleshoot-service-manager-web-app-deployment"></a>Rozwiązywanie problemów z wdrażaniem aplikacji sieci Web programu Service Manager
1.  W przypadku problemów z wdrożeniem aplikacji sieci web upewnij się, masz wystarczające uprawnienia w subskrypcji hello wymienionych toocreate/wdrażanie zasobów.
2.  Jeśli **odwołania do obiektu nie jest ustawiony tooinstance obiektu** komunikat o błędzie jest wyświetlany podczas uruchamiania hello [skryptu](log-analytics-itsmc-service-manager-script.md) upewnij się, że wprowadzono prawidłowe wartości w obszarze **Konfiguracja użytkownika**sekcji.
3.  Jeśli nie zostanie toocreate przestrzeń nazw przekaźnik magistrali usług, upewnij się, że dostawca zasobów jest zarejestrowane w subskrypcji hello wymagane tego hello. Jeśli nie jest zarejestrowany, ręcznie utwórz je z hello portalu Azure. Można również utworzyć go podczas [Tworzenie połączenia hybrydowego hello](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) z hello portalu Azure.


## <a name="contact-us"></a>Skontaktuj się z nami

Dla zapytania lub opinie na powitania łącznika zarządzania usługi IT, skontaktuj się z nami pod adresem [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).

## <a name="next-steps"></a>Następne kroki
[Dodaj tooIT produktów i usług Zarządzanie usługami IT — usługi zarządzania łącznika](log-analytics-itsmc-connections.md).
