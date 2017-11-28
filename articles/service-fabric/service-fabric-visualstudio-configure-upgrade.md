---
title: "Konfigurowanie uaktualnienia aplikacji usługi Service Fabric | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak skonfigurować ustawienia dotyczące uaktualniania aplikacji sieci szkieletowej usług za pomocą programu Microsoft Visual Studio."
services: service-fabric
documentationcenter: na
author: mikkelhegn
manager: mfussell
editor: tglee
ms.assetid: 1757ba85-0b7b-4f16-8a23-2ddaa61c86c6
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 06/29/2017
ms.author: mikkelhegn
ms.openlocfilehash: 314b29a56e4651222822f40a116af97a7372ff2c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="f4f8c-103">Konfigurowanie uaktualnienia aplikacji usługi Service Fabric w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4f8c-103">Configure the upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="f4f8c-104">Visual Studio tools dla sieci szkieletowej usług Azure zapewniają obsługę uaktualnienia publikowanie do klastrów lokalnym lub zdalnym.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing to local or remote clusters.</span></span> <span data-ttu-id="f4f8c-105">Istnieją trzy scenariusze, w których ma zostać uaktualniony do nowszej wersji zamiast zastępowania aplikacji podczas testowania i debugowania aplikacji:</span><span class="sxs-lookup"><span data-stu-id="f4f8c-105">There are three scenarios in which you want to upgrade your application to a newer version instead of replacing the application during testing and debugging:</span></span>

* <span data-ttu-id="f4f8c-106">Dane aplikacji nie będzie utracone podczas uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-106">Application data won't be lost during the upgrade.</span></span>
* <span data-ttu-id="f4f8c-107">Dostępności pozostaje wysoka, nie będzie przerw w działaniu usługi podczas uaktualniania, jeśli brak wystarczającej liczby wystąpień usługi rozmieszczenie domen uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-107">Availability remains high so there won't be any service interruption during the upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="f4f8c-108">Testy mogą być uruchamiane na aplikacji, podczas gdy jest uaktualniany.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-to-upgrade"></a><span data-ttu-id="f4f8c-109">Parametry niezbędne do uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="f4f8c-109">Parameters needed to upgrade</span></span>
<span data-ttu-id="f4f8c-110">Są dostępne dwa typy wdrażania: regularne lub uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="f4f8c-111">Regularne wdrożenia usuwa wszelkie poprzednie informacje na temat wdrażania i dane w klastrze, podczas wdrażania uaktualnienia zachowuje on.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-111">A regular deployment erases any previous deployment information and data on the cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="f4f8c-112">Podczas uaktualniania aplikacji usługi Service Fabric w programie Visual Studio, musisz podać parametry uaktualniania aplikacji i kondycji Sprawdź zasady.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-112">When you upgrade a Service Fabric application in Visual Studio, you need to provide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="f4f8c-113">Parametry uaktualniania aplikacji ograniczyć uaktualnienia, podczas gdy zasady dotyczące kondycji wyboru ustalić, czy uaktualnienie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-113">Application upgrade parameters help control the upgrade, while health check policies determine whether the upgrade was successful.</span></span> <span data-ttu-id="f4f8c-114">Zobacz [uaktualniania aplikacji usługi Service Fabric: parametry uaktualnienia](service-fabric-application-upgrade-parameters.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="f4f8c-115">Istnieją trzy tryby uaktualnienia: *monitorowanej*, *UnmonitoredAuto*, i *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="f4f8c-116">Uaktualnienie monitorowanej automatyzuje uaktualnienia i sprawdzenie kondycji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-116">A Monitored upgrade automates the upgrade and application health check.</span></span>
* <span data-ttu-id="f4f8c-117">Uaktualnienie UnmonitoredAuto automatyzuje uaktualnienia, ale pomija sprawdzanie kondycji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-117">An UnmonitoredAuto upgrade automates the upgrade, but skips the application health check.</span></span>
* <span data-ttu-id="f4f8c-118">Po wykonaniu uaktualnienia UnmonitoredManual, należy ręcznie uaktualnić każdej z domen.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-118">When you do an UnmonitoredManual upgrade, you need to manually upgrade each upgrade domain.</span></span>

<span data-ttu-id="f4f8c-119">Każdy tryb uaktualniania wymaga różnych zestawów parametrów.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="f4f8c-120">Zobacz [parametry uaktualniania aplikacji](service-fabric-application-upgrade-parameters.md) Aby dowiedzieć się więcej o dostępnych opcjach uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) to learn more about the available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="f4f8c-121">Uaktualnianie aplikacji usługi Service Fabric w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4f8c-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="f4f8c-122">Jeśli używasz narzędzia Visual Studio sieci szkieletowej usług do uaktualniania aplikacji usługi Service Fabric, można określić proces publikowania, do uaktualnienia, a nie regularnego wdrażania sprawdzając **uaktualnienie aplikacji** pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-122">If you’re using the Visual Studio Service Fabric tools to upgrade a Service Fabric application, you can specify a publish process to be an upgrade rather than a regular deployment by checking the **Upgrade the application** check box.</span></span>

