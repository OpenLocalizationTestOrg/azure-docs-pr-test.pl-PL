---
title: "więcej informacji na temat usługi Azure Service Fabric aaaLearn | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat hello podstawowych pojęć i głównych obszarów sieci szkieletowej usług Azure. Zawiera omówienie rozszerzonej platformy Service Fabric i w jaki sposób toocreate mikrousług."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/14/2017
ms.author: ryanwi
ms.openlocfilehash: 7fe8de777755be11635912613bb5b970e3fe3ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="so-you-want-toolearn-about-service-fabric"></a>Dlatego ma toolearn o sieci szkieletowej usług?
Sieć szkieletowa usług Azure to platforma systemów rozproszonych, dzięki którym toopackage łatwe, wdrażanie i zarządzanie mikrousług skalowalne i niezawodne.  Sieć szkieletowa usług ma dużej powierzchni, jednak i jest znacznie toolearn.  Ten artykuł przedstawia streszczenie sieci szkieletowej usług oraz hello podstawowe koncepcje, modeli, cyklem życia aplikacji, testowania, klastrów, monitorowanie kondycji i programowania. Witaj odczytu [omówienie](service-fabric-overview.md) i [co to są mikrousług?](service-fabric-overview-microservices.md) wprowadzenie i jak sieci szkieletowej usług mogą być używane toocreate mikrousług. W tym artykule nie zawiera pełną listę zawartości, ale łącze toooverview i pobieranie rozpoczęte artykułów dla każdej części sieci szkieletowej usług. 

## <a name="core-concepts"></a>Kluczowe pojęcia
[Terminologia usługi sieć szkieletowa](service-fabric-technical-overview.md), [model aplikacji](service-fabric-application-model.md), i [obsługiwane modele programowania](service-fabric-choose-framework.md) zapewniają większą pojęcia i opisy, ale w tym miejscu są hello podstawy.

<table><tr><th>Kluczowe pojęcia</th><th>Czas projektowania</th><th>W czasie wykonywania</th></tr>
<tr><td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/CoreConceptsVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tlkI046yC_2906218965"><img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td>
<td><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=x7CVH56yC_1406218965">
<img src="./media/service-fabric-content-roadmap/RunTimeVid.png" WIDTH="240" HEIGHT="162"></a></td></tr>
</table>

### <a name="design-time-application-type-service-type-application-package-and-manifest-service-package-and-manifest"></a>Czas projektowania: typ aplikacji, typ usługi, pakiet aplikacji i manifest, pakiet usługi i manifestu
Typem aplikacji jest hello nazwa/wersja przypisane tooa kolekcję typów usług. To jest zdefiniowany w *ApplicationManifest.xml* pliku, który jest osadzony w katalogu pakietu aplikacji. Witaj pakiet aplikacji jest następnie skopiowana klastra sieci szkieletowej usług toohello magazynu obrazów. Następnie można utworzyć nazwanego aplikacji tego typu aplikacji, która następnie działa w klastrze hello. 

Typ usługi jest przypisany hello nazwa/wersja pakiety kodu tooa usługi, danych i konfiguracji pakietów. To jest zdefiniowany w pliku ServiceManifest.xml jest osadzony w katalogu pakietów usługi. Witaj katalogu pakietu usługi jest następnie odwołuje się pakietu aplikacji *ApplicationManifest.xml* pliku. W ramach klastra hello po utworzeniu aplikacji o nazwie, można utworzyć nazwanego usługi z jednego z hello typów usługi typu aplikacji. Typ usługi jest opisane przez jego *ServiceManifest.xml* pliku. Typ usługi Hello składa się z ustawienia konfiguracji usługi kodu wykonywalnego, które są ładowane w czasie wykonywania, a dane statyczne, które jest używane przez usługę hello.

![Typy aplikacji usługi Service Fabric i usługi][cluster-imagestore-apptypes]

Witaj pakiet aplikacji jest katalogu dysku zawierającego typ aplikacji hello *ApplicationManifest.xml* pliku, który odwołuje się do hello pakietów usług dla każdego typu usług, tworzącą hello typu aplikacji. Na przykład pakiet aplikacji dla typu aplikacji poczty e-mail mogą zawierać odwołań tooa kolejki usługi pakietu, pakietu usług frontonu i bazy danych pakietu usług. Hello pliki w katalogu pakietu aplikacji hello są magazynu obrazu klastra sieci szkieletowej usług toohello skopiowane. 

Pakiet usługi jest katalogiem dysku zawierającego typ usługi hello *ServiceManifest.xml* pliku, który odwołuje się do kodu hello, danych statycznych i konfiguracji pakietów hello typu usługi. Witaj pliki w katalogu pakietów hello usługi odwołuje się typ aplikacji hello *ApplicationManifest.xml* pliku. Na przykład pakiet usługi może odnosić się zarówno kod toohello, dane statyczne i pakiety konfiguracji, które tworzą usługi bazy danych.

