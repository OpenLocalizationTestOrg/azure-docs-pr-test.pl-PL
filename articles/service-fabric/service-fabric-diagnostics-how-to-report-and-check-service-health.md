---
title: "aaaReport i sprawdzenie kondycji z sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak raporty dotyczące kondycji toosend w kodzie usługi i jak udostępnia toocheck hello kondycji usługi za pomocą narzędzia do monitorowania kondycji hello tej sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: mfussell
editor: 
ms.assetid: 7c712c22-d333-44bc-b837-d0b3603d9da8
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: bcb838fefe3f2054447e1731d709e455560260e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="report-and-check-service-health"></a>Tworzenie raportów i sprawdzanie kondycji usług
W przypadku wystąpienia problemów z usługami Twoje możliwości toorespond tooand poprawka zdarzenia i awarie jest zależna od problemów związanych z możliwością toodetect hello szybko. Jeśli raport menedżera kondycji sieci szkieletowej usług Azure toohello problemów i błędów w kodzie usługi można użyć kondycji standardowych narzędzi, że Usługa Service Fabric realizuje stan kondycji hello toocheck monitorowania.

Istnieją trzy sposoby raportowania kondycji z usługi hello:

* Użyj [partycji](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) lub [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) obiektów.  
  Można użyć hello `Partition` i `CodePackageActivationContext` obiekty kondycji hello tooreport elementów, które są częścią hello bieżącego kontekstu. Na przykład kod, który działa jako część repliki można raport kondycji tylko o tej repliki, partycji hello, że należy on do i aplikacji hello, która jest częścią.
* Użyj `FabricClient`.   
  Można użyć `FabricClient` tooreport kondycji z kodu usługi hello Jeśli hello klastra nie jest [bezpiecznego](service-fabric-cluster-security.md) lub jeśli hello jest uruchomiona z uprawnieniami administratora. Większość przypadków ze świata rzeczywistego nie za pomocą niezabezpieczonego klastrów, lub Udostępnij uprawnień administratora. Z `FabricClient`, mogą raportować kondycję na każda jednostka, która jest częścią klastra hello. Najlepiej, jeśli jednak kodu usługi należy wysłać tylko raporty, które są powiązane tooits własnych kondycji.
* Użyj hello interfejsów API REST poziomie hello klastra, aplikacji, wdrożonych aplikacji, usługi, pakiet usługi, partycji, repliki lub węzeł. Może to być kondycję tooreport używanych z znajdujące się w kontenerze.

W tym artykule przedstawiono przykład, w którym Raporty kondycji z hello usługi kodu. przykład Witaj pokazuje też, jak można stan kondycji hello używane toocheck hello narzędzi dostarczonych przez sieć szkieletowa usług. W tym artykule jest zamierzone toobe kondycję toohello szybkie wprowadzenie możliwości sieci szkieletowej usług monitorowania. Aby uzyskać szczegółowe informacje można znaleźć hello serii szczegółowe artykułów na temat kondycji rozpoczynających się od hello łącza na końcu hello w tym artykule.

## <a name="prerequisites"></a>Wymagania wstępne
Musi być zainstalowane następujące hello:

* Visual Studio 2015 lub Visual Studio 2017 r.
* Usługa SDK sieci szkieletowej

## <a name="toocreate-a-local-secure-dev-cluster"></a>toocreate klastra lokalnego bezpiecznego deweloperów
* Otwórz program PowerShell z uprawnieniami administratora, a następnie uruchom następujące polecenia hello:

