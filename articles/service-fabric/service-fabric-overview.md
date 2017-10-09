---
title: "aaaOverview sieci szkieletowej usług na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przegląd sieci szkieletowej usług, w którym aplikacje składają się z wielu mikrousług tooprovide skalowanie i odporność. Sieć szkieletowa usług to platforma systemów rozproszonych używane toobuild skalowalne, niezawodne i łatwe zarządzane aplikacje hello chmury."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: masnider
ms.assetid: bbcc652a-a790-4bc4-926b-e8cd966587c0
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/02/2017
ms.author: mfussell
ms.openlocfilehash: 427fcedf97e6b2aae42d240c63e9f85daed8d962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-service-fabric"></a>Omówienie usługi Azure Service Fabric
Sieć szkieletowa usług Azure to platforma systemów rozproszonych, dzięki którym toopackage łatwe, wdrażanie i zarządzanie mikrousług skalowalne i niezawodne i kontenerów. Sieć szkieletowa usług dotyczy również hello znaczne trudności w tworzenie i zarządzanie natywnych aplikacji w chmurze. Deweloperzy i administratorzy mogą uniknąć złożonych problemów związanych z infrastrukturą i skoncentrować się na implementowaniu wymagających obciążeń o znaczeniu strategicznym, które są skalowalne, niezawodne i łatwe w zarządzaniu. Sieć szkieletowa usług reprezentuje Platforma następnej generacji hello tworzenia oraz zarządzania nimi te klasy korporacyjnej, warstwy 1, skali chmury aplikacji uruchomionych w kontenerach.

Ten krótki film pokazuje sieci szkieletowej usług i mikrousług:<center><a target="_blank" href="https://aka.ms/servicefabricvideo">  
<img src="./media/service-fabric-overview/OverviewVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="applications-composed-of-microservices"></a>Aplikacje składa się z mikrousług 
Sieć szkieletowa usług pozwala toobuild aplikacji i zarządzanie nimi skalowalne i niezawodne składa się z mikrousług czy wykonać o wysokiej gęstości na współużytkowanej puli maszyn, które jest określane tooas klastra. Zapewnia on toobuild zaawansowane, lekkie środowisko uruchomieniowe, rozproszonych, skalowalna, bezstanowe i stanowe mikrousług uruchomione w kontenerach. Zapewnia także tooprovision możliwości zarządzania kompleksowej aplikacji, wdrażanie, monitorowanie, uaktualnienie/poprawki i usunąć wdrożonych aplikacji, takich jak konteneryzowanych usługi.

Sieć szkieletowa usług obsługuje wiele usług firmy Microsoft już dziś, łącznie z bazy danych SQL Azure, Azure DB rozwiązania Cosmos, Cortana, Microsoft Power BI, Microsoft Intune, Azure Event Hubs, Centrum IoT Azure, Dynamics 365, Skype dla firm i wiele podstawowych usług platformy Azure.

Sieć szkieletowa usług to dopasowane toocreate macierzystego usługi w chmurze można rozpoczęcie od czegoś małego, zgodnie z potrzebami, które zwiększa skalowalność toomassive, setek lub tysięcy komputerów.

Współczesne Internet skali usługi są wbudowane z mikrousług. Mikrousług przykłady bramy protokołu, profile użytkowników, zakupy wózki spisu przetwarzania, kolejek i umieszcza w pamięci podręcznej. Sieć szkieletowa usług to platforma mikrousług, która zapewnia unikatową nazwę, która może być bezstanowe i stanowe co mikrousługi (lub kontenera).

Sieć szkieletowa usług zapewnia kompleksowe środowisko wykonawcze i cyklem życia tooapplications możliwości zarządzania, które składają się z tymi mikrousług. Obsługuje mikrousług wewnątrz kontenerów, które są wdrożone i aktywowana w klastrze usługi sieć szkieletowa hello. Przenoszenie z maszyn wirtualnych toocontainers umożliwia zwiększenie kolejności o wielkości w gęstości. Podobnie innego rzędu w gęstość staje się możliwe, gdy zostanie przeniesiony z toomicroservices kontenery w tych kontenerach. Na przykład jeden klaster bazy danych SQL Azure obejmuje setki komputerów z systemem dziesiątki tysięcy kontenery hostujących łącznie setki tysięcy baz danych. Każda baza danych jest mikrousługi stanowe sieci szkieletowej usług. 

Aby uzyskać więcej informacji na temat podejścia mikrousług hello przeczytaj [Dlaczego mikrousług podejście toobuilding aplikacji?](service-fabric-overview-microservices.md)

## <a name="container-deployment-and-orchestration"></a>Wdrażanie kontenera i aranżacji
Sieć szkieletowa usług to firmy Microsoft [orchestrator kontenera](service-fabric-cluster-resource-manager-introduction.md) wdrażanie mikrousług w klastrze maszyn. Mikrousług mogą być opracowane na wiele sposobów korzystania hello [usługi sieć szkieletowa modele programowania](service-fabric-choose-framework.md), [platformy ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md), toodeploying [żadnego kodu wybór](service-fabric-deploy-existing-app.md). Ważne, można mieszać zarówno usług w procesach i usług w kontenerach w hello tej samej aplikacji. Jeśli chcesz zbyt[wdrażania i zarządzania nimi kontenery](service-fabric-containers-overview.md), sieć szkieletowa usług to doskonałe jako orchestrator kontenera.

## <a name="any-os-any-cloud"></a>Dowolnego systemu operacyjnego, wszelkie chmury
Sieć szkieletowa usług działa wszędzie. Klastrów można utworzyć dla sieci szkieletowej usług w wielu środowiskach, w tym na platformie Azure lub lokalnie, w systemie Windows Server lub w systemie Linux. Można nawet utworzyć klastry na innych chmur publicznych. Ponadto środowisko projektowe hello w hello zestawu SDK jest **identyczne** toohello środowiska produkcyjnego, z żadnych emulatorów związane. Innymi słowy co działa w klastrze lokalnym programowanie wdraża klastry toohello w innych środowiskach.

![Platforma sieci szkieletowej usług][Image1]

Więcej informacji na temat tworzenia klastrów lokalnymi, przeczytaj [tworzenia klastra w systemie Windows Server lub Linux](service-fabric-deploy-anywhere.md) lub na platformie Azure, tworzenia klastra [za pośrednictwem portalu Azure hello](service-fabric-cluster-creation-via-portal.md).

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Bezstanowe i stanowe mikrousług dla sieci szkieletowej usług
Sieć szkieletowa usług umożliwia toobuild aplikacji, które składają się z mikrousług lub kontenerów. Bezstanowe mikrousług (takie jak protokół bramy i serwerów proxy sieci web) nie obsługują modyfikowalną stanu poza żądania i odpowiedzi z usługi hello. Role procesów roboczych usługi w chmurze Azure są przykładem bezstanowego usługi. Stanowe mikrousług (na przykład konta użytkowników, baz danych, urządzeń, wózkach sklepowych zakupów i kolejek) Obsługa modyfikowalna, autorytatywnych stan poza hello żądania i odpowiedzi. Współczesnych aplikacji internetowych skali składają się z kombinacji usług bezstanowych i stanowych mikrousług. 

Klucza differentation z sieci szkieletowej usług jest jego skoncentrowanie się na tworzeniu usługi stanowej, za pomocą hello [wbudowanych modele programowania ](service-fabric-choose-framework.md) lub konteneryzowanych usług stanowych. Witaj [scenariuszy aplikacji](service-fabric-application-scenarios.md) opisano scenariusze hello, w których są używane usługi stanowej.


## <a name="application-lifecycle-management"></a>Zarządzanie cyklem życia aplikacji
Sieć szkieletowa usług zapewnia obsługę cyklu życia pełnej aplikacji hello i CI/CD, łącznie z kontenerów aplikacji w chmurze. Tego cyklu obejmuje programowanie za pomocą wdrażania, zarządzania infrastrukturą i likwidowaniu tooeventual konserwacji.

Możliwości zarządzania cyklem życia aplikacji w sieci szkieletowej usług włączyć administratorów aplikacji i tooprovision proste, niski touch przepływy pracy toouse Operatorzy IT, wdrażania, poprawki i monitorowania aplikacji. Te wbudowane przepływy pracy znacznego obniżenia hello obciążeń aplikacji tookeep Operatorzy IT ciągłej dostępności.

