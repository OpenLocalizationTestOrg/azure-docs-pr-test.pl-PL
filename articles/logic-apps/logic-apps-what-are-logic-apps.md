---
title: "aplikacje aaaConnect i integrowanie danych z przepływami pracy - Azure Logic Apps | Dokumentacja firmy Microsoft"
description: "Możesz tworzyć przepływy pracy i automatyzować procesy przez łączenie aplikacji i integrowanie danych z usługą Azure Logic Apps."
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 07765c05-72a6-4169-a8ab-f6420bfbaf07
ms.service: logic-apps
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/23/2017
ms.author: klam
ms.openlocfilehash: 53d4e165bb2205ddd56c1950719389725267ddea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-logic-apps"></a>Co to jest Logic Apps?
Aplikacje logiki Podaj toosimplify sposób i wdrażanie skalowalnej integracji i przepływów pracy w chmurze hello. Zawiera visual toomodel projektanta i automatyzacji procesu jako serię kroków znane jako przepływ pracy.  Brak [wiele łączników](../connectors/apis-list.md) między tooquickly chmurze i lokalne powitania zintegrowanie różnych usług i protokołów.  Aplikacja logiki rozpoczyna się od wyzwalacza (jak "po dodaniu konta tooDynamics CRM"), a po uruchamiania można rozpocząć liczbę kombinacji akcji, konwersje i logiki warunku.

Zalety korzystania z aplikacji logiki Hello Uwzględnij hello następujące elementy:  

* Oszczędzanie czasu Projektując złożonych procesów przy użyciu narzędzia do projektowania łatwe toounderstand
* Implementacja bezproblemowo wzorców i przepływów pracy, który byłby tooimplement trudne w kodzie
* Szybkie rozpoczynanie pracy przy użyciu szablonów
* Dostosowywanie aplikacji logiki przy użyciu własnych interfejsów API, własnego kodu i własnych akcji
* Połącz i Synchronizuj różnych systemów lokalnie i hello chmury
* Tworzenie na podstawie usług BizTalk Server, API Management, Azure Functions i Azure Service Bus z najwyższej klasy obsługą integracji

Logic Apps jest w pełni zarządzana iPaaS (Integracja platformy jako usługa) co umożliwia deweloperom nie toohave tooworry informacje o kompilowaniu hostingu, skalowalność, dostępności i zarządzania.  Logic Apps będzie skalować automatycznie toomeet żądanie.

![Projektant aplikacji przepływu](media/logic-apps-what-are-logic-apps/LogicAppCapture2.png)

Jak wspomniano, dzięki usłudze Logic Apps można automatyzować procesy biznesowe. Oto kilka przykładów:  

* Przenieś pliki przekazany tooan serwer FTP do magazynu Azure
* Przetwarzanie i kierowanie zamówień w systemach lokalnych i systemach w chmurze
* Monitorowanie wszystkich tweetów dotyczących niektórych tematu, analizowanie hello wskaźniki nastrojów klientów i tworzenie alertów i zadań dla elementy wymagające monitowania.

Scenariuszy, takich jak te można skonfigurować z hello projektanta wizualnego i bez konieczności napisania pojedynczy wiersz kodu. Rozpocznij [teraz tworzenie aplikacji logiki][create].  Napisana aplikacja logiki może być [szybko wdrażana i ponownie konfigurowana](../logic-apps/logic-apps-create-deploy-template.md) w wielu środowiskach i regionach.

## <a name="why-logic-apps"></a>Dlaczego warto korzystać z usługi Logic Apps?
Logic Apps szybkość i skalowalność powoduje przeniesienie do integracji hello korporacyjnej.  Witaj łatwość użycia hello projektanta, różnych dostępnych wyzwalacze i akcje i zaawansowane narzędzia do zarządzania należy scentralizowany swoje interfejsy API łatwiejsze niż kiedykolwiek.  Jak firm przejścia do digitalization, Logic Apps umożliwia systemów starszych i najnowocześniejsze tooconnect ze sobą.

Ponadto z naszych [konta integracji przedsiębiorstwa] [ biztalk] można skalować toomature scenariuszy integracji dzięki możliwości hello [wiadomości XML] [ xml], [zarządzania partnerami handlowymi][tpm]itd.

