---
title: "Monitorowanie sieci szkieletowej usług aaaHealth | Dokumentacja firmy Microsoft"
description: "Wprowadzenie toohello sieć szkieletowa usług Azure monitorowania kondycji modelu, który zapewnia monitorowanie hello klastra i jego aplikacji i usług."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 1d979210-b1eb-4022-be24-799fd9d8e003
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 904f36374ca6ca7e4caa1d43c92584e7e4c50087
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooservice-fabric-health-monitoring"></a>Monitorowanie kondycji sieci szkieletowej tooService wprowadzenie
Sieć szkieletowa usług Azure wprowadza modelu kondycji, który zawiera oceny kondycji sformatowanego, elastyczny i rozszerzalny i raportowania. Hello model umożliwia niemal czasie rzeczywistym monitorowania stanu hello hello klastra i usług hello uruchomionych w niej. Można łatwo uzyskać informacje o kondycji i rozwiązać potencjalne problemy przed kaskadowo i spowodować duże awarii. W modelu typowe hello usług wysyłania raportów opartych na ich lokalnych widoków i informacji o agregowana tooprovide Widok ogólny poziomie klastra.

Składniki sieci szkieletowej usług Użyj tego tooreport modelu kondycji sformatowanego ich bieżącego stanu. Można użyć hello sam mechanizm tooreport kondycji z aplikacji. Jeśli poświęcić kondycji wysokiej jakości raportowania, który przechwytuje niestandardowe warunki, można wykrywać i znacznie łatwiejsze Rozwiązywanie problemów w uruchomionej aplikacji.

Witaj następujące Microsoft Virtual Academy wideo opisano również model kondycji sieci szkieletowej usług hello i sposobie ich użycia:<center><a target="_blank" href="https://mva.microsoft.com/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=tevZw56yC_1906218965">
<img src="./media/service-fabric-health-introduction/HealthIntroVid.png" WIDTH="360" HEIGHT="244">
</a></center>

> [!NOTE]
> Możemy uruchomić hello kondycji podsystemu tooaddress potrzebę monitorowanych uaktualnienia. Usługa Service Fabric realizuje monitorowanej aplikacji i klaster uaktualnień, które zapewnienie dostępności pełne, nie przestojów i toono minimalnej interwencji użytkownika. tooachieve tych celów, uaktualnienie hello sprawdza kondycji na podstawie skonfigurowanych zasad uaktualniania. Uaktualnienie można kontynuować tylko wtedy, gdy odpowiednie progi szanuje kondycji. W przeciwnym razie hello uaktualniania zostanie ona automatycznie wycofana lub wstrzymana Administratorzy toogive problemy z hello toofix szansy. toolearn więcej informacji na temat uaktualnienia aplikacji, zobacz [w tym artykule](service-fabric-application-upgrade.md).
> 
> 

## <a name="health-store"></a>Magazynu kondycji
magazynu kondycji Hello zachowuje z kondycją informacje na temat jednostek w klastrze hello łatwe pobieranie i oceny. Zaimplementowano jako usługi sieć szkieletowa utrwalone usługi stanowej tooensure wysokiej dostępności i skalowalności. Hello magazynu kondycji jest częścią hello **fabric: / System** aplikacji który jest dostępny, gdy klaster hello jest uruchomiony i działa.

## <a name="health-entities-and-hierarchy"></a>Jednostki kondycji i hierarchii
jednostki kondycji Hello są zorganizowane w hierarchii logicznej, która przechwytuje interakcji i zależności między różnymi jednostkami. magazynu kondycji Hello automatycznie tworzy jednostki kondycji i hierarchii, na podstawie raportów otrzymanych od składniki sieci szkieletowej usług.

jednostki kondycji Hello duplikatów hello jednostki sieci szkieletowej usług. (Na przykład **kondycji aplikacji jednostki** wystąpienie aplikacji jest zgodny wdrożone w klastrze hello, podczas gdy **jednostek node kondycji** odpowiada węźle klastra sieci szkieletowej usług.) przechwytuje hello kondycję hierarchii interakcje Hello hello jednostek systemowych i stanowi podstawę hello oceny kondycji zaawansowane. Informacje na temat podstawowych pojęć sieci szkieletowej usług w [omówienie techniczne sieci szkieletowej usług](service-fabric-technical-overview.md). Aby uzyskać więcej informacji na temat aplikacji, zobacz [model aplikacji usługi sieć szkieletowa](service-fabric-application-model.md).

jednostki kondycji Hello i hierarchii umożliwiają hello klastra i aplikacje toobe skutecznie zgłoszone, debugowania i monitorowane. model kondycji Hello udostępnia dokładne, *szczegółowego* reprezentację kondycję hello hello wielu części przenoszenie hello klastra.

![Kondycja jednostki.][1]
Witaj kondycji jednostki, zorganizowanych w hierarchii, na podstawie relacji nadrzędny podrzędny.

[1]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy.png

