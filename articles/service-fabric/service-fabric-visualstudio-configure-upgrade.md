---
title: "uaktualnienie hello aaaConfigure aplikacji usługi Service Fabric | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooconfigure hello ustawienia dotyczące uaktualniania aplikacji sieci szkieletowej usług za pomocą programu Microsoft Visual Studio."
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
ms.openlocfilehash: 8ca50aa9d911f3c98f017490c8fe29011e8d80cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-upgrade-of-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="38d20-103">Skonfiguruj hello uaktualnienie aplikacji usługi Service Fabric w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38d20-103">Configure hello upgrade of a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="38d20-104">Visual Studio tools dla sieci szkieletowej usług Azure zapewniają obsługę uaktualnienia publikowania toolocal lub zdalnych klastrów.</span><span class="sxs-lookup"><span data-stu-id="38d20-104">Visual Studio tools for Azure Service Fabric provide upgrade support for publishing toolocal or remote clusters.</span></span> <span data-ttu-id="38d20-105">Istnieją trzy scenariusze, w których chcesz tooupgrade Twojej aplikacji tooa nowsza wersja zamiast zastępowania aplikacji hello podczas testowania i debugowania:</span><span class="sxs-lookup"><span data-stu-id="38d20-105">There are three scenarios in which you want tooupgrade your application tooa newer version instead of replacing hello application during testing and debugging:</span></span>

* <span data-ttu-id="38d20-106">Dane aplikacji nie będzie utracone podczas uaktualniania hello.</span><span class="sxs-lookup"><span data-stu-id="38d20-106">Application data won't be lost during hello upgrade.</span></span>
* <span data-ttu-id="38d20-107">Dostępności pozostaje wysoka, nie będzie przerw w działaniu usługi podczas uaktualniania hello, jeśli brak wystarczającej liczby wystąpień usługi rozmieszczenie domen uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="38d20-107">Availability remains high so there won't be any service interruption during hello upgrade, if there are enough service instances spread across upgrade domains.</span></span>
* <span data-ttu-id="38d20-108">Testy mogą być uruchamiane na aplikacji, podczas gdy jest uaktualniany.</span><span class="sxs-lookup"><span data-stu-id="38d20-108">Tests can be run against an application while it's being upgraded.</span></span>

## <a name="parameters-needed-tooupgrade"></a><span data-ttu-id="38d20-109">Parametry wymagane tooupgrade</span><span class="sxs-lookup"><span data-stu-id="38d20-109">Parameters needed tooupgrade</span></span>
<span data-ttu-id="38d20-110">Są dostępne dwa typy wdrażania: regularne lub uaktualniania.</span><span class="sxs-lookup"><span data-stu-id="38d20-110">You can choose from two types of deployment: regular or upgrade.</span></span> <span data-ttu-id="38d20-111">Regularne wdrożenia usuwa wszelkie poprzednie informacje na temat wdrażania i dane w klastrze hello podczas wdrażania uaktualnienia zachowuje on.</span><span class="sxs-lookup"><span data-stu-id="38d20-111">A regular deployment erases any previous deployment information and data on hello cluster, while an upgrade deployment preserves it.</span></span> <span data-ttu-id="38d20-112">Podczas uaktualniania aplikacji usługi Service Fabric w programie Visual Studio należy parametry uaktualnienia tooprovide aplikacji i zasad dotyczących kondycji wyboru.</span><span class="sxs-lookup"><span data-stu-id="38d20-112">When you upgrade a Service Fabric application in Visual Studio, you need tooprovide application upgrade parameters and health check policies.</span></span> <span data-ttu-id="38d20-113">Parametry uaktualniania aplikacji pomocy formantu hello uaktualnieniu podczas kondycji Sprawdź zasady określają, czy hello uaktualnienie zakończyło się pomyślnie.</span><span class="sxs-lookup"><span data-stu-id="38d20-113">Application upgrade parameters help control hello upgrade, while health check policies determine whether hello upgrade was successful.</span></span> <span data-ttu-id="38d20-114">Zobacz [uaktualniania aplikacji usługi Service Fabric: parametry uaktualnienia](service-fabric-application-upgrade-parameters.md) więcej szczegółów.</span><span class="sxs-lookup"><span data-stu-id="38d20-114">See [Service Fabric application upgrade: upgrade parameters](service-fabric-application-upgrade-parameters.md) for more details.</span></span>

<span data-ttu-id="38d20-115">Istnieją trzy tryby uaktualnienia: *monitorowanej*, *UnmonitoredAuto*, i *UnmonitoredManual*.</span><span class="sxs-lookup"><span data-stu-id="38d20-115">There are three upgrade modes: *Monitored*, *UnmonitoredAuto*, and *UnmonitoredManual*.</span></span>

