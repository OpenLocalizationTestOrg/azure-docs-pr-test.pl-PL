---
title: "aaaAzure Model Hosting sieci szkieletowej usług | Dokumentacja firmy Microsoft"
description: "Opisuje relację między repliki (lub wystąpień) wdrożonej usługi sieci szkieletowej Servic i procesu hosta usługi."
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Model obsługi sieci szkieletowej usług
Ten artykuł zawiera omówienie hosting modeli dostarczonych przez sieć szkieletowa usług aplikacji, a także opis hello różnice między hello **udostępnionego procesu** i **wyłącznego procesu** modeli. Opisuje wygląd wdrożonej aplikacji na węzeł sieci szkieletowej usług i relacji między repliki (lub wystąpień) hello usługi i hello procesu hosta usługi.

Przed kontynuacją, upewnij się, że znasz [Model aplikacji sieci szkieletowej usług] [ a1] i zrozumienie różnych pojęcia i relacji między nimi. 

> [!NOTE]
> W tym artykule, dla uproszczenia chyba że jawnie wymienionych:
>
> - Wszystkie używa programu word *repliki* odwołuje się tooboth repliki usługi stanowej lub wystąpienia statless usługi.
> - *Elementu CodePackage* jest odpowiednikiem poddanego zbyt*ServiceHost* procesu, który rejestruje *ServiceType* i replik hostów usług tego *ServiceType*.
>

toounderstand hello modelu hostingu, poinformuj nas zapoznaj się z przykładem. Daj nam powiedzieć mamy *atrybutów ApplicationType* MyAppType, który ma *ServiceType* MyServiceType, który jest dostarczany przez *ServicePackage* MyServicePackage, który ma *Elementu CodePackage* MyCodePackage, która rejestruje *ServiceType* "MyServiceType" po uruchomieniu.

Załóżmy, że mamy 3 węzła klastra i utworzymy *aplikacji* **fabric: / App1** typu "MyAppType". Wewnątrz to *aplikacji* **fabric: / App1** utworzymy usługi **sieci szkieletowej: / App1/ServiceA** typu MyServiceType, która ma 2 partycjach (powiedzieć **P1**  &  **P2**) i 3 replik jednej partycji. Witaj Poniższy diagram przedstawia widok hello tej aplikacji, w jakiej kończy się wdrożonej w węźle.

<center>
![Widok węzła wdrożonej aplikacji][node-view-one]
</center>

Sieć szkieletowa usług aktywowany MyServicePackage, który rozpoczął MyCodePackage, który jest hostem repliki z obu partycji hello tj. **P1** & **P2**. Należy zauważyć, że wszystkie węzły hello w klastrze hello będzie tego samego widoku, ponieważ wybrano liczby replik na partycji toonumber równy węzłów w klastrze hello. Utwórz nową usługę **sieci szkieletowej: / App1/ServiceB** w aplikacji **sieci szkieletowej: / App1** mającego 1 partycji (powiedzieć **P3**) i 3 replik jednej partycji. Poniższy diagram przedstawia hello nowy widok w węźle hello:

<center>
![Widok węzła wdrożonej aplikacji][node-view-two]
</center>

Jak widać, Service Fabric umieszczone hello nowej repliki dla partycji **P3** usługi **fabric: / App1/ServiceB** w istniejących aktywacji "MyServicePackage" hello. Umożliwia teraz utworzyć inną *aplikacji* **sieci szkieletowej: / App2** typu "MyAppType" i wewnątrz **sieci szkieletowej: / App2** Utwórz usługę **sieci szkieletowej: / App2/ServiceA** mającego 2 partycjach (powiedzieć **P4** & **5**) i 3 replik jednej partycji. Następujące diagramy przedstawia hello nowy widok węzła:

<center>
![Widok węzła wdrożonej aplikacji][node-view-three]
</center>

Teraz usługi sieć szkieletowa aktywował nową kopię MyServicePackage, która uruchamia nową kopię "MyCodePackage" i repliki z obu partycji usługi **fabric: / App2/ServiceA** (tj. **P4**  &  **5**) są umieszczane w tej nowej kopii "MyCodePackage".

