---
title: "aaaAzure sieci szkieletowej usług z zarządzanie interfejsami API — omówienie | Dokumentacja firmy Microsoft"
description: "W tym artykule jest wprowadzenie toousing Azure API Management jako aplikacje sieci szkieletowej usług tooyour bramy."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 96176149-69bb-4b06-a72e-ebbfea84454b
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/22/2017
ms.author: vturecek
ms.openlocfilehash: f01dc570a11e68cd4a2d878abbe6019e209e2f5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-with-azure-api-management-overview"></a>Sieć szkieletowa usług z usługi Azure API Management — omówienie

Aplikacje w chmurze zazwyczaj konieczne tooprovide frontonu bramy pojedynczy punkt wejściowych dla użytkowników, urządzeń lub innych aplikacji. W sieci szkieletowej usług, brama może być dowolnym usługi bezstanowej takich jak [aplikacji platformy ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), lub inna usługa przeznaczone dla ruch przychodzący, takich jak [usługi Event Hubs](https://docs.microsoft.com/azure/event-hubs/), [Centrum IoT](https://docs.microsoft.com/azure/iot-hub/), lub [Azure API Management](https://docs.microsoft.com/azure/api-management/).

W tym artykule jest wprowadzenie toousing Azure API Management jako aplikacje sieci szkieletowej usług tooyour bramy. Zarządzanie interfejsami API integruje się bezpośrednio z usługi Service Fabric, umożliwiając toopublish interfejsy API z bogaty zestaw usług sieci szkieletowej usług zaplecza tooyour routingu reguły. 

## <a name="architecture"></a>Architektura
Architektura usługi Service Fabric korzysta z aplikacji jednej strony sieci web, która nawiązuje połączeń HTTP tooback usług z użyciem interfejsów API protokołu HTTP. Witaj [usługi Service Fabric — wprowadzenie przykładowej aplikacji](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started) przedstawiono przykład tej architektury.

W tym scenariuszu usługi bezstanowej sieci web służy jako brama hello na powitania aplikacji usługi Service Fabric. Ta metoda wymaga toowrite usługi sieci web, który można serwera proxy HTTP żądania usług tooback-end, jak pokazano w powitania po diagramu:

![Sieć szkieletowa usług Azure API Management topologii Przegląd][sf-web-app-stateless-gateway]

Jak aplikacje zwiększa się złożoność, więc hello bram, które musi przedstawić interfejsu API przed wiele usług zaplecza. Zarządzanie interfejsami API Azure jest zaprojektowana toohandle interfejsów API złożonych za pomocą reguły routingu kontroli dostępu, limitów szybkości, monitorowanie, rejestrowanie zdarzeń i buforowania odpowiedzi z minimalnym nakładu pracy. Azure API Management obsługuje odnajdowania usługi sieć szkieletowa usług, rozwiązania partycji i replik wybór toointelligently trasy bezpośrednio żądania usług tooback-end w sieci szkieletowej usług, dzięki czemu nie trzeba toowrite własne bezstanowych bramy interfejsu API. 

W tym scenariuszu interfejsu użytkownika jest nadal obsługiwane za pośrednictwem usługi sieci web podczas wywołania interfejsu API protokołu HTTP sieci web hello są zarządzane i kierowane za pomocą usługi Azure API Management, jak pokazano w powitania po diagramu:

![Sieć szkieletowa usług Azure API Management topologii Przegląd][sf-apim-web-app]

## <a name="application-scenarios"></a>Scenariusze aplikacji

Usługi w sieci szkieletowej usług mogą być bezstanowe i stanowe i mogą być partycjonowane, przy użyciu jednej z trzech schematy: pojedyncze, int-64 zakresu i nazwane. Rozpoznanie punktu końcowego usługi wymaga identyfikacji określonej partycji wystąpienia określonej usługi. W trakcie rozwiązywania punktu końcowego usługi, zarówno hello nazwy wystąpienia usługi (na przykład `fabric:/myapp/myservice`) również muszą być określone hello określonej partycji usługi hello, chyba że w przypadku hello pojedynczych partycji.

Zarządzanie interfejsami API Azure może służyć z dowolną kombinację usług bezstanowych, stanowych usług i wszelkie schemat partycjonowania.

## <a name="send-traffic-tooa-stateless-service"></a>Wyślij usługi bezstanowej tooa ruchu

W przypadku najprostszym hello jest przekazywane wystąpienie usługi bezstanowej tooa. tooachieve, operacja interfejsu API zarządzania zawiera zasady przetwarzania przychodzącego z sieci szkieletowej usług zaplecza mapujący wystąpienia określonej usługi bezstanowej tooa w wewnętrznej sieci szkieletowej usług hello. Żądania wysyłane toothat usługi są wysyłane tooa losowe repliki wystąpienia usługi bezstanowej hello.

#### <a name="example"></a>Przykład
W następujących scenariuszy hello, aplikacji usługi Service Fabric zawiera usługi bezstanowej o nazwie `fabric:/app/fooservice`, który uwidacznia wewnętrzny API protokołu HTTP. Nazwa wystąpienia usługi Hello dobrze znanych i może być ustalony bezpośrednio w hello zarządzanie interfejsami API przetwarzania przychodzących zasad. 

![Sieć szkieletowa usług Azure API Management topologii Przegląd][sf-apim-static-stateless]

## <a name="send-traffic-tooa-stateful-service"></a>Wyślij usługi stanowej tooa ruchu

Podobny scenariusz usługi bezstanowej toohello ruchu może być przekazywany tooa usługi stanowej wystąpienia. W takim przypadku operacja interfejsu API zarządzania zawiera zasady przetwarzania przychodzącego z sieci szkieletowej usług zaplecza mapujący żądania tooa określonej partycji określonego *stateful* wystąpienie usługi. Witaj toomap partycji toois każdego żądania obliczane przy użyciu metody lambda za pomocą niektórych danych wejściowych z hello przychodzące żądanie HTTP, takie jak wartość w hello ścieżki adresu URL. Hello zasad może być skonfigurowany toosend żądań toohello tylko replika podstawowa lub tooa repliki losowych operacji odczytu.

#### <a name="example"></a>Przykład

W powitania od scenariusza, aplikacji usługi Service Fabric zawiera podzielonym na partycje usługi stanowej o nazwie `fabric:/app/userservice` który uwidacznia wewnętrzny API protokołu HTTP. Nazwa wystąpienia usługi Hello dobrze znanych i może być ustalony bezpośrednio w hello zarządzanie interfejsami API przetwarzania przychodzących zasad.  

Witaj usługi jest podzielona na partycje przy użyciu hello Int64 schemat partycji z dwóch partycji i zakres klucza, który obejmuje `Int64.MinValue` zbyt`Int64.MaxValue`. Hello wewnętrznych zasad oblicza klucza partycji w ramach tego zakresu, konwertując hello `id` wartość podana w hello adresu URL żądania ścieżki tooa 64-bitową liczbę całkowitą, mimo że dowolny algorytm może być kluczem partycji hello używane toocompute tutaj. 

![Sieć szkieletowa usług Azure API Management topologii Przegląd][sf-apim-static-stateful]

## <a name="send-traffic-toomultiple-stateless-services"></a>Wysyłaj ruch usługi bezstanowej toomultiple

W bardziej zaawansowanych scenariuszy można zdefiniować operacji interfejsu API zarządzania czy mapy żądań toomore niż jedna usługa wystąpienia. W przypadku każdej operacji zawiera zasady, która mapuje żądań tooa wystąpienia określonej usługi na podstawie wartości z hello przychodzące żądanie HTTP, takie jak ciąg adresu URL hello ścieżkę lub kwerendę, a w przypadku hello stanowych usług, partycji w obrębie hello wystąpienie usługi . 

tooachieve to zarządzanie interfejsami API operacji zawiera zasady przetwarzania przychodzącego z sieci szkieletowej usług zaplecza mapujący tooa wystąpienie usługi bezstanowej hello sieci szkieletowej usług zaplecza na podstawie wartości pobierane z hello przychodzące żądanie HTTP. Wystąpienie usługi tooa żądania są wysyłane tooa repliki losowe hello wystąpienia usługi.

#### <a name="example"></a>Przykład

W tym przykładzie nowego wystąpienia usługi bezstanowej utworzono dla poszczególnych użytkowników aplikacji o nazwie dynamicznie generowanym przy użyciu hello następującej formuły:
 
 - `fabric:/app/users/<username>`

 Każda usługa ma unikatową nazwę, ale hello nazwy nie są znane początkowych ponieważ hello usług są tworzone w odpowiedzi toouser lub administratora danych wejściowych, jak i w związku z tym nie może być ustalony do zasad APIM lub reguły routingu. Zamiast tego nazwy hello hello usługi toowhich toosend żądanie jest generowana w definicji zasad zaplecza hello z hello `name` wartość podana w ścieżka żądania hello adresu URL. Na przykład:

  - A zbyt żądania`/api/users/foo` routingiem tooservice wystąpienia`fabric:/app/users/foo`
  - A zbyt żądania`/api/users/bar` routingiem tooservice wystąpienia`fabric:/app/users/bar`

![Sieć szkieletowa usług Azure API Management topologii Przegląd][sf-apim-dynamic-stateless]

## <a name="send-traffic-toomultiple-stateful-services"></a>Wysyłaj ruch usługi stanowej toomultiple

Podobny przykład toohello bezstanowych usługi Zarządzanie interfejsami API operacji można mapować żądań toomore niż jeden **stateful** wystąpienie usługi, w którym to przypadku należy również może być konieczne tooperform rozpoznawania partycji dla każdej usługi stanowej wystąpienie.

tooachieve to zarządzanie interfejsami API operacji zawiera zasady przetwarzania przychodzącego z sieci szkieletowej usług zaplecza mapujący tooa wystąpienie usługi stanowej hello sieci szkieletowej usług zaplecza na podstawie wartości pobierane z hello przychodzące żądanie HTTP. Ponadto toomapping wystąpienie usługi toospecific żądania, żądania hello można także zamapowanych tooa określonej partycji w ramach hello wystąpienie usługi i opcjonalnie repliki podstawowej hello tooeither lub losowych repliki pomocniczej w hello partycji.

#### <a name="example"></a>Przykład

W tym przykładzie nowe wystąpienie usługi stanowej jest tworzone dla poszczególnych użytkowników aplikacji hello nazwą dynamicznie generowanym, za pomocą następującej formuły hello:
 
 - `fabric:/app/users/<username>`

 Każda usługa ma unikatową nazwę, ale hello nazwy nie są znane początkowych ponieważ hello usług są tworzone w odpowiedzi toouser lub administratora danych wejściowych, jak i w związku z tym nie może być ustalony do zasad APIM lub reguły routingu. Zamiast tego nazwy hello hello usługi toowhich toosend żądanie jest generowana w definicji zasad zaplecza hello z hello `name` ścieżka żądania adresu URL hello podana wartość. Na przykład:

  - A zbyt żądania`/api/users/foo` routingiem tooservice wystąpienia`fabric:/app/users/foo`
  - A zbyt żądania`/api/users/bar` routingiem tooservice wystąpienia`fabric:/app/users/bar`

Każde wystąpienie usługi są również podzielone na partycje przy użyciu hello Int64 schemat partycji z dwóch partycji i zakres klucza, który obejmuje `Int64.MinValue` zbyt`Int64.MaxValue`. Hello wewnętrznych zasad oblicza klucza partycji w ramach tego zakresu, konwertując hello `id` wartość podana w hello adresu URL żądania ścieżki tooa 64-bitową liczbę całkowitą, mimo że dowolny algorytm może być kluczem partycji hello używane toocompute tutaj. 

![Sieć szkieletowa usług Azure API Management topologii Przegląd][sf-apim-dynamic-stateful]

## <a name="next-steps"></a>Następne kroki

Wykonaj hello [Przewodnik Szybki start dotyczący](service-fabric-api-management-quick-start.md) tooset się pierwszy sieci szkieletowej usług klaster z interfejsu API zarządzania i przepływ żądań za pośrednictwem interfejsu API zarządzania tooyour usług.

<!-- links -->

<!-- pics -->
[sf-apim-web-app]: ./media/service-fabric-api-management-overview/sf-apim-web-app.png
[sf-web-app-stateless-gateway]: ./media/service-fabric-api-management-overview/sf-web-app-stateless-gateway.png
[sf-apim-static-stateless]: ./media/service-fabric-api-management-overview/sf-apim-static-stateless.png
[sf-apim-static-stateful]: ./media/service-fabric-api-management-overview/sf-apim-static-stateful.png
[sf-apim-dynamic-stateless]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateless.png
[sf-apim-dynamic-stateful]: ./media/service-fabric-api-management-overview/sf-apim-dynamic-stateful.png