* <span data-ttu-id="38d20-116">Uaktualnienie monitorowanej automatyzuje hello uaktualnienia i aplikacji sprawdzania kondycji.</span><span class="sxs-lookup"><span data-stu-id="38d20-116">A Monitored upgrade automates hello upgrade and application health check.</span></span>
* <span data-ttu-id="38d20-117">Uaktualnienie UnmonitoredAuto automatyzuje hello uaktualnienia, ale pomija hello sprawdzenie kondycji aplikacji.</span><span class="sxs-lookup"><span data-stu-id="38d20-117">An UnmonitoredAuto upgrade automates hello upgrade, but skips hello application health check.</span></span>
* <span data-ttu-id="38d20-118">Po wykonaniu uaktualnienia UnmonitoredManual należy toomanually każdej z domen uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="38d20-118">When you do an UnmonitoredManual upgrade, you need toomanually upgrade each upgrade domain.</span></span>

<span data-ttu-id="38d20-119">Każdy tryb uaktualniania wymaga różnych zestawów parametrów.</span><span class="sxs-lookup"><span data-stu-id="38d20-119">Each upgrade mode requires different sets of parameters.</span></span> <span data-ttu-id="38d20-120">Zobacz [parametry uaktualniania aplikacji](service-fabric-application-upgrade-parameters.md) toolearn więcej informacji na temat dostępnych opcji uaktualniania hello.</span><span class="sxs-lookup"><span data-stu-id="38d20-120">See [Application upgrade parameters](service-fabric-application-upgrade-parameters.md) toolearn more about hello available upgrade options.</span></span>

## <a name="upgrade-a-service-fabric-application-in-visual-studio"></a><span data-ttu-id="38d20-121">Uaktualnianie aplikacji usługi Service Fabric w programie Visual Studio</span><span class="sxs-lookup"><span data-stu-id="38d20-121">Upgrade a Service Fabric application in Visual Studio</span></span>
<span data-ttu-id="38d20-122">Jeśli używasz hello sieci szkieletowej usług programu Visual Studio tools tooupgrade aplikacji usługi Service Fabric, można określić toobe proces publikowania uaktualnienia zamiast regularnego wdrażania sprawdzając hello **uaktualnienia aplikacji hello** Sprawdź pole.</span><span class="sxs-lookup"><span data-stu-id="38d20-122">If you’re using hello Visual Studio Service Fabric tools tooupgrade a Service Fabric application, you can specify a publish process toobe an upgrade rather than a regular deployment by checking hello **Upgrade hello application** check box.</span></span>

### <a name="tooconfigure-hello-upgrade-parameters"></a><span data-ttu-id="38d20-123">Parametry uaktualniania hello tooconfigure</span><span class="sxs-lookup"><span data-stu-id="38d20-123">tooconfigure hello upgrade parameters</span></span>
1. <span data-ttu-id="38d20-124">Kliknij przycisk hello **ustawienia** przycisku Dalej toohello pole wyboru.</span><span class="sxs-lookup"><span data-stu-id="38d20-124">Click hello **Settings** button next toohello check box.</span></span> <span data-ttu-id="38d20-125">Witaj **Edytuj parametry uaktualnienia** zostanie wyświetlone okno dialogowe.</span><span class="sxs-lookup"><span data-stu-id="38d20-125">hello **Edit Upgrade Parameters** dialog box appears.</span></span> <span data-ttu-id="38d20-126">Witaj **Edytuj parametry uaktualnienia** okno dialogowe obsługuje hello monitorowana, UnmonitoredAuto i UnmonitoredManual tryby uaktualnienia.</span><span class="sxs-lookup"><span data-stu-id="38d20-126">hello **Edit Upgrade Parameters** dialog box supports hello Monitored, UnmonitoredAuto, and UnmonitoredManual upgrade modes.</span></span>
2. <span data-ttu-id="38d20-127">Wybierz tryb uaktualniania hello mają toouse, a następnie wypełnij hello parametru siatki.</span><span class="sxs-lookup"><span data-stu-id="38d20-127">Select hello upgrade mode that you want toouse and then fill out hello parameter grid.</span></span>

    <span data-ttu-id="38d20-128">Każdy parametr ma wartości domyślnej.</span><span class="sxs-lookup"><span data-stu-id="38d20-128">Each parameter has default values.</span></span> <span data-ttu-id="38d20-129">Witaj opcjonalny parametr *DefaultServiceTypeHealthPolicy* przyjmuje wprowadzania tabeli skrótów.</span><span class="sxs-lookup"><span data-stu-id="38d20-129">hello optional parameter *DefaultServiceTypeHealthPolicy* takes a hash table input.</span></span> <span data-ttu-id="38d20-130">Oto przykład hello skrótu tabeli format wejściowy *DefaultServiceTypeHealthPolicy*:</span><span class="sxs-lookup"><span data-stu-id="38d20-130">Here’s an example of hello hash table input format for *DefaultServiceTypeHealthPolicy*:</span></span>

    ```
    @{ ConsiderWarningAsError = "false"; MaxPercentUnhealthyDeployedApplications = 0; MaxPercentUnhealthyServices = 0; MaxPercentUnhealthyPartitionsPerService = 0; MaxPercentUnhealthyReplicasPerPartition = 0 }
    ```

    <span data-ttu-id="38d20-131">*ServiceTypeHealthPolicyMap* jest inny opcjonalnym parametrem, który przyjmuje wprowadzania tabeli skrótów hello następującego formatu:</span><span class="sxs-lookup"><span data-stu-id="38d20-131">*ServiceTypeHealthPolicyMap* is another optional parameter that takes a hash table input in hello following format:</span></span>

    ```    
    @ {"ServiceTypeName" : "MaxPercentUnhealthyPartitionsPerService,MaxPercentUnhealthyReplicasPerPartition,MaxPercentUnhealthyServices"}
    ```

    <span data-ttu-id="38d20-132">Oto przykład rzeczywistych:</span><span class="sxs-lookup"><span data-stu-id="38d20-132">Here's a real-life example:</span></span>

    ```
    @{ "ServiceTypeName01" = "5,10,5"; "ServiceTypeName02" = "5,5,5" }
    ```