### <a name="run-time-clusters-and-nodes-named-applications-named-services-partitions-and-replicas"></a>Czas wykonywania: klastry i węzły o nazwie aplikacji o nazwie usług, partycji i replik
[Klaster usługi Service Fabric](service-fabric-deploy-anywhere.md) jest połączonym z siecią zestawem maszyn wirtualnych lub fizycznych, w którym wdraża się mikrousługi i nimi zarządza. Klastrów można skalować toothousands maszyn.

Komputer lub maszynę Wirtualną, która jest częścią klastra jest nazywany węzłem. Każdy węzeł przypisano nazwę węzła (ciąg). Węzły mają właściwości, takie jak właściwości umieszczania. Każdy komputer lub maszyna wirtualna jest automatycznie uruchamiana usługa systemu Windows, `FabricHost.exe`, której zacznie działać po rozruchu, a następnie uruchamia dwa pliki wykonywalne: `Fabric.exe` i `FabricGateway.exe`. Te dwa pliki wykonywalne tworzą hello węzła. Do rozwoju lub testowania scenariuszy może obsługiwać wiele węzłów na jednym komputerze lub maszynie Wirtualnej, uruchamiając wiele wystąpień `Fabric.exe` i `FabricGateway.exe`.

Aplikacja o nazwie jest kolekcję o nazwie usług wykonuje niektórych funkcji lub funkcji. Usługa wykonuje funkcję pełny i autonomiczne (go można uruchomić i przeprowadzić niezależnie od innych usług) i składa się z kodu, konfiguracji i danych. Po pakietu aplikacji jest skopiowany toohello obrazu magazyn, należy utworzyć wystąpienie aplikacji hello w ramach klastra hello określając pakiet aplikacji hello typu aplikacji (przy użyciu jego nazwa/wersja). Każde wystąpienie typu aplikacji jest przypisany nazwa identyfikatora URI, który wygląda jak *fabric: / MyNamedApp*. W ramach klastra można utworzyć wiele aplikacji o nazwie z typem pojedynczej aplikacji. Można również utworzyć nazwanego aplikacje z typów inną aplikację. Każda aplikacja o nazwie jest niezależnie zarządzane i numerów wersji.

Po utworzeniu aplikacji o nazwie, można utworzyć wystąpienia jednego z jego typów usług (usługa o nazwie) w klastrze hello, określając hello typ usługi (za pomocą jego nazwa/wersja). Każdego wystąpienia typu usługi przypisano nazwę identyfikatora URI zakres w obszarze jej aplikację o nazwie identyfikatora URI. Na przykład, jeśli tworzysz "Mojabazadanych" o nazwie service w "MyNamedApp" o nazwie aplikacji hello URI wygląda: *fabric: / MyNamedApp/mojabazadanych*. W ramach aplikacji o nazwie można utworzyć co najmniej jedną usługę o nazwie. Każda usługa o nazwie może być schemat partycji i liczby wystąpień/repliki. 

Istnieją dwa typy usług: bezstanowych i stanowych. Usługi bezstanowej można przechowywać trwały stan usługi magazynu zewnętrznego, takiego jak magazyn Azure, baza danych SQL Azure lub bazy danych Azure rozwiązania Cosmos. Użyj usługi bezstanowej, gdy usługa hello ma nie magazynu trwałego na wszystkich. Usługi stanowej używa usługi sieć szkieletowa toomanage stanu usługi za pośrednictwem jej wiarygodnych kolekcje lub Reliable Actors modele programowania. 

Podczas tworzenia usługi o nazwie, należy określić schemat partycji. Usługi z dużą ilością stanu podzielić hello danych na partycji. Każda partycja jest odpowiedzialny za część hello stanu ukończenia hello usługi, które jest dystrybuowane między węzłami klastra hello. W partycji bezstanowych usługi o nazwie jest wystąpień podczas stanowych usług o nazwie jest replik. Zazwyczaj bezstanowych usługi o nazwie istniało tylko jedną partycję, ponieważ mają one nie stan wewnętrzny. Obsługa stateful o nazwie usługi ich stan w obrębie repliki i każda partycja ma własną zestawu replik. Operacje odczytu i zapisu są wykonywane w jednej replice (nazywane hello podstawowym). Toostate zmiany z zapisu, które operacje są replikowane toomultiple innych replik (nazywane aktywne pomocnicze bazy danych). 

Witaj Poniższy diagram przedstawia hello relacji między aplikacjami i wystąpień usług, partycji i replik.