## <a name="shared-process-model"></a>Udostępnione modelu procesów
Co widzieliśmy powyżej jest domyślnym hello model udostępniane przez usługi sieć szkieletowa usług hostowania i jest określana tooas **udostępnionego procesu** modelu. W tym modelu dla danego *aplikacji*tylko jeden kopia danego *ServicePackage* została aktywowana w *węzła* (co spowoduje włączenie wszystkich hello *CodePackages* zawarte w niej) i hello wszystkich replik wszystkich usług danego *ServiceType* są umieszczane w hello *elementu CodePackage* który który rejestruje *ServiceType*. Innymi słowy, wszystkie hello replik wszystkich usług danego *ServiceType* udostępnianie hello tego samego procesu.

## <a name="exclusive-process-model"></a>Model procesu wyłączności
Witaj innych hostingu model udostępniane przez usługi sieć szkieletowa jest **wyłącznego procesu** modelu. W tym modelu na danym *węzła*, objęcia każdej repliki usługi Service Fabric aktywuje nową kopię *ServicePackage* (co spowoduje włączenie wszystkich hello *CodePackages* zawarte w niej ) i replika znajduje się w hello *elementu CodePackage* tego zarejestrowanych hello *ServiceType* z toowhich usługi hello należy repliki. Innymi słowy każda replika znajduje się w dedykowanym procesie. 

Ten model jest obsługiwana wersja 5.6 sieci szkieletowej usług. **Proces wyłącznego** modelu można wybrać w momencie hello tworzenie hello usługi (za pomocą [PowerShell][p1], [REST] [ r1]lub [klienta fabricclient z rolą][c1]), określając **ServicePackageActivationMode** jako "ExclusiveProcess".

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Jeśli korzystasz z usługi domyślne w manifeście aplikacji, możesz wybrać **wyłącznego procesu** modelu, określając **ServicePackageActivationMode** atrybutu, jak pokazano poniżej:

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
Kontynuowaniem w naszym przykładzie powyżej, umożliwia tworzenie innej usługi **fabric: / App1/ServiceC** w aplikacji **sieci szkieletowej: / App1** mającego 2 partycjach (powiedzieć **P6**  &  **P7**) i 3 replik jednej partycji z **ServicePackageActivationMode** ustawić too'ExclusiveProcess. Poniższy diagram przedstawia nowy widok w węźle hello:

<center>
![Widok węzła wdrożonej aplikacji][node-view-four]
</center>

Jak widać, Service Fabric aktywowany dwóch nowych kopii "MyServicePackage" (po jednej dla każdej repliki z partycji **P6** & **P7**) i każdej repliki jego dedykowanych kopii *Elementu CodePackage*. Inny toonote co w tym miejscu jest, gdy **wyłącznego procesu** model używany dla danego *aplikacji*, wielu kopii danego *ServicePackage* mogą być używane w  *Węzeł*. W powyżej przykładzie przedstawiono trzy kopie "MyServicePackage" i działają dla **fabric: / App1**. Każdy z tych active kopii "MyServicePackage" ma **ServicePackageAtivationId** skojarzonych z nim, który identyfikuje ją w *aplikacji* **fabric: / App1**.

Gdy tylko **udostępnionego procesu** modelu służy do *aplikacji*, takiej jak **sieci szkieletowej: / App2** w powyżej przykład istnieje tylko jedna kopia active *ServicePackage*  na *węzła* i **ServicePackageAtivationId** w przypadku tego aktywacji *ServicePackage* jest "pustego ciągu".

> [!NOTE]
>- **Udostępnione procesu** model hostowania odpowiada za**ServicePackageAtivationMode** równy **SharedProcess**. Jest to domyślna hello model hostowania i **ServicePackageAtivationMode** nie muszą być określane w czasie hello tworzenie hello usługi.
>
>- **Proces wyłącznego** model hostowania odpowiada za**ServicePackageAtivationMode** równy **ExclusiveProcess** i wymagają toobe jawnie określone w chwili hello tworzenia hello Usługa. 
>
>- Hostingu modelu usługi może być znane, badając hello [opis usługi] [ p2] i spojrzenie na wartość **ServicePackageAtivationMode**.
>
>

