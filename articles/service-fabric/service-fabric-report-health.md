---
title: "Niestandardowe raporty kondycji sieci szkieletowej usług aaaAdd | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak toosend kondycji niestandardowych raportów jednostki kondycji sieci szkieletowej usług tooAzure. Zawiera zalecenia dotyczące projektowania i wdrażania raportów o kondycji jakości."
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 0a00a7d2-510e-47d0-8aa8-24c851ea847f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: oanapl
ms.openlocfilehash: 12c9f664e2a457b4e1e8f340873ca60ebcefb097
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-service-fabric-health-reports"></a>Dodawanie niestandardowych raportów kondycji usługi Service Fabric
Sieć szkieletowa usług Azure wprowadza [model kondycji](service-fabric-health-introduction.md) tooflag zła klastra oraz warunki aplikacji na konkretnych obiektów. model kondycji Hello używa **Raporty kondycji** (składników systemu i watchdogs). Celem Hello jest łatwe i szybkie diagnozowanie i naprawy. Moduły zapisujące usługi należy toothink wyprzedzeniem o kondycji. Należy podać żadnych warunek, który może mieć wpływ na kondycję, zwłaszcza, jeśli może pomóc problemów flagi zamknąć toohello głównego. informacje o kondycji Hello można zapisać ilość czasu, na analizie i debugowania. Witaj przydatność jest szczególnie wyczyszczone po hello usługa jest uruchomiona na dużą skalę w chmurze hello (prywatny czy Azure).