![Partycji i replik w ramach usługi][cluster-application-instances]

### <a name="partitioning-scaling-and-availability"></a>Podział na partycje, skalowanie i dostępności
[Partycjonowanie](service-fabric-concepts-partitioning.md) nie jest unikatowy tooService sieci szkieletowej. Formularz dobrze znanych partycjonowania jest podział danych lub dzielenia na fragmenty. Usługi stanowe z dużą ilością stanu podzielić hello danych na partycji. Każda partycja jest odpowiedzialny za część hello stan ukończenia hello usługi. 

Hello replik każdej partycji są rozkładane na węzłach klastra hello, co pozwala stan usługi o nazwie zbyt[skali](service-fabric-concepts-scalability.md). Danych hello wymogów, partycje powiększania i sieci szkieletowej usług rebalances partycje między węzłami toomake efektywne wykorzystanie zasobów sprzętowych. Po dodaniu nowego klastra toohello węzłów sieci szkieletowej usług będzie ponowne zrównoważenie replik partycji hello między hello zwiększenie liczby węzłów. Ogólne poprawia wydajność aplikacji i zmniejsza rywalizacji o toomemory dostępu. Jeśli nie są wydajnie używane hello węzłów w klastrze hello, można zmniejszyć hello liczby węzłów w klastrze hello. Sieć szkieletowa usług ponownie rebalances replik partycji hello między hello zmniejszyć liczbę węzłów toomake lepsze wykorzystanie sprzętu hello w każdym węźle.

W partycji bezstanowych usługi o nazwie jest wystąpień podczas stanowych usług o nazwie jest replik. Zazwyczaj bezstanowych usługi o nazwie istniało tylko jedną partycję, ponieważ mają one nie stan wewnętrzny. Podaj wystąpienia partycji Hello [dostępności](service-fabric-availability-services.md). Jeśli jedno wystąpienie nie powiedzie się, inne wystąpienia kontynuował normalne toooperate, a następnie sieć szkieletowa usług tworzy nowe wystąpienie. Obsługa stateful o nazwie usługi ich stan w obrębie repliki i każda partycja ma własną zestawu replik. Operacje odczytu i zapisu są wykonywane w jednej replice (nazywane hello podstawowym). Toostate zmiany z zapisu, które operacje są replikowane toomultiple innych replik (nazywane aktywne pomocnicze bazy danych). Replika ulegnie awarii, sieć szkieletowa usług tworzy nową replikę z istniejących replik hello.

## <a name="stateless-and-stateful-microservices-for-service-fabric"></a>Bezstanowe i stanowe mikrousług dla sieci szkieletowej usług
Sieć szkieletowa usług umożliwia toobuild aplikacji, które składają się z mikrousług lub kontenerów. Bezstanowe mikrousług (takie jak protokół bramy i serwerów proxy sieci web) nie obsługują modyfikowalną stanu poza żądania i odpowiedzi z usługi hello. Role procesów roboczych usługi w chmurze Azure są przykładem bezstanowego usługi. Stanowe mikrousług (na przykład konta użytkowników, baz danych, urządzeń, wózkach sklepowych zakupów i kolejek) Obsługa modyfikowalna, autorytatywnych stan poza hello żądania i odpowiedzi. Współczesnych aplikacji internetowych skali składają się z kombinacji usług bezstanowych i stanowych mikrousług. 

Klucza differentation z sieci szkieletowej usług jest jego skoncentrowanie się na tworzeniu usługi stanowej, za pomocą hello [wbudowane modele programowania ](service-fabric-choose-framework.md) lub konteneryzowanych usług stanowych. Witaj [scenariuszy aplikacji](service-fabric-application-scenarios.md) opisano scenariusze hello, w których są używane usługi stanowej.

Dlaczego masz stanowe mikrousług wraz z nich bezstanowych? Witaj dwie główne przyczyny to:

* Można tworzyć wysokiej przepustowości, małe opóźnienia, przetwarzanie odpornych transakcji online (OLTP) usług przy zachowaniu kodu i danych Zamknij na hello tym samym komputerze. Przykłady są interaktywne sklepy, wyszukiwania, systemów Internetu rzeczy (IoT), systemów handlu, systemy wykrywania oszustw i przetwarzania kart kredytowych i zarządzania osobiste rekordu.
* Upraszcza projektowanie aplikacji. Stanowe mikrousług Usuń hello potrzebę dodatkowe kolejki i pamięci podręczne, które są zazwyczaj wymaganiami tooaddress hello dostępności i opóźnienia czysto bezstanowych aplikacji. Stanowe usług są naturalnie wysokiej dostępności i małe opóźnienia, co zmniejsza liczbę hello przenoszenie toomanage części w aplikacji jako całość.