jednostki kondycji Hello są:

* **Klaster**. Reprezentuje kondycję hello klastra sieci szkieletowej usług. Raporty kondycji klastra opisują warunki, które mają wpływ na powitania całego klastra. Te warunki mają wpływ na wiele jednostek w klastrze hello lub hello samego klastra. Na podstawie hello warunku, osoby zgłaszającej hello nie można ograniczyć problem hello tooone lub więcej elementów podrzędnych w złej kondycji. Przykładami inteligencji hello klastra hello dzielenia powodu toonetwork partycjonowanie lub komunikacji problemy.
* **Węzeł**. Reprezentuje kondycji hello węzła sieci szkieletowej usług. Raporty kondycji węzła opisują warunki, które mają wpływ na funkcjonalność węzła hello. Zazwyczaj wpływają na wszystkie jednostki hello wdrożone w niej uruchomiona. Przykłady węzeł mało miejsca na dysku (lub inne właściwości komputera, takie jak pamięć, połączenia) i gdy węzeł nie działa. jednostek node Hello jest identyfikowane przez nazwę węzła hello (ciąg).
* **Aplikacja**. Reprezentuje kondycję hello wystąpienie aplikacji uruchomionych w klastrze hello. Raporty kondycji aplikacji opisują warunki, które mają wpływ na powitania ogólną kondycję aplikacji hello. Nie można ich zawęzić dzieci tooindividual (usługi lub aplikacje wdrożone). Przykładami hello end-to-end interakcji między różnych usług w aplikacji hello. Jednostka aplikacji Hello jest identyfikowane przez nazwę aplikacji hello (URI).
* **Usługa**. Reprezentuje hello kondycji usługi uruchomione w klastrze hello. Kondycja usługi Raporty opisują warunki, które mają wpływ na powitania ogólną kondycję hello usługi. osoby zgłaszającej Hello nie zawęzić hello problem tooan zła partycji lub repliki. Przykładami konfiguracji usługi (np. port lub udziału plików zewnętrznych), będący przyczyną problemów dla wszystkich partycji. jednostki usługi Hello jest identyfikowany przez hello nazwy usługi (URI).
* **Partycja**. Reprezentuje kondycji hello partycji usługi. Raporty kondycji partycji opisują warunki, które mają wpływ na powitania całym zestawie replik. Przykładami przy poniżej docelowa liczba hello liczby replik i gdy partycja jest w wyniku utraty kworum. Jednostka partycji Hello jest identyfikowany przez partycję hello Identyfikatora (GUID).
* **Replika**. Reprezentuje kondycję hello repliki usługi stanowej lub wystąpienie usługi bezstanowej. Replika Hello jest hello najmniejsza jednostka, która watchdogs i składniki systemu mogą raport na temat aplikacji. Dla stanowych usług przykładami replikę podstawową, którego nie można replikować toosecondaries operacji i powolne replikacji. Ponadto bezstanowych wystąpienia może raportować zaczyna brakować zasobów lub ma problemy z połączeniem. jednostki repliki Hello jest oznaczona hello Identyfikatora (GUID) i hello repliki lub wystąpienie identyfikator partycji (long).
* **DeployedApplication**. Reprezentuje hello kondycję *aplikacji uruchomionej w węźle*. Raportów o kondycji wdrożonej aplikacji opisu aplikacji toohello określonych warunków na powitania węzła, który nie może być zawęzić pakiety tooservice wdrożone na powitania tym samym węźle. Przykłady obejmują błędy, gdy nie można pobrać pakietu aplikacji w tym węźle i problemy dotyczące konfigurowania aplikacji podmiotów zabezpieczeń w węźle hello. Aplikacja Hello wdrożone jest identyfikowane przez nazwę aplikacji (URI) i nazwę węzła (ciąg).
* **DeployedServicePackage**. Reprezentuje kondycję hello uruchomione w węźle w klastrze hello pakietu usług. Opisuje on warunków określonych tooa usługi pakietu, który nie ma wpływu na powitania inne pakiety usługi na powitania sam węzeł hello tej samej aplikacji. Przykładami pakiet kodu w pakiecie usługi hello, której nie można uruchomić i pakiet konfiguracji, który nie może zostać odczytany. Witaj wdrożony pakiet usługi jest identyfikowane przez nazwę aplikacji (URI), nazwę węzła (ciąg), nazwa manifestu usługi (ciąg) i identyfikator aktywacji usługi pakietu (ciąg).

poziom szczegółowości Hello model kondycji hello umożliwia łatwe toodetect i rozwiązać problemy. Na przykład, jeśli usługa nie odpowiada, jest to wykonalne tooreport, który hello wystąpienia aplikacji jest zła. Raportowanie na czy poziom nie jest idealnym rozwiązaniem, jednak ponieważ hello problem może nie mieć wpływ na wszystkie usługi hello tej aplikacji. Raport Hello powinien być zastosowany toohello usługi w złej kondycji lub tooa podrzędne określonej partycji, jeśli partycji toothat wskazuje więcej informacji. Witaj dane automatycznie powierzchnie przez hierarchię hello i partycji zła stają się widoczne na poziomach usług i aplikacji. Ta agregacja pomaga toopinpoint i rozwiązać hello główną przyczynę problemu, hello szybciej.