## <a name="working-with-deployed-service-package"></a>Praca z wdrożony pakiet usługi
Aktywne kopię *ServicePackage* w węźle jest określana jako [wdrożony pakiet usługi][p3]. Jak wcześniej wspomniano powyżej, gdy **wyłącznego procesu** model jest używany do tworzenia usług dla danego *aplikacji*, może istnieć wiele wdrożonej usługi pakietami hello sam  *ServicePackage*. Podczas wykonywania operacji, takich jak pakiet usługi określonego toodeployed [raportowania kondycji pakietu wdrożonej usługi] [ p4] lub [ponownego uruchamiania pakietu kodupakietuwdrożonejusługi] [ p5] itp., **ServicePackageActivationId** toobe musi podać tooidentify pakietu określonych wdrożonej usługi.

 **ServicePackageActivationId** wdrożonej usługi można uzyskać pakietu badając hello lista [wdrożonych pakietów usługi] [ p3] w węźle. Podczas wykonywania zapytania [wdrożone typów usług][p6], [wdrożone replik] [ p7] i [wdrożone pakiety kodu] [ p8] w węźle hello wynik zapytania zawiera także hello **ServicePackageActivationId** pakiet z wdrożonej przez element nadrzędny.

> [!NOTE]
>- W obszarze **udostępnionego procesu** hostingu modelu, w danej *węzła*, dla danego *aplikacji*tylko jeden kopię *ServicePackage* jest aktywny . Ma ona **ServicePackageActivationId** równa zbyt*pusty ciąg* i nie musi być określony, podczas gdy operacje dotyczące wykonywania wdrożony pakiet usługi. 
>
> - W obszarze **wyłącznego procesu** hostingu modelu, w danej *węzła*, dla danego *aplikacji*, jednego lub większej liczby kopii *ServicePackage* może być aktywne. Każda aktywacja ma *niepustym* **ServicePackageActivationId** i musi toobe określony podczas operacji związanych z wykonywania wdrożony pakiet usługi. 
>
> - Jeśli **ServicePackageActivationId** jest ommited domyślne too'empty ciąg ". Jeśli pakiet wdrożonej usługi, która została aktywowana w obszarze **udostępnionego procesu** modelu jest obecny, a następnie będzie można wykonać operacji, w przeciwnym razie hello operacja zakończy się niepowodzeniem.
>
> - Nie zaleca się tooquery raz i pamięci podręcznej **ServicePackageActivationId** generowane dynamicznie i można zmienić z różnych przyczyn. Przed wykonaniem operacji, które należy **ServicePackageActivationId**, należy najpierw kwerendy listy hello [wdrożonych pakietów usługi] [ p3] na węzeł, a następnie użyć  *ServicePackageActivationId** z operacji oryginalnego hello tooperform wyników zapytania.
>
>

## <a name="guest-executable-and-container-applications"></a>Gość plik wykonywalny i kontenera aplikacji
Sieć szkieletowa usług traktuje [pliku wykonywalnego gościa] [ a2] i [kontenera] [ a3] aplikacji jako statless usług, które są niezależne, tj. Brak nie środowiska uruchomieniowego platformy Service Fabric w *ServiceHost* (proces lub kontenera). Ponieważ te usługi są niezależne, liczba replik na *ServiceHost* nie ma zastosowania do tych usług. Witaj najczęściej używane z tymi usługami jest Konfiguracja jednej partycji z [InstanceCount] [ c2] równa zbyt-1 (tj. jedna kopia hello kodu usługi uruchomione w każdym węźle klastra). 

Witaj domyślne **ServicePackageActivationMode** dla tych usług jest **SharedProcess** w takim przypadku platformy Service Fabric aktywuje tylko jedną kopię *ServicePackage* na *Węzła* dla danego *aplikacji* co oznacza, że tylko jedna kopia kodu usługi zostaną uruchomione *węzła*. Mają wiele kopii toorun kod z usługi w *węzła* podczas tworzenia wielu usług (*Service1* za*ServiceN*) z *ServiceType* (określony w *ServiceManifest*) lub gdy usługa jest podzielona na partycje multi, należy określić **ServicePackageActivationMode** jako **ExclusiveProcess**w czasie hello tworzenie hello usługi.

