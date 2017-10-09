---
title: "aaaLearn sieć szkieletowa usług Azure terminologia | Dokumentacja firmy Microsoft"
description: "Zawiera przegląd terminologia usługi sieci szkieletowej. W tym artykule omówiono kluczową terminologię pojęć i terminów używanych w hello reszty hello dokumentacji."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: chackdan;subramar
ms.assetid: 3a970679-e19e-43b3-9be8-71773f307c57
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/02/2017
ms.author: ryanwi
ms.openlocfilehash: 4781fc0527b8a58e534183249bc2759aded2730b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-terminology-overview"></a>Omówienie terminologii sieci szkieletowej usług
Sieć szkieletowa usług to platforma systemów rozproszonych, dzięki którym toopackage łatwe, wdrażanie i zarządzanie mikrousług skalowalne i niezawodne. Temat terminologię hello szczegóły używane przez usługi sieć szkieletowa toounderstand hello terminologia hello dokumentacji.

Witaj pojęcia wymienione w tej sekcji omówiono także w hello następujące filmy wideo Microsoft Virtual Academy: <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">podstawowe pojęcia</a>, <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965">pojęcia czasu projektowania</a>, i <a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">pojęcia dotyczące środowiska wykonawczego</a>.

## <a name="infrastructure-concepts"></a>Pojęcia dotyczące infrastruktury
**Klaster**: zestaw połączonych z siecią maszyn wirtualnych lub fizycznych, w których są wdrożone i zarządzane z mikrousług.  Klastrów można skalować toothousands maszyn.

**Węzeł**: komputer lub maszynę Wirtualną, która jest częścią klastra jest nazywany węzłem. Każdy węzeł przypisano nazwę węzła (ciąg). Węzły mają właściwości, takie jak właściwości umieszczania. Każdy komputer lub maszyna wirtualna jest automatycznie uruchamiana usługa systemu Windows, `FabricHost.exe`, której zacznie działać po rozruchu, a następnie uruchamia dwa pliki wykonywalne: `Fabric.exe` i `FabricGateway.exe`. Te dwa pliki wykonywalne tworzą hello węzła. Dla scenariuszy testowania, może obsługiwać wiele węzłów na jednym komputerze lub maszynie Wirtualnej, uruchamiając wiele wystąpień `Fabric.exe` i `FabricGateway.exe`.

## <a name="application-concepts"></a>Pojęcia dotyczące aplikacji
**Typ aplikacji**: hello nazwa/wersja przypisane tooa kolekcji typów usług. Zdefiniowane w `ApplicationManifest.xml` pliku, osadzony w katalogu pakietu aplikacji, która jest następnie kopiowane magazynu obrazu klastra sieci szkieletowej usług toohello. Następnie można utworzyć nazwanego aplikacji tego typu aplikacji w klastrze hello.

Witaj odczytu [Model aplikacji](service-fabric-application-model.md) artykułu, aby uzyskać więcej informacji.

**Pakiet aplikacji**: katalogu dysku zawierającego typ aplikacji hello `ApplicationManifest.xml` pliku. Odwołania hello pakietów usług dla każdego typu usług, tworzącą hello typu aplikacji. Hello pliki w katalogu pakietu aplikacji hello są magazynu obrazu klastra sieci szkieletowej tooService skopiowane. Na przykład pakiet aplikacji dla typu aplikacji poczty e-mail mogą zawierać odwołań tooa kolejki usługi pakietu, pakietu usług frontonu i bazy danych pakietu usług.

**O nazwie aplikacji**: po pakietu aplikacji jest skopiowany toohello obrazu magazyn, należy utworzyć wystąpienie aplikacji hello w ramach klastra hello określając pakiet aplikacji hello typu aplikacji (przy użyciu jego nazwa/wersja). Każde wystąpienie typu aplikacji jest przypisany nazwa identyfikatora URI, który wygląda następująco: `"fabric:/MyNamedApp"`. W ramach klastra można utworzyć wiele aplikacji o nazwie z typem pojedynczej aplikacji. Można również utworzyć nazwanego aplikacje z typów inną aplikację. Każda aplikacja o nazwie jest niezależnie zarządzane i numerów wersji.      