### <a name="to-configure-the-upgrade-parameters"></a><span data-ttu-id="f4f8c-123">Aby skonfigurować parametry uaktualnienia</span><span class="sxs-lookup"><span data-stu-id="f4f8c-123">To configure the upgrade parameters</span></span>
1. <span data-ttu-id="f4f8c-124">Kliknij przycisk **ustawienia** przycisk obok pola wyboru.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-124">Click the **Settings** button next to the check box.</span></span> <span data-ttu-id="f4f8c-125">**Edytuj parametry uaktualnienia** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-125">The **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="f4f8c-126">**Edytuj parametry uaktualnienia** okno dialogowe obsługuje monitorowana, UnmonitoredAuto i UnmonitoredManual tryby uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-126">The **Edit Upgrade Parameters** dialog box supports the Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="f4f8c-127">Wybierz tryb uaktualniania, który chcesz wykorzystać, a następnie wypełnij siatce parametrów.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-127">Select the upgrade mode that you want to use and then fill out the parameter grid.</span></span>

    <span data-ttu-id="f4f8c-128">Każdy parametr ma wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-128">Each parameter has default values.</span></span> <span data-ttu-id="f4f8c-129">Opcjonalny parametr *DefaultServiceTypeHealthPolicy* przyjmuje wprowadzania tabeli skrótów.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-129">The optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="f4f8c-130">Poniżej przedstawiono przykładowy format wejściowy tabeli skrótów dla *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="f4f8c-130">Here’s an example of the hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="f4f8c-131">*ServiceTypeHealthPolicyMap* jest inny opcjonalnym parametrem, który przyjmuje wprowadzania tabeli skrótów w następującym formacie:</span><span class="sxs-lookup"><span data-stu-id="f4f8c-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in the following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="f4f8c-132">Oto przykład rzeczywistych:</span><span class="sxs-lookup"><span data-stu-id="f4f8c-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="f4f8c-133">W przypadku wybrania UnmonitoredManual tryb uaktualniania, należy ręcznie uruchomić konsolę programu PowerShell, aby kontynuować, a następnie Zakończ proces uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console to continue and finish the upgrade process.</span></span> <span data-ttu-id="f4f8c-134">Zapoznaj się [uaktualniania aplikacji usługi Service Fabric: Tematy zaawansowane](service-fabric-application-upgrade-advanced.md) Aby dowiedzieć się, jak Ręczne uaktualnianie działa.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-134">Refer to [Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) to learn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="f4f8c-135">Uaktualnianie aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="f4f8c-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="f4f8c-136">Polecenia cmdlet programu PowerShell służą do uaktualnienia aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-136">You can use PowerShell cmdlets to upgrade a Service Fabric application.</span></span> <span data-ttu-id="f4f8c-137">Zobacz [samouczek uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade-tutorial.md) i [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) Aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-the-application-manifest-file"></a><span data-ttu-id="f4f8c-138">Określ zasady sprawdzania kondycji w pliku manifestu aplikacji</span><span class="sxs-lookup"><span data-stu-id="f4f8c-138">Specify a health check policy in the application manifest file</span></span>
<span data-ttu-id="f4f8c-139">Każda usługa w aplikacji platformy Service Fabric może mieć własną parametry zasad kondycji, które zastępują ustawienia domyślne.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-139">Every service in a Service Fabric application can have its own health policy parameters that override the default values.</span></span> <span data-ttu-id="f4f8c-140">Możesz podać te wartości parametrów w pliku manifestu aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-140">You can provide these parameter values in the application manifest file.</span></span>

<span data-ttu-id="f4f8c-141">Poniższy przykład pokazuje, jak zastosować zasady sprawdzania kondycji unikatowy dla poszczególnych usług w manifeście aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f4f8c-141">The following example shows how to apply a unique health check policy for each service in the application manifest.</span></span>

```xml
<Policies>
    <HealthPolicy ConsiderWarningAsError="false" MaxPercentUnhealthyDeployedApplications="20">
        <DefaultServiceTypeHealthPolicy MaxPercentUnhealthyServices="20"               
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />
        <ServiceTypeHealthPolicy ServiceTypeName="ServiceTypeName1"
                MaxPercentUnhealthyServices="20"
                MaxPercentUnhealthyPartitionsPerService="20"
                MaxPercentUnhealthyReplicasPerPartition="20" />      
    </HealthPolicy>
</Policies>
```
## <a name="next-steps"></a><span data-ttu-id="f4f8c-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f4f8c-142">Next steps</span></span>
<span data-ttu-id="f4f8c-143">Aby uzyskać więcej informacji na temat wdrażania aplikacji, zobacz [wdrażania istniejącej aplikacji w sieci szkieletowej usług Azure](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="f4f8c-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>