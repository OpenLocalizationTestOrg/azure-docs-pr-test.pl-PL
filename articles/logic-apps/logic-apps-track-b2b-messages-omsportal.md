---
title: "komunikaty aaaTrack B2B w Operations Management Suite — usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Śledzenie komunikacji B2B dla aplikacji logiki i konta integracji w Operations Management Suite (OMS) z usługi Analiza dzienników Azure"
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: f385a72008b19408bb45d61c440df0505b688175
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="track-b2b-communication-in-hello-microsoft-operations-management-suite-oms"></a>Śledzenie komunikacji B2B w hello programu Microsoft Operations Management Suite (OMS)

Po skonfigurowaniu B2B komunikacji między dwiema uruchomionych procesów biznesowych lub aplikacji za pośrednictwem konta integracji tych jednostek mogą wymieniać komunikaty ze sobą. toocheck czy komunikaty te są przetwarzane prawidłowo, można śledzić AS2, X12, i EDIFACT wiadomości z [Azure Log Analytics](../log-analytics/log-analytics-overview.md) w hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Na przykład można użyć tych możliwości śledzenia opartych na sieci web do śledzenia komunikatów:

* Liczba komunikatów i stanu
* Stan potwierdzenia
* Korelowanie wiadomości z potwierdzenia
* Szczegółowe informacje o błędzie opisy błędów
* Możliwości wyszukiwania

## <a name="requirements"></a>Wymagania

* Aplikację logiki, który został skonfigurowany z rejestrowania diagnostyki. Dowiedz się [jak toocreate aplikacji logiki](logic-apps-create-a-logic-app.md) i [jak tooset rejestrowanie dla danej aplikacji logiki danych](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

* Konta integracji, które skonfigurowano przy użyciu rejestrowania i monitorowania. Dowiedz się [jak toocreate konta integracji](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) i [jak tooset monitorowania i rejestrowania dla tego konta](../logic-apps/logic-apps-monitor-b2b-message.md).

* Jeśli nie jest jeszcze, [publikowania danych diagnostycznych tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) w OMS.

> [!NOTE]
> Po zostały spełnione wymagania poprzedniej hello, powinien mieć obszar roboczy w hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md). Należy używać tego samego pakietu OMS obszaru roboczego do śledzenia komunikacji B2B w OMS hello. 
>  
> Dowiedz się, jeśli nie masz obszar roboczy OMS [jak toocreate obszarem roboczym pakietu OMS](../log-analytics/log-analytics-get-started.md).

## <a name="add-hello-logic-apps-b2b-solution-toohello-operations-management-suite-oms"></a>Dodaj toohello rozwiązania hello B2B aplikacje logiki Operations Management Suite (OMS)

toohave OMS śledzenie wiadomości B2B aplikacji logiki, należy dodać hello **B2B aplikacje logiki** portalu OMS toohello rozwiązania. Dowiedz się więcej o [Dodawanie rozwiązania tooOMS](../log-analytics/log-analytics-get-started.md).