## <a name="supported-programming-models"></a>Obsługiwane modele programowania
Sieć szkieletowa usług oferuje wiele sposobów toowrite i zarządzania usługami. Usługi mogą używać hello interfejsów API usługi Service Fabric tootake pełne korzystanie z funkcji i platform aplikacji hello platformy. Można także wszelkie skompilowany program wykonywalny w dowolnym języku i hostowanych w klastrze usługi sieć szkieletowa usług. Aby uzyskać więcej informacji, zobacz [obsługiwane modele programowania](service-fabric-choose-framework.md).

### <a name="containers"></a>Kontenery
Domyślnie usługi sieć szkieletowa wdraża i aktywuje usługi jako procesów. Sieć szkieletowa usług można także wdrożyć usług w [kontenery](service-fabric-containers-overview.md). Ważne, można mieszać usług w procesach i usług w kontenerach w hello tej samej aplikacji. Sieć szkieletowa usług obsługuje wdrażanie kontenerów Linux kontenery systemu Windows w systemie Windows Server 2016. Można wdrożyć istniejących aplikacji usług bezstanowych i stanowych usług w kontenerach. 

### <a name="reliable-services"></a>Reliable Services
[Niezawodne usługi](service-fabric-reliable-services-introduction.md) jest lekki framework dla usług, które integrują się z platformy sieć szkieletowa usług hello i korzystać z pełnego zestawu funkcji platformy hello zapisu. Niezawodne usługi może być bezstanowej (podobne toomost usługi platform, takich jak serwery sieci web lub roli proces roboczy w usług Azure Cloud Services), których stan jest umieszczany w zewnętrznych rozwiązania, takie jak bazy danych platformy Azure lub magazynu tabel Azure. Niezawodne usługi mogą być również stateful, gdzie bezpośrednio w samej przy użyciu kolekcji niezawodnej usługi hello jest trwały stan. Staje się stan [wysokiej dostępności](service-fabric-availability-services.md) przy użyciu replikacji i rozprowadzane za pośrednictwem [partycjonowania](service-fabric-concepts-partitioning.md)wszystkie zarządzane automatycznie przez sieć szkieletowa usług.

### <a name="reliable-actors"></a>Reliable Actors
Wbudowane niezawodne usługi, hello [niezawodnego aktora](service-fabric-reliable-actors-introduction.md) framework jest struktury aplikacji, która implementuje wzorca aktora wirtualnego hello, oparte na wzorcu projektowym aktora hello. Platforma niezawodnego aktora Hello korzysta niezależne jednostki zasobów obliczeniowych i stan z jednowątkowego wykonywania o nazwie złośliwych użytkowników. Witaj niezawodnego aktora framework zapewnia wbudowany komunikacji złośliwych użytkowników i trwałość stanu wstępnie ustawiona i skalowalnego w poziomie konfiguracji.

### <a name="aspnet-core"></a>ASP.NET Core
Sieć szkieletowa usług integruje się z [platformy ASP.NET Core](service-fabric-reliable-services-communication-aspnetcore.md) jako pierwszej klasie model programowania do tworzenia sieci web i aplikacji interfejsu API

### <a name="guest-executables"></a>Pliki wykonywalne gościa
A [pliku wykonywalnego gościa](service-fabric-deploy-existing-app.md) jest istniejący, dowolnego pliku wykonywalnego (zapisany w dowolnym języku) hostowanych w klastrze usługi sieć szkieletowa równolegle z innymi usługami. Pliki wykonywalne gościa nie łączyć bezpośrednio z interfejsów API usługi Service Fabric. Jednak są nadal korzystać z funkcji hello oferty platform, takich jak niestandardowe kondycji i załadować raportowania oraz usługi odnajdywania przez wywoływanie interfejsów API REST. Mają one również pełny cykl życia pomocy technicznej. 

## <a name="application-lifecycle"></a>Cykl życia aplikacji
Ponieważ z innych platform, aplikacji w sieci szkieletowej usług zwykle przechodzi przez hello następujące etapy: projekt, rozwoju, testowania, wdrożenia, uaktualniania, obsługi i usuwania. Sieć szkieletowa usług przewiduje hello pełnej aplikacji cyklem życia aplikacji w chmurze, od projektowania do wdrażania, zarządzania infrastrukturą i likwidowaniu tooeventual konserwacji najwyższej jakości pomoc techniczną. model usługi Hello umożliwia kilku różnych ról tooparticipate niezależnie w cyklu życia aplikacji hello. [Cykl życia aplikacji usługi sieć szkieletowa](service-fabric-application-lifecycle.md) zawiera omówienie hello interfejsów API i jak są używane przez różne role hello w hello etapy cyklu życia aplikacji usługi sieć szkieletowa hello. 

