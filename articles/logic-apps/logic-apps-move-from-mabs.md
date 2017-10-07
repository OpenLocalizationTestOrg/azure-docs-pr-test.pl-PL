---
title: "aaaMove aplikacji z usługi BizTalk Services tooAzure Logic Apps | Dokumentacja firmy Microsoft"
description: "Przenieś lub przeprowadzić migrację tooLogic MABS usługi BizTalk Azure aplikacji"
services: logic-apps
documentationcenter: 
author: jonfancey
manager: anneta
editor: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: ladocs; jonfan; mandia
ms.openlocfilehash: b3b065b90a37002f72305b0fc866c24231fb5f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="move-from-biztalk-services-toologic-apps"></a>Przenoszenie z usługi BizTalk Services tooLogic aplikacji

Trwa wycofywanie Microsoft Azure BizTalk usług (MABS). Za pomocą tego tematu toomove tooAzure rozwiązań integracji z MABS Logic Apps. 

## <a name="overview"></a>Omówienie

Usługi BizTalk Services składa się z dwóch usług podrzędne:

1.  Połączeń hybrydowych usług Microsoft BizTalk
2.  Usługi EAI i EDI integracji na podstawie Mostek

Jeśli szukasz toomove połączeń hybrydowych, następnie [połączeń hybrydowych usługi aplikacji Azure](../app-service/app-service-hybrid-connections.md) opisuje hello zmian i funkcji tej usługi. Azure połączeń hybrydowych zastępuje połączeń hybrydowych usługi BizTalk. Połączenia hybrydowe platformy Azure jest dostępna w usłudze Azure App Service i jest oferowany hello portalu Azure. Połączenia hybrydowe Azure udostępnia również nowe toomanage Menedżera połączeń hybrydowych istniejących połączeń hybrydowych usługi BizTalk Services i nowych połączeń hybrydowych utworzone w hello portalu. Azure App Service połączeń hybrydowych było możliwe jest ogólnie dostępna (GA).

Usługi EAI i EDI na podstawie Mostek integracji Logic Apps jest zastąpienie hello. Logic Apps oferuje wszystkie hello takie same możliwości jak usługi BizTalk Services i inne. Logic Apps oferuje skali chmury na podstawie zużycia przepływu pracy i aranżacji funkcje, które pozwalają tooquickly i łatwe tworzenie integracja złożonych rozwiązań za pomocą przeglądarki lub narzędzia w programie Visual Studio.

w poniższej tabeli Hello udostępnia mapowanie możliwości usługi BizTalk Services tooLogic aplikacji.

| BizTalk Services   | Logic Apps            | Przeznaczenie                  |
| ------------------ | --------------------- | ---------------------------- |
| Łącznik          | Łącznik             | Wysyłanie i odbieranie danych   |
| Mostek             | Aplikacja logiki             | Procesor potoku           |
| Sprawdź poprawność etap     | Sprawdzanie poprawności kodu XML akcji      | Sprawdzanie poprawności względem schematu dokumentu XML             |
| Dodawanie etapu       | Tokeny danych      | Podwyższ poziom właściwości do wiadomości lub decyzje dotyczące routingu             |
| Przekształć etap    | Przekształć akcji      | Konwertowanie z jednego formatu tooanother wiadomości XML             |
| Dekodowanie etap       | Płaski akcji dekodowanie pliku      | Konwertowanie z pliku prostego tooXML             |
| Kodowanie etap       |  Płaski akcji kodowanie pliku      | Konwertowanie z pliku XML tooflat             |
| Inspektor wiadomości       |  Środowisko Azure Functions lub aplikacje interfejsu API      | Uruchamianie niestandardowego kodu w Twojej integracji             |
| Akcja trasy      |  Warunek lub przełącznika      | Trasy tooone wiadomości z hello określony łączników             |

Istnieje wiele różnych typów artefaktów w usługi BizTalk Services.

