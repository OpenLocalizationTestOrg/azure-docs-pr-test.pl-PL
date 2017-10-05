---
title: "Omówienie sieci szkieletowej usług i kontenery | Dokumentacja firmy Microsoft"
description: "Omówienie sieci szkieletowej usług i korzystanie z kontenerów do wdrażania aplikacji mikrousługi. Ten artykuł zawiera omówienie sposobu użycia kontenery oraz możliwości dostępne w sieci szkieletowej usług."
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
ms.openlocfilehash: f770b6181a99d24ea6a6e945d505da914e1b6128
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="service-fabric-and-containers"></a>Sieć szkieletowa usług i kontenerów
> [!NOTE]
> Ta funkcja jest dostępna w wersji zapoznawczej dla systemu Linux.  Wdrażanie kontenerów do sieci szkieletowej usług klastra w systemie Windows 10 nie jest obsługiwane, ale (wkrótce). 
>   

## <a name="introduction"></a>Wprowadzenie
Sieć szkieletowa usług Azure to [orchestrator](service-fabric-cluster-resource-manager-introduction.md) usługi w klastrze maszyn z wielu lat użycia i optymalizację na ogromną skalę usług firmy Microsoft. Usługi mogą być opracowane na wiele sposobów korzystania z [usługi sieć szkieletowa modele programowania](service-fabric-choose-framework.md) wdrażanie [pliki wykonywalne gościa](service-fabric-deploy-existing-app.md). Domyślnie usługi sieć szkieletowa wdraża i aktywuje tych usług jako procesów. Procesy Podaj najszybszym aktywacji i najwyższy gęstość użycia zasobów w klastrze. Sieć szkieletowa usług można także wdrożyć usługi kontenera obrazów. Ważne można mieszać usług w procesach i usług w kontenerach w tej samej aplikacji. 

## <a name="containers-and-service-fabric-roadmap"></a>Kontenery i plan sieci szkieletowej usług
W przyszłych wersjach wiele ulepszeń są planowane do aranżacji kontenera z sieci szkieletowej usług. Ulepszenia obejmują funkcje dla rozszerzonych sieci z obsługą sieci wirtualnych w aplikacji, funkcje zabezpieczeń, ulepszoną diagnostykę i narzędzia pomocy technicznej. Sieć szkieletowa usług służy do tworzenia aplikacji mieszanie kontenery spakować z istniejącego kodu (na przykład aplikacji MVC usług IIS) z usługami utworzony przy użyciu usługi Service Fabric modele programowania.  Takie aplikacje można uruchomić w jednym klastrze. 

## <a name="what-are-containers"></a>Co to są kontenerami?
Kontenery są hermetyzowany, indywidualnie do wdrożenia składników działających jako izolowanych wystąpień w tej samej jądra, aby móc korzystać z wirtualizacji, który zawiera system operacyjny. W związku z tym każdej aplikacji i bibliotek środowiska uruchomieniowego, zależności i system uruchomienia wewnątrz kontenera pełne, prywatny dostęp do widoku kontenera własnych izolowane konstrukcji systemu operacyjnego. Wraz z przenośnością poziomu izolacji zabezpieczeń i zasobów jest głównym korzyści korzystania z usługi Service Fabric uruchamianego w przeciwnym razie usług w procesach przy użyciu kontenerów.

Kontenery są technologii wirtualizacji, która Wirtualizuje system operacyjny z aplikacji. Kontenery dostarczenia niezmienne środowiska aplikacji do uruchamiania w różnym stopniu izolacji. Kontenery działają bezpośrednio jądra i izolowane widok systemu plików i innych zasobów. Kontenery w porównaniu do maszyn wirtualnych, ma następujące zalety:

* **Mała**: kontenery Użyj jednego miejsca i wersji warstwy i aktualizacje, aby zwiększyć wydajność.
* **Szybkie**: kontenery nie trzeba uruchomić całego systemu operacyjnego, więc mogą rozpocząć znacznie szybciej, zwykle w sekundach.
* **Przenośność**: obraz konteneryzowanych aplikacji można przenieść do uruchamiania w chmurze lokalnie w maszynach wirtualnych lub bezpośrednio na maszyny fizyczne.
* **Zarządzanie zasobów**: kontener może ograniczyć zasoby fizyczne, które może zużyć na jej hosta.

## <a name="container-types"></a>Typy kontenera
Sieć szkieletowa usług obsługuje kontenery na systemie Linux i Windows i obsługuje również trybem izolacji funkcji Hyper-V na drugie. 

### <a name="docker-containers-on-linux"></a>Kontenery docker w systemie Linux
Docker zapewnia wysokiego poziomu interfejsy API umożliwiające tworzenie i zarządzanie nimi kontenerów na górze kontenery jądra systemu Linux. Centrum docker jest centralnym repozytorium do przechowywania i pobierania obrazów kontenera.
Samouczek, zobacz [wdrożenia kontenera Docker sieci szkieletowej usług](service-fabric-get-started-containers-linux.md).

### <a name="windows-server-containers"></a>Kontenery systemu Windows Server
Windows Server 2016 oferuje dwa różne typy kontenerów, które różnią się na poziomie izolacji podana. Kontenery systemu Windows Server i Docker kontenery są podobne, ponieważ zarówno ma przestrzeń nazw i plik izolacji systemu, ale udostępniać jądra hosta, na którym jest uruchomiona na. W systemie Linux izolacja tradycyjnie została dostarczona przez `cgroups` i `namespaces`, i kontenery systemu Windows Server zachowują się podobnie.