**Typ usługi**: hello nazwa/wersja przypisane pakiety kodu tooa usługi, danych i konfiguracji pakietów. Zdefiniowane w `ServiceManifest.xml` plików wbudowanych w katalogu pakietu usługi i katalog pakietu usługi hello następnie odwołuje się pakietu aplikacji `ApplicationManifest.xml` pliku. W ramach klastra hello po utworzeniu aplikacji o nazwie, można utworzyć nazwanego usługi z jednego z hello typów usługi typu aplikacji. Typ usługi Hello `ServiceManifest.xml` plik zawiera opis usługi hello.

Witaj odczytu [Model aplikacji](service-fabric-application-model.md) artykułu, aby uzyskać więcej informacji.

Istnieją dwa typy usług:

* **Stateless:** Użyj usługi bezstanowej, gdy stan trwały hello usługi jest przechowywana w usłudze magazynu zewnętrznego, takiego jak magazyn Azure, baza danych SQL Azure lub bazy danych Azure rozwiązania Cosmos. Użyj usługi bezstanowej, gdy usługa hello ma nie magazynu trwałego na wszystkich. Na przykład Kalkulator usługa gdzie wartości są przekazywane toohello usługi, obliczenia odbywa się przy użyciu tych wartości, a wynik jest zwracany.
* **Stateful:** usługi stanowej należy używać usługi sieć szkieletowa toomanage stan usługi za pośrednictwem jej wiarygodnych kolekcje lub Reliable Actors modele programowania. Określ, ile partycje ma toospread swój stan za pośrednictwem (skalowalność) podczas tworzenia usługi o nazwie. Również określić, ile razy tooreplicate swój stan między węzłami (na niezawodność). Każda usługa o nazwie ma jednej repliki podstawowej i wiele replik pomocniczych. Stan usługi o nazwie możesz zmodyfikować pisząc toohello repliki podstawowej. Sieć szkieletowa usług replikuje ten stan tooall hello replikach pomocniczych zachowuje swój stan synchronizacji. Sieć szkieletowa usług automatycznie wykrywa replikę podstawową kończy się niepowodzeniem i zamienia istniejąca replika podstawowa tooa repliki pomocniczej. Sieć szkieletowa usług tworzy następnie nową replikę pomocniczą.  

**Pakiet usługi**: katalogu dysku zawierającego typ usługi hello `ServiceManifest.xml` pliku. Odwołuje się do tego pliku, kod hello, dane statyczne i pakiety konfiguracji dla typu usługi hello. Witaj pliki w katalogu pakietów hello usługi odwołuje się typ aplikacji hello `ApplicationManifest.xml` pliku. Na przykład pakiet usługi może odnosić się zarówno kod toohello, dane statyczne i pakiety konfiguracji, które tworzą usługi bazy danych.

**O nazwie usługi**: po utworzeniu aplikacji o nazwie, można utworzyć wystąpienia jednego z jego typów usług w ramach klastra hello określając hello typ usługi (za pomocą jego nazwa/wersja). Każdego wystąpienia typu usługi przypisano nazwę identyfikatora URI zakres w obszarze jej aplikację o nazwie identyfikatora URI. Na przykład, jeśli tworzysz "Mojabazadanych" o nazwie service w "MyNamedApp" o nazwie aplikacji hello URI wygląda: `"fabric:/MyNamedApp/MyDatabase"`. W ramach aplikacji o nazwie można utworzyć kilka usług o nazwie. Każda usługa o nazwie może być schemat partycji i liczby wystąpień/repliki.

**Kod pakietu**: katalogu dysku zawierającego pliki wykonywalne typ usługi hello (zazwyczaj pliki EXE/DLL). Witaj plików w katalogu pakietów hello kod odwołuje się typ usługi hello `ServiceManifest.xml` pliku. Po utworzeniu usługi o nazwie hello pakietu kodu jest skopiowany toohello węzła lub hello toorun wybranych węzłów o nazwie usługi. Następnie kod hello zacznie działać. Istnieją dwa typy plików wykonywalnych pakietu kodu:

* **Pliki wykonywalne gościa**: pliki wykonywalne, który uruchamiany jako — znajduje się na powitania hosta systemu operacyjnego (Windows lub Linux). Oznacza to, że te pliki wykonywalne nie odwołanie tooor łącza nie wszystkie pliki środowiska uruchomieniowego platformy Service Fabric i w związku z tym nie należy używać żadnych modeli programowania sieci szkieletowej usług. Te pliki wykonywalne są toouse, które niektóre funkcje usługi sieć szkieletowa usług, takich jak hello naming service do odnajdywania punktu końcowego. Pliki wykonywalne gościa nie może zaraportować wystąpienie usługi tooeach określonej metryki obciążenia.
* **Pliki wykonywalne hosta usługi**: pliki wykonywalne, używanego przez usługi sieć szkieletowa programowania modeli łącząc tooService pliki środowiska uruchomieniowego sieci szkieletowej, włączenie funkcji sieci szkieletowej usług. Na przykład wystąpienie usługi o nazwie można zarejestrować punktów końcowych z usługą Naming Service Fabric i zgłaszać także metryki obciążenia.      

**Pakiet danych**: katalogu dysku zawierającego typ usługi hello dane statyczne, tylko do odczytu plików (zazwyczaj fotografii, dźwiękowe i wideo). Witaj pliki w katalogu pakietów hello danych odwołuje się typ usługi hello `ServiceManifest.xml` pliku. Po utworzeniu usługi o nazwie pakiet danych hello jest skopiowany toohello węzła lub hello toorun wybranych węzłów o nazwie usługi.  Kod Hello zacznie działać i mają dostęp do plików danych hello.

**Pakiet konfiguracji**: katalogu dysku zawierającego typ usługi hello statyczną, pliki tylko do odczytu konfiguracji (zazwyczaj pliki tekstowe). Witaj pliki w katalogu pakietu konfiguracji hello odwołuje się typ usługi hello `ServiceManifest.xml` pliku. Po utworzeniu usługi o nazwie hello pliki w pakiet konfiguracji hello są skopiowanych toohello, jeden lub więcej hello toorun wybranych węzłów o nazwie usługi. Następnie kod hello zacznie działać i mają dostęp do plików konfiguracyjnych hello.

**Kontenery**: domyślnie wdraża sieci szkieletowej usług i aktywuje usługi jako procesów. Sieć szkieletowa usług można także wdrożyć usługi kontenera obrazów. Kontenery są technologii wirtualizacji, która Wirtualizuje hello system operacyjny z aplikacji. Aplikacji i jej bibliotek środowiska uruchomieniowego, zależności i system uruchamiane wewnątrz kontenera z widokiem kontenera własnych izolowane toohello pełny dostęp prywatnej konstrukcji systemu operacyjnego. Sieć szkieletowa usług obsługuje kontenery Docker na kontenery systemu Linux i Windows Server.  Aby uzyskać więcej informacji, przeczytaj [sieci szkieletowej usług i kontenery](service-fabric-containers-overview.md).

**Schemat partycji**: podczas tworzenia nazwanego usługi, określ schemat partycji. Usługi z dużą ilością stanu podzielić danych hello na partycje, które rozprzestrzenia stanu hello na węzłach klastra hello. Dzięki temu usługa o nazwie tooscale stanu. W partycji bezstanowych usługi o nazwie jest wystąpień podczas stanowych usług o nazwie jest replik. Zazwyczaj bezstanowych usługi o nazwie istniało tylko jedną partycję, ponieważ mają one nie stan wewnętrzny. wystąpienia partycji Hello zapewnienia dostępności; Jeśli jedno wystąpienie nie powiedzie się, innych wystąpień kontynuował normalne toooperate, a następnie utworzy nowe wystąpienie usługi sieć szkieletowa usług. Stateful o nazwie usługi Obsługa ich stan w obrębie repliki, a każda partycja ma własną zestawu wszystkich stanów hello utrzymywane w synchronizacji replik. Replika ulegnie awarii, sieć szkieletowa usług tworzy nową replikę z istniejących replik hello.