1. W hello [portalu Azure](https://portal.azure.com), wybierz **więcej usług**. Wyszukaj "analizy dzienników", a następnie wybierz pozycję **analizy dzienników** w sposób pokazany poniżej:

   ![Znajdź analizy dzienników](media/logic-apps-track-b2b-messages-omsportal/browseloganalytics.png)

2. W obszarze **analizy dzienników**, Znajdź i wybierz obszar roboczy OMS. 

   ![Wybierz obszar roboczy OMS](media/logic-apps-track-b2b-messages-omsportal/selectla.png)

3. W obszarze **zarządzania**, wybierz **portalu OMS**.

   ![Wybierz portalu OMS](media/logic-apps-track-b2b-messages-omsportal/omsportalpage.png)

4. Po otwarciu strony głównej OMS hello wybierz **galerii rozwiązań**.    

   ![Wybierz galerii rozwiązań](media/logic-apps-track-b2b-messages-omsportal/omshomepage1.png)

5. W obszarze **wszystkie rozwiązania**, Znajdź i wybierz **B2B aplikacje logiki**.     

   ![Wybierz B2B aplikacje logiki](media/logic-apps-track-b2b-messages-omsportal/omshomepage2.png)

6. W obszarze **B2B aplikacje logiki**, wybierz **Dodaj**.

   ![Wybierz opcję Dodaj](media/logic-apps-track-b2b-messages-omsportal/omshomepage3.png)

   Na stronie głównej OMS hello hello Kafelek **wiadomości B2B aplikacje logiki** pojawi się teraz. 
   Ten Kafelek aktualizuje liczba wiadomości powitania podczas przetwarzania wiadomości B2B.

   ![Strona główna OMS, kafelka wiadomości B2B aplikacje logiki](media/logic-apps-track-b2b-messages-omsportal/omshomepage4.png)

<a name="message-status-details"></a>

## <a name="track-message-status-and-details-in-hello-operations-management-suite"></a>Śledzenie stanu komunikat i szczegóły hello Operations Management Suite

1. Po przetworzeniu wiadomości B2B można wyświetlić stan hello i szczegóły dotyczące tych wiadomości. Na stronie głównej OMS hello, wybierz hello **wiadomości B2B aplikacje logiki** kafelka.

   ![Liczba komunikatów zaktualizowane](media/logic-apps-track-b2b-messages-omsportal/omshomepage6.png)

   > [!NOTE]
   > Domyślnie program hello **wiadomości B2B aplikacje logiki** kafelka zawiera dane oparte na jeden dzień. dane hello toochange zakres tooa inny interwał, wybierz kontrola zakresu hello u góry hello hello OMS strony:
   > 
   > ![Zmień zakres danych](media/logic-apps-track-b2b-messages-omsportal/change-interval.png)
   >

2. Po stan wiadomość hello pulpitu nawigacyjnego zostanie wyświetlony, można wyświetlić więcej szczegółów dla typu określonego komunikatu, która zawiera dane oparte na jeden dzień. Wybierz Kafelek hello **AS2**, **X12**, lub **EDIFACT**.

   ![Wyświetlanie komunikatów stanu](media/logic-apps-track-b2b-messages-omsportal/omshomepage5.png)

   Zostanie wyświetlona lista komunikatów dla wybranej kafelka. 
   Opis właściwości tych wiadomości znajduje się w toolearn więcej informacji na temat hello właściwości dla każdego typu komunikatu:

   * [Właściwości komunikatu AS2](#as2-message-properties)
   * [Właściwości wiadomości X12](#x12-message-properties)
   * [Właściwości komunikatu EDIFACT](#EDIFACT-message-properties)

   Na przykład Oto jak może wyglądać AS2 listy komunikatów:

   ![Wyświetlanie komunikatów AS2](media/logic-apps-track-b2b-messages-omsportal/as2messagelist.png)

3. wejścia hello tooview lub eksportu i wyjścia dla określonych wiadomości, zaznacz tych wiadomości i wybierz polecenie **Pobierz**. Po wyświetleniu monitu, Zapisz komputera lokalnego tooyour pliku zip hello, a następnie Wyodrębnij tego pliku. 

   Hello wyodrębnionego folder zawiera folder dla każdego wybranego komunikatu. 
   Jeśli konfigurujesz potwierdzeń folderu wiadomości powitania także pliki ze szczegółami potwierdzenia. 
   Każdy komunikat znajduje się w nim co najmniej tych plików: 
   
   * Czytelny dla człowieka pliki z hello ładunku i dane wyjściowe szczegóły ładunek danych wejściowych
   * Pliki zakodowane z hello wejścia i wyjścia

   Dla każdego typu komunikatu można znaleźć folderu hello i formatów nazwy pliku:

   * [Formaty nazwę folderowi i plikowi AS2](#as2-folder-file-names)
   * [X12 folder i nazwę pliku formatów](#x12-folder-file-names)
   * [EDIFACT formatów nazwy plików i folderów](#edifact-folder-file-names)

   ![Pobieranie plików komunikatów](media/logic-apps-track-b2b-messages-omsportal/download-messages.png)

4. Uruchom wszystkie akcje, które mają takie same hello tooview identyfikator na powitania **wyszukiwania dziennika** wybierz z listy wiadomość hello wiadomości.

   Czynności te według kolumny lub wyszukaj określone wyniki można sortować.

   ![Akcje z hello sam identyfikator uruchomienia](media/logic-apps-track-b2b-messages-omsportal/logsearch.png)

   * Wybierz toosearch wyników z kwerendy wbudowane **ulubione**.

   * Dowiedz się [jak toobuild kwerendy, dodając filtry](logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md). 
   Lub Dowiedz się więcej o [jak toofind danych z dziennika wyszukuje w analizy dzienników](../log-analytics/log-analytics-log-searches.md).

   * toochange zapytanie w polu wyszukiwania hello aktualizacji hello kwerendy z kolumnami hello i wartości mają toouse jako filtry.

<a name="message-list-property-descriptions"></a>

## <a name="property-descriptions-and-name-formats-for-as2-x12-and-edifact-messages"></a>Opisy właściwości i formatów nazwy dla AS2, X 12 i EDIFACT wiadomości

Dla każdego typu komunikatu poniżej przedstawiono opisy właściwości hello i formatów nazwy plików pobranych wiadomości.

<a name="as2-message-properties"></a>

### <a name="as2-message-property-descriptions"></a>Opisy właściwości komunikatu AS2

Poniżej przedstawiono opisy właściwości powitania dla każdego komunikatu AS2.

| Właściwość | Opis |
| --- | --- |
| Nadawca | partner gościa Hello określone w **odbierania ustawień**, lub partnera hosta hello określone **ustawienia wysyłania** umowy AS2 |
| Odbiornik | Hello partnera hosta określona w **ustawienia odbierania**, lub partnera gościa hello określone **ustawienia wysyłania** umowy AS2 |
| Aplikacja logiki | gdzie są skonfigurowane akcje hello AS2 aplikacji logiki Hello |
| Stan | Witaj AS2 komunikatu stanu <br>Powodzenie = odebranych lub wysłanych prawidłowego elementu message AS2. MDN nie jest skonfigurowane. <br>Powodzenie = odebranych lub wysłanych prawidłowego elementu message AS2. Ustawianie i odebranych MDN lub MDN są wysyłane. <br>Nie powiodło się = Odebrano nieprawidłowy komunikat AS2. MDN nie jest skonfigurowane. <br>Oczekujące = odebranych lub wysłanych prawidłowego elementu message AS2. MDN jest skonfigurowany, a oczekiwano MDN. |
| ACK. | Witaj MDN komunikatu stanu <br>Zaakceptowane = odebranych lub wysłanych MDN dodatnią. <br>Oczekujące = oczekiwania tooreceive lub wysłać MDN. <br>Odrzucone = odebranych lub wysłanych MDN ujemna. <br>Nie wymaga = MDN nie jest skonfigurowany w umowie hello. |
| Kierunek | Witaj AS2 kierunek wiadomości |
| Identyfikator korelacji | Identyfikator Hello, odpowiadająca wszystkie hello wyzwalacze i akcje w aplikacji logiki |
| Identyfikator komunikatu | Identyfikator wiadomości powitania AS2 z nagłówków wiadomości powitania AS2 |
| Znacznik czasu | czas Hello przetworzenia wiadomość hello hello AS2 akcji |
|          |             |

<a name="as2-folder-file-names"></a>

### <a name="as2-name-formats-for-downloaded-message-files"></a>Nazwa AS2 formatów plików pobranych komunikatów

Poniżej przedstawiono hello formatów nazwy dla każdego folderu wiadomości AS2 pobrane i plików.

| Folder lub plik | Format nazwy |
| :------------- | :---------- |
| Folder wiadomości | [nadawcy] \_[odbiornika]\_AS2\_[identyfikator korelacji]\_[identyfikator komunikatu]\_[sygnatury czasowej] |
| Dane wejściowe, dane wyjściowe i jeśli skonfigurować potwierdzenia plików | **Wprowadzony ładunek**: [nadawcy]\_[odbiornika]\_AS2\_[identyfikator korelacji]\_input_payload.txt </p>**Ładunek danych wyjściowych**: [nadawcy]\_[odbiornika]\_AS2\_[identyfikator korelacji]\_dane wyjściowe\_payload.txt </p></p>**Dane wejściowe**: [nadawcy]\_[odbiornika]\_AS2\_[identyfikator korelacji]\_inputs.txt </p></p>**Dane wyjściowe**: [nadawcy]\_[odbiornika]\_AS2\_[identyfikator korelacji]\_outputs.txt |
|          |             |

<a name="x12-message-properties"></a>

### <a name="x12-message-property-descriptions"></a>Opisy właściwości komunikatu X12

Poniżej przedstawiono opis właściwości powitania dla każdego X12 wiadomości.

| Właściwość | Opis |
| --- | --- |
| Nadawca | partner gościa Hello określone w **odbierania ustawień**, lub partnera hosta hello określone **ustawienia wysyłania** dla X12 umowy |
| Odbiornik | Hello partnera hosta określona w **ustawienia odbierania**, lub partnera gościa hello określone w **ustawienia wysyłania** dla X12 umowy |
| Aplikacja logiki | gdzie są skonfigurowane akcje hello X12 aplikacji logiki Hello |
| Stan | Stan wiadomość Hello X12 <br>Powodzenie = odebranych lub wysłanych prawidłową X12 wiadomości. Nie potwierdzenia funkcjonalności jest skonfigurowany. <br>Powodzenie = odebranych lub wysłanych prawidłową X12 wiadomości. Ustawianie i otrzymano potwierdzenia funkcjonalności lub funkcjonalności potwierdzenia są wysyłane. <br>Nie powiodło się = odebranych lub wysłanych X12 nieprawidłowy komunikat. <br>Oczekujące = odebranych lub wysłanych prawidłową X12 wiadomości. Potwierdzenia funkcjonalności jest skonfigurowany, a oczekiwano funkcjonalności potwierdzenia. |
| ACK. | Funkcjonalności stan potwierdzenia (997) <br>Zaakceptowane = odebranych lub wysłanych dodatnią funkcjonalności potwierdzenia. <br>Odrzucone = odebranych lub wysłanych ujemna funkcjonalności potwierdzenia. <br>Oczekujące = oczekiwano potwierdzenia funkcjonalności, ale nie została odebrana. <br>Oczekujące = generowane potwierdzenia funkcjonalności, ale nie można wysłać toopartner. <br>Nie wymaga = funkcjonalne potwierdzenia nie jest skonfigurowany. |
| Kierunek | Kierunek wiadomości powitania X12 |
| Identyfikator korelacji | Identyfikator Hello, odpowiadająca wszystkie hello wyzwalacze i akcje w aplikacji logiki |
| Typ msg | Witaj EDI X 12 komunikat typu |
| ICN | Witaj Interchange numer formantu wiadomość hello X12 |
| TSCN | Witaj numer kontroli ustawić transakcji dla wiadomości powitania X12 |
| Znacznik czasu | czas Hello przetworzenia wiadomość hello hello X12 akcji |
|          |             |

<a name="x12-folder-file-names"></a>

### <a name="x12-name-formats-for-downloaded-message-files"></a>X12 nazwy formatów plików pobranych komunikatów

Poniżej przedstawiono hello formatów nazwy każdego pobierane X12 folderów i plików komunikatów.

| Folder lub plik | Format nazwy |
| :------------- | :---------- |
| Folder wiadomości | [nadawcy] \_[odbiornika]\_X12\_[ruch numer wymiany formantu]\_[numer globalnych kontroli]\_[-zestaw kontroli — numer transakcji]\_[sygnatury czasowej] |
| Dane wejściowe, dane wyjściowe i jeśli skonfigurować potwierdzenia plików | **Wprowadzony ładunek**: [nadawcy]\_[odbiornika]\_X12\_[ruch numer wymiany formantu]\_input_payload.txt </p>**Ładunek danych wyjściowych**: [nadawcy]\_[odbiornika]\_X12\_[ruch numer wymiany formantu]\_dane wyjściowe\_payload.txt </p></p>**Dane wejściowe**: [nadawcy]\_[odbiornika]\_X12\_[ruch numer wymiany formantu]\_inputs.txt </p></p>**Dane wyjściowe**: [nadawcy]\_[odbiornika]\_X12\_[ruch numer wymiany formantu]\_outputs.txt |
|          |             |

<a name="EDIFACT-message-properties"></a>

### <a name="edifact-message-property-descriptions"></a>Opisy właściwości komunikatu EDIFACT

Poniżej przedstawiono opisy właściwości powitania dla każdego komunikatu EDIFACT.

| Właściwość | Opis |
| --- | --- |
| Nadawca | partner gościa Hello określone w **odbierania ustawień**, lub partnera hosta hello określone **ustawienia wysyłania** umowy EDIFACT |
| Odbiornik | Hello partnera hosta określona w **ustawienia odbierania**, lub partnera gościa hello określone **ustawienia wysyłania** umowy EDIFACT |
| Aplikacja logiki | Witaj aplikacji logiki, gdzie hello EDIFACT akcje są skonfigurowane |
| Stan | Witaj EDIFACT komunikatu stanu <br>Powodzenie = odebranych lub wysłanych prawidłowego elementu message EDIFACT. Nie potwierdzenia funkcjonalności jest skonfigurowany. <br>Powodzenie = odebranych lub wysłanych prawidłowego elementu message EDIFACT. Ustawianie i otrzymano potwierdzenia funkcjonalności lub funkcjonalności potwierdzenia są wysyłane. <br>Nie powiodło się = odebranych lub wysłanych nieprawidłowy komunikat EDIFACT <br>Oczekujące = odebranych lub wysłanych prawidłowego elementu message EDIFACT. Potwierdzenia funkcjonalności jest skonfigurowany, a oczekiwano funkcjonalności potwierdzenia. |
| ACK. | Funkcjonalności stan potwierdzenia (997) <br>Zaakceptowane = odebranych lub wysłanych dodatnią funkcjonalności potwierdzenia. <br>Odrzucone = odebranych lub wysłanych ujemna funkcjonalności potwierdzenia. <br>Oczekujące = oczekiwano potwierdzenia funkcjonalności, ale nie została odebrana. <br>Oczekujące = generowane potwierdzenia funkcjonalności, ale nie można wysłać toopartner. <br>Nie wymaga = potwierdzenia funkcjonalności nie jest skonfigurowany. |
| Kierunek | Witaj EDIFACT kierunek wiadomości |
| Identyfikator korelacji | Identyfikator Hello, odpowiadająca wszystkie hello wyzwalacze i akcje w aplikacji logiki |
| Typ msg | Typ komunikatu EDIFACT Hello |
| ICN | Witaj Interchange numer formantu dla wiadomości powitania EDIFACT |
| TSCN | Witaj numer kontroli ustawić transakcji dla wiadomości powitania EDIFACT |
| Znacznik czasu | czas Hello przetworzenia wiadomość hello hello EDIFACT akcji |
|          |               |

<a name="edifact-folder-file-names"></a>

### <a name="edifact-name-formats-for-downloaded-message-files"></a>Nazwa EDIFACT formatów plików pobranych komunikatów

Poniżej przedstawiono hello formatów nazwy dla każdego folderu wiadomości EDIFACT pobrane i plików.

| Folder lub plik | Format nazwy |
| :------------- | :---------- |
| Folder wiadomości | [nadawcy] \_[odbiornika]\_EDIFACT\_[ruch numer wymiany formantu]\_[numer globalnych kontroli]\_[-zestaw kontroli — numer transakcji]\_[sygnatury czasowej] |
| Dane wejściowe, dane wyjściowe i jeśli skonfigurować potwierdzenia plików | **Wprowadzony ładunek**: [nadawcy]\_[odbiornika]\_EDIFACT\_[ruch numer wymiany formantu]\_input_payload.txt </p>**Ładunek danych wyjściowych**: [nadawcy]\_[odbiornika]\_EDIFACT\_[ruch numer wymiany formantu]\_dane wyjściowe\_payload.txt </p></p>**Dane wejściowe**: [nadawcy]\_[odbiornika]\_EDIFACT\_[ruch numer wymiany formantu]\_inputs.txt </p></p>**Dane wyjściowe**: [nadawcy]\_[odbiornika]\_EDIFACT\_[ruch numer wymiany formantu]\_outputs.txt |
|          |             |

## <a name="next-steps"></a>Następne kroki

* [Kwerenda dotycząca wiadomości B2B usługi Operations Management Suite](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md)
* [Schematy śledzenia AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [Schematy śledzenia X12](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [Śledzenie niestandardowych schematów](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)