Kontenery funkcji Hyper-V systemu Windows zawiera więcej izolacji i zabezpieczeń, ponieważ każdego kontenera nie udostępnia jądra systemu operacyjnego z innych kontenery lub z hosta. Z wyższego poziomu izolacji zabezpieczeń funkcji Hyper-V kontenery są przeznaczone do szkodliwy, wielodostępnym scenariusze.
Samouczek, zobacz [wdrożenia kontenera systemu Windows w sieci szkieletowej usług](service-fabric-get-started-containers.md).

Na poniższej ilustracji przedstawiono różne typy dostępnych w systemie operacyjnym poziomów wirtualizacji i izolacji.
![Platforma sieci szkieletowej usług][Image1]

## <a name="scenarios-for-using-containers"></a>Scenariusze korzystania z kontenerów
Poniżej przedstawiono typowe przykłady gdzie jest dobrym rozwiązaniem, kontener:

* **Usługi IIS Podnieś i przesunięcia**: Jeśli masz istniejące [ASP.NET MVC](https://www.asp.net/mvc) aplikacje, które mają w dalszym ciągu korzystać, umieść je w kontenerze zamiast migracji je do platformy ASP.NET Core. Te aplikacje ASP.NET MVC zależeć na Internet Information Services (IIS). Można spakować te aplikacje do kontenera obrazów z precreated obrazu usług IIS, a następnie wdrożyć je z sieci szkieletowej usług. Zobacz [kontener obrazów w systemie Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/quick_start/quick_start_images) informacji o sposobie tworzenia obrazów usług IIS.
* **Mieszać kontenery i sieci szkieletowej usług mikrousług**: Użyj istniejącego obrazu kontenera części aplikacji. Na przykład może użyć [kontener NGINX](https://hub.docker.com/_/nginx/) dla frontonu sieci web, aplikacji i usług stanowych do bardziej intensywnie obliczeń zaplecza.
* **Ograniczenia wpływu usług "zakłócenia sąsiadów"**: możliwości zarządzania zasób kontenerów służy do ograniczania zasobów używanych przez usługi na hoście. Jeśli usługi może korzystać z wielu zasobów i negatywnie wpłynąć na wydajność innych (na przykład operacji długotrwałych, typu kwerendy), należy rozważyć wprowadzenie tych usług do kontenerów, które mają ładu zasobów.

## <a name="service-fabric-support-for-containers"></a>Obsługa sieci szkieletowej usług dla kontenerów
Sieć szkieletowa usług obecnie obsługuje wdrażanie kontenerów Docker kontenerów systemu Linux i Windows Server w systemie Windows Server 2016, wraz z możliwością w trybie izolacji funkcji Hyper-V. 

W sieci szkieletowej usług [model aplikacji](service-fabric-application-model.md), kontener reprezentuje hosta aplikacji, w których wiele usługi repliki są umieszczane. Usługi sieć szkieletowa można uruchamiać żadnych kontenerów oraz scenariusz jest podobny do [scenariusza pliku wykonywalnego gościa](service-fabric-deploy-existing-app.md), gdy pakiet istniejącej aplikacji wewnątrz kontenera. Ten scenariusz jest często zdarza używany dla kontenerów i przykłady, uruchomienie aplikacji napisane przy użyciu dowolnego języka lub struktury, ale nie za pomocą wbudowanych modele programowania sieci szkieletowej usług.

Ponadto można uruchomić usługi sieć szkieletowa usług wewnątrz również kontenerów. Obsługa uruchomione usługi sieć szkieletowa usług wewnątrz kontenerów jest ograniczona, ale obecnie, aby zostać poprawione w przyszłych wersjach.

* **Niezawodne usługi bezstanowej wewnątrz kontenerów**: bezstanowej niezawodnej usługi za pomocą niezawodnych usług modele programowania są obsługiwane tylko w systemie Linux. Obsługa usługi bezstanowej niezawodnej w kontenerach systemu Windows jest planowane w przyszłości.
* **Usługi stanowej wewnątrz kontenerów**: te usługi korzystają z modelu programowania Reliable Actors lub niezawodne usługi. Pomocy technicznej na uruchamianie usług stanowych w kontenerach zostanie dodana w przyszłych wersji.

Sieć szkieletowa usług ma kilka możliwości kontenera, które pomagają tworzyć aplikacje, które składają się z mikrousług, które są konteneryzowanych. Sieć szkieletowa usług oferuje następujące możliwości konteneryzowanych usług:

* Kontener obrazu wdrożenia i aktywacji.
* Zarządzanie zasobów.
* Uwierzytelnianie repozytorium.
* Port kontenera do mapowania port hosta.
* Odnajdywanie kontenera do kontenera i komunikacji.
* Możliwość konfigurowania i ustaw zmienne środowiskowe.

## <a name="next-steps"></a>Następne kroki
W tym artykule przedstawiono o kontenerów, sieć szkieletowa usług to kontener programu orchestrator, czy tej usługi Service Fabric zawiera funkcje, które obsługuje kontenery. Jako kolejny krok możemy będą przekazywane przykłady każdą z funkcji pokazanie sposobu ich używania.

[Wdrażanie kontenera systemu Windows w sieci szkieletowej usług w systemie Windows Server 2016](service-fabric-get-started-containers.md)

[Wdrażanie kontenera Docker sieci szkieletowej usług w systemie Linux](service-fabric-get-started-containers-linux.md)

[Image1]: media/service-fabric-containers/Service-Fabric-Types-of-Isolation.png