## <a name="changing-hosting-model-of-an-existing-service"></a>Zmiana modelu hostingu istniejącej usługi
Zmiana modelu hostingu istniejącą usługę z **udostępnionego procesu** za**wyłącznego procesu** i na odwrót za pośrednictwem uaktualnić lub zaktualizować mechanizmu (lub w domyślnym obsługi specyfikacji w aplikacji manifest) nie jest obecnie obsługiwane. Obsługa tej funkcji wejdzie w przyszłych wersjach.

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>Wybór między procesu współużytkowanego i model procesu wyłączności
Zarówno mają one modele hostingu, jego zalet i wad i użytkownik musi tooevaluate, które z nich najlepiej pasuje do swoich wymagań. **Udostępnione procesu** model umożliwia lepsze wykorzystanie zasobów systemu operacyjnego, ponieważ procesy mniej jest zduplikowany, wiele replik w hello sam proces może współużytkować portów itp. Jednak jeden z replik hello trafienia wystąpił błąd, których potrzebuje toobring dół hello hosta usługi, będzie miało wpływ wszystkich replik w tym samym procesie.

 **Proces wyłącznego** modelu zapewnia lepszą izolację z każdej repliki w swoim własnym procesie i zachowania repliki nie ma wpływu na pozostałe repliki. Chodzi przydatną w przypadku których udostępnianie portów nie jest obsługiwana przez protokół komunikacyjny hello. Ułatwia on hello możliwości tooapply zasobów ładu na poziomie repliki. Witaj w drugiej strony, **wyłącznego procesu** zajmie więcej zasobów systemu operacyjnego, zgodnie z jego spowoduje utworzenie jednego procesu dla każdej repliki w węźle hello.

## <a name="exclusive-process-model-and-application-model-considerations"></a>Model procesu wyłączności i aplikacji zagadnienia dotyczące modelu
Witaj zalecany sposób toomodel aplikacji w sieci szkieletowej usług jest tookeep jedną *ServiceType* na *ServicePackage* i ten model działa dobrze w przypadku większości aplikacji hello. 

Jednak scenariusze specjalne tooenable w przypadku, gdy jeden *ServiceType* na *ServicePackage* jest pożądane, funkcjonalnie sieci szkieletowej usług umożliwia toohave więcej niż jednego *ServiceType* na *ServicePackage* (jeden *elementu CodePackage* można zarejestrować więcej niż jeden *ServiceType*). Poniżej przedstawiono niektóre scenariusze hello, gdzie te konfiguracje mogą być przydatne:

- Ma wykorzystania zasobów systemu operacyjnego toooptimize dochodzi do uruchamiania procesów mniej i po zwiększeniu repliki na proces.
- Repliki z różnych Serivcetype muszą tooshare niektóre wspólne dane inicjowania wysokiej lub pamięci kosztów.
- Oferty bezpłatnej usługi, i trzeba tooput limit wykorzystania zasobów przez umieszczenie wszystkich replik usługi hello w tym samym procesie.

**Proces wyłącznego** model hostowania nie jest spójna z modelem aplikacji istnieniem wielu *Serivcetype* na *ServicePackage*. Jest to spowodowane wielu *Serivcetype* na *ServicePackage* jest zasobem wyższym zaprojektowanego tooachieve udostępnianie między replikami i umożliwia zwiększeniu repliki na proces. Jest to sprzeczne toowhat **wyłącznego procesu** model jest zaprojektowana tooachieve.

Rozważmy przykład hello wielu *Serivcetype* na *ServicePackage* z różnymi *elementu CodePackage* zarejestrowanie każdego *ServiceType*. Załóżmy, że mamy *ServicePackage* MultiTypeServicePackge, która ma dwa *CodePackages*:

- MyCodePackageA, która rejestruje *ServiceType* "MyServiceTypeA".
- MyCodePackageB, która rejestruje *ServiceType* "MyServiceTypeB".

