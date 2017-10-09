---
title: "aaaOverview sieci szkieletowej usług i kontenery | Dokumentacja firmy Microsoft"
description: "Omówienie sieci szkieletowej usług i hello Użyj kontenery toodeploy mikrousługi aplikacji. Ten artykuł zawiera omówienie sposobu kontenery mogą być używane i hello możliwości dostępne w sieci szkieletowej usług."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: c98b3fcb-c992-4dd9-b67d-2598a9bf8aab
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: fce94c4b476351c90f23f706aab8bc17319cce22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-and-containers"></a>Sieć szkieletowa usług i kontenerów
> [!NOTE]
> Ta funkcja jest dostępna w wersji zapoznawczej dla systemu Linux.  Wdrażanie kontenerów tooa klastra sieci szkieletowej usług w systemie Windows 10 nie jest obsługiwane, ale (wkrótce). 
>   

## <a name="introduction"></a>Wprowadzenie
Sieć szkieletowa usług Azure to [orchestrator](service-fabric-cluster-resource-manager-introduction.md) usługi w klastrze maszyn z wielu lat użycia i optymalizację na ogromną skalę usług firmy Microsoft. Usługi mogą być opracowane na wiele sposobów, używana jest hello [usługi sieć szkieletowa modele programowania](service-fabric-choose-framework.md) toodeploying [pliki wykonywalne gościa](service-fabric-deploy-existing-app.md). Domyślnie usługi sieć szkieletowa wdraża i aktywuje tych usług jako procesów. Procesy Podaj hello najszybszym aktywacji i najwyższy użycia gęstość hello zasobów w klastrze. Sieć szkieletowa usług można także wdrożyć usługi kontenera obrazów. Ważne, można mieszać usług w procesach i usług w kontenerach w hello tej samej aplikacji. 

## <a name="containers-and-service-fabric-roadmap"></a>Kontenery i plan sieci szkieletowej usług
W przyszłych wersjach wiele ulepszeń są planowane do aranżacji kontenera z sieci szkieletowej usług. Ulepszenia obejmują funkcje dla rozszerzonych sieci z obsługą sieci wirtualnych w aplikacji, funkcje zabezpieczeń, ulepszoną diagnostykę i narzędzia pomocy technicznej. Sieć szkieletowa usług umożliwia aplikacji toocreate mieszanie kontenery z istniejącego kodu (na przykład aplikacji MVC usług IIS) z usługami utworzony przy użyciu modele programowania hello sieci szkieletowej usług.  Takie aplikacje można uruchomić w jednym klastrze. 

## <a name="what-are-containers"></a>Co to są kontenerami?
Kontenery są hermetyzowane, indywidualnie do wdrożenia składników, które działają jako izolowanych wystąpień na hello tego samego jądra tootake zaletą wirtualizacji, który zawiera system operacyjny. W związku z tym każdej aplikacji i jej bibliotek środowiska uruchomieniowego, zależności i system Uruchom wewnątrz kontenera z widokiem kontenera własnych izolowane toohello pełny dostęp prywatnej konstrukcji systemu operacyjnego. Wraz z przenośnością poziomu izolacji zabezpieczeń i zasobu nie przynosi hello głównego pomocą kontenerów sieci szkieletowej usług, uruchamianego w przeciwnym razie usług w procesach.

Kontenery są technologii wirtualizacji, która Wirtualizuje hello system operacyjny z aplikacji. Kontenery dostarczenia niezmienne środowiska aplikacji toorun różnym stopniu izolacji. Kontenery Uruchom bezpośrednio na powitania jądra i mają odizolowane widoku hello systemu plików i innych zasobów. W porównaniu toovirtual maszyny kontenery mają hello następujące korzyści:

* **Mała**: kontenery, użyj jednego miejsca i warstwy wersje i aktualizacje tooincrease wydajność magazynu.
* **Szybkie**: kontenery nie mają tooboot całego systemu operacyjnego, więc mogą rozpocząć znacznie szybciej, zwykle w sekundach.
* **Przenośność**: obraz konteneryzowanych aplikacji można przenieść toorun w chmurze hello, lokalnie w maszynach wirtualnych lub bezpośrednio na maszyny fizyczne.
* **Zarządzanie zasobów**: kontener może ograniczyć hello zasoby fizyczne, które może zużyć na jej hosta.

## <a name="container-types"></a>Typy kontenera
Sieć szkieletowa usług obsługuje kontenery na systemie Linux i Windows i obsługuje również trybem izolacji funkcji Hyper-V na powitania ostatnie. 