![Jak polecenia przedstawiające toocreate klastra bezpiecznego deweloperów](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a>toodeploy aplikacji i sprawdź jej kondycję
1. Otwórz program Visual Studio jako administrator.
2. Tworzenie projektu przy użyciu hello **usługi Stateful** szablonu.
   
    ![Tworzenie aplikacji platformy Service Fabric przy Stateful usługi](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. Naciśnij klawisz **F5** aplikacji hello toorun w trybie debugowania. Aplikacja Hello jest wdrożone toohello klastra lokalnego.
4. Po uruchomieniu aplikacji hello, kliknij prawym przyciskiem myszy ikonę Menedżera klastra lokalnego hello w obszarze powiadomień hello i wybierz **Zarządzaj klastrem lokalnym** z tooopen menu skrótów hello Service Fabric Explorer.
   
    ![Otwórz Eksploratora usługi sieć szkieletowa z obszaru powiadomień](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. Kondycja aplikacji Hello powinna być wyświetlana tak jak ten obraz. W tej chwili aplikacji hello powinna być w dobrej kondycji bez błędów.
   
    ![Aplikacja działa prawidłowo w narzędziu Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. Możesz również sprawdzić kondycję hello przy użyciu programu PowerShell. Można użyć ```Get-ServiceFabricApplicationHealth``` toocheck kondycji aplikacji, a można użyć ```Get-ServiceFabricServiceHealth``` toocheck usługi kondycji. Witaj raport o kondycji dla hello tej samej aplikacji w programie PowerShell jest do tego obrazu.
   
    ![Aplikacja działa prawidłowo w programie PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a>Kod usługi tooyour tooadd kondycji niestandardowe zdarzenia
Szablony projektu sieci szkieletowej usług Hello w programie Visual Studio zawiera przykładowy kod. Witaj poniższej procedurze pokazano, jak mogą raportować kondycję niestandardowych zdarzeń w kodzie usługi. Raporty takie wyświetlane automatycznie w hello standardowych narzędzi do monitorowania, czy Usługa Service Fabric realizuje, takich jak Service Fabric Explorer, widok kondycji portalu Azure i programu PowerShell kondycji.

1. Otwórz ponownie aplikacji hello, utworzony wcześniej w programie Visual Studio lub Utwórz nową aplikację przy użyciu hello **usługi Stateful** szablonu Visual Studio.
2. Otwórz plik Stateful1.cs hello i Znajdź hello `myDictionary.TryGetValueAsync` wywołania w hello `RunAsync` metody. Widać, że ta metoda zwraca `result` blokad hello bieżącą wartość licznika hello, ponieważ hello klucza w tej aplikacji jest tookeep bieżącą liczbę. Jeśli była to rzeczywista aplikacji i brak hello wyniku reprezentowane awarii, odpowiedni będzie tooflag tego zdarzenia.
3. tooreport zdarzenie kondycji, jeśli brak hello wyniku reprezentuje awaria, Dodaj hello następujące kroki.
   
    a. Dodaj hello `System.Fabric.Health` pliku Stateful1.cs toohello przestrzeni nazw.
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    b. Dodaj następującego kodu po hello hello `myDictionary.TryGetValueAsync` wywołania
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    Firma Microsoft raport kondycji repliki, ponieważ jest raportowany przez usługi stanowej. Witaj `HealthInformation` parametr zapisuje informacje o problemie kondycji hello, który jest raportowany.
   
    Jeśli została utworzona usługi bezstanowej, użyj następującego kodu hello
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. Jeśli usługa jest uruchomiona z uprawnieniami administratora lub jeśli hello klastra nie jest [bezpiecznego](service-fabric-cluster-security.md), można również użyć `FabricClient` tooreport kondycji, jak pokazano w hello następujące kroki.  
   
    a. Utwórz hello `FabricClient` wystąpienia po hello `var myDictionary` deklaracji.
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    b. Dodaj następującego kodu po hello hello `myDictionary.TryGetValueAsync` wywołania.
   
    ```csharp
    if (!result.HasValue)
    {
       var replicaHealthReport = new StatefulServiceReplicaHealthReport(
            this.Context.PartitionId,
            this.Context.ReplicaId,
            new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error));
        fabricClient.HealthManager.ReportHealth(replicaHealthReport);
    }
    ```
5. Załóżmy symulować tego błędu i wyświetlić je w narzędziach do monitorowania kondycji hello. Błąd hello toosimulate, komentarz hello pierwszy wiersz kondycji hello kod dodanego wcześniej raportowania. Po komentarz hello pierwszy wiersz, hello kod będzie wyglądać hello poniższy przykład.
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   Ten kod uruchamia raport o kondycji hello zawsze `RunAsync` wykonuje. Po wprowadzeniu zmiany hello naciśnij **F5** toorun hello aplikacji.
6. Po uruchomieniu aplikacji hello Otwórz Eksploratora usługi sieć szkieletowa toocheck hello kondycji aplikacji hello. Teraz, Service Fabric Explorer pokazuje, że aplikacja hello jest zła. Jest to spowodowane hello błąd, który został zgłoszony z kodu hello, że dodane wcześniej.
   
    ![Zła aplikacji w narzędziu Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. W przypadku wybrania hello repliki podstawowej w widoku drzewa hello Service Fabric Explorer, zostanie wyświetlone **kondycja** zbyt wskazuje błąd. Service Fabric Explorer wyświetla również szczegółowe informacje, które zostały dodane toohello raport o kondycji hello `HealthInformation` parametru w kodzie hello. Widać hello tego samego raportów o kondycji w programie PowerShell i hello portalu Azure.
   
    ![Kondycja repliki w narzędziu Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

Ten raport pozostaje w Menedżera kondycji hello, dopóki nie został on zastąpiony przez inny raport lub do momentu usunięcia tej repliki. Ponieważ firma Microsoft nie określono `TimeToLive` dla tego raportu kondycji w hello `HealthInformation` obiektu raportu hello nigdy nie wygasa.

Zaleca się, że kondycji należy podać na najbardziej szczegółowym poziomie hello, w tym przypadku jest hello repliki. Można również raporty kondycji dotyczące `Partition`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

Kondycja tooreport na `Application`, `DeployedApplication`, i `DeployedServicePackage`, użyj `CodePackageActivationContext`.

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a>Następne kroki
* [Nowości dotyczące kondycji sieci szkieletowej usług](service-fabric-health-introduction.md)
* [Interfejs API REST dla raportowania kondycji usługi](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [Interfejs API REST dla raportowania kondycji aplikacji](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