monitor raporty usługi sieć szkieletowa Hello określone warunki odsetek. Zgłaszają przy użyciu tych warunków na podstawie ich lokalnego widoku. Witaj [magazynu kondycji](service-fabric-health-introduction.md#health-store) agreguje dane kondycji wysyłane przez wszystkie toodetermine raporty, czy jednostki są globalnie dobrej kondycji. Hello model jest zamierzone toobe toouse sformatowanego, elastyczne i łatwe. jakość Hello raportów o kondycji hello Określa dokładność hello widoku kondycji hello hello klastra. Fałszywych alarmów, przedstawiających błędnie zła problemów może niekorzystnie wpłynąć na uaktualnienia lub innych usług używających danych kondycji. Przykładami takich usług są usługi repair i mechanizmów alertów. W związku z tym rozwagą jest tooprovide potrzebne raporty, które przechwytywania warunki zainteresowanie hello najlepsze możliwe sposób.

toodesign i wdrożenie kondycji raportowania, watchdogs i składnikach systemu musi:

* Zdefiniuj warunek hello są zainteresowani, jak hello jest monitorowany i hello wpływ na funkcjonalność klastra lub aplikacji hello. Na podstawie tych informacji, decyduje o hello raportu właściwości oraz kondycji stanu kondycji.
* Określić hello [jednostki](service-fabric-health-introduction.md#health-entities-and-hierarchy) że hello raport dotyczy.
* Ustal, gdzie hello raportowania jest wykonywana, z poziomu hello usługi lub wewnętrznych lub zewnętrznych programu alarmowego.
* Zdefiniuj źródło używane tooidentify hello reportera.
* Wybierz strategię raportowania, okresowo lub na przejścia. Witaj zalecany sposób jest okresowo, ponieważ wymaga prostsze kodu i jest mniej podatne tooerrors.
* Jak długo hello raportu należy określić zła warunki powinny pozostać w magazynie kondycji hello i w jaki sposób ma zostać wyczyszczona. Korzystając z tych informacji, zdecyduj, raport hello toolive i Usuń na wygaśnięcia zachowania w czasie.

Jak wspomniano, raportowanie może odbywać się od:

* Witaj monitorowane repliki usługi sieć szkieletowa usług.
* Wewnętrzny watchdogs wdrożony jako usługa sieci szkieletowej usług (na przykład sieci szkieletowej usług bezstanowych Usługa monitoruje warunki i generuje raporty). Witaj watchdogs może być wdrożony wszystkie węzły lub może być skoligaconym toohello monitorowane usługi.
* Wewnętrzny watchdogs, uruchom na powitania węzłów sieci szkieletowej usług, które są *nie* zaimplementowane jako usługi sieci szkieletowej usług.
* Zewnętrzne watchdogs zasobu hello sondowania z *poza* klastra sieci szkieletowej usług hello (na przykład monitorowania usługi, takiej jak Gomez).

> [!NOTE]
> Fabrycznej hello klastra hello jest wypełniana wysyłane przez składniki systemu hello raportów o kondycji. Dowiedz się więcej o [przy użyciu kondycji systemu raportów do rozwiązywania problemów](service-fabric-understand-and-troubleshoot-with-system-health-reports.md). Witaj raporty użytkownika musi zostać wysłany [jednostki kondycji](service-fabric-health-introduction.md#health-entities-and-hierarchy) które już zostały utworzone przez hello system.
> 
> 

Raz hello projektu raportowania kondycji jest wyczyszczone, łatwo można wysyłać raporty o kondycji. Można użyć [klienta fabricclient z rolą](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) tooreport kondycji, jeśli hello klastra nie jest [bezpiecznego](service-fabric-cluster-security.md) lub jeśli powitania klienta programu fabric ma uprawnienia administratora. Raportowanie może odbywać się za pośrednictwem hello interfejsu API przez przy użyciu [FabricClient.HealthManager.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth), za pomocą programu PowerShell lub za pośrednictwem REST. Konfiguracja pokrętła partii raportów, aby uzyskać lepszą wydajność.

> [!NOTE]
> Raport kondycji jest synchroniczne, i reprezentuje tylko hello weryfikacji pracy na powitania po stronie klienta. Witaj fakt, że hello raportu jest akceptowane przez hello kondycji klienta lub hello `Partition` lub `CodePackageActivationContext` obiektów nie oznacza, że jest ono stosowane w magazynie hello. Jest wysyłane asynchronicznie, być może umieścić w zadaniu wsadowym razem z innymi raportami. Hello przetwarzania na serwerze hello nadal może zakończyć się niepowodzeniem: numer sekwencyjny hello może być stałe, jednostki hello na powitania, które należy zastosować raport został usunięty, itp.
> 
> 

## <a name="health-client"></a>Kondycji klienta
Raporty kondycji Hello są wysyłane toohello magazynu kondycji za pomocą klienta kondycji, które znajdują się wewnątrz powitania klienta sieci szkieletowej. Witaj kondycji klienta można skonfigurować za pomocą hello następujące ustawienia:

* **HealthReportSendInterval**: hello opóźnienia między hello czasie — raport hello jest dodany toohello klienta i hello czasu jest wysyłane toohello magazynu kondycji. Raporty toobatch używanych w pojedynczym komunikacie zamiast wysyłania jeden komunikat dla każdego raportu. Przetwarzanie wsadowe Hello poprawia wydajność. Wartość domyślna: 30 sekund.
* **HealthReportRetrySendInterval**: interwał powitania, w których hello kondycji klienta wysyła ponownie kondycji wszystkich raportów toohello magazynu kondycji. Wartość domyślna: 30 sekund.
* **HealthOperationTimeout**: hello limit czasu dla komunikatu raport wysyłany toohello magazynu kondycji. Jeśli upłynie limit czasu wiadomości, hello kondycji klient ponawia próbę go do momentu magazynu kondycji hello potwierdza hello raport został przetworzony. Wartość domyślna: dwie minuty.

> [!NOTE]
> Gdy są przetwarzane wsadowo hello raporty, powitania klienta programu fabric musi utrzymywać ich aktywność dla co najmniej hello tooensure HealthReportSendInterval, które są wysyłane. Jeśli wiadomość hello zostało utracone lub hello magazynu kondycji nie może zastosować je ze względu na błędy tootransient, powitania klienta sieci szkieletowej muszą być przechowywane aktywności toogive dłużej go tooretry szansy.
> 
> 

buforowanie Hello na powitania klienta ma unikatowości hello hello raportów pod uwagę. Na przykład określonego zły osoby zgłaszającej zgłoszenie 100 raportów na sekundę na powitania sama właściwość hello tej samej jednostki, hello raporty są zamieniane na powitania ostatniej wersji. Istnieje co najwyżej jeden taki raport w kolejce klienta hello. Jeśli skonfigurowano przetwarzanie wsadowe hello liczbę raportów wysłano toohello magazynu kondycji jest tylko jeden interwał wysyłania. Ten raport jest hello ostatniego dodany raport, która odzwierciedla hello najbardziej bieżącego stanu jednostki hello.
Określ parametry konfiguracji po `FabricClient` jest tworzony przez przekazanie [FabricClientSettings](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclientsettings) z hello żądane wartości dla wpisy dotyczące kondycji.

Witaj poniższy przykład tworzy klienta sieci szkieletowej i określa, czy mają być wysyłane raporty hello po ich dodaniu. Limity czasu i błędy, które można ponowić ponownych prób nastąpić co 40 sekund.

```csharp
var clientSettings = new FabricClientSettings()
{
    HealthOperationTimeout = TimeSpan.FromSeconds(120),
    HealthReportSendInterval = TimeSpan.FromSeconds(0),
    HealthReportRetrySendInterval = TimeSpan.FromSeconds(40),
};
var fabricClient = new FabricClient(clientSettings);
```

Zaleca się pozostawienie sieci szkieletowej domyślne hello ustawienia klienta, które `HealthReportSendInterval` too30 sekund. To ustawienie zapewni optymalną wydajność toobatching ukończenia. Krytyczne raportów, które muszą zostać przesłane tak szybko, jak to możliwe, należy użyć `HealthReportSendOptions` z Immediate `true` w [FabricClient.HealthClient.ReportHealth](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.reporthealth) interfejsu API. Raporty natychmiastowego obejścia hello przetwarzanie wsadowe interwału. Użyj tej flagi ostrożność; chcemy tootake zaletą hello kondycji klienta przetwarzanie wsadowe, jeśli to możliwe. Natychmiastowe wysyłania jest również przydatny podczas zamykania powitania klienta sieci szkieletowej (na przykład procesu hello wykrył nieprawidłowy stan i musi tooshut tooprevent efekty uboczne w dół). Zapewnia send optymalnych hello zebranych raportów. Po dodaniu jeden raport z flagą natychmiastowego hello kondycji klienta partii wszystkie raporty hello zgromadzonych od czasu ostatniego wysłania.

Takie same parametry można określić podczas tworzenia klastra tooa połączenia za pomocą programu PowerShell. Poniższy przykład Hello uruchamia klastra lokalnego tooa połączenia:

```powershell
PS C:\> Connect-ServiceFabricCluster -HealthOperationTimeoutInSec 120 -HealthReportSendIntervalInSec 0 -HealthReportRetrySendIntervalInSec 40
True

ConnectionEndpoint   :
FabricClientSettings : {
                       ClientFriendlyName                   : PowerShell-1944858a-4c6d-465f-89c7-9021c12ac0bb
                       PartitionLocationCacheLimit          : 100000
                       PartitionLocationCacheBucketCount    : 1024
                       ServiceChangePollInterval            : 00:02:00
                       ConnectionInitializationTimeout      : 00:00:02
                       KeepAliveInterval                    : 00:00:20
                       HealthOperationTimeout               : 00:02:00
                       HealthReportSendInterval             : 00:00:00
                       HealthReportRetrySendInterval        : 00:00:40
                       NotificationGatewayConnectionTimeout : 00:00:00
                       NotificationCacheUpdateTimeout       : 00:00:00
                       }
GatewayInformation   : {
                       NodeAddress                          : localhost:19000
                       NodeId                               : 1880ec88a3187766a6da323399721f53
                       NodeInstanceId                       : 130729063464981219
                       NodeName                             : Node.1
                       }
```

Podobnie tooAPI, raporty można wysyłać przy użyciu `-Immediate` przełącznika toobe wysyłane natychmiast, niezależnie od hello `HealthReportSendInterval` wartość.

Dla pozostałych hello raporty są wysyłane bramy sieci szkieletowej usług toohello, którego klient wewnętrznej sieci szkieletowej. Domyślnie ten klient jest skonfigurowany toosend raporty umieścić w zadaniu wsadowym co 30 sekund. Interwał partii powitania można zmienić za pomocą ustawienia konfiguracji klastra hello `HttpGatewayHealthReportSendInterval` na `HttpGateway`. Jak wspomniano, lepszym rozwiązaniem jest toosend hello raporty z `Immediate` wartość true. 

> [!NOTE]
> tooensure, który nieautoryzowany usługi nie można utworzyć raportu kondycji przed hello jednostek w klastrze hello, skonfiguruj powitania serwera tooaccept żądania tylko zabezpieczonych klientów. Witaj `FabricClient` używane na potrzeby raportowania musi mieć z włączonymi zabezpieczeniami toobe toocommunicate stanie hello klastra (na przykład z uwierzytelnianiem Kerberos lub certyfikatów). Przeczytaj więcej na temat [klastra zabezpieczeń](service-fabric-cluster-security.md).
> 
> 

## <a name="report-from-within-low-privilege-services"></a>Raport z niskim poziomem uprawnień Services
Usługa sieci szkieletowej usług nie ma klastra toohello dostępu administratora, możesz zgłosić kondycji na jednostek z bieżącego kontekstu hello za pośrednictwem `Partition` lub `CodePackageActivationContext`.

* W przypadku usług bezstanowych użyj [IStatelessServicePartition.ReportInstanceHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatelessservicepartition.reportinstancehealth) tooreport na powitania bieżącego wystąpienia usługi.
* Usługi stanowej, użyj [IStatefulServicePartition.ReportReplicaHealth](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition.reportreplicahealth) tooreport na bieżącej repliki.
* Użyj [IServicePartition.ReportPartitionHealth](https://docs.microsoft.com/dotnet/api/system.fabric.iservicepartition.reportpartitionhealth) tooreport na powitania bieżącego obiektu partycji.
* Użyj [CodePackageActivationContext.ReportApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportapplicationhealth) tooreport w bieżącej aplikacji.
* Użyj [CodePackageActivationContext.ReportDeployedApplicationHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedapplicationhealth) tooreport w bieżącej aplikacji hello wdrożone na powitania bieżącego węzła.
* Użyj [CodePackageActivationContext.ReportDeployedServicePackageHealth](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext.reportdeployedservicepackagehealth) tooreport na pakiet usługi dla aplikacji hello wdrożone na powitania bieżącego węzła.

> [!NOTE]
> Witaj, `Partition` i hello `CodePackageActivationContext` przechowywania kondycji klient skonfigurowany przy użyciu ustawień domyślnych. Zgodnie z objaśnieniem dla hello [kondycji klienta](service-fabric-report-health.md#health-client), raporty są umieszczane w partii i wysyłane przez czasomierz. obiekty Hello powinny być przechowywane aktywności toohave raportu hello toosend szansy.
> 
> 

Można określić `HealthReportSendOptions` podczas wysyłania raportów za pośrednictwem `Partition` i `CodePackageActivationContext` kondycji interfejsów API. Jeśli masz krytyczne raportów, które muszą zostać przesłane tak szybko, jak to możliwe, użyj `HealthReportSendOptions` z Immediate `true`. Raporty natychmiastowego obejścia hello przetwarzanie wsadowe interwał hello wewnętrzny kondycji klienta. Jak wspomniano wcześniej, użyj tej flagi ostrożność; chcemy tootake zaletą hello kondycji klienta przetwarzanie wsadowe, jeśli to możliwe.

## <a name="design-health-reporting"></a>Projektowanie raportowania kondycji
Witaj pierwszym krokiem podczas generowania raportów wysokiej jakości identyfikuje hello warunki, które może wpłynąć na kondycję hello hello usługi. Wszelkie warunek, który może pomóc flagi problemów w usłudze hello lub klastra podczas jego uruchamiania--lub lepszy, zanim się stanie, problem — może potencjalnie zapisać miliardów dolarów. Hello zalety mniej czas przestoju, mniejszą liczbę godzin nocy poświęcony na wykrywanie i naprawianie problemów i wyższe zadowolenia klienta.

Po zidentyfikowaniu warunki hello autorzy programu alarmowego muszą toofigure limit hello najlepsze sposób toomonitor je na równowaga między koszty i użyteczność. Rozważmy na przykład usługi, który wykonuje obliczenia złożonych, które używają niektóre pliki tymczasowe w udziale. Programu alarmowego można monitorować hello udziału tooensure, że jest dostępna wystarczająca ilość miejsca. Można go nasłuchiwania powiadomień o zmianach pliku lub katalogu. Można go raportować ostrzeżenie, jeśli próg góry, a zgłaszać błąd, gdy udział hello jest pełna. Na ostrzeżenie, można uruchomić system naprawy, czyszczenie starszych plików w udziale hello. W przypadku wystąpienia błędu systemu naprawy można przenieść węzła tooanother repliki usługi hello. Należy pamiętać, opisu stanów warunku hello pod względem kondycji: hello stan hello warunek, który jest uznawana za dobrej kondycji (ok) lub złej kondycji (ostrzeżenia lub błędu).

Po ustawieniu hello szczegóły monitorowania, moduł zapisujący programu alarmowego musi toofigure się jak tooimplement hello programu alarmowego. Jeśli warunki hello można ustalić na podstawie w ramach usługi hello, programu alarmowego hello mogą być częścią sama usługa hello monitorowane. Na przykład hello kodu usługi można sprawdzanie hello udziału, a następnie składają raporty za każdym razem, gdy próbuje toowrite pliku. Witaj zaletą tej metody jest raportowania proste. Należy zachować ostrożność usterki programu alarmowego tooprevent z wpływu na funkcjonalność usługi hello.

Raportowania w ramach usługi monitorowane hello nie zawsze jest opcją. Strażnika w ramach usługi hello może nie być możliwe toodetect hello warunków. Nie może mieć hello logikę i dane toomake hello określenie. koszty Hello monitorowania warunków hello może być wysokie. warunki Hello również może nie być tooa określonej usługi, ale zamiast tego na interakcje między usługami. Innym rozwiązaniem jest watchdogs toohave w klastrze hello jako osobne procesy. Hello watchdogs monitorowanie warunków hello i raport, bez wywierania wpływu na powitania usług w dowolny sposób. Na przykład watchdogs te można zaimplementowane jako usługi bezstanowej w hello tej samej aplikacji wdrożone na wszystkich węzłach lub hello samych węzłów jako usługa hello.

Czasami programu alarmowego uruchomiona w klastrze hello nie jest opcją albo. Gdy warunek hello monitorowane jest dostępności hello lub funkcji usługi hello użytkownicy widzą go, jest najlepszym watchdogs hello toohave w hello w tym samym miejscu jako hello użytkownika klientów. Istnieje, można przetestować operacji hello w hello tych samych użytkowników sposób połączeń telefonicznych z nimi. Na przykład można mieć programu alarmowego, znajduje się poza klastrem hello, wystawia żądań toohello usługi i sprawdza hello opóźnienia i poprawność wyników hello. (Dla usługi Kalkulator, na przykład 2 + 2 zwróci 4 w rozsądnym czasie?)

Po sfinalizowany szczegóły dotyczące programu alarmowego hello, należy podjąć decyzję dotyczącą na identyfikator źródła, który unikatowo identyfikuje go. Jeśli wiele watchdogs z hello mieszkają tego samego typu w hello klastra, klienci muszą raportu na różnych jednostkach, lub, jeśli ich raport dotyczący hello tej samej jednostki, użyj innego źródła Identyfikatora lub właściwości. W ten sposób ich raporty mogą współistnieć. Właściwość Hello raport o kondycji hello powinien przechwytywania warunku hello monitorowane. (Na przykład hello powyżej, może być właściwości hello **ShareSize**.) Jeśli wiele raportów stosować toohello sam warunek, hello właściwość powinna zawierać informacje dynamiczne umożliwia toocoexist raportów. Na przykład, jeśli wiele udziałów muszą toobe monitorowane, nazwa właściwości hello może być **ShareSize sharename**.

> [!NOTE]
> Czy *nie* Użyj informacji o stanie tookeep hello kondycji magazynu. Należy podać tylko informacje dotyczące kondycji jako kondycji jako tej oceny kondycji informacji wpływa na powitania jednostki. magazynu kondycji Hello nie został zaprojektowany jako magazynu ogólnego przeznaczenia. Używa tooaggregate logiki oceny kondycji wszystkich danych do stanu kondycji hello. Wysyłanie informacji niepowiązanych toohealth (takich jak raportowanie stanu ze stanem kondycji OK) bez wpływu na powitania zagregowane stan kondycji, ale może negatywnie wpłynąć na wydajność magazynu kondycji hello hello.
> 
> 

Hello dalej podjęcie decyzji, czy znajduje się na które tooreport jednostki. W większości przypadków hello warunku hello wyraźnie idetifies hello jednostki. Wybierz jednostki hello z najlepsze możliwe stopnia szczegółowości. Jeśli warunek ma wpływ na wszystkie repliki na partycji, raport dotyczący hello partycji, nie na powitania usługi. Brak sytuacjach wyjątkowych, gdy potrzebne jest więcej myśl, mimo że. Jeśli warunek hello ma wpływ na jednostkę, takich jak repliki, ale hello desire jest warunek hello toohave oflagowane więcej niż czas trwania hello życia repliki, należy podać na powitania partycji. W przeciwnym razie po usunięciu hello repliki magazynu kondycji hello czyści jego raporty. Autorzy programu alarmowego muszą myśleć o hello okresy istnienia hello jednostki i hello raportu. Musi być jasne podczas raportu należy oczyścić z magazynu (na przykład błędu zgłoszonego z jednostką już ma zastosowanie).

Oto przykład, w którym umieszcza ze sobą, I opisano punktów hello. Należy rozważyć aplikacji usługi sieć szkieletowa składa się z głównym usługi stanowej trwałe i dodatkowej usługi bezstanowej wdrożone na wszystkich węzłach (jeden typ dodatkowej usługi dla poszczególnych typów zadań). wzorzec Hello ma kolejki przetwarzania zawierającej toobe polecenia wykonywane przez pomocnicze bazy danych. Hello pomocnicze bazy danych wykonaj hello żądań przychodzących i wysyłanie sygnałów wstecz potwierdzenia. Jeden warunek, który może być monitorowany jest hello hello kolejki przetwarzania wzorca. Jeśli długość kolejki głównej hello osiągnie próg, ostrzeżenie jest raportowana. Ostrzeżenie Hello wskazuje, że hello pomocnicze bazy danych nie może obsłużyć obciążenia hello. Jeśli kolejki hello osiągnie hello maksymalną długość polecenia są usuwane, jest zgłaszany błąd, jako hello usługi nie można odzyskać. Witaj raporty mogą być we właściwości hello **QueueStatus**. programu alarmowego Hello znajdują się wewnątrz hello usługi i jest okresowo przesyłane na powitania wzorca repliki podstawowej. czas Hello toolive wynosi dwie minuty, a wysłaniem okresowo co 30 sekund. Jeśli hello podstawowy ulegnie awarii, raport hello jest automatycznie czyszczone z magazynu. Jeśli repliki usługi hello jest uruchomiony, ale jest typu lub inne problemy, hello raportu wygaśnie w magazynie kondycji hello. W takim przypadku jednostki hello jest oceniane w błąd.

Inny warunek, który może być monitorowany jest czas wykonania zadania. Witaj wzorca dystrybuuje zadania toohello pomocnicze bazy danych na podstawie hello zadań typu. W zależności od projektu hello wzorca hello można sondować hello pomocnicze bazy danych dla stanu zadania. Po wykonaniu go można również poczekaj sygnały wstecz potwierdzenia toosend pomocnicze bazy danych. W drugim przypadku hello należy uważać sytuacjach toodetect gdzie struktury pomocnicze bazy danych lub komunikaty zostaną utracone. Jedną z opcji jest dla wzorca toosend hello toohello żądanie ping sam dodatkowej, której odsyła jego stan. Jeśli brak stan nie zostanie odebrana, głównego hello uzna awarii i zmienia harmonogram zadań hello. To zachowanie zakłada, że zadania hello są idempotentności.

warunek Hello monitorowane można przekonwertować jako ostrzeżenie, jeśli zadanie hello nie odbywa się w określonym czasie (**t1**, na przykład 10 minut). Jeśli hello zadanie nie zostało ukończone w czasie (**t2**, na przykład 20 minut), hello monitorowane warunku można przetłumaczyć jako błąd. Ta raportowania może odbywać się na wiele sposobów:

* repliki podstawowej wzorca Hello raporty okresowo od siebie samego. Może mieć jedną właściwość dla wszystkich zadań oczekujących w kolejce hello. Jeśli co najmniej jedno zadanie trwa dłużej, stan raportu hello we właściwości hello **PendingTasks** jest ostrzeżenia lub błędu, zależnie od potrzeb. Jeśli nie ma żadnych oczekujących zadań lub wszystkich zadań rozpoczął wykonywanie sekwencji, stan raportu hello jest OK. zadania Hello są trwałe. Jeśli hello podstawowy ulegnie awarii, hello nowo podwyższenia poziomu podstawowego nadal tooreport poprawnie.
* Inny proces programu alarmowego (w chmurze hello lub zewnętrznego) sprawdza hello zadania (z zewnątrz, na podstawie hello żądanego wyniku zadania) toosee, jeśli zostały one zakończone. Jeśli ich nie przestrzega hello progów, raport jest wysyłany na powitania głównej usługi. Raport jest również przesyłany dla każdego zadania, który obejmuje hello identyfikatora zadania, takie jak **PendingTask + taskId**. Raporty mają być wysyłane tylko w stan złej kondycji. Ustaw czas toolive tooa kilka minut i oznacz toobe raporty hello usuwane, gdy wygasną tooensure oczyszczania.
* Hello dodatkowej, która wykonuje zadania raportów, gdy trwa dłużej niż oczekiwano toorun go. Raporty dla wystąpienia usługi hello we właściwości hello **PendingTasks**. Raport Hello określa hello wystąpienie usługi, które występują problemy, ale nie przechwytuje hello sytuacji, gdy zaniku hello wystąpienia. Raporty Hello są następnie wyczyścić. Można go raport dotyczący hello dodatkowej usługi. Hello dodatkowej wykona hello zadań, wystąpienie dodatkowej hello czyści hello raportu z magazynu hello. Raport Hello nie przechwytuje hello sytuacji, gdy komunikat potwierdzenia hello zostaną utracone i hello zadanie nie zostało zakończone z punktu widzenia głównego hello.

Jednak hello raportowania odbywa się w przypadku hello opisane powyżej, raporty hello są przechwytywane kondycji aplikacji podczas oceny kondycji.

## <a name="report-periodically-vs-on-transition"></a>Raport okresowo a na przejście
Używając raportowania modelu kondycji hello watchdogs raporty można wysyłać okresowo lub przejścia. Hello zalecany sposób programu alarmowego raportowania jest okresowo, ponieważ kod hello jest znacznie prostsza i mniej podatna tooerrors. Hello watchdogs należy dążyć toobe najprostszą możliwe tooavoid usterki, które mogą powodować nieprawidłowe raporty. Niepoprawna *zła* wpływ na raporty oceny kondycji i scenariusze, w oparciu o kondycji, w tym uaktualnienia. Niepoprawna *dobrej kondycji* raporty ukrycie problemów w klastrze hello, co nie jest wymagana.

Okresowe raportowania programu alarmowego hello można zaimplementować z czasomierzem. Wywołanie zwrotne czasomierza programu alarmowego hello można Sprawdź stan hello i wysłać raport na podstawie bieżącego stanu hello. Nie ma żadnych toosee potrzeba, który raport został wysłany wcześniej lub wprowadzić żadnych optymalizacji pod względem obsługi wiadomości. Hello kondycji klienta jest przetwarzanie wsadowe toohelp logiki z wydajnością. Gdy hello kondycji klienta jest aktywne, ponowną wewnętrznie aż do raportu hello zostaje potwierdzony przez magazynu kondycji hello lub programu alarmowego hello generuje raport nowszej z hello tego samego obiektu, właściwości i źródła.

Raporty dotyczące przejścia wymaga obsługi dokładne stanu. programu alarmowego Hello monitoruje niektóre warunki i raporty tylko wtedy, gdy zmianie hello warunków. Witaj do góry nogami takie podejście jest potrzebne są mniej raportów. Wadą interfejsu Hello jest złożone hello logiki programu alarmowego hello. programu alarmowego Hello muszą zachować warunki hello lub raportów hello, dzięki czemu można je kontrolowanego toodetermine zmian stanu. W tryb failover należy uważać z raportami dodane, ale nie zostały jeszcze wysłane toohello magazynu kondycji. numer sekwencyjny Hello musi być coraz większe. Jeśli nie, raporty hello odrzucone jako przestarzałe. W rzadkich przypadkach hello gdzie poniesienia utraty danych synchronizacji mogą być wymagane między hello stan osoby zgłaszającej hello i stan hello hello kondycji magazynu.

Raporty dotyczące przejścia sens dla usług raportowania, za pomocą `Partition` lub `CodePackageActivationContext`. Gdy hello lokalnego obiektu (repliki lub wdrożony pakiet usługi / wdrożonych aplikacji) jest usunięty, jego raporty zostaną również usunięte. To automatyczne oczyszczanie zwalnia hello potrzebę synchronizacja osoby zgłaszającej i magazynu kondycji. Jeśli raport hello jest partycji nadrzędnej lub aplikacji nadrzędnej, należy uważać, pracy awaryjnej tooavoid starych raportów w magazynie kondycji hello na. Logika musi zostać dodany stan hello toomaintain i wyczyść hello raportu z magazynu, jeśli nie jest już potrzebne.

## <a name="implement-health-reporting"></a>Implementowanie raportowania kondycji
Po zatwierdzeniu hello jednostki i raport szczegóły Wyczyść, wysyłania raportów o kondycji jest możliwe za pośrednictwem interfejsu API hello, programu PowerShell lub REST.

### <a name="api"></a>Interfejs API
tooreport za pośrednictwem hello interfejsu API, należy toocreate typu jednostki toohello określonego raportu kondycji, które mają tooreport na. Nadaj hello raport tooa kondycji klienta. Można również utworzyć informacje o kondycji i przekaż go toocorrect metod raportowania na `Partition` lub `CodePackageActivationContext` tooreport na bieżącym jednostek.

Witaj poniższy przykład przedstawia okresowych raportów z strażnika w ramach klastra hello. programu alarmowego Hello sprawdza, czy zasób zewnętrzny można uzyskać z w węźle. zasób Hello są wymagane przez aplikacji hello manifestu usługi. Jeśli hello zasób jest niedostępny, hello innych usług w aplikacji hello mogą nadal działać prawidłowo. W związku z tym hello raport jest wysyłany na powitania wdrożone usługi pakietu jednostki co 30 sekund.

```csharp
private static Uri ApplicationName = new Uri("fabric:/WordCount");
private static string ServiceManifestName = "WordCount.Service";
private static string NodeName = FabricRuntime.GetNodeContext().NodeName;
private static Timer ReportTimer = new Timer(new TimerCallback(SendReport), null, 30 * 1000, 30 * 1000);
private static FabricClient Client = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });

public static void SendReport(object obj)
{
    // Test whether hello resource can be accessed from hello node
    HealthState healthState = this.TestConnectivityToExternalResource();

    // Send report on deployed service package, as hello connectivity is needed by hello specific service manifest
    // and can be different on different nodes
    var deployedServicePackageHealthReport = new DeployedServicePackageHealthReport(
        ApplicationName,
        ServiceManifestName,
        NodeName,
        new HealthInformation("ExternalSourceWatcher", "Connectivity", healthState));

    // TODO: handle exception. Code omitted for snippet brevity.
    // Possible exceptions: FabricException with error codes
    // FabricHealthStaleReport (non-retryable, hello report is already queued on hello health client),
    // FabricHealthMaxReportsReached (retryable; user should retry with exponential delay until hello report is accepted).
    Client.HealthManager.ReportHealth(deployedServicePackageHealthReport);
}
```

### <a name="powershell"></a>PowerShell
Wysyłanie raportów o kondycji z  **ServiceFabric wysyłania*EntityType*HealthReport **.

Witaj poniższy przykład przedstawia okresowych raportów na wartościach Procesora w węźle. Raporty Hello mają być wysyłane co 30 sekund i mają czasu toolive wynosi dwie minuty. Jeśli wygasną, osoby zgłaszającej hello występują problemy, więc węzeł hello jest oceniane w błąd. Gdy hello Procesora jest powyżej wartości progowej, hello raportu ma stan kondycji ostrzeżenia. Jeśli hello Procesora pozostaje powyżej progu przez ponad hello skonfigurowany czas, będzie zgłaszane jako błąd. W przeciwnym razie osoby zgłaszającej hello wysyła kondycję OK.

```powershell
PS C:\> Send-ServiceFabricNodeHealthReport -NodeName Node.1 -HealthState Warning -SourceId PowershellWatcher -HealthProperty CPU -Description "CPU is above 80% threshold" -TimeToLiveSec 120

PS C:\> Get-ServiceFabricNodeHealth -NodeName Node.1
NodeName              : Node.1
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='CPU', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 5
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : CPU
                        HealthState           : Warning
                        SequenceNumber        : 130741236814913394
                        SentAt                : 4/21/2015 9:01:21 PM
                        ReceivedAt            : 4/21/2015 9:01:21 PM
                        TTL                   : 00:02:00
                        Description           : CPU is above 80% threshold
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:01:21 PM
```

Hello poniższy przykład raporty przejściowej ostrzeżenie dotyczące repliki. Najpierw pobiera identyfikator partycji: hello, a następnie hello identyfikator repliki usługi hello, który jest zainteresowana. Następnie wysyła raport z **PowershellWatcher** we właściwości hello **ResourceDependency**. Raport Hello ma znaczenie tylko dwóch minut, a zostanie usunięte z magazynu hello automatycznie.

```powershell
PS C:\> $partitionId = (Get-ServiceFabricPartition -ServiceName fabric:/WordCount/WordCount.Service).PartitionId

PS C:\> $replicaId = (Get-ServiceFabricReplica -PartitionId $partitionId | where {$_.ReplicaRole -eq "Primary"}).ReplicaId

PS C:\> Send-ServiceFabricReplicaHealthReport -PartitionId $partitionId -ReplicaId $replicaId -HealthState Warning -SourceId PowershellWatcher -HealthProperty ResourceDependency -Description "hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes." -TimeToLiveSec 120 -RemoveWhenExpired

PS C:\> Get-ServiceFabricReplicaHealth  -PartitionId $partitionId -ReplicaOrInstanceId $replicaId


PartitionId           : 8f82daff-eb68-4fd9-b631-7a37629e08c0
ReplicaId             : 130740415594605869
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='PowershellWatcher', Property='ResourceDependency', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130740768777734943
                        SentAt                : 4/21/2015 8:01:17 AM
                        ReceivedAt            : 4/21/2015 8:02:12 AM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/21/2015 8:02:12 AM

                        SourceId              : PowershellWatcher
                        Property              : ResourceDependency
                        HealthState           : Warning
                        SequenceNumber        : 130741243777723555
                        SentAt                : 4/21/2015 9:12:57 PM
                        ReceivedAt            : 4/21/2015 9:12:57 PM
                        TTL                   : 00:02:00
                        Description           : hello external resource that hello primary is using has been rebooted at 4/21/2015 9:01:21 PM. Expect processing delays for a few minutes.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : ->Warning = 4/21/2015 9:12:32 PM
```

### <a name="rest"></a>REST
Wysyłanie raportów o kondycji za pomocą usługi REST z żądania POST, przejdź toohello potrzeby jednostki, które ma w opis raportu kondycji hello treści hello. Na przykład, zobacz, jak REST toosend [klastra raportów o kondycji](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-cluster) lub [raportów o kondycji usługi](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service). Obsługiwane są wszystkie jednostki.

## <a name="next-steps"></a>Następne kroki
Na podstawie danych kondycji hello, moduły zapisujące usługi i Administratorzy klastra/aplikacji można traktować informacji hello tooconsume sposobów. Na przykład można ustawić alerty oparte na kondycji stanu toocatch poważne problemy, zanim one powodować awarie. Administratorzy mogą również skonfigurować naprawy systemów toofix problemów automatycznie.

[Wprowadzenie tooService kondycji sieci szkieletowej monitorowania](service-fabric-health-introduction.md)

[Wyświetl raporty dotyczące kondycji sieci szkieletowej usług](service-fabric-view-entities-aggregated-health.md)

[Jak tooreport i zaznacz pole wyboru usługi kondycji](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Użyj systemowych raportów kondycji do rozwiązywania problemów](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Monitorowanie i diagnozowania usług lokalnie](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Uaktualnianie aplikacji sieci szkieletowej usług](service-fabric-application-upgrade.md)