Witaj odczytu [niezawodne usługi sieć szkieletowa usług partycji](service-fabric-concepts-partitioning.md) artykułu, aby uzyskać więcej informacji.

## <a name="system-services"></a>Usług systemowych
Brak usług systemowych, które są tworzone w każdym klastrze zapewniające hello możliwości platformy Service Fabric.

**Usługa nazewnictwa**: klastra sieci szkieletowej usług każdy ma usługi nazewnictwa, która rozwiązuje lokalizacji tooa nazwy usługi w klastrze hello. Zarządzanie hello usługi nazwy i właściwości, podobne tooan internet usługi nazw domen (DNS) dla hello klastra. Klienci bezpiecznego komunikowania się z w dowolnym węźle klastra hello przy użyciu hello Naming Service tooresolve nazwę usługi i jego lokalizacji.  Przenieś aplikacje w klastrze hello na przykład powodu toofailures, równoważenia zasobów lub hello rozmiaru hello klastra. Można programować usług i klientów, które rozwiązanie hello bieżącą lokalizację sieciową. Klienci uzyskać adres IP rzeczywistego maszyny hello i port, na którym jest obecnie uruchomiona.

Odczyt [komunikacja z usługami](service-fabric-connect-and-communicate-with-services.md) Aby uzyskać więcej informacji na powitania klienta i usługi komunikacji interfejsów API, które pracować z hello Naming service.

**Usługa magazynu obrazów**: klastra sieci szkieletowej usług każdy ma usługi składnika Image Store gdzie są przechowywane pakietów aplikacji wdrożonych, numerów wersji. Skopiuj toohello pakietu aplikacji magazynu obrazów, a następnie zarejestruj typ aplikacji hello zawartych w tym pakiecie aplikacji. Po udostępnieniu typ aplikacji hello można utworzyć aplikację o nazwie z niego. Po usunięciu wszystkich nazwanego aplikacji można wyrejestrować typu aplikacji z hello usługi magazynu obrazów.

Odczyt [zrozumieć ustawienie element ImageStoreConnectionString hello](service-fabric-image-store-connection-string.md) uzyskać więcej informacji o hello usługi magazynu obrazów.

Witaj odczytu [wdrażania aplikacji](service-fabric-deploy-remove-applications.md) artykułu, aby uzyskać więcej informacji na temat wdrażania usługi magazynu obrazu toohello aplikacji.

## <a name="built-in-programming-models"></a>Wbudowane modele programowania
Modele programowania .NET Framework są dostępne dla Ciebie toobuild usługi sieć szkieletowa usług:

**Niezawodne usługi**: usługi bezstanowe i stanowe toobuild interfejsu API. Usługi stanowej przechowywania ich stan w kolekcjach niezawodnej (na przykład słownika lub kolejki). Otrzymasz również tooplug w różnych stosy komunikacji, takie jak interfejsu API sieci Web i usługi Windows Communication Foundation (WCF).

**Reliable Actors**: interfejs API obiektów bezstanowe i stanowe toobuild za pośrednictwem wirtualnej modelu programowania hello aktora. W tym modelu mogą być przydatne, jeśli masz wiele niezależnych jednostki obliczeń/stanu. Ponieważ ten model korzysta z modelu wątkowości Włącz, jest najlepszym kod tooavoid, który uwidacznia tooother złośliwych użytkowników lub usług, ponieważ poszczególnych aktora nie może przetworzyć innych żądań przychodzących do momentu jego żądania wychodzącego została ukończona.

Witaj odczytu [wybierz Model programowania dla usługi](service-fabric-choose-framework.md) artykułu, aby uzyskać więcej informacji.

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Następne kroki
więcej informacji na temat sieci szkieletowej usług toolearn:

* [Omówienie sieci szkieletowej usług](service-fabric-overview.md)
* [Dlaczego mikrousług podejścia toobuilding aplikacji?](service-fabric-overview-microservices.md)
* [Scenariusze aplikacji](service-fabric-application-scenarios.md)

