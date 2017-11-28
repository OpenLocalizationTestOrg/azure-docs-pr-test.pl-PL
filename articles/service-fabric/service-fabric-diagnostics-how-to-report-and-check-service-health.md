---
title: "Raport i Sprawdź kondycję z sieci szkieletowej usług Azure | Dokumentacja firmy Microsoft"
description: "Więcej informacji, sposobu wysyłania raportów o kondycji z kodu usługi i sprawdzać stan usługi za pomocą narzędzi monitorowania kondycji, które zapewnia sieć szkieletowa usług Azure."
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
ms.openlocfilehash: 83981d5bec14c06c509f1a8a4153dc23298f5ce0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="report-and-check-service-health"></a><span data-ttu-id="24f82-103">Tworzenie raportów i sprawdzanie kondycji usług</span><span class="sxs-lookup"><span data-stu-id="24f82-103">Report and check service health</span></span>
<span data-ttu-id="24f82-104">W przypadku wystąpienia problemów z usługami możliwość uwzględniał i naprawić zdarzenia i awarie zależy od możliwości szybko wykrywać problemy.</span><span class="sxs-lookup"><span data-stu-id="24f82-104">When your services encounter problems, your ability to respond to and fix incidents and outages depends on your ability to detect the issues quickly.</span></span> <span data-ttu-id="24f82-105">Jeśli zgłaszanie problemów i błędów Menedżera kondycji sieci szkieletowej usług Azure w kodzie usługi, możesz użyć standardowego monitorowania narzędzi dostarczanych do sprawdzania stanu kondycji sieci szkieletowej usług kondycji.</span><span class="sxs-lookup"><span data-stu-id="24f82-105">If you report problems and failures to the Azure Service Fabric health manager from your service code, you can use standard health monitoring tools that Service Fabric provides to check the health status.</span></span>

<span data-ttu-id="24f82-106">Istnieją trzy sposoby raportowania kondycji usługi:</span><span class="sxs-lookup"><span data-stu-id="24f82-106">There are three ways that you can report health from the service:</span></span>

* <span data-ttu-id="24f82-107">Użyj [partycji](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) lub [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) obiektów.</span><span class="sxs-lookup"><span data-stu-id="24f82-107">Use [Partition](https://docs.microsoft.com/dotnet/api/system.fabric.istatefulservicepartition) or [CodePackageActivationContext](https://docs.microsoft.com/dotnet/api/system.fabric.codepackageactivationcontext) objects.</span></span>  
  <span data-ttu-id="24f82-108">Można użyć `Partition` i `CodePackageActivationContext` obiektów do raportu kondycji elementów, które są częścią bieżącego kontekstu.</span><span class="sxs-lookup"><span data-stu-id="24f82-108">You can use the `Partition` and `CodePackageActivationContext` objects to report the health of elements that are part of the current context.</span></span> <span data-ttu-id="24f82-109">Na przykład kod, który działa jako część repliki może raportować kondycję tylko w tej repliki, należącego do partycji i aplikacji, która jest częścią.</span><span class="sxs-lookup"><span data-stu-id="24f82-109">For example, code that runs as part of a replica can report health only on that replica, the partition that it belongs to, and the application that it is a part of.</span></span>
* <span data-ttu-id="24f82-110">Użyj `FabricClient`.</span><span class="sxs-lookup"><span data-stu-id="24f82-110">Use `FabricClient`.</span></span>   
  <span data-ttu-id="24f82-111">Można użyć `FabricClient` do raportu kondycji z kodem usługi, jeśli klaster nie jest [bezpiecznego](service-fabric-cluster-security.md) lub jeśli usługa jest uruchomiona z uprawnieniami administratora.</span><span class="sxs-lookup"><span data-stu-id="24f82-111">You can use `FabricClient` to report health from the service code if the cluster is not [secure](service-fabric-cluster-security.md) or if the service is running with admin privileges.</span></span> <span data-ttu-id="24f82-112">Większość przypadków ze świata rzeczywistego nie za pomocą niezabezpieczonego klastrów, lub Udostępnij uprawnień administratora.</span><span class="sxs-lookup"><span data-stu-id="24f82-112">Most real-world scenarios do not use unsecured clusters, or provide admin privileges.</span></span> <span data-ttu-id="24f82-113">Z `FabricClient`, mogą raportować kondycję na każda jednostka, która jest częścią klastra.</span><span class="sxs-lookup"><span data-stu-id="24f82-113">With `FabricClient`, you can report health on any entity that is a part of the cluster.</span></span> <span data-ttu-id="24f82-114">Najlepiej, jeśli jednak kodu usługi należy wysłać tylko raporty, które są związane z własną kondycji.</span><span class="sxs-lookup"><span data-stu-id="24f82-114">Ideally, however, service code should only send reports that are related to its own health.</span></span>
* <span data-ttu-id="24f82-115">Użyć interfejsów API REST w klastra, aplikacji, wdrożonych aplikacji, usługi, pakiet usługi, partycji, repliki lub poziomy węzła.</span><span class="sxs-lookup"><span data-stu-id="24f82-115">Use the REST APIs at the cluster, application, deployed application, service, service package, partition, replica, or node levels.</span></span> <span data-ttu-id="24f82-116">Może to służyć do raportu kondycji z znajdujące się w kontenerze.</span><span class="sxs-lookup"><span data-stu-id="24f82-116">This can be used to report health from within a container.</span></span>

<span data-ttu-id="24f82-117">W tym artykule przedstawiono przykład, w którym Raporty kondycji z kodem usługi.</span><span class="sxs-lookup"><span data-stu-id="24f82-117">This article walks you through an example that reports health from the service code.</span></span> <span data-ttu-id="24f82-118">W przykładzie przedstawiono również sposób z narzędzi dostarczanych przez sieć szkieletowa usług może służyć do sprawdzania stanu kondycji.</span><span class="sxs-lookup"><span data-stu-id="24f82-118">The example also shows how the tools provided by Service Fabric can be used to check the health status.</span></span> <span data-ttu-id="24f82-119">Ten artykuł ma być szybkie wprowadzenie do monitorowania możliwości sieci szkieletowej usług kondycji.</span><span class="sxs-lookup"><span data-stu-id="24f82-119">This article is intended to be a quick introduction to the health monitoring capabilities of Service Fabric.</span></span> <span data-ttu-id="24f82-120">Aby uzyskać szczegółowe informacje można znaleźć serii szczegółowe artykułów na temat kondycji rozpoczynających się od łącza na końcu tego artykułu.</span><span class="sxs-lookup"><span data-stu-id="24f82-120">For more detailed information, you can read the series of in-depth articles about health that start with the link at the end of this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24f82-121">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="24f82-121">Prerequisites</span></span>
<span data-ttu-id="24f82-122">Musi być zainstalowane następujące oprogramowanie:</span><span class="sxs-lookup"><span data-stu-id="24f82-122">You must have the following installed:</span></span>

* <span data-ttu-id="24f82-123">Visual Studio 2015 lub Visual Studio 2017 r.</span><span class="sxs-lookup"><span data-stu-id="24f82-123">Visual Studio 2015 or Visual Studio 2017</span></span>
* <span data-ttu-id="24f82-124">Usługa SDK sieci szkieletowej</span><span class="sxs-lookup"><span data-stu-id="24f82-124">Service Fabric SDK</span></span>

## <a name="to-create-a-local-secure-dev-cluster"></a><span data-ttu-id="24f82-125">Aby utworzyć klaster lokalny deweloperów bezpiecznego</span><span class="sxs-lookup"><span data-stu-id="24f82-125">To create a local secure dev cluster</span></span>
* <span data-ttu-id="24f82-126">Otwórz program PowerShell z uprawnieniami administratora i uruchom następujące polecenia:</span><span class="sxs-lookup"><span data-stu-id="24f82-126">Open PowerShell with admin privileges, and run the following commands:</span></span>

![Polecenia, które pokazują, jak utworzyć klaster bezpiecznego deweloperów](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-secure-dev-cluster.png)

## <a name="to-deploy-an-application-and-check-its-health"></a><span data-ttu-id="24f82-128">Aby wdrożyć aplikację i sprawdzić jego kondycji</span><span class="sxs-lookup"><span data-stu-id="24f82-128">To deploy an application and check its health</span></span>
1. <span data-ttu-id="24f82-129">Otwórz program Visual Studio jako administrator.</span><span class="sxs-lookup"><span data-stu-id="24f82-129">Open Visual Studio as an administrator.</span></span>
2. <span data-ttu-id="24f82-130">Tworzenie projektu za pomocą **usługi Stateful** szablonu.</span><span class="sxs-lookup"><span data-stu-id="24f82-130">Create a project by using the **Stateful Service** template.</span></span>
   
    ![Tworzenie aplikacji platformy Service Fabric przy Stateful usługi](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/create-stateful-service-application-dialog.png)
3. <span data-ttu-id="24f82-132">Naciśnij klawisz **F5** do uruchomienia aplikacji w trybie debugowania.</span><span class="sxs-lookup"><span data-stu-id="24f82-132">Press **F5** to run the application in debug mode.</span></span> <span data-ttu-id="24f82-133">Aplikacja jest wdrażana na lokalny klaster.</span><span class="sxs-lookup"><span data-stu-id="24f82-133">The application is deployed to the local cluster.</span></span>
4. <span data-ttu-id="24f82-134">Po uruchomieniu aplikacji, kliknij prawym przyciskiem myszy ikonę Local Cluster Manager w obszarze powiadomień i wybierz **Zarządzaj klastrem lokalnym** z menu skrótów, aby otworzyć Eksploratora usługi sieć szkieletowa.</span><span class="sxs-lookup"><span data-stu-id="24f82-134">After the application is running, right-click the Local Cluster Manager icon in the notification area and select **Manage Local Cluster** from the shortcut menu to open Service Fabric Explorer.</span></span>
   
    ![Otwórz Eksploratora usługi sieć szkieletowa z obszaru powiadomień](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/LaunchSFX.png)
5. <span data-ttu-id="24f82-136">Kondycja aplikacji powinna być wyświetlana tak jak ten obraz.</span><span class="sxs-lookup"><span data-stu-id="24f82-136">The application health should be displayed as in this image.</span></span> <span data-ttu-id="24f82-137">W tej chwili aplikacja powinna być w dobrej kondycji bez błędów.</span><span class="sxs-lookup"><span data-stu-id="24f82-137">At this time, the application should be healthy with no errors.</span></span>
   
    ![Aplikacja działa prawidłowo w narzędziu Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-healthy-app.png)
6. <span data-ttu-id="24f82-139">Możesz również sprawdzić kondycję przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24f82-139">You can also check the health by using PowerShell.</span></span> <span data-ttu-id="24f82-140">Można użyć ```Get-ServiceFabricApplicationHealth``` można użyć do sprawdzenia kondycji aplikacji, a ```Get-ServiceFabricServiceHealth``` do sprawdzenia kondycji usługi.</span><span class="sxs-lookup"><span data-stu-id="24f82-140">You can use ```Get-ServiceFabricApplicationHealth``` to check an application's health, and you can use ```Get-ServiceFabricServiceHealth``` to check a service's health.</span></span> <span data-ttu-id="24f82-141">Raport o kondycji dla tej samej aplikacji w programie PowerShell jest do tego obrazu.</span><span class="sxs-lookup"><span data-stu-id="24f82-141">The health report for the same application in PowerShell is in this image.</span></span>
   
    ![Aplikacja działa prawidłowo w programie PowerShell](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/ps-healthy-app-report.png)

## <a name="to-add-custom-health-events-to-your-service-code"></a><span data-ttu-id="24f82-143">Aby dodać niestandardowe kondycji zdarzenia do kodu usługi</span><span class="sxs-lookup"><span data-stu-id="24f82-143">To add custom health events to your service code</span></span>
<span data-ttu-id="24f82-144">Szablony projektu sieci szkieletowej usług w programie Visual Studio zawiera przykładowy kod.</span><span class="sxs-lookup"><span data-stu-id="24f82-144">The Service Fabric project templates in Visual Studio contain sample code.</span></span> <span data-ttu-id="24f82-145">W poniższej procedurze pokazano, jak mogą raportować kondycję niestandardowych zdarzeń w kodzie usługi.</span><span class="sxs-lookup"><span data-stu-id="24f82-145">The following steps show how you can report custom health events from your service code.</span></span> <span data-ttu-id="24f82-146">Raporty takie wyświetlane automatycznie w standardowych narzędzi do monitorowania kondycji, czy Usługa Service Fabric realizuje, takich jak Service Fabric Explorer, widok kondycji portalu Azure i programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="24f82-146">Such reports show up automatically in the standard tools for health monitoring that Service Fabric provides, such as Service Fabric Explorer, Azure portal health view, and PowerShell.</span></span>

1. <span data-ttu-id="24f82-147">Otwórz ponownie aplikację utworzonego wcześniej w programie Visual Studio lub Utwórz nową aplikację przy użyciu **usługi Stateful** szablonu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="24f82-147">Reopen the application that you created previously in Visual Studio, or create a new application by using the **Stateful Service** Visual Studio template.</span></span>
2. <span data-ttu-id="24f82-148">Otwórz plik Stateful1.cs i Znajdź `myDictionary.TryGetValueAsync` wywołanie w `RunAsync` metody.</span><span class="sxs-lookup"><span data-stu-id="24f82-148">Open the Stateful1.cs file, and find the `myDictionary.TryGetValueAsync` call in the `RunAsync` method.</span></span> <span data-ttu-id="24f82-149">Widać, że ta metoda zwraca `result` zawierający bieżącą wartość licznika, ponieważ klucza logikę w tej aplikacji jest zachowanie wynik jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="24f82-149">You can see that this method returns a `result` that holds the current value of the counter because the key logic in this application is to keep a count running.</span></span> <span data-ttu-id="24f82-150">Jeśli była to rzeczywista aplikacji i brak wyniku reprezentowane awarii, czy chcesz Flaga tego zdarzenia.</span><span class="sxs-lookup"><span data-stu-id="24f82-150">If this were a real application, and if the lack of result represented a failure, you would want to flag that event.</span></span>
3. <span data-ttu-id="24f82-151">Aby zgłosić zdarzenie kondycji w przypadku braku wyników reprezentuje awarii, należy dodać następujące kroki.</span><span class="sxs-lookup"><span data-stu-id="24f82-151">To report a health event when the lack of result represents a failure, add the following steps.</span></span>
   
    <span data-ttu-id="24f82-152">a.</span><span class="sxs-lookup"><span data-stu-id="24f82-152">a.</span></span> <span data-ttu-id="24f82-153">Dodaj `System.Fabric.Health` przestrzeni nazw do pliku Stateful1.cs.</span><span class="sxs-lookup"><span data-stu-id="24f82-153">Add the `System.Fabric.Health` namespace to the Stateful1.cs file.</span></span>
   
    ```csharp
    using System.Fabric.Health;
    ```
   
    <span data-ttu-id="24f82-154">b.</span><span class="sxs-lookup"><span data-stu-id="24f82-154">b.</span></span> <span data-ttu-id="24f82-155">Dodaj następujący kod po `myDictionary.TryGetValueAsync` wywołania</span><span class="sxs-lookup"><span data-stu-id="24f82-155">Add the following code after the `myDictionary.TryGetValueAsync` call</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
    <span data-ttu-id="24f82-156">Firma Microsoft raport kondycji repliki, ponieważ jest raportowany przez usługi stanowej.</span><span class="sxs-lookup"><span data-stu-id="24f82-156">We report replica health because it's being reported from a stateful service.</span></span> <span data-ttu-id="24f82-157">`HealthInformation` Parametr zapisuje informacje o problemie kondycji, który jest raportowany.</span><span class="sxs-lookup"><span data-stu-id="24f82-157">The `HealthInformation` parameter stores information about the health issue that's being reported.</span></span>
   
    <span data-ttu-id="24f82-158">Jeśli chcesz utworzyć usługi bezstanowej, należy użyć poniższego kodu</span><span class="sxs-lookup"><span data-stu-id="24f82-158">If you had created a stateless service, use the following code</span></span>
   
    ```csharp
    if (!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportInstanceHealth(healthInformation);
    }
    ```
4. <span data-ttu-id="24f82-159">Jeśli usługa jest uruchomiona z uprawnieniami administratora lub klastra nie jest [bezpiecznego](service-fabric-cluster-security.md), można również użyć `FabricClient` do raportu kondycji, jak pokazano w poniższych krokach.</span><span class="sxs-lookup"><span data-stu-id="24f82-159">If your service is running with admin privileges or if the cluster is not [secure](service-fabric-cluster-security.md), you can also use `FabricClient` to report health as shown in the following steps.</span></span>  
   
    <span data-ttu-id="24f82-160">a.</span><span class="sxs-lookup"><span data-stu-id="24f82-160">a.</span></span> <span data-ttu-id="24f82-161">Utwórz `FabricClient` wystąpienie po `var myDictionary` deklaracji.</span><span class="sxs-lookup"><span data-stu-id="24f82-161">Create the `FabricClient` instance after the `var myDictionary` declaration.</span></span>
   
    ```csharp
    var fabricClient = new FabricClient(new FabricClientSettings() { HealthReportSendInterval = TimeSpan.FromSeconds(0) });
    ```
   
    <span data-ttu-id="24f82-162">b.</span><span class="sxs-lookup"><span data-stu-id="24f82-162">b.</span></span> <span data-ttu-id="24f82-163">Dodaj następujący kod po `myDictionary.TryGetValueAsync` wywołania.</span><span class="sxs-lookup"><span data-stu-id="24f82-163">Add the following code after the `myDictionary.TryGetValueAsync` call.</span></span>
   
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
5. <span data-ttu-id="24f82-164">Załóżmy symulować tego błędu i wyświetlić je w narzędziach do monitorowania kondycji.</span><span class="sxs-lookup"><span data-stu-id="24f82-164">Let's simulate this failure and see it show up in the health monitoring tools.</span></span> <span data-ttu-id="24f82-165">Aby symulować niepowodzenia komentarz w pierwszym wierszu kodu raportowania kondycji dodanego wcześniej.</span><span class="sxs-lookup"><span data-stu-id="24f82-165">To simulate the failure, comment out the first line in the health reporting code that you added earlier.</span></span> <span data-ttu-id="24f82-166">Po komentarz pierwszy wiersz, kod będzie wyglądać jak w następującym przykładzie.</span><span class="sxs-lookup"><span data-stu-id="24f82-166">After you comment out the first line, the code will look like the following example.</span></span>
   
    ```csharp
    //if(!result.HasValue)
    {
        HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
        this.Partition.ReportReplicaHealth(healthInformation);
    }
    ```
   <span data-ttu-id="24f82-167">Ten kod generowane raport o kondycji, w każdym `RunAsync` wykonuje.</span><span class="sxs-lookup"><span data-stu-id="24f82-167">This code fires the health report each time `RunAsync` executes.</span></span> <span data-ttu-id="24f82-168">Po wprowadzeniu zmian, naciśnij klawisz **F5** do uruchomienia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24f82-168">After you make the change, press **F5** to run the application.</span></span>
6. <span data-ttu-id="24f82-169">Po uruchomieniu aplikacji, otwórz Eksploratora usługi sieć szkieletowa, aby sprawdzić kondycji tej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="24f82-169">After the application is running, open Service Fabric Explorer to check the health of the application.</span></span> <span data-ttu-id="24f82-170">Teraz, Service Fabric Explorer pokazuje, że aplikacja jest zła.</span><span class="sxs-lookup"><span data-stu-id="24f82-170">This time, Service Fabric Explorer shows that the application is unhealthy.</span></span> <span data-ttu-id="24f82-171">Wynika to z błędu, który został zgłoszony z kodu, że dodane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="24f82-171">This is because of the error that was reported from the code that we added previously.</span></span>
   
    ![Zła aplikacji w narzędziu Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/sfx-unhealthy-app.png)
7. <span data-ttu-id="24f82-173">W przypadku wybrania repliki podstawowej w widoku drzewa Eksploratora usługi sieć szkieletowa będzie informacja, że **kondycja** zbyt wskazuje błąd.</span><span class="sxs-lookup"><span data-stu-id="24f82-173">If you select the primary replica in the tree view of Service Fabric Explorer, you will see that **Health State** indicates an error, too.</span></span> <span data-ttu-id="24f82-174">Service Fabric Explorer wyświetla również szczegóły raportu kondycji, które zostały dodane do `HealthInformation` parametru w kodzie.</span><span class="sxs-lookup"><span data-stu-id="24f82-174">Service Fabric Explorer also displays the health report details that were added to the `HealthInformation` parameter in the code.</span></span> <span data-ttu-id="24f82-175">Widać tego samego raportów kondycji w programie PowerShell i portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="24f82-175">You can see the same health reports in PowerShell and the Azure portal.</span></span>
   
    ![Kondycja repliki w narzędziu Service Fabric Explorer](./media/service-fabric-diagnostics-how-to-report-and-check-service-health/replica-health-error-report-sfx.png)

<span data-ttu-id="24f82-177">Ten raport pozostaje w Menedżera kondycji, dopóki nie został on zastąpiony przez inny raport lub do momentu usunięcia tej repliki.</span><span class="sxs-lookup"><span data-stu-id="24f82-177">This report remains in the health manager until it is replaced by another report or until this replica is deleted.</span></span> <span data-ttu-id="24f82-178">Ponieważ firma Microsoft nie określono `TimeToLive` dla tego raportu kondycji w `HealthInformation` obiektu raportu nigdy nie wygasa.</span><span class="sxs-lookup"><span data-stu-id="24f82-178">Because we did not set `TimeToLive` for this health report in the `HealthInformation` object, the report never expires.</span></span>

<span data-ttu-id="24f82-179">Zaleca się, że kondycji należy podać na poziomie będącego w tym przypadku jest repliką.</span><span class="sxs-lookup"><span data-stu-id="24f82-179">We recommend that health should be reported on the most granular level, which in this case is the replica.</span></span> <span data-ttu-id="24f82-180">Można również raporty kondycji dotyczące `Partition`.</span><span class="sxs-lookup"><span data-stu-id="24f82-180">You can also report health on `Partition`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
this.Partition.ReportPartitionHealth(healthInformation);
```

<span data-ttu-id="24f82-181">Do raportu kondycji na `Application`, `DeployedApplication`, i `DeployedServicePackage`, użyj `CodePackageActivationContext`.</span><span class="sxs-lookup"><span data-stu-id="24f82-181">To report health on `Application`, `DeployedApplication`, and `DeployedServicePackage`, use  `CodePackageActivationContext`.</span></span>

```csharp
HealthInformation healthInformation = new HealthInformation("ServiceCode", "StateDictionary", HealthState.Error);
var activationContext = FabricRuntime.GetActivationContext();
activationContext.ReportApplicationHealth(healthInformation);
```

## <a name="next-steps"></a><span data-ttu-id="24f82-182">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="24f82-182">Next steps</span></span>
* [<span data-ttu-id="24f82-183">Nowości dotyczące kondycji sieci szkieletowej usług</span><span class="sxs-lookup"><span data-stu-id="24f82-183">Deep dive on Service Fabric health</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="24f82-184">Interfejs API REST dla raportowania kondycji usługi</span><span class="sxs-lookup"><span data-stu-id="24f82-184">REST API for reporting service health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-a-service)
* [<span data-ttu-id="24f82-185">Interfejs API REST dla raportowania kondycji aplikacji</span><span class="sxs-lookup"><span data-stu-id="24f82-185">REST API for reporting application health</span></span>](https://docs.microsoft.com/rest/api/servicefabric/report-the-health-of-an-application)