Hierarchia kondycji Hello składa się z relacjami nadrzędny podrzędny. Klaster składa się z węzłów i aplikacji. Aplikacje usług i wdrożone aplikacje. Wdrożone aplikacje wdrożeniu usługi pakietów. Usługi mają partycje, a każda partycja zawiera jeden lub więcej repliki. Brak specjalne relacji między węzłami i wdrożone jednostek. Węzłów w złej kondycji zgłoszonych przez jego składnik systemu urzędu hello usługą Failover Manager service ma wpływ na powitania wdrożone aplikacje, pakiety usługi i repliki na nim wdrożone.

Witaj kondycję hierarchii reprezentuje hello najnowszy stan systemu hello oparte na powitania najnowsze raportów kondycji, która jest prawie w czasie rzeczywistym informacje.
Na tej samej jednostki na podstawie logiki specyficzne dla aplikacji lub niestandardowe warunki monitorowanych hello zgłosić watchdogs wewnętrznych i zewnętrznych. Raporty użytkownika współistnienie hello systemu raportów.

Planowanie tooinvest w sposób toohealth tooreport i odpowiadać podczas hello projekt usługi w chmurze duże. Ta początkowych inwestycyjny sprawia, że hello usługi łatwiejsze toodebug, monitorowania i obsługi.

## <a name="health-states"></a>Stany kondycji
Sieci szkieletowej usług używa trzech toodescribe stanów kondycji, czy jednostka jest uszkodzony lub nie: OK ostrzeżeń i błędów. Każdy raport wysłane magazynu kondycji toohello należy określić jedną z tych stanów. wynik oceny kondycji Hello jest jeden z tych stanów.

Witaj możliwe [stanów kondycji](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthstate) są:

* **OK**. jednostki Hello jest w dobrej kondycji. Nie są znane problemy zgłoszone go lub jego elementów podrzędnych (jeśli jest to wymagane).
* **Ostrzeżenie**. Jednostka Hello ma kilka problemów, ale mogą nadal działać prawidłowo. Na przykład występują opóźnienia, ale nie powoduje żadnych problemów funkcjonalnych jeszcze. W niektórych przypadkach stan ostrzeżenia hello może rozwiązać się bez interwencji zewnętrznych. W takich przypadkach raportów o kondycji podnieść świadomość i zapewniają wgląd w co się dzieje. W innych przypadkach stan ostrzeżenia hello może pogorszyć poważny problem, bez interwencji użytkownika.
* **Błąd**. Jednostka Hello jest zła. Należy podjąć akcję stanu hello toofix hello jednostki, ponieważ nie może działać prawidłowo.
* **Nieznany**. Hello jednostka nie istnieje w magazynie kondycji hello. Wynik ten można uzyskać z zapytań hello rozproszonych, które łączą się wyniki z wielu składników. Na przykład hello get węzła listy zapytania prowadzi zbyt**FailoverManager**, **ClusterManager**, i **HealthManager**; uzyskiwanie aplikacji zapytanie listy prowadzi zbyt **ClusterManager** i **HealthManager**. Te zapytania scalania wyniki z wielu składników systemu. Jeśli inny składnik systemu zwraca jednostki, która nie znajduje się w magazynie kondycji, hello scalonych wyników ma nieznany stan kondycji. Jednostka nie jest w magazynie, ponieważ nie zostały jeszcze przetworzone Raporty kondycji lub hello jednostki zostały wyczyszczone po usunięciu.

## <a name="health-policies"></a>Zasady dotyczące kondycji
magazynu kondycji Hello stosuje toodetermine zasady kondycji, czy jednostka jest w dobrej kondycji na podstawie jego raporty i jego elementów podrzędnych.

> [!NOTE]
> Zasady dotyczące kondycji można określić w manifeście klastra hello (dla klastra i węzła oceny kondycji) lub w manifeście aplikacji hello (w przypadku ocena aplikacji i wszystkich jego elementów podrzędnych). Żądania oceny kondycji można również przekazać w ramach zasad oceny kondycji niestandardowych, które są używane tylko w przypadku tej oceny.
> 
> 

Domyślnie usługi sieć szkieletowa stosuje ścisłych zasad (wszystko musi wskazywać dobrej kondycji) dla hierarchicznych relacji nadrzędny podrzędny hello. Jeśli jedno zdarzenie złej kondycji, nawet jednego z elementów podrzędnych hello nadrzędnego hello jest określana jako zła.