### <a name="docker-containers-on-linux"></a>Kontenery docker w systemie Linux
Docker zapewnia wysokiego poziomu toocreate interfejsów API kontenerów i zarządzanie nimi na górze kontenery jądra systemu Linux. Centrum docker jest toostore centralnym repozytorium i pobrać obrazy kontenera.
Samouczek, zobacz [wdrażanie tooService kontenera Docker sieci szkieletowej](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Kontenery systemu Windows Server
Windows Server 2016 udostępnia dwa różne typy kontenerów, które różnią się w hello poziom izolacji podana. Kontenery systemu Windows Server i Docker kontenery są podobne, ponieważ mają przestrzeni nazw i plik systemu izolacji, ale udziału hello jądra z hostem hello, w którym jest uruchomiona na. W systemie Linux izolacja tradycyjnie została dostarczona przez `cgroups` i `namespaces`, i kontenery systemu Windows Server zachowują się podobnie.

Kontenery funkcji Hyper-V systemu Windows zawiera więcej izolacji i zabezpieczeń, ponieważ inne kontenery lub hosta hello każdego kontenera nie udostępnia hello jądra systemu operacyjnego. Z wyższego poziomu izolacji zabezpieczeń funkcji Hyper-V kontenery są przeznaczone do szkodliwy, wielodostępnym scenariusze.
Samouczek, zobacz [wdrażania systemu Windows tooService kontenera sieci szkieletowej](service-fabric-get-started-containers.md).

Witaj poniższej ilustracji przedstawiono hello różne typy dostępnych w systemie operacyjnym hello poziomów wirtualizacji i izolacji.
![Platforma sieci szkieletowej usług][Image1]

## <a name="scenarios-for-using-containers"></a>Scenariusze korzystania z kontenerów
Poniżej przedstawiono typowe przykłady gdzie jest dobrym rozwiązaniem, kontener:

* **IIS Podnieś i przesunięcia**: Jeśli masz istniejące [ASP.NET MVC](https://www.asp.net/mvc) aplikacje, które mają toocontinue toouse, umieść je w kontenerze zamiast migracji ich tooASP.NET Core. Te aplikacje ASP.NET MVC zależeć na Internet Information Services (IIS). Można spakować te aplikacje do kontenera obrazów z hello precreated obraz usług IIS, a następnie wdrożyć je z sieci szkieletowej usług. Zobacz [kontener obrazów w systemie Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) informacje na temat toocreate obrazów usług IIS.
* **Mieszać kontenery i sieci szkieletowej usług mikrousług**: Użyj istniejącego obrazu kontenera części aplikacji. Na przykład może użyć hello [kontener NGINX](https://hub.docker.com/_/nginx/) dla hello frontonu sieci web aplikacji i usług stanowych hello bardziej intensywnie obliczeń zaplecza.
* **Ograniczenia wpływu usług "zakłócenia sąsiadów"**: korzystając z możliwości zarządzania zasobów hello kontenery toorestrict hello zasobów używanych przez usługi na hoście. Jeśli usługi może korzystać z wielu zasobów i negatywnie wpłynąć na wydajność hello innych (na przykład operacji długotrwałych, typu kwerendy), należy rozważyć wprowadzenie tych usług do kontenerów, które mają ładu zasobów.

## <a name="service-fabric-support-for-containers"></a>Obsługa sieci szkieletowej usług dla kontenerów
Sieć szkieletowa usług obecnie obsługuje wdrażanie kontenerów Docker kontenerów systemu Linux i Windows Server w systemie Windows Server 2016, wraz z możliwością w trybie izolacji funkcji Hyper-V. 

W sieci szkieletowej usług hello [model aplikacji](service-fabric-application-model.md), kontener reprezentuje hosta aplikacji, w których wiele usługi repliki są umieszczane. Sieć szkieletowa usług można uruchamiać żadnych kontenerów i scenariusz hello jest podobne toohello [scenariusza pliku wykonywalnego gościa](service-fabric-deploy-existing-app.md), gdy pakiet istniejącej aplikacji wewnątrz kontenera. Ten scenariusz jest hello wspólnej przypadek użycia dla kontenerów i przykłady, uruchomienie aplikacji napisane przy użyciu dowolnego języka lub struktury, ale nie za pomocą wbudowanych modele programowania hello sieci szkieletowej usług.

Ponadto można uruchomić usługi sieć szkieletowa usług wewnątrz również kontenerów. Obsługa uruchomione usługi sieć szkieletowa usług wewnątrz kontenerów wynosi obecnie, ale toobe rozszerzone w przyszłych wersjach.

* **Niezawodne usługi bezstanowej wewnątrz kontenerów**: bezstanowej niezawodnej usługi za pomocą usług niezawodnej hello modele programowania są obsługiwane tylko w systemie Linux. Obsługa usługi bezstanowej niezawodnej w kontenerach systemu Windows jest planowane w przyszłości.
* **Usługi stanowej wewnątrz kontenerów**: hello Reliable Actors lub niezawodne usługi model programowania używać tych usług. Pomocy technicznej na uruchamianie usług stanowych w kontenerach zostanie dodana w przyszłych wersji.

Sieć szkieletowa usług ma kilka możliwości kontenera, które pomagają tworzyć aplikacje, które składają się z mikrousług, które są konteneryzowanych. Sieć szkieletowa usług oferuje następujące funkcje dla usług konteneryzowanych hello:

* Kontener obrazu wdrożenia i aktywacji.
* Zarządzanie zasobów.
* Uwierzytelnianie repozytorium.
* Mapowanie portów toohost port kontenera.
* Odnajdywanie kontenera do kontenera i komunikacji.
* Możliwość tooconfigure i ustaw zmienne środowiskowe.

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono o kontenerów, sieć szkieletowa usług to kontener programu orchestrator, czy tej usługi Service Fabric zawiera funkcje, które obsługuje kontenery. Jako kolejny krok, możemy będą przekazywane przykłady każdego tooshow funkcje hello należy jak toouse je.

[Wdrażanie systemu Windows tooService kontenera sieci szkieletowej w systemie Windows Server 2016](service-fabric-get-started-containers.md)

[Wdrażanie tooService kontenera Docker sieci szkieletowej w systemie Linux](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
