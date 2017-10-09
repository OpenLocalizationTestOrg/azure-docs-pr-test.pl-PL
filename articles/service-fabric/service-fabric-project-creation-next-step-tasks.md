---
title: kroki dalej tworzenia projektu sieci szkieletowej aaaService | Dokumentacja firmy Microsoft
description: "Ten artykuł zawiera łącza tooa zestaw zadań związanych z projektowaniem core dla sieci szkieletowej usług"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: rwike77
ms.openlocfilehash: 45598bfabedf280fba8af449ef920f40b409a609
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="your-service-fabric-application-and-next-steps"></a>Sieć szkieletowa usług aplikacji i następne kroki
Utworzono aplikację sieci szkieletowej usług Azure. W tym artykule opisano w skład hello projektu i potencjalne poniższe kroki.

## <a name="your-application"></a>Aplikacja
Każdej nowej aplikacji zawiera projekt aplikacji. Może to być jeden lub dwa dodatkowe projekty, w zależności od typu hello wybrane usługi.

### <a name="hello-application-project"></a>Projekt aplikacji Hello
Projekt aplikacji Hello obejmuje:

* Zestaw odwołuje się do toohello usług, które składają się na aplikację.
* Profilów (węzła 1 lokalnego, 5 węzła lokalnego i chmura) służy toomaintain preferencje dotyczące pracy z różnych środowiskach — na przykład punktu końcowego klastra pokrewne tooa preferencji i czy tooperform uaktualniania wdrożenia domyślnie trzy publikowania.
* Trzy pliki parametrów aplikacji (tak samo jak powyżej) można toomaintain konfiguracje specyficzne dla środowiska aplikacji, takie jak liczba hello toocreate partycji dla usługi.
* Skrypt wdrożenia, których można używać toodeploy z wiersza polecenia hello lub w ramach automatycznych ciągłego potoku integracji i wdrażania aplikacji.
* manifest aplikacji Hello, który opisuje aplikacji hello. Hello manifest można znaleźć w folderze ApplicationPackageRoot hello.

### <a name="stateless-service"></a>Usługi bezstanowej
Po dodaniu nowej usługi bezstanowej Visual Studio dodaje rozwiązania tooyour projektu usługi, który zawiera typ podrzędne w stosunku `StatelessService`. Usługa Hello zwiększa zmienną lokalną w licznika.

### <a name="stateful-service"></a>Usługi stanowej
Po dodaniu nowej usługi stanowej, Visual Studio dodaje rozwiązania tooyour projektu usługi, który zawiera typ podrzędne w stosunku `StatefulService`. Witaj usługi zwiększa licznik w jego `RunAsync` — metoda i magazyny wynik hello w `ReliableDictionary`.

### <a name="actor-service"></a>Usługa aktora
Po dodaniu nowego niezawodnego aktora Visual Studio dodaje dwa projekty tooyour rozwiązania: aktora projektu i projektu interfejsu.

Projekt aktora Hello udostępnia metody dla ustawienia i uzyskiwanie hello wartości licznika, który jest niezawodnie utrwalone w ramach stanu aktora hello. Witaj projektu interfejsu udostępnia interfejs, że inne usługi można użyć tooinvoke hello aktora.

### <a name="stateless-web-api"></a>Bezstanowe interfejsu API sieci Web
Hello bezstanowych projektu interfejsu API sieci Web udostępnia podstawowego usługi, których można używać tooopen klientów tooexternal aplikacji sieci web. Aby uzyskać więcej informacji na temat struktury projektu hello, zobacz [usług interfejsu API sieci Web sieci szkieletowej usług za pomocą hostingu samodzielnego OWIN](service-fabric-reliable-services-communication-webapi.md).


### <a name="aspnet-core"></a>Platformy ASP.NET core
Witaj zestawu SDK usług sieci szkieletowej udostępnia hello sam zestaw platformy ASP.NET Core szablonów, które są dostępne dla projektów platformy ASP.NET Core autonomicznej: pusta, [interfejsu API sieci Web][aspnet-webapi], i [aplikacji sieci Web][aspnet-webapp].

### <a name="guest-executables-and-guest-containers"></a>Gość kontenerów plików wykonywalnych i gościa

Usługa sieci szkieletowej "Gość" to usługa, która jest kompilowany bez modele programowania hello platformy. Pliki binarne hello gościa można spakować albo [bezpośrednio w pakiecie aplikacji hello](service-fabric-deploy-existing-app.md) lub [za pośrednictwem obrazu kontenera](service-fabric-deploy-container.md). W obu przypadkach program Visual Studio tworzy hello artefakty niezbędne w hello **ApplicationPackageRoot** folderu projekt aplikacji hello. Visual Studio nie utworzy nowy projekt usługi, ponieważ kod hello już istnieje w innym miejscu. Jeśli chcesz toomanage użytkownika gościa projektów obok projekt aplikacji hello sieci szkieletowej usług, możesz dodać je toohello tym samym rozwiązaniu Visual Studio.

## <a name="next-steps"></a>Następne kroki
### <a name="create-an-azure-cluster"></a>Tworzenie klastra platformy Azure
Witaj zestawu SDK usług sieci szkieletowej udostępnia klastra lokalnego dla projektowania i testowania. toocreate klastra na platformie Azure, zobacz [konfigurowania klastra sieci szkieletowej usług z portalu Azure hello][create-cluster-in-portal].

### <a name="publish-your-application-tooazure"></a>Publikowanie tooAzure Twojej aplikacji
Można opublikować aplikacji bezpośrednio z programu Visual Studio tooan klastrze platformy Azure. toolearn, zobacz temat [publikowania tooAzure Twojej aplikacji][publish-app-to-azure].

### <a name="use-service-fabric-explorer-toovisualize-your-cluster"></a>Użyj Eksploratora usługi sieć szkieletowa toovisualize klastra
Service Fabric Explorer oferuje łatwe toovisualize klastra, w tym wdrożone aplikacje i fizycznego układu. toolearn więcej, zobacz [wizualizacja klastra przy użyciu Eksploratora usługi sieć szkieletowa][visualize-with-sfx].

### <a name="version-and-upgrade-your-services"></a>Wersja i uaktualniania usług
Sieć szkieletowa usług umożliwia niezależnie od wersji i uaktualniania usług niezależne w aplikacji. toolearn więcej, zobacz [wersji i uaktualniania usług][app-upgrade-tutorial].

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a>Konfigurowanie ciągłej integracji z Visual Studio Team Services
toolearn proces ciągłej integracji można skonfigurować dla aplikacji sieci szkieletowej usług, zobacz [skonfigurować ciągłe integrację z programem Visual Studio Team Services][ci-with-vso].

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