Większość aplikacji składają się z kombinacji mikrousług bezstanowe i stanowe, kontenery i inne pliki wykonywalne, które są wdrożone razem. Dzięki użyciu silne typów w przypadku aplikacji hello, sieci szkieletowej usług umożliwia wdrożenie hello wiele wystąpień aplikacji. Każde wystąpienie jest zarządzane i zaktualizować niezależnie. Ważne sieci szkieletowej usług można wdrożyć kontenerów lub wszystkie pliki wykonywalne i ich niezawodne. Na przykład sieci szkieletowej usług można wdrażać .NET, platformy ASP.NET Core, node.js, Windows kontenerów, Linux kontenerów, Java maszyn wirtualnych, skrypty, kątową lub dosłownie wszystko, co stanowi aplikacji.

Sieć szkieletowa usług jest zintegrowany z elementu konfiguracji/CD narzędzi takich jak [Visual Studio Team Services](https://www.visualstudio.com/team-services/), [Wpięć](https://jenkins.io/index.html), i [wdrażanie Ośmiornica](https://octopus.com/) i mogą być używane z innych popularnych narzędzi CI/CD.

Aby uzyskać więcej informacji dotyczących zarządzania cyklem życia aplikacji, przeczytaj [cyklem życia aplikacji](service-fabric-application-lifecycle.md). Aby uzyskać więcej informacji na temat toodeploy dowolny kod, zobacz [wdrażanie pliku wykonywalnego gościa](service-fabric-deploy-existing-app.md).

## <a name="key-capabilities"></a>Najważniejsze możliwości
Przy użyciu usługi Service Fabric, można:

* Wdróż tooAzure lub tooon lokalnych centrów danych, uruchomienia systemu Windows lub Linux z zero zmian w kodzie. Jednokrotnego zapisu, a następnie wdrożyć dowolnym tooany klastra sieci szkieletowej usług.
* Tworzenie skalowalnych aplikacji, które składają się z mikrousług przy użyciu modele programowania hello sieci szkieletowej usług, w pojemnikach lub dowolny kod.
* Opracowywania wysoce niezawodne bezstanowe i stanowe mikrousług. Uprościć hello projektowania aplikacji przy użyciu mikrousług stanowych. 
* Za pomocą hello nowych Reliable Actors programowania modelu toocreate obiekty chmury samodzielną kod i stanu.
* Wdrażanie i organizowania kontenerów, które obejmują kontenery systemu Windows i Linux kontenerów. Sieć szkieletowa usług to orchestrator wiedzieć, stanowe, kontenera danych.
* Wdrażanie aplikacji w sekundach o wysokiej gęstości z setkami lub tysiącami aplikacji lub kontenery dla poszczególnych komputerów.
* Wdrażanie różnych wersji hello tej samej aplikacji obok i uaktualnić niezależnie każdej aplikacji.
* Zarządzanie cyklem życia hello aplikacji bez żadnych przestojów, w tym aktualizacje krytyczne i nierozdzielających.
* Skalowanie w poziomie oraz skalowanie hello liczby węzłów w klastrze. Podczas skalowania węzłów, aplikacje są skalowane automatycznie.
* Monitorowanie i diagnozowanie hello kondycji aplikacji oraz ustawić zasady wykonywania automatycznej naprawy.
* Obejrzyj równoważenia zasobów hello organizowania hello rozpowszechnianie aplikacji hello klastrze. Sieć szkieletowa usług odzyskiwania z błędami i optymalizuje hello rozkład obciążenia na podstawie dostępnych zasobów.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
* Więcej informacji:
  * [Dlaczego mikrousług podejścia toobuilding aplikacji?](service-fabric-overview-microservices.md)
  * [Terminologia — omówienie](service-fabric-technical-overview.md)
* Konfigurowanie sieci szkieletowej usług [Środowisko deweloperskie](service-fabric-get-started.md)  
* Uzyskaj informacje o [opcjach pomocy technicznej usługi Service Fabric](service-fabric-support.md)

[Image1]: media/service-fabric-overview/Service-Fabric-Overview.png