Teraz, umożliwia powiedzieć, utworzymy *aplikacji* **sieci szkieletowej: / SpecialApp** i wewnątrz **sieci szkieletowej: / SpecialApp** utworzymy następujące dwie usługi z **wyłączności Proces** modelu:

- Usługi **fabric: / SpecialApp/ServiceA** typu "MyServiceTypeA" z dwóch partycji (powiedzieć **P1** i **P2**) i 3 replik jednej partycji.
- Usługi **fabric: / SpecialApp/ServiceB** typu "MyServiceTypeB" z dwóch partycji (powiedzieć **P3** i **P4**) i 3 replik jednej partycji.

W danym węźle obie te usługi hello ma dwie repliki. Ponieważ użyliśmy **wyłącznego procesu** modelu toocreate hello usług, Service Fabric uaktywni nową kopię "MyServicePackge" dla każdej repliki. Każda aktywacja "MultiTypeServicePackge" spowoduje uruchomienie kopię "MyCodePackageA" i "MyCodePackageB". Jednak tylko jeden "MyCodePackageA" lub "MyCodePackageB" będzie obsługiwał replikę hello, dla którego został aktywowany "MultiTypeServicePackge". Poniższy diagram przedstawia widok węzła hello:

<center>
![Widok węzła wdrożonej aplikacji][node-view-five]
</center>

 Jak widać, w hello aktywacji "MultiTypeServicePackge" dla replik partycji **P1** usługi **fabric: / SpecialApp/ServiceA**, "MyCodePackageA" jest hostem repliki hello i " MyCodePackageB "jest tylko do pracy. Podobnie w przypadku aktywacji "MultiTypeServicePackge" dla replik partycji **P3** usługi **fabric: / SpecialApp/ServiceB**, "MyCodePackageB" jest hostem repliki hello i jest "MyCodePackageA" po prostu działa prawidłowo i tak dalej. W związku z tym więcej hello liczba *CodePackages* (rejestrowanie różnych *Serivcetype*) na *ServicePackage*, wyższy będzie użycie zasobów nadmiarowe. 
 
 Na hello drugiej strony, jeśli utworzymy usługami **sieci szkieletowej: / SpecialApp/ServiceA** i **sieci szkieletowej: / SpecialApp/ServiceB** z **udostępnionego procesu** modelu spowoduje sieci szkieletowej usług aktywować tylko jedną kopię "MultiTypeServicePackge" dla *aplikacji* **fabric: / SpecialApp** (zgodnie z wcześniej widzieliśmy). "MyCodePackageA" będzie obsługiwać wszystkie repliki usługi **sieci szkieletowej: / SpecialApp/ServiceA** (lub dowolnej usługi typu "MyServiceTypeA" toobe dokładniejsze) i "MyCodePackageB" będzie obsługiwać wszystkie repliki usługi **sieci szkieletowej: / SpecialApp/ServiceB** (lub dowolnej usługi typu "MyServiceTypeB" toobe dokładniejsze). Poniższy diagram przedstawia widok węzła hello tego ustawienia: 

<center>
![Widok węzła wdrożonej aplikacji][node-view-six]
</center>

W hello powyżej przykładzie, może być uważasz, że jeśli "MyCodePackageA" rejestruje zarówno "MyServiceTypeA" i "MyServiceTypeB" i "MyCodePackageB" nie istnieje, a następnie nie będzie nie nadmiarowe *elementu CodePackage* uruchomiona. To jest prawidłowa, jednak jak już wspomniano, ten model aplikacji nie jest wyrównana z **wyłącznego procesu** model hostowania. Jeśli celem jest tooput każdej repliki we własnym dedykowanym procesie następnie rejestrując zarówno *Serivcetype* z samej *elementu CodePackage* nie są potrzebne i umieszczanie każdego *ServiceType* w własne *ServicePacakge* jest bardziej naturalne wyborem.

## <a name="next-steps"></a>Następne kroki
[Pakiet aplikacji] [ a4] i skonfigurowania jej toodeploy gotowe.

[Wdrażanie i usunąć aplikacje] [ a5] w tym artykule opisano sposób toouse PowerShell toomanage aplikacji wystąpień.

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage