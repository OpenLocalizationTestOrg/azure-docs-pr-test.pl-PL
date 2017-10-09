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
# <a name="report-and-check-service-health"></a><span data-ttu-id="dc7ae-103">Tworzenie raportów i sprawdzanie kondycji usług</span><span class="sxs-lookup"><span data-stu-id="dc7ae-103">Report and check service health</span></span>
<span data-ttu-id="dc7ae-104">W przypadku wystąpienia problemów z usługami Twoje możliwości toorespond tooand poprawka zdarzenia i awarie jest zależna od problemów związanych z możliwością toodetect hello szybko.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-104">When your services encounter problems, your ability toorespond tooand fix incidents and outages depends on your ability toodetect hello issues quickly.</span></span> <span data-ttu-id="dc7ae-105">Jeśli raport menedżera kondycji sieci szkieletowej usług Azure toohello problemów i błędów w kodzie usługi można użyć kondycji standardowych narzędzi, że Usługa Service Fabric realizuje stan kondycji hello toocheck monitorowania.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-105">If you report problems and failures toohello Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides toocheck hello health status.</span></span>

<span data-ttu-id="dc7ae-106">Istnieją trzy sposoby raportowania kondycji z usługi hello:</span><span class="sxs-lookup"><span data-stu-id="dc7ae-106">There are three ways that you can report health from hello service:</span></span>

* <span data-ttu-id="dc7ae-107">Użyj [partycji](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) lub [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) obiektów.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="dc7ae-108">Można użyć hello `Partition` i `CodePackageActivationContext` obiekty kondycji hello tooreport elementów, które są częścią hello bieżącego kontekstu.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-108">You can use hello `Partition` and `CodePackageActivationContext` objects tooreport hello health of elements that are part of hello current context.</span></span> <span data-ttu-id="dc7ae-109">Na przykład kod, który działa jako część repliki można raport kondycji tylko o tej repliki, partycji hello, że należy on do i aplikacji hello, która jest częścią.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-109">For example, code that runs as part of a replica can report health only on that replica, hello partition that it belongs to, and hello application that it is a part of.</span></span>
* <span data-ttu-id="dc7ae-110">Użyj `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="dc7ae-111">Można użyć `FabricClient` tooreport kondycji z kodu usługi hello Jeśli hello klastra nie jest [bezpiecznego](service-fabric-cluster-security.md) lub jeśli hello jest uruchomiona z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-111">You can use `FabricClient` tooreport health from hello service code if hello cluster is not [secure](service-fabric-cluster-security.md) or if hello service is running with admin privileges.</span></span> <span data-ttu-id="dc7ae-112">Większość przypadków ze świata rzeczywistego nie za pomocą niezabezpieczonego klastrów, lub Udostępnij uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="dc7ae-113">Z `FabricClient`, mogą raportować kondycję na każda jednostka, która jest częścią klastra hello.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-113">With `FabricClient`, you can report health on any entity that is a part of hello cluster.</span></span> <span data-ttu-id="dc7ae-114">Najlepiej, jeśli jednak kodu usługi należy wysłać tylko raporty, które są powiązane tooits własnych kondycji.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-114">Ideally, however, service code should only send reports that are related tooits own health.</span></span>
* <span data-ttu-id="dc7ae-115">Użyj hello interfejsów API REST poziomie hello klastra, aplikacji, wdrożonych aplikacji, usługi, pakiet usługi, partycji, repliki lub węzeł.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-115">Use hello REST APIs at hello cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="dc7ae-116">Może to być kondycję tooreport używanych z znajdujące się w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-116">This can be used tooreport health from within a container.</span></span>

<span data-ttu-id="dc7ae-117">W tym artykule przedstawiono przykład, w którym Raporty kondycji z hello usługi kodu.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-117">This article walks you through an example that reports health from hello service code.</span></span> <span data-ttu-id="dc7ae-118">przykład Witaj pokazuje też, jak można stan kondycji hello używane toocheck hello narzędzi dostarczonych przez sieć szkieletowa usług.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-118">hello example also shows how hello tools provided by Service Fabric can be used toocheck hello health status.</span></span> <span data-ttu-id="dc7ae-119">W tym artykule jest zamierzone toobe kondycję toohello szybkie wprowadzenie możliwości sieci szkieletowej usług monitorowania.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-119">This article is intended toobe a quick introduction toohello health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="dc7ae-120">Aby uzyskać szczegółowe informacje można znaleźć hello serii szczegółowe artykułów na temat kondycji rozpoczynających się od hello łącza na końcu hello w tym artykule.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-120">For more detailed information, you can read hello series of in-depth articles about health that start with hello link at hello end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc7ae-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="dc7ae-121">Prerequisites</span></span>
<span data-ttu-id="dc7ae-122">Musi być zainstalowane następujące hello:</span><span class="sxs-lookup"><span data-stu-id="dc7ae-122">You must have hello following installed:</span></span>

* <span data-ttu-id="dc7ae-123">Visual Studio 2015 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="dc7ae-124">Usługa SDK sieci szkieletowej</span><span class="sxs-lookup"><span data-stu-id="dc7ae-124">Service Fabric SDK</span></span>

## <a name="toocreate-a-local-secure-dev-cluster"></a><span data-ttu-id="dc7ae-125">toocreate klastra lokalnego bezpiecznego deweloperów</span><span class="sxs-lookup"><span data-stu-id="dc7ae-125">toocreate a local secure dev cluster</span></span>
* <span data-ttu-id="dc7ae-126">Otwórz program PowerShell z uprawnieniami administratora, a następnie uruchom następujące polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="dc7ae-126">Open PowerShell with admin privileges, and run hello following commands:</span></span>

![Jak polecenia przedstawiające toocreate klastra bezpiecznego deweloperów](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="toodeploy-an-application-and-check-its-health"></a><span data-ttu-id="dc7ae-128">toodeploy aplikacji i sprawdź jej kondycję</span><span class="sxs-lookup"><span data-stu-id="dc7ae-128">toodeploy an application and check its health</span></span>
1. <span data-ttu-id="dc7ae-129">Otwórz program Visual Studio jako administrator.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="dc7ae-130">Tworzenie projektu przy użyciu hello **usługi Stateful** szablonu.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-130">Create a project by using hello **Stateful Service** template.</span></span>
   
    ![Tworzenie aplikacji platformy Service Fabric przy Stateful usługi](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="dc7ae-132">Naciśnij klawisz **F5** aplikacji hello toorun w trybie debugowania.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-132">Press **F5** toorun hello application in debug mode.</span></span> <span data-ttu-id="dc7ae-133">Aplikacja Hello jest wdrożone toohello klastra lokalnego.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-133">hello application is deployed toohello local cluster.</span></span>
4. <span data-ttu-id="dc7ae-134">Po uruchomieniu aplikacji hello, kliknij prawym przyciskiem myszy ikonę Menedżera klastra lokalnego hello w obszarze powiadomień hello i wybierz **Zarządzaj klastrem lokalnym** z tooopen menu skrótów hello Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-134">After hello application is running, right-click hello Local Cluster Manager icon in hello notification area and select **Manage Local Cluster** from hello shortcut menu tooopen Service Fabric Explorer.</span></span>
   
    ![Otwórz Eksploratora usługi sieć szkieletowa z obszaru powiadomień](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="dc7ae-136">Kondycja aplikacji Hello powinna być wyświetlana tak jak ten obraz.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-136">hello application health should be displayed as in this image.</span></span> <span data-ttu-id="dc7ae-137">W tej chwili aplikacji hello powinna być w dobrej kondycji bez błędów.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-137">At this time, hello application should be healthy with no errors.</span></span>
   
    ![Aplikacja działa prawidłowo w narzędziu Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="dc7ae-139">Możesz również sprawdzić kondycję hello przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-139">You can also check hello health by using PowerShell.</span></span> <span data-ttu-id="dc7ae-140">Można użyć ```Get-ServiceFabricApplicationHealth``` toocheck kondycji aplikacji, a można użyć ```Get-ServiceFabricServiceHealth``` toocheck usługi kondycji.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-140">You can use ```Get-ServiceFabricApplicationHealth``` toocheck an application's health, and you can use ```Get-ServiceFabricServiceHealth``` toocheck a service's health.</span></span> <span data-ttu-id="dc7ae-141">Witaj raport o kondycji dla hello tej samej aplikacji w programie PowerShell jest do tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-141">hello health report for hello same application in PowerShell is in this image.</span></span>
   
    ![Aplikacja działa prawidłowo w programie PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="tooadd-custom-health-events-tooyour-service-code"></a><span data-ttu-id="dc7ae-143">Kod usługi tooyour tooadd kondycji niestandardowe zdarzenia</span><span class="sxs-lookup"><span data-stu-id="dc7ae-143">tooadd custom health events tooyour service code</span></span>
<span data-ttu-id="dc7ae-144">Szablony projektu sieci szkieletowej usług Hello w programie Visual Studio zawiera przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-144">hello Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="dc7ae-145">Witaj poniższej procedurze pokazano, jak mogą raportować kondycję niestandardowych zdarzeń w kodzie usługi.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-145">hello following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="dc7ae-146">Raporty takie wyświetlane automatycznie w hello standardowych narzędzi do monitorowania, czy Usługa Service Fabric realizuje, takich jak Service Fabric Explorer, widok kondycji portalu Azure i programu PowerShell kondycji.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-146">Such reports show up automatically in hello standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="dc7ae-147">Otwórz ponownie aplikacji hello, utworzony wcześniej w programie Visual Studio lub Utwórz nową aplikację przy użyciu hello **usługi Stateful** szablonu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-147">Reopen hello application that you created previously in Visual Studio, or create a new application by using hello **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="dc7ae-148">Otwórz plik Stateful1.cs hello i Znajdź hello `myDictionary.TryGetValueAsync` wywołania w hello `RunAsync` metody.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-148">Open hello Stateful1.cs file, and find hello `myDictionary.TryGetValueAsync` call in hello `RunAsync` method.</span></span> <span data-ttu-id="dc7ae-149">Widać, że ta metoda zwraca `result` blokad hello bieżącą wartość licznika hello, ponieważ hello klucza w tej aplikacji jest tookeep bieżącą liczbę.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-149">You can see that this method returns a `result` that holds hello current value of hello counter because hello key logic in this application is tookeep a count running.</span></span> <span data-ttu-id="dc7ae-150">Jeśli była to rzeczywista aplikacji i brak hello wyniku reprezentowane awarii, odpowiedni będzie tooflag tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-150">If this were a real application, and if hello lack of result represented a failure, you would want tooflag that event.</span></span>
3. <span data-ttu-id="dc7ae-151">tooreport zdarzenie kondycji, jeśli brak hello wyniku reprezentuje awaria, Dodaj hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-151">tooreport a health event when hello lack of result represents a failure, add hello following steps.</span></span>
   
    <span data-ttu-id="dc7ae-152">a.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-152">a.</span></span> <span data-ttu-id="dc7ae-153">Dodaj hello `System.Fabric.Health` pliku Stateful1.cs toohello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-153">Add hello `System.Fabric.Health` namespace toohello Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="dc7ae-154">b.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-154">b.</span></span> <span data-ttu-id="dc7ae-155">Dodaj następującego kodu po hello hello `myDictionary.TryGetValueAsync` wywołania</span><span class="sxs-lookup"><span data-stu-id="dc7ae-155">Add hello following code after hello `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="dc7ae-156">Firma Microsoft raport kondycji repliki, ponieważ jest raportowany przez usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="dc7ae-157">Witaj `HealthInformation` parametr zapisuje informacje o problemie kondycji hello, który jest raportowany.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-157">hello `HealthInformation` parameter stores information about hello health issue that's being reported.</span></span>
   
    <span data-ttu-id="dc7ae-158">Jeśli została utworzona usługi bezstanowej, użyj następującego kodu hello</span><span class="sxs-lookup"><span data-stu-id="dc7ae-158">If you had created a stateless service, use hello following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="dc7ae-159">Jeśli usługa jest uruchomiona z uprawnieniami administratora lub jeśli hello klastra nie jest [bezpiecznego](service-fabric-cluster-security.md), można również użyć `FabricClient` tooreport kondycji, jak pokazano w hello następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-159">If your service is running with admin privileges or if hello cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` tooreport health as shown in hello following steps.</span></span>  
   
    <span data-ttu-id="dc7ae-160">a.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-160">a.</span></span> <span data-ttu-id="dc7ae-161">Utwórz hello `FabricClient` wystąpienia po hello `var myDictionary` deklaracji.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-161">Create hello `FabricClient` instance after hello `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="dc7ae-162">b.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-162">b.</span></span> <span data-ttu-id="dc7ae-163">Dodaj następującego kodu po hello hello `myDictionary.TryGetValueAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-163">Add hello following code after hello `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="dc7ae-164">Załóżmy symulować tego błędu i wyświetlić je w narzędziach do monitorowania kondycji hello.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-164">Let's simulate this failure and see it show up in hello health monitoring tools.</span></span> <span data-ttu-id="dc7ae-165">Błąd hello toosimulate, komentarz hello pierwszy wiersz kondycji hello kod dodanego wcześniej raportowania.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-165">toosimulate hello failure, comment out hello first line in hello health reporting code that you added earlier.</span></span> <span data-ttu-id="dc7ae-166">Po komentarz hello pierwszy wiersz, hello kod będzie wyglądać hello poniższy przykład.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-166">After you comment out hello first line, hello code will look like hello following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="dc7ae-167">Ten kod uruchamia raport o kondycji hello zawsze `RunAsync` wykonuje.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-167">This code fires hello health report each time `RunAsync` executes.</span></span> <span data-ttu-id="dc7ae-168">Po wprowadzeniu zmiany hello naciśnij **F5** toorun hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-168">After you make hello change, press **F5** toorun hello application.</span></span>