3. <span data-ttu-id="38d20-133">W przypadku wybrania UnmonitoredManual tryb uaktualniania należy ręcznie uruchomić toocontinue konsoli programu PowerShell i Zakończ proces uaktualniania hello.</span><span class="sxs-lookup"><span data-stu-id="38d20-133">If you select UnmonitoredManual upgrade mode, you must manually start a PowerShell console toocontinue and finish hello upgrade process.</span></span> <span data-ttu-id="38d20-134">Odwołuje się zbyt[uaktualniania aplikacji sieci szkieletowej usług: Tematy zaawansowane](service-fabric-application-upgrade-advanced.md) toolearn sposób ręcznego uaktualnienia działa.</span><span class="sxs-lookup"><span data-stu-id="38d20-134">Refer too[Service Fabric application upgrade: advanced topics](service-fabric-application-upgrade-advanced.md) toolearn how manual upgrade works.</span></span>

## <a name="upgrade-an-application-by-using-powershell"></a><span data-ttu-id="38d20-135">Uaktualnianie aplikacji przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="38d20-135">Upgrade an application by using PowerShell</span></span>
<span data-ttu-id="38d20-136">Możesz użyć tooupgrade poleceń cmdlet programu PowerShell aplikacji sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="38d20-136">You can use PowerShell cmdlets tooupgrade a Service Fabric application.</span></span> <span data-ttu-id="38d20-137">Zobacz [samouczek uaktualniania aplikacji sieci szkieletowej usług](service-fabric-application-upgrade-tutorial.md) i [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) Aby uzyskać szczegółowe informacje.</span><span class="sxs-lookup"><span data-stu-id="38d20-137">See [Service Fabric application upgrade tutorial](service-fabric-application-upgrade-tutorial.md) and [Start-ServiceFabricApplicationUpgrade](https://msdn.microsoft.com/library/mt125975.aspx) for detailed information.</span></span>

## <a name="specify-a-health-check-policy-in-hello-application-manifest-file"></a><span data-ttu-id="38d20-138">Określ zasady sprawdzania kondycji w pliku manifestu aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="38d20-138">Specify a health check policy in hello application manifest file</span></span>
<span data-ttu-id="38d20-139">Każda usługa w aplikacji platformy Service Fabric może mieć własne parametry zasad kondycji, które zastąpić wartości domyślne hello.</span><span class="sxs-lookup"><span data-stu-id="38d20-139">Every service in a Service Fabric application can have its own health policy parameters that override hello default values.</span></span> <span data-ttu-id="38d20-140">Możesz podać te wartości parametrów w pliku manifestu aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="38d20-140">You can provide these parameter values in hello application manifest file.</span></span>

<span data-ttu-id="38d20-141">Witaj poniższy przykład przedstawia sposób tooapply unikatowy kondycji Sprawdź zasady dla każdej usługi w manifeście aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="38d20-141">hello following example shows how tooapply a unique health check policy for each service in hello application manifest.</span></span>

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
## <a name="next-steps"></a><span data-ttu-id="38d20-142">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="38d20-142">Next steps</span></span>
<span data-ttu-id="38d20-143">Aby uzyskać więcej informacji na temat wdrażania aplikacji, zobacz [wdrażania istniejącej aplikacji w sieci szkieletowej usług Azure](service-fabric-deploy-existing-app.md).</span><span class="sxs-lookup"><span data-stu-id="38d20-143">For more information about deploying an application, see [Deploy an existing application in Azure Service Fabric](service-fabric-deploy-existing-app.md).</span></span>