* **Narzędzia do projektowania łatwe toouse** -Logic Apps może być zaprojektowana end-to-end w przeglądarce hello lub za pomocą narzędzi Visual Studio. Rozpocznij od wyzwalacza — od toowhen prosty harmonogram, tworzony jest problem GitHub. Następnie Zorganizuj dowolną liczbę akcji przy użyciu bogatej galerii łączników hello.
* **Łatwe podłączanie interfejsów API** — nawet zadania tworzenia są łatwe toodescribe są trudne tooimplement w kodzie. Logic Apps umożliwia łatwe tooconnect różnych systemów. Mają tooconnect chmury rozwiązanie marketingowe tooyour lokalnym systemem rozliczeniowym? Chcesz toocentralize wiadomości na interfejsy API i w systemach z magistralą usług przedsiębiorstwa? Aplikacje logiki to hello najszybsze i najbardziej niezawodne toodeliver rozwiązania toothese problemów.
* **Szybkie rozpoczynanie pracy z szablonami** -toohelp Rozpoczynanie pracy przygotowaliśmy [galerii szablonów] [ templates] umożliwiającą toorapidly tworzenie niektórych typowych rozwiązań. Od zaawansowanych rozwiązań B2B toosimple SaaS łączności, a nawet kilka po prostu "do zabawy" — galerii hello jest hello najszybszy sposób tooget wprowadzenie hello możliwości usługi Logic Apps.
* **Możliwość rozszerzania** — nie widzisz łącznika hello należy? Logic Apps jest zaprojektowana toowork z własnych interfejsów API i kodu; można łatwo tworzyć własne toouse aplikacji interfejsu API jako niestandardowy łącznik lub wywołują [funkcji platformy Azure](https://functions.azure.com) tooexecute wstawek kodu na żądanie. 
* **Moc prawdziwej integracji** — łatwe rozpoczynanie pracy i rozwój w miarę potrzeb. Logic Apps można w prosty sposób korzystać hello możliwości usługi BizTalk, firmy Microsoft branży wiodące rozwiązanie tooenable integracji specjalistów toobuild hello rozwiązań integracji potrzebnych im. Dowiedz się więcej o hello [pakiet integracyjny dla przedsiębiorstw](../logic-apps/logic-apps-enterprise-integration-overview.md).

## <a name="logic-app-concepts"></a>Pojęcia dotyczące Aplikacji logiki
Witaj poniżej przedstawiono niektóre hello kluczowych elementów składających się na środowisko pracy Logic Apps hello. 

* **Przepływ pracy** -Logic Apps oferuje toomodel graficzny procesów biznesowych w postaci serii kroków lub przepływu pracy.
* **Zarządzane łączniki** — aplikacje logiki muszą uzyskać dostęp do toodata i usług. Zarządzanych łączników są tworzone specjalnie tooaid możesz podczas łączenia z tooand pracy z danymi. Lista hello łączników jest teraz dostępna w [zarządzanych łączników][managedapis].
* **Wyzwalacze** — niektóre zarządzane łączniki mogą również działać jako wyzwalacze. Wyzwalacz uruchamia nowe wystąpienie przepływu pracy na podstawie określonego zdarzenia, takie jak hello nadejście wiadomości e-mail lub zmiana konta usługi Azure Storage.
* **Akcje** — każdy krok po wyzwalaczu hello w przepływie pracy jest nazywany akcją. Każda akcja jest przeważnie mapowana tooan operacji na łącznika zarządzanych lub niestandardowych aplikacjach interfejsu API.
* **Pakiet integracyjny dla przedsiębiorstw** — w przypadku bardziej zaawansowanych scenariuszy integracji usługa Logic Apps oferuje możliwości usługi BizTalk. BizTalk to wiodąca w branży platforma integracji firmy Microsoft. łączniki pakiet integracyjny dla przedsiębiorstw Hello pozwalają tooeasily obejmują sprawdzania poprawności, przekształcania i więcej informacji, zobacz tooyour przepływów pracy aplikacji logiki.

## <a name="getting-started"></a>Wprowadzenie
* tooget pracy z usługą Logic Apps, wykonaj hello [tworzenie aplikacji logiki] [ create] samouczka.  
* [Wyświetlanie typowych przykładów i scenariuszy](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Dzięki usłudze Logic Apps możesz automatyzować procesy biznesowe](http://channel9.msdn.com/Events/Build/2016/T694) 
* [Dowiedz się, jak tooIntegrate systemy z usługą Logic Apps](http://channel9.msdn.com/Events/Build/2016/P462)

[biztalk]: logic-apps-enterprise-integration-accounts.md
[appservice]: ../app-service/app-service-value-prop-what-is.md
[create]: logic-apps-create-a-logic-app.md
[managedapis]: ../connectors/apis-list.md
[tpm]: logic-apps-enterprise-integration-accounts.md
[xml]: logic-apps-enterprise-integration-b2b.md
[templates]: logic-apps-use-logic-app-templates.md
