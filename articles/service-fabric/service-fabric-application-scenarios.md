---
title: aaaApplication scenariuszy i projektu | Dokumentacja firmy Microsoft
description: "Przegląd kategorie aplikacji w sieci szkieletowej usług w chmurze. W tym artykule omówiono projekt aplikacji, która korzysta z usług stanowe i bezstanowe."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3a8ca6ea-b8e9-4bc3-9e20-262437d2528e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 7/02/2017
ms.author: mfussell
ms.openlocfilehash: e36d5b2d21a6a1e3e85c9b21190072616e4921e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-scenarios"></a>Scenariusze aplikacji sieci szkieletowej usług
Sieć szkieletowa usług Azure oferuje niezawodny i elastyczny platformę umożliwiającą toowrite i uruchomić wiele typów usług i aplikacji biznesowych. Te aplikacje i mikrousług może być bezstanowe i stanowe i są równoważenia zasobów przez maszyny wirtualne toomaximize wydajności. Witaj unikatowy architektury sieci szkieletowej usług umożliwia tooperform niemal analizy danych w czasie rzeczywistym, obliczeń w pamięci, równoległych transakcji i przetwarzania zdarzeń w aplikacjach. Można łatwo skalować aplikacji w górę lub w dół (naprawdę przychodzący lub wychodzący), w zależności od zmieniających się wymagań dotyczących zasobów.

platformy Service Fabric Hello na platformie Azure jest idealny dla następującej kategorii aplikacji hello:

* **Wysoką dostępność usług**: usługi sieci szkieletowej usług zapewniają szybki trybu failover, tworząc wiele replik pomocniczych usługi. Jeśli węzeł, proces lub pojedynczej usługi ulegnie awarii, toohardware lub inne niepowodzenia, jedną z replik pomocniczych hello jest awansowana tooa repliki podstawowej przy minimalnej utracie usługi.
* **Skalowalnych usług**: poszczególnych usług mogą być partycjonowane, co pozwala na skalowanie w klastrze hello toobe stanu. Ponadto poszczególnych usług można tworzyć i usunąć na bieżąco hello. Usługi można szybko i łatwo skalować w poziomie z kilku wystąpień na kilka węzłów toothousands wystąpień na wielu węzłach, a następnie wyświetlane w ponownie, w zależności od potrzeb zasobów. Można użyć usługi sieć szkieletowa toobuild tych usług i zarządzania ich pełne cykle.
* **Obliczenia na danych Niestatyczne**: sieć szkieletowa usług pozwala toobuild danych, wejścia/wyjścia i obliczeń znacznym aplikacji stanowych. Sieć szkieletowa usług umożliwia kolokacji hello przetwarzania (obliczeń) i danych w aplikacjach. Zwykle, gdy aplikacja wymaga dostępu toodata, jest skojarzone z warstwą pamięci podręcznej lub magazynu danych zewnętrznych opóźnienia sieci. Za pomocą usług sieci szkieletowej usług stanowych tego opóźnienia została pominięta, włączanie więcej wydajności operacji odczytu i zapisu. Na przykład załóżmy, że masz aplikację, która wykonuje obok opcji zalecenia w czasie rzeczywistym dla klientów z wymaganiem czasu Rundy mniej niż 100 milisekund. Witaj opóźnienia i cechy jej wydajności usługi sieć szkieletowa usług (gdzie obliczeń hello zaznaczenia zalecenie jest współistnieje z hello danych i zasady) zapewnia toohello reakcji środowisko użytkownika w porównaniu z hello standardowej implementacji Model o toofetch hello niezbędne dane z magazynu zdalnego.  
* **Oparte na sesji aplikacji interaktywnych**: usługi sieć szkieletowa jest przydatne w przypadku aplikacji, takich jak gier online lub wiadomości błyskawicznych, wymagają małych opóźnieniach odczyty i zapisy. Sieć szkieletowa usług umożliwia toobuild możesz tych aplikacji interaktywnych, stanowe bez konieczności toocreate oddzielny magazyn lub pamięci podręcznej, co jest wymagane dla aplikacji bezstanowych. (Zwiększa to opóźnienie i potencjalnie wprowadza problemy niespójności.).
* **Analiza danych i przepływów pracy**: hello szybkie odczyty i zapisy sieci szkieletowej usług umożliwia aplikacjom niezawodnie musi przetworzyć zdarzenia lub strumieni danych. Sieć szkieletowa usług umożliwia również aplikacji, które opisują potoków przetwarzania, w którym wyniki muszą być wiarygodne i przekazany na toohello następnego przetwarzania etap bez utraty. Obejmują one systemów transakcyjnych i finansowych, gdzie gwarancje spójności i obliczanie danych są istotne.
* **Zbieranie IoT i przetwarzania danych**: ponieważ sieci szkieletowej usług obsługi dużej skali oraz małe opóźnienia za pośrednictwem jego usługi stanowej, jest idealny dla przetwarzania danych na milionów urządzeń gdzie są dane hello hello urządzenia i obliczeń hello wspólnie.
Zaobserwowano kilku klientów, którzy mają wbudowane systemy IoT przy użyciu usługi Service Fabric w tym [BMW](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/24/service-fabric-customer-profile-bmw-technology-corporation/), [elektrycznego Schneider](https://blogs.msdn.microsoft.com/azureservicefabric/2016/08/05/service-fabric-customer-profile-schneider-electric/) i [siatki systemów](https://blogs.msdn.microsoft.com/azureservicefabric/2016/06/20/service-fabric-customer-profile-mesh-systems/).

## <a name="application-design-case-studies"></a>Analizy przypadków projektowania aplikacji
Liczba przypadków pokazujący, jak sieć szkieletowa usług to toodesign używane aplikacje są publikowane na powitania [blog zespołu usługi sieć szkieletowa](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/) i hello [mikrousług rozwiązań lokacji](https://azure.microsoft.com/solutions/microservice-applications/).

## <a name="design-applications-composed-of-stateless-and-stateful-microservices"></a>Projektowanie aplikacji składający się z mikrousług bezstanowe i stanowe
Kompilowanie aplikacji za pomocą usługi w chmurze Azure roli proces roboczy jest przykładem bezstanowego usługi. Z kolei mikrousług stanowe Obsługa stanu autorytatywne poza hello żądania i odpowiedzi. Zapewnia wysoką dostępność i spójności stanu hello za pośrednictwem prostych interfejsów API, który transakcyjne zagwarantować kopii za pomocą replikacji. Usługa sieć szkieletowa usług stanowych democratize wysokiej dostępności w jednym tooall typy aplikacji, a nie tylko baz danych i innych magazynów danych. Jest to fizyczne postępu. Aplikacje już zostały przeniesione od używania tylko relacyjne bazy danych dla baz danych tooNoSQL wysokiej dostępności. Teraz same aplikacje hello może mieć ich stanu "gorących" i danych zarządzanych w nich dla wzrost wydajności dodatkowe bez ograniczania niezawodności, spójność i dostępności.

Podczas tworzenia aplikacji składający się z mikrousług, zazwyczaj mają kombinację aplikacji bezstanowych sieci web (ASP.NET, Node.js, itp.) wywołanie do usług warstwy środkowej bezstanowe i stanowe biznesowych, wszystkich wdrożonych w hello sam klaster sieci szkieletowej usług za pomocą poleceń wdrażania hello sieci szkieletowej usług. Każdy z tych usług jest niezależny z uwzględnieniem tooscale, niezawodności i użycie zasobów, znacznie poprawia elastyczność w zarządzaniu rozwoju i cyklem życia.

Stanowe mikrousług uprościć projektów aplikacji, ponieważ będą oni mogli usunąć hello potrzebę hello dodatkowe kolejki i pamięci podręczne, które zazwyczaj były wymagane tooaddress hello dostępności i opóźnienia wymagania aplikacji bezstanowych czysto. Ponieważ usługi stanowej naturalnie wysokiej dostępności i małego opóźnienia, oznacza to, czy mniej przenoszenie toomanage części w aplikacji jako całość. Hello poniższych diagramach przedstawiono hello różnice między projektowaniu aplikacji bezstanowych, który jest obiektem stanowym. Dzięki wykorzystaniu hello [niezawodne usługi](service-fabric-reliable-services-introduction.md) i [Reliable Actors](service-fabric-reliable-actors-introduction.md) modele programowania usług stanowych uproszczeniu aplikacji uzyskanie wysokiej przepływności i małe opóźnienia.

## <a name="an-application-built-using-stateless-services"></a>Aplikacji utworzonej przy użyciu usług bezstanowych
![Przy użyciu usługi bezstanowej aplikacji][Image1]

## <a name="an-application-built-using-stateful-services"></a>Aplikacji utworzony za pomocą usługi stanowej
![Przy użyciu usługi bezstanowej aplikacji][Image2]

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki

* Nasłuchiwanie na zbyt[analizy przypadków](https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=qDJnf86yC_5206218965
)
* Przeczytaj informacje o [analizy przypadków](https://blogs.msdn.microsoft.com/azureservicefabric/tag/customer-profile/)
* Dowiedz się więcej o [wzorców i scenariusze](service-fabric-patterns-and-scenarios.md)

* Rozpocząć tworzenie usług bezstanowych i stanowych z hello sieci szkieletowej usług [niezawodne usługi](service-fabric-reliable-services-quick-start.md) i [niezawodnej podmiotów](service-fabric-reliable-actors-get-started.md) modele programowania.
* Zobacz też hello następujące tematy:
  * [Podaj informacje o mikrousług](service-fabric-overview-microservices.md)
  * [Definiowanie i zarządzanie nimi stanu usługi](service-fabric-concepts-state.md)
  * [Dostępność usług sieci szkieletowej usług](service-fabric-availability-services.md)
  * [Skaluj usługi sieci szkieletowej usług](service-fabric-concepts-scalability.md)
  * [Partycji usługi sieci szkieletowej usług](service-fabric-concepts-partitioning.md)

[Image1]: media/service-fabric-application-scenarios/AppwithStatelessServices.jpg
[Image2]: media/service-fabric-application-scenarios/AppwithStatefulServices.jpg
