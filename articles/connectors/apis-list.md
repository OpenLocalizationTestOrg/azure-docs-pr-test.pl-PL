---
title: "aaaConnectors dla usługi Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Wybierz z wszystkich toobuild dostępnych łączników zarządzany przez firmę Microsoft hello i tworzenia aplikacji logiki"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: f1f1fd50-b7f9-4d13-824a-39678619aa7a
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/21/2017
ms.author: mandia; ladocs
ms.openlocfilehash: d681d13d642e6e1512d1f8ab0e1078a194b5da83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connectors-list"></a>Lista łączników
> [!TIP]
> Witaj [A-Z pełną listą](#az) (w tym temacie) Wyświetla wszystkie łączniki dostępne hello, można użyć w aplikacjach logiki. [Szczegóły łącznika](/connectors/) Wyświetla wszelkie wyzwalacze i akcje zdefiniowane w hello swagger oraz ich żadnych limitów dla poszczególnych łączników.

Łączniki są integralną częścią procesu tworzenia aplikacji logiki. Przy użyciu tych łączników, należy naprawdę rozwiń lokalną i aplikacje toodo różne dane, które możesz utworzyć i dane, które mają już w chmurze. łączniki Hello są dostępne w hello następujące kategorie: 

* **Łączniki standardowe**: są automatycznie udostępniane i dołączane podczas korzystania z aplikacji logiki. Przykłady: Service Bus, Power BI, Oracle Database, OneDrive i wiele innych.

* **Łączniki konta integracji**: są udostępniane po zakupieniu konta integracji. Za pomocą tych łączników można przekształcać i sprawdzać poprawność kodu XML, przetwarzać komunikaty przesyłane między firmami zgodnie ze specyfikacjami AS2 / X12 / EDIFACT oraz kodować i dekodować pliki proste. Podczas pracy z BizTalk Server, a następnie te łączniki są bardzo dopasowania tooexpand BizTalk przepływy pracy na platformie Azure.  

    BizTalk Server ma również [Logic Apps karty](https://msdn.microsoft.com/library/mt787163.aspx) zawierającą odbierania z aplikacji logiki i wysyłanie tooa aplikacji logiki.

* **Łączniki dla przedsiębiorstw**: zawierają MQ i SAP. Są dostępne za dodatkową opłatą. 

[Cennik aplikacje logiki](https://azure.microsoft.com/pricing/details/logic-apps/) i [modelu cennik](../logic-apps/logic-apps-pricing.md) zawierają więcej szczegółowych informacji na powitania kosztów. 

## <a name="popular-connectors"></a>Popularne łączniki
Za pomocą tych łączników tysiące aplikacji w milionach wykonań pomyślnie przetwarzają dane i informacje. Witaj w poniższej tabeli wymieniono hello najpopularniejszych i niektóre ulubionych z naszych użytkowników:

| |  |  |  |
| --- | --- | --- | --- |
| [![Ikona interfejsu API][AzureBlobStorageicon]<br/>**Azure Blob<br/>Storage**][AzureBlobStoragedoc] | Jeśli chcesz tooautomate wszystkie zadania z konta magazynu, powinien wyglądać w ten łącznik. Obsługuje operacje tworzenia, odczytu, aktualizacji i usuwania (CRUD). | [![Ikona interfejsu API][Azure-Functionsicon]<br/>**Azure Functions**][azure-functionsdoc] | Umożliwia tworzenie funkcji, które uruchamiają niestandardowe fragmenty języka C# lub node.js, a następnie użycie tych funkcji w aplikacjach logiki.  |
| [![Ikona interfejsu API][Dynamics-365icon]<br/>**Dynamics 365<br/>CRM Online**][Dynamics-365doc] | Jeden z hello najczęściej zadawane dla łączników. Ma ona toohelp wyzwalacze i akcje automatyczne przepływy pracy o potencjalnych klientów i inne. | [![Ikona interfejsu API][Event-Hubs-icon]<br/>**Event Hubs**][event-hubs-doc] | Publikuj zdarzenia i korzystaj z nich w centrum zdarzeń. Na przykład można pobierać dane wyjściowe z aplikacji logiki za pomocą usługi Event Hubs, a następnie wyślij dostawcy analiz w czasie rzeczywistym tooa hello w danych wyjściowych. |
| [![Ikona interfejsu API][FTPicon]<br/>**FTP**][FTPdoc] | Jeśli jest dostępny z serwera FTP hello internet, a następnie można zautomatyzować toowork przepływy pracy z plikami i folderami. <br/><br/>SFTP jest również dostępna z łącznikiem SFTP hello. | [![Ikona interfejsu API][HTTPicon]<br/>**HTTP**][httpdoc] | Użyj toocommunicate aplikacji logiki z dowolnego punktu końcowego za pośrednictwem protokołu HTTP. |
| [![Ikona interfejsu API][Office-365-Outlookicon]<br/>**Office 365<br/>Outlook**][office365-outlookdoc] | Wiele wyzwalaczy i znacznie większą akcje toouse usługi Office 365 w wiadomości e-mail i zdarzeń w ramach przepływów pracy. <br/><br/>Ten łącznik obejmuje *wiadomości e-mail zatwierdzania* żądania urlopu tooapprove akcji, raportu z wydatków i tak dalej. <br/><br/>Użytkownicy usługi Office 365 są także dostępne hello łącznik użytkowników usługi Office 365.| [![Ikona interfejsu API][HTTP-Requesticon]<br/>**Request / Response**][HTTP-Requestdoc] | Ten łącznik udostępnia adres URL HTTPS. Aplikacji logiki hello odebrania URL toothis żądania rozpoczyna się hello aplikacji logiki. |
| [![Ikona interfejsu API][Salesforceicon]<br/>**Salesforce**][salesforcedoc] | Łatwo Zaloguj się przy użyciu programu Salesforce konta tooget dostępu tooobjects, takich jak potencjalnych klientów i inne. |  [![Ikona interfejsu API][Service-Busicon]<br/>**Service Bus**][Service-Busdoc] | Łącznik najpopularniejszych Hello w usłudze logic apps, zawiera wyzwalacze i akcje toodo asynchroniczną obsługę wiadomości i publikowania/subskrypcji z kolejki, subskrypcje i tematy. |
|  [![Ikona interfejsu API][SharePointicon]<br/>**SharePoint<br/>Online**][SharePointdoc] | Jeśli korzystasz z programu SharePoint i możesz uzyskać korzyści z automatyzacji, zalecamy przyjrzenie się temu łącznikowi. Można go używać z lokalnym programem SharePoint i usługą SharePoint Online. | [![Ikona interfejsu API][SQL-Servericon]<br/>**SQL Server**][SQL-Serverdoc] | Jedną z hello najczęściej używane łączników, można połączyć tooan lokalne programu SQL Server i bazy danych SQL Azure. | 
| [![Ikona interfejsu API][Twittericon]<br/>**Twitter**][Twitterdoc] | Pozwala łatwo logować się za pomocą konta w serwisie Twitter i umożliwia uruchamianie przepływu pracy po opublikowaniu nowego tweeta. Następnie zapisz te bazy danych SQL tooa tweetów lub listę programu SharePoint. | | | 

## <a name="integration-account-connectors"></a>Łączniki konta integracji 

Witaj pakiet integracji przedsiębiorstwa (EIP) zawiera łączniki, które są znane toohello społeczności BizTalk Server. Po zakupie [konta integracji](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md), również uzyskać następujące łączniki hello: 

|  |  |  |  |
| --- | --- | --- | --- |
| [![Ikona interfejsu API][as2icon]<br/>**Dekodowanie</br> AS2**][as2decode] | [![Ikona interfejsu API][as2icon]<br/>**Kodowanie</br> AS2**][as2encode] | [![Ikona interfejsu API][x12icon]<br/>**Dekodowanie</br> EDIFACT**][EDIFACTdecode] | [![Ikona interfejsu API][x12icon]<br/>**Kodowanie</br> EDIFACT**][EDIFACTencode] |
[![Ikona interfejsu API][flatfileicon]<br/>**Kodowanie</br> plików prostych**][flatfiledoc] | [![Ikona interfejsu API][flatfiledecodeicon]<br/>**Dekodowanie</br> plików prostych**][flatfiledecodedoc] | [![Ikona interfejsu API][integrationaccounticon]<br/>**Konto<br/>integracji**][integrationaccountdoc] | [![Ikona interfejsu API][xmltransformicon]<br/>**Przekształcanie<br/>kodu XML**][xmltransformdoc] |
| [![Ikona interfejsu API][x12icon]<br/>**Dekodowanie</br> X12**][x12decode] | [![Ikona interfejsu API][x12icon]<br/>**Kodowanie</br> X12**][x12encode] | [![Ikona interfejsu API][xmlvalidateicon]<br/>**Walidacja<br/>XML**][xmlvalidatedoc] | |

## <a name="enterprise-connectors"></a>Łączniki dla przedsiębiorstw

Połącz tooyour przedsiębiorstwa aplikacji w usłudze logic apps.

|  |  |
| --- | --- |
|[![Ikona interfejsu API][MQicon]<br/>**MQ**][mqdoc]|[![Ikona interfejsu API][SAPicon]<br/>**SAP**][sapconnector]|


## <a name="az"></a>Pełna lista od A do Z

[Szczegóły łącznika](/connectors/) listy wszelkie wyzwalacze i akcje zdefiniowane w hello swagger oraz ich żadnych limitów dla poszczególnych łączników.

| | | | | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| [**1**](#1) | [**A**](#a) | [**B**](#b) | [**C**](#c) | [**D**](#d) | [**E**](#e) | [**F**](#f) | [**G**](#g) | [**H**](#h) | [**I**](#i) | [**J**](#j) | [**L**](#l) | [**M**](#m) |
| [**N**](#n) | [**O**](#o) | [**P**](#p) | [**R**](#r) | [**S**](#s) | [**T**](#t) | [**U**](#u) | [**V**](#v) | [**W**](#w) | [**X**](#x) | [**Y**](#y) | [**Z**](#z) | | 

| | |
|---|---|
|<a name="1"></a>10to8 — planowanie terminów<br/><br/><a name="a"></a>Act!<br/>Adobe Creative Cloud<br/>appFigures<br/>[AS2][as2doc]<br/>Asana<br/>Azure Active Directory (AD)<br/>Usługa Azure API Management<br/>Azure App Services<br/>Azure Application<br/>Azure Automation<br/>[Azure Blob Storage][azureblobstoragedoc]<br/>Azure Data Lake<br/>Azure DocumentDB (Cosmos DB)<br/>[Azure Functions][azure-functionsdoc]<br/>[Azure Logic Apps][nested-logic-appdoc]<br/>AzureML<br/>Azure Queues<br/>Azure Resource Manager<br/>[Azure SQL Database][sql-serverdoc]<br/><br/><a name="b"></a>Basecamp 2<br/>Basecamp 3<br/>Batch<br/>Benchmark Email<br/>Wyszukiwanie Bing<br/>Bitbucket<br/>Bitly<br/>Platforma BizTalk Server<br/>Blogger<br/>Box<br/>Buffer<br/><br/><a name="c"></a>Calendly<br/>Campfire<br/>Capsule CRM<br/>Chatter<br/>Cognito Forms<br/>Interfejs API przetwarzania obrazów usług Cognitive Services<br/>Interfejs API rozpoznawania twarzy usług Cognitive Services<br/>Cognitive Services LUIS<br/>Analiza tekstu usług Cognitive Services<br/>Common Data Service<br/>Konwersja zawartości<br/>Control-Terminate<br/>[Niestandardowe interfejsy API / Web Apps][api/web-appdoc]<br/><br/><a name="d"></a>Operacje na danych<br/>[DB2][db2doc]<br/>Disqus<br/>DocuSign<br/>Do Until<br/>Dropbox<br/>[Dynamics 365 CRM Online][Dynamics-365doc]<br/>Dynamics 365 for Financials<br/>Dynamics 365 for Operations<br/>Dynamics NAV<br/><br/><a name="e"></a>Easy Redmine<br/>EDIFACT<br/>[Event Hubs][event-hubs-doc]<br/>Eventbrite<br/><br/><a name="f"></a>Facebook<br/>[File System][filesystemdoc]<br/>[Flat File][flatfiledoc]<br/>FreshBooks<br/>Freshdesk<br/>Freshservice<br/>[FTP][ftpdoc]<br/><br/><a name="g"></a>GitHub<br/>Gmail<br/>Kalendarz Google<br/>Kontakty Google<br/>Dysk Google<br/>Arkusze Google<br/>Zadania Google<br/>GoToMeeting<br/>GoToTraining<br/>GoToWebinar<br/><br/><a name="h"></a>Harvest<br/>HelloSign<br/>HipChat<br/>[HTTP][httpdoc]<br/>[HTTP + Swagger][http-swaggerdoc]<br/>[HTTP Webhook][webhookdoc]<br/><br/><a name="i"></a>[Informix][informixdoc]<br/>Infusionsoft<br/>Inoreader<br/>Insightly<br/>Instagram<br/>Instapaper<br/>Konto integracji<br/>Intercom | <a name="j"></a>JotForm<br/>JIRA<br/><br/><a name="l"></a>LeanKit<br/>LiveChat<br/><br/><a name="m"></a>MailChimp<br/>Mandrill<br/>Medium<br/>Microsoft Forms<br/>Microsoft Teams<br/>Microsoft Translator<br/>[MQ][mqdoc]<br/>MSN Weather<br/>Muhimbi PDF<br/>MySQL<br/><br/><a name="n"></a>Nexmo<br/><br/><a name="o"></a>[Office 365 Outlook][office365-outlookdoc]<br/>Office 365 Users<br/>Office 365 Video<br/>OneDrive<br/>OneDrive dla Firm<br/>OneNote (dla firm)<br/>[Baza danych Oracle][oracle-db-doc]<br/>Outlook Customer Manager<br/>Outlook Tasks<br/>Outlook.com<br/><br/><a name="p"></a>PagerDuty<br/>Parserr<br/>Paylocity<br/>Pinterest<br/>Pipedrive<br/>Pivotal Tracker<br/>Planner<br/>PostgreSQL<br/>Power BI<br/>Project Online<br/><br/><a name="r"></a>Redmine<br/>[Request / Response][http-requestdoc]<br/>RSS<br/><br/><a name="s"></a>[Salesforce][salesforcedoc]<br/>[SAP Application Server][sapconnector]<br/>[SAP Message Server][sapconnector]<br/>[Schedule][recurrencedoc]<br/>Zakres<br/>SendGrid<br/>Wysyłanie wiadomości toobatch<br/>[Service Bus][service-busdoc]<br/>SFTP<br/>[SharePoint Online][sharepointdoc]<br/>[SharePoint Server][sharepointserver]<br/>Slack<br/>Smartsheet<br/>SMTP<br/>SparkPost<br/>[SQL Server][sql-serverdoc]<br/>Stripe<br/>SurveyMonkey<br/>Switch Case<br/><br/><a name="t"></a>Teamwork Projects<br/>Teradata<br/>Todoist<br/>Toodledo<br/>[Przekształcanie kodu XML][xmltransformdoc]<br/>Trello<br/>Twilio<br/>[Twitter][twitterdoc]<br/>Typeform<br/><br/><a name="u"></a>UserVoice<br/><br/><a name="v"></a>Variables<br/>Vimeo<br/>Visual Studio Team Services<br/><br/><a name="w"></a>WebMerge<br/>WordPress<br/>Wunderlist<br/><br/><a name="x"></a>[X12][x12doc]<br/>[Walidacja kodu XML][xmlvalidatedoc]<br/><br/><a name="y"></a>Yammer<br/>YouTube<br/><br/><a name="z"></a>Zendesk |

> [!TIP]
> tooget wprowadzenie do usługi Azure Logic Apps przed utworzeniem konta platformy Azure, przejdź zbyt[spróbuj Logic Apps](https://tryappservice.azure.com/?appservice=logic). Możesz od razu utworzyć krótkotrwałą wersję początkową aplikacji logiki. Bez kart kredytowych i bez zobowiązań.

## <a name="connectors-as-triggers-and-actions"></a>Łączniki jako wyzwalacze i akcje

**Wyzwalacz** rozpoczyna lub uruchamia wystąpienie aplikacji logiki. Niektóre łączniki udostępniają wyzwalacze, które powiadamiają aplikację w przypadku wystąpienia określonych zdarzeń. Na przykład łącznik hello FTP ma hello `OnUpdatedFile` wyzwalacz, który uruchamia aplikację logiki, kiedy plik został zaktualizowany. 

Aplikacje logiki to hello następujące typy wyzwalaczy:  

* *Wyzwalacze sondowania*: te wyzwalacze sondują usługę na toocheck określona częstotliwość dla nowych danych. 

    Jeśli nowe dane są dostępne, uruchamia nowe wystąpienie aplikacji logiki z danymi hello danych wejściowych. 

* *Wyzwalacze wypychania*: te wyzwalacze nasłuchują danych w punkcie końcowym lub zdarzenia toohappen, następnie uruchamia nowe wystąpienie aplikacji logiki.

* *Wyzwalacz cykliczny*: ten wyzwalacz tworzy wystąpienie aplikacji logiki zgodnie z ustalonym harmonogramem.

Łączniki udostępniają również **akcje**, których można używać w przepływie pracy. Na przykład aplikacja logiki może wyszukiwać dane, a następnie używać ich w późniejszym czasie. W szczególności można wyszukiwać dane klienta z bazy danych programu SQL, a następnie użyć tego toobuild danych klienta przepływu pracy. 

> [!TIP]
> Aby uzyskać więcej szczegółów na temat wyzwalaczy i akcji, zobacz [Przegląd łączników](connectors-overview.md). 


## <a name="message-manipulation-actions"></a>Akcje manipulowania komunikatami

Aplikacje logiki zawierają wbudowane akcje, które mogą zmieniać dane ładunku i umożliwiają manipulowanie nimi. wbudowane Hello **operacji danych** łącznik obejmuje hello następujące akcje: 

| | |
|---|---|
| **Redaguj** | Tworzenie Generowanie wartości lub obiektów toouse później lub podczas tworzenia przepływu pracy. Na przykład można utworzyć obiekt JSON wartościami z wielu kroków lub obliczyć stałej tooreference później w aplikacji logiki, uruchom. |
| **Utwórz tabelę CSV**<br/>**Utwórz tabelę HTML** | Przekształć tablicowy zestaw wyników w tabelę CSV lub HTML. Na przykład dodać akcję "Rekordy do listy" CRM hello i dodać filtr dla rekordów dodawanych dzisiaj. Następnie wysyłać wyniki hello jako tabeli HTML w wiadomości e-mail. |
| **Filtruj tablicę** (zapytanie) | Filtruj pozycje toohello zestaw wyników, interesujące. Na przykład wyszukiwanie wszystkich tweety z `#Azure`, a następnie "filter" hello zwracana tweetów tooonly wyniki zwracane, które są `Tweeted_by_followers > 50`. |
| **Dołącz** | Dołącz tablicę według ogranicznika. Na przykład hello operacji wykrywania fraz klucza zwraca tablicę fraz klucza. Można je „dołączyć” za pomocą znaku `,` lub innego ogranicznika. Na przykład zamiast fraz `["Some", "Phrase"]` zostanie zwrócona fraza `"Some, Phrase"`. |
| **Przeanalizuj dane JSON** | Analizowanie się i uzyskiwać dostęp do wartości z obiektu JSON w Projektancie hello. Na przykład jeśli funkcja Azure zwraca ładunek JSON, następnie można przeanalizować jej właściwości JSON hello tooaccess później w kolejnym kroku. Akcja Hello jest również sprawdzane, że hello dopasowań hello określonego schematu JSON w czasie wykonywania. | 
| **Wybierz** | Wybierz niektóre właściwości tablicy do dalszego przetwarzania. Jeśli korzystasz z akcji „Wyświetl rekordy” względem bazy danych SQL i w wyniku działania tej akcji zostanie zwróconych 15 kolumn, wybierz tylko niektóre z nich do dalszego przetwarzania. dane wyjściowe Hello jest tablica zawierająca tylko właściwości hello, którą wybierzesz. |

## <a name="custom-connectors-and-azure-certification"></a>Niestandardowe łączniki i certyfikaty platformy Azure 

toocall do interfejsów API, które uruchomienia niestandardowego kodu lub nie są dostępne jako łączniki, można rozszerzyć hello aplikacje logiki platformy przez [tworzenie opartego na interfejsie REST API Apps, łączników niestandardowych](../logic-apps/logic-apps-create-api-app.md). 

Jeśli chcesz toomake Twojego niestandardowe aplikacje interfejsu API publicznego i dostępne toouse na platformie Azure, przesłać toohello Twojego nominacji [programu Microsoft Azure certyfikowane](https://azure.microsoft.com/marketplace/programs/certified/logic-apps/).

## <a name="get-help"></a>Uzyskiwanie pomocy

pytania tooask, odpowiadanie na pytania i robią innych użytkowników usługi Azure Logic Apps, zobacz go toohello [forum usługi Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).

toohelp poprawy usługi Azure Logic Apps i łącznikami, Zagłosuj lub Prześlij pomysłów na powitania [witrynę opinii użytkowników Logic Apps](http://aka.ms/logicapps-wish).

Czy pominęliśmy jakiś temat dotyczący łączników albo jakieś informacje, które uważasz za istotne? Jeśli tak, Pomóż nam przez dodanie tooour istniejących tematów lub napisać własny. Nasza dokumentacja jest typu open source i jest hostowana w usłudze GitHub. Zacznij, przechodząc do naszego [repozytorium GitHub](https://github.com/Microsoft/azure-docs). 

## <a name="next-steps"></a>Następne kroki
* [Tworzenie pierwszej aplikacji logiki](../logic-apps/logic-apps-create-a-logic-app.md)
* [Tworzenie niestandardowych interfejsów API dla aplikacji logiki](../logic-apps/logic-apps-create-api-app.md)
* [Monitorowanie aplikacji logiki](../logic-apps/logic-apps-monitor-your-logic-apps.md)

<!--Connectors Documentation-->

[api/web-appdoc]: ../logic-apps/logic-apps-custom-hosted-api.md "Integracja aplikacji logiki z usługą App Service API Apps"
[azureblobstoragedoc]: ./connectors-create-api-azureblobstorage.md "Zarządzanie plikami w kontenerze obiektów blob za pomocą łącznika usługi Azure Blob Storage"
[azure-functionsdoc]: ../logic-apps/logic-apps-azure-functions.md "Integracja aplikacji logiki z usługą Azure Functions"
[db2doc]: ./connectors-create-api-db2.md "Połącz tooIBM bazy danych DB2 w chmurze hello lub lokalnie. Aktualizowanie wiersza, pobieranie tabeli oraz inne funkcje"
[Dynamics-365doc]: ./connectors-create-api-crmonline.md "Połącz tooDynamics CRM Online, aby można było pracować z danymi CRM Online"
[event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Połącz tooAzure Event Hubs. Odbieranie i wysyłanie zdarzeń między aplikacjami logiki i usługą Event Hubs"
[filesystemdoc]: ../logic-apps/logic-apps-using-file-connector.md "Połącz tooan lokalnego systemu plików"
[ftpdoc]: ./connectors-create-api-ftp.md "Połącz tooan FTP / FTPS serwera FTP zadań, takich jak przekazywanie, pobieranie, usuwanie plików i inne"
[httpdoc]: ./connectors-native-http.md "Wywoływanie usług HTTP z łącznikiem HTTP hello"
[http-requestdoc]: ./connectors-native-reqres.md "Dodaj akcje dla protokołu HTTP żądania i odpowiedzi tooyour aplikacje logiki"
[http-swaggerdoc]: ./connectors-native-http-swagger.md "Nawiązywanie połączeń HTTP za pomocą łącznika protokołu HTTP + Swagger"
[informixdoc]: ./connectors-create-api-informix.md "Połącz tooInformix w chmurze hello lub lokalnie. Przeczytaj wiersza, listy tabel hello i innych"
[nested-logic-appdoc]: ../logic-apps/logic-apps-http-endpoint.md "Integracja aplikacji logiki z zagnieżdżonymi przepływami pracy"
[office365-outlookdoc]: ./connectors-create-api-office365-outlook.md "Połącz konto tooyour usługi Office 365. Wysyłanie i odbieranie wiadomości e-mail, zarządzanie kalendarzem i kontaktami oraz inne funkcje"
[oracle-db-doc]: ./connectors-create-api-oracledatabase.md "Połącz tooadd bazy danych Oracle tooan, wstawiania, usunąć wiersze i"
[mqdoc]: ./connectors-create-api-mq.md "Połącz tooMQ lokalnych lub platformy Azure oraz wysyłanie i odbieranie wiadomości"
[recurrencedoc]:  ./connectors-native-recurrence.md "Wyzwalanie akcji cyklicznych dla aplikacji logiki"
[salesforcedoc]: ./connectors-create-api-salesforce.md "Połącz tooyour konta usług Salesforce. Zarządzanie kontami, potencjalnymi klientami i możliwościami sprzedaży oraz inne funkcje"
[sapconnector]: ../logic-apps/logic-apps-using-sap-connector.md "Połącz tooan lokalnego systemu SAP"
[service-busdoc]: ./connectors-create-api-servicebus.md "Wysyłanie komunikatów z tematów i kolejek usługi Service Bus oraz odbieranie komunikatów z subskrypcji i kolejek usługi Service Bus"
[sharepointdoc]: ./connectors-create-api-sharepointonline.md "Połącz tooSharePoint w trybie Online. Zarządzanie dokumentami i elementami list oraz inne funkcje"
[sharepointserver]: ./connectors-create-api-sharepointserver.md "Połącz tooSharePoint na serwerze lokalnym. Zarządzanie dokumentami i elementami list oraz inne funkcje"
[sql-serverdoc]: ./connectors-create-api-sqlazure.md "Połącz tooAzure SQL Database lub SQL server. Tworzenie, aktualizowanie, pobieranie i usuwanie wpisów w tabeli bazy danych SQL."
[twitterdoc]: ./connectors-create-api-twitter.md "Połącz tooTwitter. Pobieranie osi czasu, publikowanie tweetów i inne funkcje"
[webhookdoc]: ./connectors-native-webhook.md "Dodawanie elementu Webhook działań i wyzwalaczy tooyour logiki aplikacji"

[as2doc]: ../logic-apps/logic-apps-enterprise-integration-as2.md "Więcej informacji na temat integracji dla przedsiębiorstw — AS2."
[x12doc]: ../logic-apps/logic-apps-enterprise-integration-x12.md "Więcej informacji na temat integracji dla przedsiębiorstw — X12."
[flatfiledoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Więcej informacji na temat integracji dla przedsiębiorstw — plik prosty."
[flatfiledecodedoc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Więcej informacji na temat integracji dla przedsiębiorstw — plik prosty."
[xmlvalidatedoc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Więcej informacji na temat integracji dla przedsiębiorstw — walidacja XML."
[xmltransformdoc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Więcej informacji na temat integracji dla przedsiębiorstw — transformacje."
[as2decode]: ../logic-apps/logic-apps-enterprise-integration-as2-decode.md "Więcej informacji na temat integracji dla przedsiębiorstw — dekodowanie komunikatów AS2."
[as2encode]:../logic-apps/logic-apps-enterprise-integration-as2-encode.md "Więcej informacji na temat integracji dla przedsiębiorstw — kodowanie komunikatów AS2."
[X12decode]: ../logic-apps/logic-apps-enterprise-integration-X12-decode.md "Więcej informacji na temat integracji dla przedsiębiorstw — dekodowanie komunikatów X12."
[X12encode]: ../logic-apps/logic-apps-enterprise-integration-X12-encode.md "Więcej informacji na temat integracji dla przedsiębiorstw — kodowanie komunikatów X12."
[EDIFACTdecode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-decode.md "Więcej informacji na temat integracji dla przedsiębiorstw — dekodowanie komunikatów EDIFACT."
[EDIFACTencode]: ../logic-apps/logic-apps-enterprise-integration-EDIFACT-encode.md "Więcej informacji na temat integracji dla przedsiębiorstw — kodowanie komunikatów EDIFACT."
[integrationaccountdoc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Wyszukiwanie schematów, map partnerów i innych elementów na koncie integracji"


[boxDoc]: ./connectors-create-api-box.md "Połącz tooBox. Przekazywanie, pobieranie, usuwanie i wyświetlanie listy plików oraz inne funkcje"
[delaydoc]: ./connectors-native-delay.md "Wykonywanie akcji z opóźnieniem"
[dropboxdoc]: ./connectors-create-api-dropbox.md "Połącz tooDropbox. Przekazywanie, pobieranie, usuwanie i wyświetlanie listy plików oraz inne funkcje"
[facebookdoc]: ./connectors-create-api-facebook.md "Połącz tooFacebook. Post tooa osi czasu, Pobierz strony źródła danych i inne"
[githubdoc]: ./connectors-create-api-github.md "Połącz tooGitHub i śledzenie problemów"
[google-drivedoc]: ./connectors-create-api-googledrive.md "Połącz tooGoogleDrive, dzięki czemu można pracować z danymi"
[google-sheetsdoc]: ./connectors-create-api-googlesheet.md "Połącz arkusze tooGoogle, można więc można modyfikować arkuszy"
[google-tasksdoc]: ./connectors-create-api-googletasks.md "Łączy tooGoogle zadania, a więc można zarządzać zadań"
[google-calendardoc]: ./connectors-create-api-googlecalendar.md "Łączy tooGoogle kalendarza i zarządzać kalendarza."
[http-responsedoc]: ./connectors-native-reqres.md "Dodaj akcje dla protokołu HTTP żądania i odpowiedzi tooyour aplikacje logiki"
[instagramdoc]: ./connectors-create-api-instagram.md "Połącz tooInstagram. Wyzwalanie zdarzeń lub reagowanie na nie"
[mailchimpdoc]: ./connectors-create-api-mailchimp.md "Połącz tooyour MailChimp konta. Automatyzowanie obsługi wiadomości e-mail i zarządzanie nimi"
[mandrilldoc]: ./connectors-create-api-mandrill.md "Połącz tooMandrill komunikacji"
[microsoft-translatordoc]: ./connectors-create-api-microsofttranslator.md "Połącz tooMicrosoft translatora. Tłumaczenie tekstu, wykrywanie języków i inne funkcje" 
[office365-usersdoc]: ./connectors-create-api-office365-users.md 
[office365-videodoc]: ./connectors-create-api-office365-video.md "Pobieranie informacji o filmach wideo, list i kanałów wideo oraz adresów URL odtwarzania dla filmów wideo usługi Office 365"
[onedrivedoc]: ./connectors-create-api-onedrive.md "Połącz tooyour osobistych Microsoft OneDrive. Przekazywanie, usuwanie i wyświetlanie listy plików oraz inne funkcje"
[onedrive-for-businessdoc]: ./connectors-create-api-onedriveforbusiness.md "Połącz tooyour biznesowa Microsoft OneDrive. Przekazywanie, usuwanie i wyświetlanie listy plików oraz inne funkcje"
[outlook.comdoc]: ./connectors-create-api-outlook.md "Połączyć skrzynkę pocztową programu Outlook tooyour. Zarządzanie pocztą e-mail, kalendarzami i kontaktami oraz inne funkcje"
[project-onlinedoc]: ./connectors-create-api-projectonline.md "Połącz tooMicrosoft Project Online. Zarządzanie projektami, zadaniami i zasobami oraz inne funkcje"
[querydoc]: ./connectors-native-query.md "Wybierz i filtrowanie tablic z akcją zapytań hello"
[rssdoc]: ./connectors-create-api-rss.md "Publikowanie i pobieranie elementów strumieniowego źródła danych, wyzwalanie operacji po tooan opublikowanych danych RSS jest nowy element źródła danych."
[sendgriddoc]: ./connectors-create-api-sendgrid.md "Połącz tooSendGrid. Wysyłanie wiadomości e-mail i zarządzanie listami adresatów"
[sftpdoc]: ./connectors-create-api-sftp.md "Połącz tooyour SFTP konta. Przekazywanie, pobieranie i usuwanie plików oraz inne funkcje"
[slackdoc]: ./connectors-create-api-slack.md "Połącz tooSlack i publikowanie wiadomości tooSlack kanałów"
[smtpdoc]: ./connectors-create-api-smtp.md "Połącz tooa serwera SMTP i wysyłanie wiadomości e-mail z załącznikami"
[sparkpostdoc]: ./connectors-create-api-sparkpost.md "Łączy tooSparkPost komunikacji"
[trellodoc]: ./connectors-create-api-trello.md "Połącz tooTrello. Zarządzanie projektami i organizowanie dowolnych rzeczy z dowolnymi osobami"
[twiliodoc]: ./connectors-create-api-twilio.md "Połącz tooTwilio. Wysyłanie i pobieranie wiadomości, pobieranie dostępnych numerów, zarządzanie przychodzącymi numerami telefonów i inne funkcje"
[wunderlistdoc]: ./connectors-create-api-wunderlist.md "Połącz tooWunderlist. Zarządzanie zadaniami i listami zadań do wykonania, synchronizowanie danych oraz inne funkcje"
[yammerdoc]: ./connectors-create-api-yammer.md "Połącz tooYammer. Publikowanie wiadomości, pobieranie nowych wiadomości i inne funkcje"
[youtubedoc]: ./connectors-create-api-youtube.md "Połącz tooYouTube. Zarządzanie filmami wideo i kanałami"


<!--Icon references-->
[appFiguresicon]: ./media/apis-list/appfigures.png
[Asanaicon]: ./media/apis-list/asana.png
[Azure-Automation-icon]: ./media/apis-list/azure-automation.png
[AzureBlobStorageicon]: ./media/apis-list/azureblob.png
[Azure-Data-Lake-icon]: ./media/apis-list/azure-data-lake.png
[Azure-DocumentDBicon]: ./media/apis-list/azure-documentdb.png
[Azure-MLicon]: ./media/apis-list/azureml.png
[Azure-Resource-Manager-icon]: ./media/apis-list/azure-resource-manager.png
[Azure-Queues-icon]: ./media/apis-list/azure-queues.png
[Basecamp-3icon]: ./media/apis-list/basecamp.png
[Bitbucket-icon]: ./media/apis-list/bitbucket.png
[Bitlyicon]: ./media/apis-list/bitly.png
[BizTalk-Servericon]: ./media/apis-list/biztalk.png
[Bloggericon]: ./media/apis-list/blogger.png
[Boxicon]: ./media/apis-list/box.png
[Campfireicon]: ./media/apis-list/campfire.png
[Cognitive-Services-Text-Analyticsicon]: ./media/apis-list/cognitiveservicestextanalytics.png
[DB2icon]: ./media/apis-list/db2.png
[Dropboxicon]: ./media/apis-list/dropbox.png
[Dynamics-365icon]: ./media/apis-list/dynamicscrmonline.png
[Dynamics-365-for-Financialsicon]: ./media/apis-list/madeira.png
[Dynamics-365-for-Operationsicon]: ./media/apis-list/dynamicsax.png
[Easy-Redmineicon]: ./media/apis-list/easyredmine.png
[Event-Hubs-icon]: ./media/apis-list/eventhubs.png
[Facebookicon]: ./media/apis-list/facebook.png
[FTPicon]: ./media/apis-list/ftp.png
[GitHubicon]: ./media/apis-list/github.png
[Google-Calendaricon]: ./media/apis-list/googlecalendar.png
[Google-Driveicon]: ./media/apis-list/googledrive.png
[Google-Sheetsicon]: ./media/apis-list/googlesheet.png
[Google-Tasksicon]: ./media/apis-list/googletasks.png
[HideKeyicon]: ./media/apis-list/hidekey.png
[HipChaticon]: ./media/apis-list/hipchat.png
[Informixicon]: ./media/apis-list/informix.png
[Insightlyicon]: ./media/apis-list/insightly.png
[Instagramicon]: ./media/apis-list/instagram.png
[Instapapericon]: ./media/apis-list/instapaper.png
[JIRAicon]: ./media/apis-list/jira.png
[MailChimpicon]: ./media/apis-list/mailchimp.png
[Mandrillicon]: ./media/apis-list/mandrill.png
[Microsoft-Translatoricon]: ./media/apis-list/microsofttranslator.png
[MQicon]: ./media/apis-list/mq.png
[Office-365-Outlookicon]: ./media/apis-list/office365.png
[Office-365-Usersicon]: ./media/apis-list/office365users.png
[Office-365-Videoicon]: ./media/apis-list/office365video.png
[OneDriveicon]: ./media/apis-list/onedrive.png
[OneDrive-for-Businessicon]: ./media/apis-list/onedriveforbusiness.png
[Oracle-DB-icon]: ./media/apis-list/oracle-db.png
[Outlook.comicon]: ./media/apis-list/outlook.png
[PagerDutyicon]: ./media/apis-list/pagerduty.png
[Pinteresticon]: ./media/apis-list/pinterest.png
[Project-Onlineicon]: ./media/apis-list/projectonline.png
[Redmineicon]: ./media/apis-list/redmine.png
[RSSicon]: ./media/apis-list/rss.png
[Common-Data-Serviceicon]: ./media/apis-list/runtimeservice.png
[Salesforceicon]: ./media/apis-list/salesforce.png
[SAPicon]: ./media/apis-list/sap.png
[SendGridicon]: ./media/apis-list/sendgrid.png
[Service-Busicon]: ./media/apis-list/servicebus.png
[SFTPicon]: ./media/apis-list/sftp.png
[SharePointicon]: ./media/apis-list/sharepointonline.png
[Slackicon]: ./media/apis-list/slack.png
[Smartsheeticon]: ./media/apis-list/smartsheet.png
[SMTPicon]: ./media/apis-list/smtp.png
[SparkPosticon]: ./media/apis-list/sparkpost.png
[SQL-Servericon]: ./media/apis-list/sql.png
[Todoisticon]: ./media/apis-list/todoist.png
[Trelloicon]: ./media/apis-list/trello.png
[Twilioicon]: ./media/apis-list/twilio.png
[Twittericon]: ./media/apis-list/twitter.png
[Vimeoicon]: ./media/apis-list/vimeo.png
[Visual-Studio-Team-Servicesicon]: ./media/apis-list/visualstudioteamservices.png
[WordPressicon]: ./media/apis-list/wordpress.png
[Wunderlisticon]: ./media/apis-list/wunderlist.png
[Yammericon]: ./media/apis-list/yammer.png
[YouTubeicon]: ./media/apis-list/youtube.png

<!-- Primitive Icons -->
[API/Web-Appicon]: ./media/apis-list/api.png
[Azure-Functionsicon]: ./media/apis-list/function.png
[Delayicon]: ./media/apis-list/delay.png
[FileSystemIcon]: ./media/apis-list/filesystem.png
[HTTPicon]: ./media/apis-list/http.png
[HTTP-Requesticon]: ./media/apis-list/request.png
[HTTP-Responseicon]: ./media/apis-list/response.png
[HTTP-Swaggericon]: ./media/apis-list/http_swagger.png
[Nested-Logic-Appicon]: ./media/apis-list/workflow.png
[Recurrenceicon]: ./media/apis-list/recurrence.png
[Queryicon]: ./media/apis-list/query.png
[Webhookicon]: ./media/apis-list/webhook.png

<!-- EIP Icons -->
[as2icon]: ./media/apis-list/as2.png
[x12icon]: ./media/apis-list/x12new.png
[flatfileicon]: ./media/apis-list/flatfileencoding.png
[flatfiledecodeicon]: ./media/apis-list/flatfiledecoding.png
[xmlvalidateicon]: ./media/apis-list/xmlvalidation.png
[xmltransformicon]: ./media/apis-list/xsltransform.png
[integrationaccounticon]: ./media/apis-list/integrationaccount.png