### <a name="cluster-health-policy"></a>Zasady dotyczące kondycji klastra
Witaj [klastra zasad dotyczących kondycji](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy) jest używane tooevaluate hello klastra kondycji stanów kondycji stanu i węzła. Witaj zasady można definiować w manifeście klastra hello. Jeśli nie jest obecny, hello domyślnych zasad (zero tolerowaną awarii) jest używany.
zasady dotyczące kondycji Hello klastra zawiera:

* [Elementów ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.considerwarningaserror). Określa, czy tootreat ostrzeżenie raporty dotyczące kondycji jako błędy podczas oceny kondycji. Domyślnie: false.
* [MaxPercentUnhealthyApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthyapplications). Określa maksymalny procent tolerowaną hello aplikacji, które mogą być zła, zanim klaster hello zostanie uznane za błąd.
* [MaxPercentUnhealthyNodes](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.maxpercentunhealthynodes). Określa maksymalny procent tolerowaną hello węzłów, które mogą być zła, zanim klaster hello zostanie uznane za błąd. W dużych klastrach niektóre węzły są zawsze dół lub wychodzących do naprawy, tak wartość ta powinna być skonfigurowana tootolerate który.
* [ApplicationTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.clusterhealthpolicy.applicationtypehealthpolicymap). Witaj aplikacji typu kondycji zasad mapy może służyć podczas typy specjalne aplikacji toodescribe oceny kondycji klastrów. Domyślnie wszystkie aplikacje są umieszczane w puli i oceniać za pomocą MaxPercentUnhealthyApplications. Niektóre typy aplikacji powinny być traktowane inaczej, mogą być wykonywane poza hello globalnej puli. Zamiast tego są one oceniane przed wartości procentowe hello skojarzony z jego nazwą typu aplikacji hello mapy. Na przykład w klastrze istnieją tysiące aplikacji o różnych typach i kilka wystąpień aplikacji formantu typu specjalnej aplikacji. Błąd nigdy nie powinna mieć Hello kontroli aplikacji. Globalne tootolerate % too20 MaxPercentUnhealthyApplications można określić pewne awarie, ale dla hello hello MaxPercentUnhealthyApplications too0 ustawiony typ aplikacji "ControlApplicationType". Dzięki temu w przypadku niektórych hello wiele aplikacji jest w złej kondycji, ale poniżej globalnych procent zła hello, będzie klastra hello obliczone tooWarning. Uaktualnianie klastra nie ma wpływu na ostrzegawczy stan kondycji lub innym monitorowania wyzwolone przez stanu kondycji błędu. Ale nawet jednego sterowania błędu spowodowałoby klastra złej kondycji, które wyzwala wycofywania lub wstrzymuje hello Uaktualnianie klastra, w zależności od konfiguracji uaktualnienia hello.
  Dla typów aplikacji hello zdefiniowanych w mapie hello wszystkich wystąpień aplikacji są wyjmowane z hello globalnej puli aplikacji. Są oceniane na podstawie całkowitej liczby aplikacji hello typu aplikacji hello, przy użyciu hello określonych MaxPercentUnhealthyApplications z hello mapy. Wszystkie pozostałe hello aplikacji hello pozostają w puli globalnej hello i są oceniane przy MaxPercentUnhealthyApplications.

Poniższy przykład Hello jest fragment manifestu klastra. toodefine wpisy mapy typu aplikacji hello, poprzedź nazwę parametru hello z "ApplicationTypeMaxPercentUnhealthyApplications-", a następnie według nazwy typu aplikacji hello.

```xml
<FabricSettings>
  <Section Name="HealthManager/ClusterHealthPolicy">
    <Parameter Name="ConsiderWarningAsError" Value="False" />
    <Parameter Name="MaxPercentUnhealthyApplications" Value="20" />
    <Parameter Name="MaxPercentUnhealthyNodes" Value="20" />
    <Parameter Name="ApplicationTypeMaxPercentUnhealthyApplications-ControlApplicationType" Value="0" />
  </Section>
</FabricSettings>
```

### <a name="application-health-policy"></a>Zasady kondycji aplikacji
Witaj [zasady kondycji aplikacji](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy) w tym artykule opisano, jak oceny hello zdarzeń oraz Stany podrzędnych agregacji jest wykonywane dla aplikacji i ich elementy podrzędne. Może być zdefiniowany w manifeście aplikacji hello **ApplicationManifest.xml**, w pakiecie aplikacji hello. Jeśli nie określono żadnych zasad, usługi sieć szkieletowa zakłada, że jednostka hello zła, jeśli ma ona raport o kondycji lub element podrzędny na powitania stanu kondycji ostrzeżenia lub błędu.
można skonfigurować zasady Hello są:

* [Elementów ConsiderWarningAsError](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.considerwarningaserror.aspx). Określa, czy tootreat ostrzeżenie raporty dotyczące kondycji jako błędy podczas oceny kondycji. Domyślnie: false.
* [MaxPercentUnhealthyDeployedApplications](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.maxpercentunhealthydeployedapplications). Umożliwia określenie wartości procentowej hello Maksymalna dopuszczalne wdrożone aplikacje, które mogą być zła, zanim aplikacja hello zostanie uznane za błąd. Tej wartości procentowej jest obliczana przez podzielenie hello liczba zła wdrożonych aplikacji hello liczby węzłów, które aplikacji hello na są wdrożone w klastrze hello. obliczenia Hello Zaokrągla wartość w górę tootolerate jednym błędem na małej liczby węzłów. Domyślna wartość procentowa: zero.
* [DefaultServiceTypeHealthPolicy](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.defaultservicetypehealthpolicy). Określa hello domyślne usługi typu kondycji zasad, które zastępuje hello domyślne kondycji zasady dla wszystkich typów usług w aplikacji hello.
* [ServiceTypeHealthPolicyMap](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthpolicy.servicetypehealthpolicymap). Miejsce mapy zasad dotyczących kondycji usługi dla typów usług. Te zasady zastępują hello zasady dotyczące kondycji typu usługi domyślne dla każdego określonego typu. Na przykład jeśli aplikacja ma typ usługi bezstanowej bramy i typ usługi stanowej aparatu, możesz można skonfigurować zasady dotyczące kondycji hello ich oceny inaczej. Po określeniu zasad dla typów usług można uzyskać większą kontrolę nad kondycji hello hello usługi.

### <a name="service-type-health-policy"></a>Zasady dotyczące kondycji usługi typu
Witaj [obsługi zasad dotyczących kondycji typu](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy) określa sposób tooevaluate i agregacji hello usług i hello dzieci usług. zasada Hello zawiera:

* [MaxPercentUnhealthyPartitionsPerService](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthypartitionsperservice). Określa procent hello Maksymalna dopuszczalne zła partycji, zanim usługa jest określana jako zła. Domyślna wartość procentowa: zero.
* [MaxPercentUnhealthyReplicasPerPartition](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyreplicasperpartition). Określa procent hello Maksymalna dopuszczalne repliki w złej kondycji, zanim partycji jest określana jako zła. Domyślna wartość procentowa: zero.
* [MaxPercentUnhealthyServices](https://docs.microsoft.com/dotnet/api/system.fabric.health.servicetypehealthpolicy.maxpercentunhealthyservices). Określa procent hello Maksymalna dopuszczalne usługi w złej kondycji, zanim aplikacji hello jest określana jako zła. Domyślna wartość procentowa: zero.

Poniższy przykład Hello jest fragment manifest aplikacji:

```xml
    <Policies>
        <HealthPolicy ConsiderWarningAsError="true" MaxPercentUnhealthyDeployedApplications="20">
            <DefaultServiceTypeHealthPolicy
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="10"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="FrontEndServiceType"
                   MaxPercentUnhealthyServices="0"
                   MaxPercentUnhealthyPartitionsPerService="20"
                   MaxPercentUnhealthyReplicasPerPartition="0"/>
            <ServiceTypeHealthPolicy ServiceTypeName="BackEndServiceType"
                   MaxPercentUnhealthyServices="20"
                   MaxPercentUnhealthyPartitionsPerService="0"
                   MaxPercentUnhealthyReplicasPerPartition="0">
            </ServiceTypeHealthPolicy>
        </HealthPolicy>
    </Policies>
```

## <a name="health-evaluation"></a>Oceny kondycji
Użytkowników i usług automatycznych można obliczyć kondycji dla dowolnej jednostki w dowolnym momencie. tooevaluate kondycja jednostki, hello zagregowanych danych z magazynu kondycji kondycji wszystkich raportów w jednostce hello i oblicza wszystkie elementy podrzędne (jeśli jest to wymagane). Witaj kondycji agregacji algorytm używa zasad dotyczących kondycji, które określają jak raporty dotyczące kondycji tooevaluate i jak kondycji podrzędnych tooaggregate Stany (jeśli jest to wymagane).

### <a name="health-report-aggregation"></a>Agregacja raportów kondycji
Jeden podmiot może mieć wiele raportów kondycji wysyłane przez różne raporty (składników systemowych lub watchdogs) na inne właściwości. używa agregacji Hello hello zasady dotyczące kondycji skojarzony w szczególności hello Członkowskie elementów ConsiderWarningAsError, aplikacji lub klastra zasad dotyczących kondycji. Określa elementów ConsiderWarningAsError jak tooevaluate ostrzeżenia.

Witaj zagregowane kondycja jest wyzwalany przez hello *najgorszy* Raporty kondycji na powitania jednostki. W przypadku co najmniej jeden błąd raport o kondycji, hello zagregowany stan kondycji jest błąd.

![Agregacja raportu kondycji z raportu o błędach.][2]

Jednostki kondycji, która ma co najmniej jeden błąd Raport kondycji jest traktowane jako błąd. Witaj dotyczy to także raport o kondycji wygasłe, niezależnie od jej stan kondycji.

[2]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-error.png

Jeśli istnieją nie raporty o błędach i co najmniej jedno ostrzeżenie, hello zagregowany stan kondycji jest ostrzeżenia lub błędu, w zależności od hello elementów ConsiderWarningAsError zasad flagi.

![Agregacja raportu kondycji z raportem ostrzeżenie i elementów ConsiderWarningAsError false.][3]

Agregacja raportu kondycji z raportem ostrzeżenie i elementów ConsiderWarningAsError ustawić toofalse (ustawienie domyślne).

[3]: ./media/service-fabric-health-introduction/servicefabric-health-report-eval-warning.png

### <a name="child-health-aggregation"></a>Agregacja kondycji podrzędne
Witaj zagregowane kondycja jednostki odzwierciedla hello stanów kondycji podrzędnych (jeśli jest to wymagane). Algorytm Hello do agregowania stanów kondycji podrzędnych używa hello zasady dotyczące kondycji stosowane na podstawie hello typu jednostki.

![Agregacja kondycji jednostek podrzędnych.][4]

Na podstawie zasad kondycji agregacji podrzędnych.

[4]: ./media/service-fabric-health-introduction/servicefabric-health-hierarchy-eval.png

Po oceniane magazynu kondycji hello wszystkie podrzędne hello agreguje ich stany kondycji oparte na powitania skonfigurowany maksymalny procent elementów podrzędnych w złej kondycji. Ta wartość jest pobierana z hello zasad na podstawie typu jednostki i podrzędny hello.

* Jeśli wszystkie elementy podrzędne OK stanów, stan kondycji podrzędnych zagregowane hello jest OK.
* Jeśli zarówno OK i ostrzeżenie stanów elementów podrzędnych, hello podrzędnych zagregowane kondycji jest w stanie ostrzegawczym.
* Jeśli istnieją elementy podrzędne z stanów błędów, które nie przestrzega hello maksymalny dozwolony odsetek podrzędne o złej kondycji, hello stan kondycji zagregowane, występuje błąd.
* Jeśli elementy podrzędne hello z hello względem Państwa błąd maksymalny dozwolony procent zła dzieci hello zagregowane kondycji jest w stanie ostrzegawczym.

## <a name="health-reporting"></a>Raportowania kondycji
Składniki systemu, aplikacji sieci szkieletowej systemu i wewnętrznej/zewnętrznej watchdogs może raportować względem jednostki sieci szkieletowej usług. Raporty Hello upewnij *lokalnego* oznaczeń hello kondycji jednostek hello monitorowane, na podstawie warunków hello są one monitorowania. Nie potrzebują toolook dowolnego stan globalny i agregowanie danych. Witaj żądane zachowanie jest toohave raporty proste i złożone organizmy, wymagające toolook na wiele tooinfer rzeczy, jakie toosend informacji.

magazynu kondycji danych toohello toosend kondycji, osoby zgłaszającej musi tooidentify hello dotyczy jednostki i tworzenia raportu dotyczącego kondycji. Raport hello toosend, użyj hello [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) interfejsu API, Raport kondycji interfejsów API narażone na powitania `Partition` lub `CodePackageActivationContext` obiektów, poleceń cmdlet programu PowerShell i REST.

### <a name="health-reports"></a>Raportów o kondycji
Witaj [raportów o kondycji](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthreport) dla poszczególnych jednostek hello w klastrze hello zawierają hello następujących informacji:

* **SourceId**. Ciąg unikatowo identyfikujący osoby zgłaszającej hello hello kondycji zdarzenia.
* **Identyfikator jednostki**. Identyfikuje jednostki hello których raport hello jest stosowane. Różni się pod względem hello [typu jednostki](service-fabric-health-introduction.md#health-entities-and-hierarchy):
  
  * Klaster. Brak.
  * Węzeł. Nazwa węzła (ciąg).
  * Aplikacja. Nazwa aplikacji (URI). Reprezentuje nazwę wystąpienia aplikacji hello wdrożone w klastrze hello hello.
  * Usługa. Nazwa usługi (URI). Reprezentuje nazwę hello wystąpienia usługi hello wdrożone w klastrze hello.
  * Partycja. Identyfikator (GUID). Reprezentuje hello partycji Unikatowy identyfikator.
  * Repliki. Identyfikator repliki usługi stanowej Hello lub identyfikator wystąpienia usługi bezstanowej hello (INT64).
  * DeployedApplication. Nazwa aplikacji (URI) i nazwę węzła (ciąg).
  * DeployedServicePackage. Nazwa aplikacji (URI), nazwę węzła (ciąg) i service manifest nazwę (ciąg).
* **Właściwość**. A *ciąg* (nie stałej wyliczenia) umożliwiająca osoby zgłaszającej hello toocategorize hello kondycji zdarzenie dla konkretnej właściwości hello jednostki. Na przykład osoby zgłaszającej A może raportować kondycję hello właściwość "Magazynu" hello Node01 i osoby zgłaszającej B może raportować kondycję hello hello Node01 "Łączności" właściwości. W magazynie kondycji hello te raporty są traktowane jako osobne kondycji zdarzenia hello Node01 jednostki.
* **Opis elementu**. Ciąg, który umożliwia tooprovide osoby zgłaszającej szczegółowe informacje na temat hello kondycji zdarzenie. **SourceId**, **właściwości**, i **HealthState** pełni powinna zawierać opis hello raportu. Opis Hello dodaje czytelny dla człowieka informacje na temat hello raportu. tekst Hello ułatwia administratorom i użytkownikom toounderstand hello raport o kondycji.
* **HealthState**. [Wyliczenie](service-fabric-health-introduction.md#health-states) opisujący stan kondycji hello hello raportu. Witaj akceptowane wartości to OK, ostrzeżenia i błędu.
* **Wartość TimeToLive**. Obiekt timespan, która wskazuje, jak długo raport o kondycji hello jest prawidłowy. Połączone z **RemoveWhenExpired**, umożliwia magazynu kondycji hello wiedzieć, jak tooevaluate ważność zdarzenia. Domyślnie wartość hello to nieskończoność, a raport hello jest prawidłowy w nieskończoność.
* **RemoveWhenExpired**. Wartość logiczna. Jeśli ustawiona tootrue, hello wygasłe kondycji raportu zostanie automatycznie usunięta z magazynu kondycji hello i bez wpływu na powitania raport oceny kondycji jednostki. Używany, gdy raport hello jest ważny przez okres określony tylko raz, a osoby zgłaszającej hello nie wymagają tooexplicitly wyczyszczenie go. Ma również używane toodelete raporty z magazynu kondycji hello (na przykład programu alarmowego zostało zmienione i zatrzymuje wysyłanie raportów o poprzednim źródła i właściwości). Wszelkie poprzednie stan z magazynu kondycji hello może wysłać raport o krótki TimeToLive wraz z RemoveWhenExpired tooclear. Jeśli wartość hello ustawiono toofalse, hello wygasłe raportu jest traktowana jako błąd na powitania oceny kondycji. wartość false Hello sygnały magazynu kondycji toohello źródła hello Zgłoś okresowo dla tej właściwości. W przeciwnym razie należy problem ze programu alarmowego hello. kondycji strażnika Hello są przechwytywane z uwzględnieniem zdarzeń hello jako błąd.
* **SequenceNumber**. Dodatnia liczba całkowita, która wymaga toobe eliminując, reprezentuje kolejność hello hello raportów. Jest on używany przez hello magazynu toodetect starych raportów kondycji odebranych opóźnienia z powodu opóźnienia sieci lub inne problemy. Raport został odrzucony, jeśli numer sekwencji hello jest mniejsza lub równa hello numer toohello ostatnio zastosowane do tej samej jednostki źródłowej właściwości oraz. Jeśli nie zostanie określony, numer kolejny hello jest generowany automatycznie. Tylko wtedy, gdy raportowanie przy zmianie stanu jest konieczne tooput hello numeru sekwencji. W takiej sytuacji źródła hello musi tooremember raporty, które go wysyłane i hello informacji odzyskiwania w tryb failover.

Te cztery części informacji — SourceId, identyfikator jednostki i właściwości oraz HealthState — są wymagane dla każdego raportu o kondycji. Hello SourceId ciąg nie jest dozwolona toostart z prefiksem hello "**systemu.**", który jest zarezerwowany dla raportów systemu. Dla hello tej samej jednostki, jest tylko jednego raportu dla hello tego samego źródła i właściwości. Wiele raportów z hello tego samego źródła i właściwości zastąpienia siebie, na stronie powitania kondycji klienta (jeśli są przetwarzane wsadowo) lub po stronie magazynu kondycji hello. zastąpienie Hello jest oparta na numerów; Raporty nowszej (o wyższych numerach) zastąpić starszą raportów.

### <a name="health-events"></a>Zdarzenia kondycji
Wewnętrznie śledzi magazynu kondycji hello [zdarzenia kondycji](https://docs.microsoft.com/dotnet/api/system.fabric.health.healthevent), które zawierają wszystkie hello informacje z raportów hello i dodatkowe metadane. metadane Hello zawierają hello czas jego modyfikacji na powitania po stronie serwera i czas hello raportu hello podano toohello kondycji klienta. zdarzenia kondycji Hello są zwracane przez [zapytań o kondycję](service-fabric-view-entities-aggregated-health.md#health-queries).

Witaj dodano metadane zawierają:

* **SourceUtcTimestamp**. Raport hello czasu Hello podano toohello kondycji klienta (Coordinated Universal Time).
* **LastModifiedUtcTimestamp**. Raport hello czasu Hello ostatniej modyfikacji po stronie serwera hello (Coordinated Universal Time).
* **IsExpired**. A Flaga tooindicate, czy raport hello wygasła w momencie hello zapytania została wykonana przez hello magazynu kondycji. Zdarzenia mogą wygasnąć tylko wtedy, gdy RemoveWhenExpired ma wartość false. W przeciwnym razie hello zdarzeń nie są zwracane przez zapytanie i zostanie usunięty z magazynu hello.
* **LastOkTransitionAt**, **LastWarningTransitionAt**, **LastErrorTransitionAt**. Witaj czas ostatniej OK/ostrzeżenie/błąd przejścia. Te pola nadaj hello historię hello przejść stanu kondycji zdarzenie hello.

Umożliwia pola przejścia stanu Hello inteligentny alertów lub "historyczne" kondycji zdarzenie informacji. Umożliwiają one scenariuszy takich jak:

* Generuj alert, jeśli właściwość została na ostrzeżenie/błąd dla więcej niż X minut. Sprawdzanie warunku hello w danym okresie czasu pozwala uniknąć alertów dotyczących tymczasowych warunków. Na przykład można przetłumaczyć alert, gdy stan kondycji hello ma zostały ostrzeżenie przez więcej niż pięć minut (HealthState == ostrzeżenie i LastWarningTransitionTime teraz - > 5 minut).
* Alert tylko na warunki, które zostały zmienione w hello ostatnich X minut. Jeśli raport został już przy błędzie przed hello określony czas, można zignorować, ponieważ zostało już zasygnalizowane wcześniej.
* Jeśli właściwość jest przełączania się między ostrzeżenia i błędu, określić, jak długo był nieprawidłowy (to znaczy nie OK). Na przykład można przetłumaczyć alert, gdy właściwość hello nie został dobrej kondycji na więcej niż pięć minut (HealthState! = Ok i teraz - LastOkTransitionTime > 5 minut).

## <a name="example-report-and-evaluate-application-health"></a>Przykład: Raport i oceny kondycji aplikacji
Witaj poniższy przykład wysyła raport dotyczący kondycji za pomocą programu PowerShell w aplikacji hello **fabric: / WordCount** ze źródła hello **MyWatchdog**. Raport o kondycji Hello zawiera informacje o hello kondycji właściwości "availability" w stanie kondycji błędu z TimeToLive nieskończoną. A następnie wysyła zapytanie kondycji aplikacji hello, która zwraca wartość zagregowana błędy stanu kondycji i hello zgłoszone zdarzenia kondycji hello liście zdarzenia kondycji.

```powershell
PS C:\> Send-ServiceFabricApplicationHealthReport –ApplicationName fabric:/WordCount –SourceId "MyWatchdog" –HealthProperty "Availability" –HealthState Error

PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            :
                                  Error event: SourceId='MyWatchdog', Property='Availability'.

ServiceHealthStates             :
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error

                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok

DeployedApplicationHealthStates :
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok

                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok

HealthEvents                    :
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 360
                                  SentAt                : 3/22/2016 7:56:53 PM
                                  ReceivedAt            : 3/22/2016 7:56:53 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 3/22/2016 7:56:53 PM, LastWarning = 1/1/0001 12:00:00 AM

                                  SourceId              : MyWatchdog
                                  Property              : Availability
                                  HealthState           : Error
                                  SequenceNumber        : 131032204762818013
                                  SentAt                : 3/23/2016 3:27:56 PM
                                  ReceivedAt            : 3/23/2016 3:27:56 PM
                                  TTL                   : Infinite
                                  Description           :
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Ok->Error = 3/23/2016 3:27:56 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="health-model-usage"></a>Sposób użycia modelu kondycji
model kondycji Hello umożliwia usługi w chmurze i hello podstawowej tooscale platformy Service Fabric, ponieważ monitorowania i kondycji są rozmieszczone hello różnych monitorów w ramach klastra hello.
Inne systemy ma jeden, scentralizowane usługi na poziomie klastra hello, która analizuje wszystkie hello *potencjalnie* przydatnych informacji na temat emitowane przez usługi. Takie podejście przeszkadza ich skalowalności. On również nie zezwala określone informacje toocollect toohelp zidentyfikować problemy i potencjalnych problemów jako Zamknij toohello główną przyczynę, jak to możliwe.

model kondycji Hello ciężko monitorowania i diagnostyki dla oceny kondycji klastra i aplikacji i monitorowanych uaktualnienia. Innych usług Użyj kondycji, które naprawia tooperform danych automatyczne, tworzenia Historia kondycji klastra i wystawiania alerty w przypadku niektórych warunków.

## <a name="next-steps"></a>Następne kroki
[Wyświetl raporty dotyczące kondycji sieci szkieletowej usług](service-fabric-view-entities-aggregated-health.md)

[Użyj systemowych raportów kondycji do rozwiązywania problemów](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Jak tooreport i zaznacz pole wyboru usługi kondycji](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Dodawanie niestandardowych raportów kondycji sieci szkieletowej usług](service-fabric-report-health.md)

[Monitorowanie i diagnozowania usług lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Uaktualnianie aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md)