6. <span data-ttu-id="dc7ae-169">Po uruchomieniu aplikacji hello Otwórz Eksploratora usługi sieć szkieletowa toocheck hello kondycji aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-169">After hello application is running, open Service Fabric Explorer toocheck hello health of hello application.</span></span> <span data-ttu-id="dc7ae-170">Teraz, Service Fabric Explorer pokazuje, że aplikacja hello jest zła.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-170">This time, Service Fabric Explorer shows that hello application is unhealthy.</span></span> <span data-ttu-id="dc7ae-171">Jest to spowodowane hello błąd, który został zgłoszony z kodu hello, że dodane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-171">This is because of hello error that was reported from hello code that we added previously.</span></span>
   
    ![Zła aplikacji w narzędziu Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="dc7ae-173">W przypadku wybrania hello repliki podstawowej w widoku drzewa hello Service Fabric Explorer, zostanie wyświetlone **kondycja** zbyt wskazuje błąd.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-173">If you select hello primary replica in hello tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="dc7ae-174">Service Fabric Explorer wyświetla również szczegółowe informacje, które zostały dodane toohello raport o kondycji hello `HealthInformation` parametru w kodzie hello.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-174">Service Fabric Explorer also displays hello health report details that were added toohello `HealthInformation` parameter in hello code.</span></span> <span data-ttu-id="dc7ae-175">Widać hello tego samego raportów o kondycji w programie PowerShell i hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-175">You can see hello same health reports in PowerShell and hello Azure portal.</span></span>
   
    ![Kondycja repliki w narzędziu Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="dc7ae-177">Ten raport pozostaje w Menedżera kondycji hello, dopóki nie został on zastąpiony przez inny raport lub do momentu usunięcia tej repliki.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-177">This report remains in hello health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="dc7ae-178">Ponieważ firma Microsoft nie określono `TimeToLive` dla tego raportu kondycji w hello `HealthInformation` obiektu raportu hello nigdy nie wygasa.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-178">Because we did not set `TimeToLive` for this health report in hello `HealthInformation` object, hello report never expires.</span></span>

<span data-ttu-id="dc7ae-179">Zaleca się, że kondycji należy podać na najbardziej szczegółowym poziomie hello, w tym przypadku jest hello repliki.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-179">We recommend that health should be reported on hello most granular level, which in this case is hello replica.</span></span> <span data-ttu-id="dc7ae-180">Można również raporty kondycji dotyczące `Partition`.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="dc7ae-181">Kondycja tooreport na `Application`, `DeployedApplication`, i `DeployedServicePackage`, użyj `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="dc7ae-181">tooreport health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="dc7ae-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dc7ae-182">Next steps</span></span>
* [<span data-ttu-id="dc7ae-183">Nowości dotyczące kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="dc7ae-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="dc7ae-184">Interfejs API REST dla raportowania kondycji usługi</span><span class="sxs-lookup"><span data-stu-id="dc7ae-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="dc7ae-185">Interfejs API REST dla raportowania kondycji aplikacji</span><span class="sxs-lookup"><span data-stu-id="dc7ae-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