## <a name="connectors"></a>Łączniki
Łączników w usługi BizTalk Services umożliwiają toosend mostków i odbierać dane, w tym dwukierunkowe mostki włączone interakcje oparte na protokole HTTP żądanie/odpowiedź. W aplikacjach logiki hello tego samego terminologii jest używany. Łączniki w aplikacjach logiki służyć hello sam cel, a także ponad 140 podłączoną tooa szeroką gamę technologii i usług, zarówno lokalnie przy użyciu hello bramy danych lokalnych (zastępując hello BizTalk karty usługi używane przez usługi BizTalk Services), i w chmurze usługi SaaS i PaaS, takie jak OneDrive, usługi Office 365, Dynamics CRM i wiele innych.

Źródeł w usługi BizTalk Services są ograniczone tooFTP, SFTP i kolejką usługi Service Bus lub subskrypcję tematu.

![](media/logic-apps-move-from-mabs/sources.png)

Każdy mostek ma punkt końcowy HTTP domyślnie, dla którego jest skonfigurowany hello adres środowiska uruchomieniowego i właściwości adres względny hello mostka hello. tooachieve hello same z usługą Logic Apps, użyj hello [żądań i odpowiedzi](../connectors/connectors-native-reqres.md) akcje.

## <a name="xml-processing-and-bridges"></a>Przetwarzanie kodu XML i mostków
Mostek w usługi BizTalk Services jest analogiczna tooa przetwarzania potoku. Mostek może zająć danych otrzymywanych z łącznika, i czy niektóre pracować z danymi hello, a następnie wyślij ją tooanother systemu. Dzięki obsłudze hello tej samej interakcji z potoku wzorce jako usługi BizTalk Services, a także wiele innych wzorcach integracji hello tej samej logiki aplikacji. Witaj [Mostek żądanie-odpowiedź XML](https://msdn.microsoft.com/library/azure/hh689781.aspx) w usługi BizTalk Services nosi nazwę potoku VETER składające się z etapów, które można:

* V sprawdzania poprawności
* (E) dodawanie
* (T) transform
* (E) dodawanie
* (R) trasy

Jak pokazano w powitania po obrazu, przetwarzania hello są dzielone na żądanie i odpowiedź i zapewnia kontrolę nad hello żądania i hello ścieżkach odpowiedzi oddzielnie (na przykład przy użyciu różnych mapy dla każdego):

![](media/logic-apps-move-from-mabs/xml-request-reply.png)

Ponadto XML jednokierunkowe Mostek dodaje dekodowania i kodowanie na powitania początek i koniec przetwarzania i hello Mostek przekazywanego zawiera jeden etap Enrich.

### <a name="message-processing-and-decodingencoding"></a>Przetwarzania komunikatu i dekodowania kodowania
W usługi BizTalk Services otrzymujesz wiadomości XML o różnych typach i określić hello zgodnego schematu dla Odebrano wiadomość hello. To jest wykonywane w hello **typów komunikatów** etap hello odbierania przetwarzania potoku. Następnie hello etap dekodowania toodecode typu wiadomość hello wykryto go używa hello podane schematu. Jeśli schemat hello jest schematu pliku prostego, konwertuje przychodzące tooXML pliku prostego powitania. 

Logic Apps oferuje podobne możliwości. Odbieranie pliku prostego przez wiele różnych protokołów przy użyciu wyzwalaczy różnych łącznika hello (systemu plików, FTP, HTTP i tak dalej) i używać hello [płaskiej dekodowanie pliku](../logic-apps/logic-apps-enterprise-integration-flatfile.md) akcji tooconvert hello przychodzących danych tooXML. Można przenosić z istniejących schematów pliku prostego, bezpośrednio toologic aplikacji bez konieczności wszelkie zmiany, a następnie przekaż schematy tooyour konta integracji.

### <a name="validation"></a>Walidacja
Po hello przychodzących danych przekonwertowanego tooXML (lub jeśli XML został odebrany format wiadomość hello), sprawdzanie poprawności jest uruchamiana toodetermine, gdy wiadomość hello zgodnego schematu XSD tooyour. toodo to w aplikacjach logiki, użyj hello [sprawdzanie poprawności kodu XML](../logic-apps/logic-apps-enterprise-integration-xml-validation.md) akcji. Ponownie, można użyć hello tego samego schematów z usługi BizTalk Services bez wprowadzania żadnych zmian.

### <a name="transform-messages"></a>Przekształć wiadomości
W usługi BizTalk Services etapu przekształcenia hello konwertuje jeden tooanother format komunikatu opartych na języku XML. Jest to realizowane przez zastosowanie mapy, przy użyciu mapowania na podstawie TRFM hello. W aplikacjach logiki hello proces jest podobny. Hello akcji przekształcenia wykonuje mapy z Twojego konta integracji. Witaj podstawowa różnica polega na tym, że mapy w aplikacjach logiki są w formacie XSLT. XSLT obejmuje tooreuse możliwości hello istniejące już, łącznie z mapy utworzone dla serwera BizTalk, zawierające functoids XSLT. 

### <a name="routing-rules"></a>Reguły routingu
Usługi BizTalk Services sprawia, że decyzje dotyczące routingu o punkcie końcowym/łącznik toosend przychodzących komunikatów/danych. tooselect możliwości Hello, jeden z wielu punktów końcowych wstępnie skonfigurowane jest możliwe przy użyciu opcji filtr routingu hello:

![](media/logic-apps-move-from-mabs/route-filter.png)

Logic Apps oferuje bardziej zaawansowanych możliwości logiki z [warunku](../logic-apps/logic-apps-use-logic-app-features.md) i [przełącznika](../logic-apps/logic-apps-switch-case.md), włączanie przepływu sterowania zaawansowane i routing. Konwertowanie filtrów routingu w usługi BizTalk Services uzyskuje się za pomocą **warunku** *Jeśli* dostępne są tylko dwie opcje. Jeśli istnieje więcej niż dwa, użyj **przełącznika**.

### <a name="enrich"></a>Dodawanie
Witaj Enrich etapów przetwarzania usługi BizTalk Services dodaje kontekstu wiadomości toohello właściwości skojarzone z odebrane dane hello. Na przykład promowanie toouse właściwości, dla routingu (opisanych poniżej) z wyszukiwania w bazie danych lub wyodrębniając wartość za pomocą wyrażenia XPath. Logic Apps udostępnia dane wyjściowe dane kontekstowe tooall dostępu z poprzedzających akcje, dzięki czemu proste tooreplicate hello takie samo zachowanie. Na przykład za pomocą hello `Get Row` akcji połączenia SQL, zwracanych danych z bazy danych programu SQL Server i użyj hello danych przez akcję decyzji dla routingu. Podobnie, właściwości przychodzące usługi Service Bus wiadomości w kolejce przez wyzwalacz są adresowanego, jak również za pomocą wyrażenia języka definicji przepływu pracy xpath hello XPath.

### <a name="use-custom-code"></a>Użyj niestandardowego kodu
Usługi BizTalk Services umożliwia określenie hello zbyt[uruchomienia niestandardowego kodu](https://msdn.microsoft.com/library/azure/dn232389.aspx) przekazany w własne zestawy. Ten sposób jest implementowany przez hello [IMessageInspector](https://msdn.microsoft.com/library/microsoft.biztalk.services.imessageinspector.aspx) interfejsu. Na każdym z etapów Mostek hello obejmuje dwie właściwości (na inspektora wprowadź i na inspektora zakończenia) zapewniające hello typ architektury .net utworzonego który implementuje ten interfejs. Kod niestandardowy pozwala tooperform bardziej złożonych przetwarzania na powitania danych, a także ponowne użycie istniejący kod w zestawach, wykonujących wspólnej logiki biznesowej. 

Logic Apps oferuje dwa podstawowe sposoby tooexecute niestandardowego kodu: usługi Azure Functions i aplikacji API Apps. Azure Functions można utworzyć i wywoływać z aplikacji logiki. Zobacz [Dodaj i wykonywania kodu niestandardowego dla usługi logic apps za pomocą usługi Azure Functions](../logic-apps/logic-apps-azure-functions.md). Korzystanie z aplikacji interfejsu API, część usługi Azure App Service, toocreate, swoje własne wyzwalacze i akcje. Dowiedz się więcej o [Tworzenie niestandardowych toouse interfejsu API z usługą Logic Apps](../logic-apps/logic-apps-create-api-app.md). 

Jeśli masz kod niestandardowy w assmeblies, który można wywołać z usługi BizTalk Services można albo przenieść to kodu funkcji tooAzure lub tworzenie niestandardowych interfejsów API z aplikacji interfejsu API. w zależności od jest implementacja. Na przykład jeśli masz kod, który opakowuje innej usługi, że aplikacje logiki nie ma łącznika, następnie utwórz aplikację interfejsu API i używać hello akcje, które zapewnia aplikacji interfejsu API w aplikacjach logiki. Jeśli masz funkcje pomocnicze lub bibliotek usługi Azure Functions jest prawdopodobnie hello najlepszego dopasowania.

### <a name="edi-processing-and-trading-partner-management"></a>EDI przetwarzania i Zarządzanie partnerami handlowymi
Usługi BizTalk Services zawiera przetwarzanie EDI i B2B z obsługą AS2 (zastosowania instrukcji 2), X12 i EDIFACT. Podobnie jak Logic Apps. W usługach BizTalk Twojej Tworzenie mostków EDI i Utwórz/Zarządzanie partnerami handlowymi i umów w hello dedykowanego portalu zarządzania i śledzenia.

W aplikacjach logiki, ta funkcja jest dołączana hello [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md). Ten krok składa się działań konta integracji i B2B hello EDI i B2B przetwarzania. Witaj [konta integracji](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) jest używane toocreate i zarządzanie nimi [partnerami handlowymi](../logic-apps/logic-apps-enterprise-integration-partners.md) i [umowy](../logic-apps/logic-apps-enterprise-integration-agreements.md). Po utworzeniu konta integracji można skojarzyć co najmniej jednego konta toohello aplikacji logiki. Jeden raz, można użyć tooaccess akcje B2B hello handlowymi informacje o partnerze w aplikacjach logiki. dostępne są następujące akcje Hello:

* Kodowanie AS2
* Dekodowanie AS2
* Kodowanie X12
* Dekodowanie X12
* Kodowanie EDIFACT
* Dekodowanie EDIFACT

W przeciwieństwie do usługi BizTalk Services te akcje są całkowicie niezależna od hello protokołów. Dlatego podczas tworzenia aplikacji logiki, uzyskuje się większą elastyczność na które łączniki Użyj toosend i odbierać dane. Na przykład jego jest możliwe tooreceive X12 pliki jako załączniki wiadomości e-mail, a następnie przetwórz tych plików w aplikacji logiki. 

## <a name="manage-and-monitor"></a>Monitorowanie i zarządzanie nim
A także zarządzania partnerami handlowymi, hello dedykowanego portalu dla usługi BizTalk Services pod warunkiem toomonitor możliwości śledzenia i rozwiązywania problemów. 

Logic Apps oferuje bardziej zaawansowane funkcje monitorowania i funkcji monitorowania w hello [portalu Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md)oraz z hello [rozwiązanie B2B usługi Operations Management Suite](../logic-apps/logic-apps-monitor-b2b-message.md); w tym aplikacji mobilnej dla śledzeniu na rzeczy Jeśli jesteś na powitania przejście.

## <a name="high-availability"></a>Wysoka dostępność
tooachieve wysokiej dostępności (HA) w usługach BizTalk, należy użyć więcej niż jedno wystąpienie w hello tooshare danego regionu, obciążenia przetwarzania. Dzięki aplikacjom logiki wysokiej dostępności w regionie jest wbudowana i pochodzi bez ponoszenia dodatkowych kosztów. Do odzyskiwania po awarii poza regionem do przetwarzania B2B usługi BizTalk proces tworzenia kopii zapasowej i przywracania jest wymagana. W aplikacjach logiki, cross-region aktywny/pasywny [możliwości DR](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md) podano; hello synchronizacji danych B2B co pozwala na kontach integracji w różnych regionach dla ciągłość prowadzenia działalności biznesowej.

## <a name="next"></a>Następne kroki
* [Dowiedzieć się, co to są aplikacje logiki](logic-apps-what-are-logic-apps.md)
* [Utworzyć swoją pierwszą aplikację logiki](logic-apps-create-a-logic-app.md) lub szybko rozpocząć pracę przy użyciu [wstępnie utworzonego szablonu](logic-apps-use-logic-app-templates.md)  
* [Widok hello wszystkie dostępne łączniki](../connectors/apis-list.md) można używać w aplikacji logiki