cykl życia całej aplikacji Hello można zarządzać za pomocą [poleceń cmdlet programu PowerShell](/powershell/module/ServiceFabric/), [interfejsów API języka C#](/dotnet/api/system.fabric.fabricclient.applicationmanagementclient), [interfejsów API języka Java](/java/api/system.fabric._application_management_client), i [interfejsów API REST](/rest/api/servicefabric/). Można także skonfigurować ciągłej integracji/ciągłego potoki wdrożenia za pomocą narzędzi takich jak [Visual Studio Team Services](service-fabric-set-up-continuous-integration.md) lub [Wpięć](service-fabric-cicd-your-linux-java-application-with-jenkins.md).

Witaj poniższe wideo Microsoft Virtual Academy opisano sposób toomanage cyklu użytkowania Twojej aplikacji:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=My3Ka56yC_6106218965">
<img src="./media/service-fabric-content-roadmap/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="test-applications-and-services"></a>Testowanie aplikacji i usług
toocreate naprawdę usług skali chmury jest krytyczne tooverify, że aplikacje i usługi może wytrzymać rzeczywistych błędów. Hello błędów Analysis Services jest przeznaczony do testowania usług, które są wbudowane w sieci szkieletowej usług. Z hello [usługi analiza błędów](service-fabric-testability-overview.md), można wywołać znaczenie błędów i uruchom scenariusze ukończenia testowej względem aplikacji. Te błędy i scenariuszy wykonywania i sprawdzania poprawności hello wiele stanów i przejść, które usługa może wystąpić w całym cyklu eksploatacji w sposób kontrolowany, bezpieczne i zgodne.

[Akcje](service-fabric-testability-actions.md) docelowa usługi do testowania za pomocą poszczególnych błędów. Projektant usługi można użyć je jako bloków konstrukcyjnych toowrite skomplikowane scenariuszy. Przykłady symulowane błędów:

* Uruchom ponownie toosimulate węzła dowolną liczbę sytuacji, w którym ponownego uruchomienia komputera lub maszyny Wirtualnej.
* Przenieś repliki równoważenia obciążenia toosimulate usługi stanowej, trybu failover, lub uaktualniania aplikacji.
* Wywołaj utraty kworum toocreate usługi stanowej sytuacji, gdy nie można kontynuować operacje zapisu dla, ponieważ nie ma wystarczającej liczby replik "kopii zapasowych" i "secondary" tooaccept nowych danych.
* Wywołanie toocreate usługi stanowej sytuacji, w którym całkowicie wyczyszczeniem wszystkich stanów w pamięci poza utraty danych.

[Scenariusze](service-fabric-testability-scenarios.md) złożonych operacji składają się z co najmniej jednej akcji. Hello błędów Analysis Services zawiera dwa wbudowane pełne scenariusze:

* [Scenariusz chaos](service-fabric-controlled-chaos.md)-symuluje błędów stałego, przeplotem (bezpieczne i nieprawidłowego) w całym klastrze hello przez dłuższy czas.
* [Scenariusz trybu failover](service-fabric-testability-scenarios.md#failover-test)— wersja hello chaos testu scenariusza przeznaczonego partycji określonej usługi, pozostawiając nie dotyczy innych usług.

## <a name="clusters"></a>Klastrów
[Klaster usługi Service Fabric](service-fabric-deploy-anywhere.md) jest połączonym z siecią zestawem maszyn wirtualnych lub fizycznych, w którym wdraża się mikrousługi i nimi zarządza. Klastrów można skalować toothousands maszyn. Komputer lub maszynę Wirtualną, która jest częścią klastra jest nazywany węzłem klastra. Każdy węzeł przypisano nazwę węzła (ciąg). Węzły mają właściwości, takie jak właściwości umieszczania. Każdy komputer lub maszyna wirtualna jest automatycznie uruchamiana usługa `FabricHost.exe`, której zacznie działać po rozruchu, a następnie uruchamia dwa pliki wykonywalne: Fabric.exe i FabricGateway.exe. Te dwa pliki wykonywalne tworzą hello węzła. Dla scenariuszy testowania, może obsługiwać wiele węzłów na jednym komputerze lub maszynie Wirtualnej, uruchamiając wiele wystąpień `Fabric.exe` i `FabricGateway.exe`.

Klastrów sieci szkieletowej usług mogą być tworzone na maszynach wirtualnych lub fizycznych z systemem Windows Server lub Linux. Są w stanie toodeploy i uruchamianie aplikacji sieci szkieletowej usług w każdym środowisku, w którym znajduje się zestaw komputerów systemu Windows Server lub Linux, które są połączone ze sobą: lokalnymi, Microsoft Azure lub u innego dostawcy chmury.

Witaj poniższe wideo Microsoft Virtual Academy opisano klastrów sieci szkieletowej usług:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tbuZM46yC_5206218965">
<img src="./media/service-fabric-content-roadmap/ClusterOverview.png" WIDTH="360" HEIGHT="244">
</a></center>

### <a name="clusters-on-azure"></a>Klastry na platformie Azure
Działające klastry usługi sieć szkieletowa usług Azure zapewnia integrację z innymi funkcje platformy Azure i usługi, co sprawia, że operacje i zarządzania klastra hello łatwiejsze i bardziej niezawodny. Klaster jest zasobów usługi Azure Resource Manager, więc można modelu klastrów, takich jak innymi zasobami na platformie Azure. Menedżer zasobów umożliwia również łatwe zarządzanie wszystkie zasoby używane przez klaster hello jako pojedyncza jednostka. Klastry na platformie Azure są zintegrowane z usługą Diagnostyka Azure i analizy dzienników. Typy węzłów klastra są [zestawy skalowania maszyny wirtualnej](/azure/virtual-machine-scale-sets/index), więc jest wbudowane funkcje skalowania automatycznego.

Można utworzyć klaster na platformie Azure za pośrednictwem hello [portalu Azure](service-fabric-cluster-creation-via-portal.md), z [szablonu](service-fabric-cluster-creation-via-arm.md), lub z [programu Visual Studio](service-fabric-cluster-creation-via-visual-studio.md).

Podgląd Hello sieci szkieletowej usług w systemie Linux pozwala toobuild, wdrażania i zarządzania wysoce skalowalne, wysoko dostępne aplikacje w systemie Linux, tak jak w systemie Windows. platformy Service Fabric Hello (Reliable Services i Reliable Actors) są dostępne w języku Java w systemie Linux w dodanie tooC # (.NET Core). Można również tworzyć [usługi pliku wykonywalnego gościa](service-fabric-deploy-existing-app.md) z dowolnego języka lub struktury. Ponadto hello preview obsługuje również organizowanie kontenery Docker. Kontenery docker można uruchamiać pliki wykonywalne gościa lub macierzysty usług sieci szkieletowej usług, korzystających z platformy Service Fabric hello. Aby uzyskać więcej informacji, przeczytaj [sieci szkieletowej usług w systemie Linux](service-fabric-linux-overview.md).

Ponieważ usługa Service Fabric w systemie Linux jest w wersji zapoznawczej, pewne funkcje, które są obsługiwane w systemie Windows, nie są obsługiwane w systemie Linux. toolearn, przeczytaj [różnice między sieci szkieletowej usług w systemie Linux i Windows](service-fabric-linux-windows-differences.md).

### <a name="standalone-clusters"></a>Klastry autonomiczne
Sieć szkieletowa usług przewiduje pakietu instalacyjnego, możesz toocreate autonomicznej usługi sieć szkieletowa klastrów lokalnymi lub dowolnego dostawcy chmury. Autonomiczny klastrów hello toohost swobodę klastra wszędzie tam, gdzie chcesz podać. Jeśli dane są toocompliance podmiotu lub ograniczenia prawne lub ma tookeep lokalne dane, może obsługiwać własny klastra i aplikacji. Aplikacje sieci szkieletowej usług mogą działać w wielu środowiskach hostingu bez zmian, więc swoją wiedzę na temat tworzenia aplikacji są przenoszone z jednego tooanother Środowisko hostingu. 

[Tworzenie pierwszego autonomicznej klastra sieci szkieletowej usług](service-fabric-get-started-standalone-cluster.md)

Klastry z systemem Linux autonomiczny nie są jeszcze obsługiwane.

### <a name="cluster-security"></a>Zabezpieczenia klastra
Klastry muszą być użytkownikami zabezpieczonych tooprevent nieautoryzowany łączenie tooyour klastra, szczególnie w przypadku, gdy ma na nim uruchomione obciążeń produkcyjnych. Chociaż możliwe toocreate niezabezpieczona klastra, dzięki temu użytkownicy anonimowi tooconnect tooit Jeśli punkty końcowe zarządzania są udostępniane toohello publicznej sieci internet. Nie jest możliwe toolater Włącz security w klastrze niezabezpieczona: zabezpieczeń klastra jest włączony podczas tworzenia klastra.

scenariusze zabezpieczeń klastra Hello są następujące:
* Zabezpieczenia węzła do węzła
* Węzeł klienta zabezpieczeń
* Kontrola dostępu oparta na rolach (RBAC)

Aby uzyskać więcej informacji, przeczytaj [Secure klastra](service-fabric-cluster-security.md).

### <a name="scaling"></a>Skalowanie
Po dodaniu nowego klastra toohello węzłów sieci szkieletowej usług rebalances hello replik partycji i wystąpień między hello zwiększenie liczby węzłów. Ogólne poprawia wydajność aplikacji i zmniejsza rywalizacji o toomemory dostępu. Jeśli nie są wydajnie używane hello węzłów w klastrze hello, można zmniejszyć hello liczby węzłów w klastrze hello. Sieć szkieletowa usług ponownie rebalances hello replik partycji i wystąpień między hello zmniejszyć liczbę węzłów toomake lepsze wykorzystanie sprzętu hello w każdym węźle. Możesz skalować klastrów w systemie Azure albo [ręcznie](service-fabric-cluster-scale-up-down.md) lub [programowo](service-fabric-cluster-programmatic-scaling.md). Autonomiczny klastrów mogą być skalowane [ręcznie](service-fabric-cluster-windows-server-add-remove-nodes.md).

### <a name="cluster-upgrades"></a>Uaktualnienia klastra
Okresowo są wydawane nowe wersje środowiska uruchomieniowego platformy Service Fabric hello. Wykonaj uaktualnienia środowiska uruchomieniowego lub sieci szkieletowej, w klastrze, aby zawsze działają [obsługiwana wersja](service-fabric-support.md). Ponadto uaktualnia toofabric, można także zaktualizować konfigurację klastra, takich jak certyfikaty lub porty aplikacji.

Klaster sieci szkieletowej usług jest z zasobem, który jest właścicielem, ale jest częściowo zarządzany przez firmę Microsoft. Microsoft jest odpowiedzialny za stosowania poprawek hello podstawowego systemu operacyjnego i przeprowadzanie uaktualnienia sieci szkieletowej w klastrze. Można ustawić sieci szkieletowej automatyczne tooreceive klastra uaktualnień, gdy firma Microsoft publikuje nową wersję, lub wybierz tooselect wersji obsługiwanych sieci szkieletowej, które mają. Uaktualnienia sieci szkieletowej i konfiguracji można ustawić za pomocą hello portalu Azure lub za pomocą Menedżera zasobów. Aby uzyskać więcej informacji, przeczytaj [uaktualnienia klastra usługi sieć szkieletowa](service-fabric-cluster-upgrade.md). 

Zasób jest klaster z autonomicznej tego posiadana całkowicie. Jest odpowiedzialny za stosowania poprawek hello podstawowego systemu operacyjnego i zainicjowaniu uaktualnienia sieci szkieletowej. Jeśli klaster można połączyć za[https://www.microsoft.com/download](https://www.microsoft.com/download), można ustawić pobieranie tooautomatically klastra i udostępnić hello nowej sieci szkieletowej usług pakietu środowiska wykonawczego. Następnie będzie inicjować hello uaktualnienia. Jeśli nie ma dostępu do klastra [https://www.microsoft.com/download](https://www.microsoft.com/download), możesz ręcznie pobrać hello nowe środowisko uruchomieniowe pakietu z maszyny podłączonej do Internetu i inicjuje uaktualnienie hello. Aby uzyskać więcej informacji, przeczytaj [uaktualnienia klastra usługi sieć szkieletowa autonomiczny](service-fabric-cluster-upgrade-windows-server.md).

## <a name="health-monitoring"></a>Monitorowanie kondycji
Sieć szkieletowa usług wprowadza [model kondycji](service-fabric-health-introduction.md) tooflag zła klastra oraz warunki aplikacji na konkretnych obiektów (na przykład węzłów klastra i repliki usługi). model kondycji Hello używa Raporty kondycji (składników systemu i watchdogs). Celem Hello jest łatwe i szybkie diagnozowanie i naprawy. Moduły zapisujące usługi należy toothink wyprzedzeniem o kondycji i sposobie zbyt[projektowania raportowania kondycji](service-fabric-report-health.md#design-health-reporting). Należy podać żadnych warunek, który może mieć wpływ na kondycję, zwłaszcza, jeśli może pomóc problemów flagi zamknąć toohello głównego. informacje o kondycji Hello można zapisać ilość czasu, na debugowanie i badania po hello usługa działa i działa na dużą skalę w środowisku produkcyjnym.

monitor raporty usługi sieć szkieletowa Hello określone warunki odsetek. Zgłaszają przy użyciu tych warunków na podstawie ich lokalnego widoku. Witaj [magazynu kondycji](service-fabric-health-introduction.md#health-store) agreguje dane kondycji wysyłane przez wszystkie toodetermine raporty, czy jednostki są globalnie dobrej kondycji. Hello model jest zamierzone toobe toouse sformatowanego, elastyczne i łatwe. jakość Hello raportów o kondycji hello Określa dokładność hello widoku kondycji hello hello klastra. Fałszywych alarmów, przedstawiających błędnie zła problemów może niekorzystnie wpłynąć na uaktualnienia lub innych usług używających danych kondycji. Przykładami takich usług są usługi repair i mechanizmów alertów. W związku z tym rozwagą jest tooprovide potrzebne raporty, które przechwytywania warunki zainteresowanie hello najlepsze możliwe sposób.

Raportowanie może odbywać się od:
* Witaj monitorowane repliki usługi sieć szkieletowa usług lub wystąpienia.
* Wewnętrzny watchdogs wdrożony jako usługa sieci szkieletowej usług (na przykład sieci szkieletowej usług bezstanowych Usługa monitoruje warunki i generuje raporty). Hello watchdogs można wdrożyć na wszystkich węzłach lub może być usługą skoligaconym toohello monitorowane.
* Wewnętrzny watchdogs, uruchom na powitania węzłów sieci szkieletowej usług, które nie są zaimplementowane jako usługi sieci szkieletowej usług.
* Zewnętrzne watchdogs sondowania hello zasobu z klastra sieci szkieletowej usług hello zewnętrznych (na przykład monitorowania usługi, takiej jak Gomez).

Fabrycznej hello składniki sieci szkieletowej usług Raport kondycji na wszystkich jednostek w klastrze hello. [Raportów o kondycji systemu](service-fabric-understand-and-troubleshoot-with-system-health-reports.md) zapewniają wgląd w klastra i aplikacji funkcji i flagi błędów za pomocą kondycji. Dla aplikacji i usług systemowych raportów kondycji Sprawdź, czy jednostki są zaimplementowane i są działa prawidłowo z punktu widzenia hello środowiska uruchomieniowego platformy Service Fabric hello. Raporty Hello nie zapewniają wszelkie monitorowanie kondycji hello logiki biznesowej usługi hello lub wykryć zawieszone procesy. Logika tooadd kondycji informacji tooyour określonej usługi [zaimplementować raportowania kondycji niestandardowych](service-fabric-report-health.md) w usługach.

Sieć szkieletowa usług zawiera zbyt wiele sposobów[wyświetlanie raportów kondycji](service-fabric-view-entities-aggregated-health.md) zagregowane w magazynie kondycji hello:
* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) lub innych narzędzi wizualizacji.
* Zapytań o kondycję (za pośrednictwem [PowerShell](/powershell/module/ServiceFabric/), hello [C# interfejsów API klienta fabricclient z rolą](/api/system.fabric.fabricclient.healthclient) i [interfejsów API klienta fabricclient z rolą Java](/java/api/system.fabric._health_client), lub [interfejsów API REST](/rest/api/servicefabric)).
* Ogólne zapytań, które zwraca listę podmiotów, które mają kondycji jako jedna z właściwości hello (za pośrednictwem programu PowerShell, interfejsu API hello lub REST).

Witaj następujące Microsoft Virtual Academy wideo w tym artykule opisano model kondycji sieci szkieletowej usług hello i sposobie ich użycia:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-content-roadmap/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="next-steps"></a>Następne kroki
* Dowiedz się, jak toocreate [klastra w systemie Azure](service-fabric-cluster-creation-via-portal.md) lub [autonomicznych klastrów w systemie Windows](service-fabric-cluster-creation-for-windows-server.md).
* Spróbuj utworzyć usługę za pomocą hello [niezawodne usługi](service-fabric-reliable-services-quick-start.md) lub [Reliable Actors](service-fabric-reliable-actors-get-started.md) modele programowania.
* Dowiedz się, jak za[migracji z usługi w chmurze](service-fabric-cloud-services-migration-differences.md).
* Dowiedz się zbyt[monitorowanie i diagnozowanie usług](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md). 
* Dowiedz się zbyt[testowania aplikacji i usług](service-fabric-testability-overview.md).
* Dowiedz się zbyt[zarządzania i organizowania zasobów klastra](service-fabric-cluster-resource-manager-introduction.md).
* Przejrzyj hello [przykłady usługi Service Fabric](http://aka.ms/servicefabricsamples).
* Dowiedz się więcej o [opcje pomocy technicznej usługi sieć szkieletowa](service-fabric-support.md).
* Witaj odczytu [blogu zespołu](https://blogs.msdn.microsoft.com/azureservicefabric/) dla artykułów i anonsów.


[cluster-application-instances]: media/service-fabric-content-roadmap/cluster-application-instances.png
[cluster-imagestore-apptypes]: ./media/service-fabric-content-roadmap/cluster-imagestore-apptypes.png
