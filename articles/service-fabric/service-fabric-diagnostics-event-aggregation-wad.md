---
title: "Usługi sieci szkieletowej zdarzeń agregacji z systemu Windows Azure Diagnostics aaaAzure | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat agregowania i zbierania zdarzeń przy użyciu WAD monitorowania i diagnostyki klastrów sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: 4827ce66620e61c5b4a8682db55952333113188a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-windows-azure-diagnostics"></a><span data-ttu-id="069be-103">Agregacja zdarzeń i kolekcji przy użyciu systemu Windows Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="069be-103">Event aggregation and collection using Windows Azure Diagnostics</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="069be-104">Windows</span><span class="sxs-lookup"><span data-stu-id="069be-104">Windows</span></span>](service-fabric-diagnostics-event-aggregation-wad.md)
> * [<span data-ttu-id="069be-105">Linux</span><span class="sxs-lookup"><span data-stu-id="069be-105">Linux</span></span>](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

<span data-ttu-id="069be-106">Jeśli korzystasz z klastra usługi sieć szkieletowa usług Azure, jest dobrze toocollect hello dzienniki ze wszystkich węzłów hello w centralnej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="069be-106">When you're running an Azure Service Fabric cluster, it's a good idea toocollect hello logs from all hello nodes in a central location.</span></span> <span data-ttu-id="069be-107">O dzienniki hello w centralnej lokalizacji ułatwiają analizowanie i rozwiązywanie problemów w klastrze, lub problemy w hello aplikacje i usługi działające w klastrze.</span><span class="sxs-lookup"><span data-stu-id="069be-107">Having hello logs in a central location helps you analyze and troubleshoot issues in your cluster, or issues in hello applications and services running in that cluster.</span></span>

<span data-ttu-id="069be-108">Zbieranie dzienników i tooupload jedną z metod jest rozszerzenie systemu Windows Azure Diagnostics (WAD) hello toouse, który przekazuje dzienniki tooAzure magazynu, a także ma hello opcja toosend dzienniki tooAzure usługi Application Insights lub Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="069be-108">One way tooupload and collect logs is toouse hello Windows Azure Diagnostics (WAD) extension, which uploads logs tooAzure Storage, and also has hello option toosend logs tooAzure Application Insights or Event Hubs.</span></span> <span data-ttu-id="069be-109">Można również użyć procesu zewnętrznego tooread hello zdarzenia z magazynu i umieścić w produkcie platformy analizy, takich jak [analizy dzienników OMS](../log-analytics/log-analytics-service-fabric.md) lub innego rozwiązania do analizowania dziennika.</span><span class="sxs-lookup"><span data-stu-id="069be-109">You can also use an external process tooread hello events from storage and place them in an analysis platform product, such as [OMS Log Analytics](../log-analytics/log-analytics-service-fabric.md) or another log-parsing solution.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="069be-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="069be-110">Prerequisites</span></span>
<span data-ttu-id="069be-111">Te narzędzia są używane tooperform niektóre operacje hello w tym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="069be-111">These tools are used tooperform some of hello operations in this document:</span></span>

* <span data-ttu-id="069be-112">[Diagnostyka Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) (dotyczących tooAzure usługi w chmurze, lecz jest dobrym informacje i przykłady)</span><span class="sxs-lookup"><span data-stu-id="069be-112">[Azure Diagnostics](../cloud-services/cloud-services-dotnet-diagnostics.md) (related tooAzure Cloud Services but has good information and examples)</span></span>
* [<span data-ttu-id="069be-113">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="069be-113">Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="069be-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="069be-114">Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="069be-115">Klient usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="069be-115">Azure Resource Manager client</span></span>](https://github.com/projectkudu/ARMClient)
* [<span data-ttu-id="069be-116">Szablon usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="069be-116">Azure Resource Manager template</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="log-and-event-sources"></a><span data-ttu-id="069be-117">Źródła dziennika i zdarzenie</span><span class="sxs-lookup"><span data-stu-id="069be-117">Log and event sources</span></span>

### <a name="service-fabric-platform-events"></a><span data-ttu-id="069be-118">Zdarzenia platformy Service Fabric</span><span class="sxs-lookup"><span data-stu-id="069be-118">Service Fabric platform events</span></span>
<span data-ttu-id="069be-119">Zgodnie z opisem w [w tym artykule](service-fabric-diagnostics-event-generation-infra.md), Service Fabric konfiguruje możesz z kilku kanałów rejestrowania poza pole, z którym hello następujących kanałów łatwo są skonfigurowane przy użyciu WAD toosend monitorowania i diagnostyki danych tooa tabeli magazynu lub w innym miejscu:</span><span class="sxs-lookup"><span data-stu-id="069be-119">As discussed in [this article](service-fabric-diagnostics-event-generation-infra.md), Service Fabric sets you up with a few out-of-the-box logging channels, of which hello following channels are easily configured with WAD toosend monitoring and diagnostics data tooa storage table or elsewhere:</span></span>
  * <span data-ttu-id="069be-120">Zdarzenia operacyjne: operacje wyższego poziomu, które hello wykonuje platformy sieci szkieletowej usług.</span><span class="sxs-lookup"><span data-stu-id="069be-120">Operational events: higher-level operations that hello Service Fabric platform performs.</span></span> <span data-ttu-id="069be-121">Tworzenie aplikacji i usług, zmian stanu węzła i informacje o uaktualnianiu przykładami.</span><span class="sxs-lookup"><span data-stu-id="069be-121">Examples include creation of applications and services, node state changes, and upgrade information.</span></span> <span data-ttu-id="069be-122">Te są emitowane jako dzienniki zdarzeń śledzenia dla systemu Windows (ETW)</span><span class="sxs-lookup"><span data-stu-id="069be-122">These are emitted as Event Tracing for Windows (ETW) logs</span></span>
  * [<span data-ttu-id="069be-123">Reliable Actors zdarzeń modelu programowania</span><span class="sxs-lookup"><span data-stu-id="069be-123">Reliable Actors programming model events</span></span>](service-fabric-reliable-actors-diagnostics.md)
  * [<span data-ttu-id="069be-124">Niezawodne usługi zdarzeń modelu programowania</span><span class="sxs-lookup"><span data-stu-id="069be-124">Reliable Services programming model events</span></span>](service-fabric-reliable-services-diagnostics.md)

### <a name="application-events"></a><span data-ttu-id="069be-125">Zdarzenia aplikacji</span><span class="sxs-lookup"><span data-stu-id="069be-125">Application events</span></span>
 <span data-ttu-id="069be-126">Zdarzenia wysyłanego z Twojej aplikacji i usług kodu i zapisany przy użyciu klasy pomocy EventSource hello postanowień hello szablony programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="069be-126">Events emitted from your applications' and services' code and written out by using hello EventSource helper class provided in hello Visual Studio templates.</span></span> <span data-ttu-id="069be-127">Aby uzyskać więcej informacji dotyczących sposobu toowrite źródła zdarzeń logowania z aplikacji, zobacz [monitora i diagnozowania usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span><span class="sxs-lookup"><span data-stu-id="069be-127">For more information on how toowrite EventSource logs from your application, see [Monitor and diagnose services in a local machine development setup](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).</span></span>

## <a name="deploy-hello-diagnostics-extension"></a><span data-ttu-id="069be-128">Wdrażanie rozszerzenia diagnostyki hello</span><span class="sxs-lookup"><span data-stu-id="069be-128">Deploy hello Diagnostics extension</span></span>
<span data-ttu-id="069be-129">pierwszym krokiem Hello zbierania dzienników jest rozszerzeniem diagnostyki hello toodeploy na poszczególnych maszyn wirtualnych hello w klastrze usługi sieć szkieletowa hello.</span><span class="sxs-lookup"><span data-stu-id="069be-129">hello first step in collecting logs is toodeploy hello Diagnostics extension on each of hello VMs in hello Service Fabric cluster.</span></span> <span data-ttu-id="069be-130">Hello rozszerzenia diagnostyki zbiera dzienniki na każdej maszynie Wirtualnej i przekazuje je toohello konta magazynu, który określisz.</span><span class="sxs-lookup"><span data-stu-id="069be-130">hello Diagnostics extension collects logs on each VM and uploads them toohello storage account that you specify.</span></span> <span data-ttu-id="069be-131">kroki Hello zależą od nieco przy użyciu hello portalu Azure lub usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="069be-131">hello steps vary a little based on whether you use hello Azure portal or Azure Resource Manager.</span></span> <span data-ttu-id="069be-132">kroki Hello również różnić w zależności od czy wdrożenia hello jest częścią tworzenia klastra lub dla klastra, który już istnieje.</span><span class="sxs-lookup"><span data-stu-id="069be-132">hello steps also vary based on whether hello deployment is part of cluster creation or is for a cluster that already exists.</span></span> <span data-ttu-id="069be-133">Przyjrzyjmy się hello kroki dla każdego scenariusza.</span><span class="sxs-lookup"><span data-stu-id="069be-133">Let's look at hello steps for each scenario.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-through-azure-portal"></a><span data-ttu-id="069be-134">Wdrażanie rozszerzenia diagnostyki hello w ramach tworzenia klastra za pośrednictwem portalu Azure</span><span class="sxs-lookup"><span data-stu-id="069be-134">Deploy hello Diagnostics extension as part of cluster creation through Azure portal</span></span>
<span data-ttu-id="069be-135">toodeploy hello diagnostyki rozszerzenia toohello maszyn wirtualnych w klastrze hello w ramach tworzenia klastra, użyj panelu Ustawienia diagnostyki hello pokazano poniżej hello obrazu — upewnij się, że diagnostyki ustawiono zbyt**na** (hello ustawienie domyślne) .</span><span class="sxs-lookup"><span data-stu-id="069be-135">toodeploy hello Diagnostics extension toohello VMs in hello cluster as part of cluster creation, you use hello Diagnostics settings panel shown in hello following image - ensure that Diagnostics is set too**On** (hello default setting).</span></span> <span data-ttu-id="069be-136">Po utworzeniu klastra hello, nie możesz zmienić te ustawienia przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="069be-136">After you create hello cluster, you can't change these settings by using hello portal.</span></span>

![Azure ustawień diagnostyki w portalu hello tworzenia klastra](media/service-fabric-diagnostics-event-aggregation-wad/azure-enable-diagnostics.png)

<span data-ttu-id="069be-138">Podczas tworzenia klastra przy użyciu portalu hello, zalecamy pobranie szablonu hello **przed kliknięciem przycisku OK** toocreate hello klastra.</span><span class="sxs-lookup"><span data-stu-id="069be-138">When you're creating a cluster by using hello portal, we highly recommend that you download hello template **before you click OK** toocreate hello cluster.</span></span> <span data-ttu-id="069be-139">Aby uzyskać więcej informacji, zobacz zbyt[Konfigurowanie klastra sieci szkieletowej usług za pomocą szablonu usługi Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="069be-139">For details, refer too[Set up a Service Fabric cluster by using an Azure Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="069be-140">Zmiany toomake szablonu hello będą potrzebne później, ponieważ nie można wprowadzić kilka zmian przy użyciu portalu hello.</span><span class="sxs-lookup"><span data-stu-id="069be-140">You'll need hello template toomake changes later, because you can't make some changes by using hello portal.</span></span>

### <a name="deploy-hello-diagnostics-extension-as-part-of-cluster-creation-by-using-azure-resource-manager"></a><span data-ttu-id="069be-141">Wdrażanie rozszerzenia diagnostyki hello w ramach tworzenia klastra przy użyciu usługi Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="069be-141">Deploy hello Diagnostics extension as part of cluster creation by using Azure Resource Manager</span></span>
<span data-ttu-id="069be-142">toocreate klastra za pomocą Menedżera zasobów, należy tooadd hello diagnostyki konfiguracji szablonu JSON w toohello pełne klastra Menedżera zasobów przed utworzeniem klastra hello.</span><span class="sxs-lookup"><span data-stu-id="069be-142">toocreate a cluster by using Resource Manager, you need tooadd hello Diagnostics configuration JSON toohello full cluster Resource Manager template before you create hello cluster.</span></span> <span data-ttu-id="069be-143">Udostępniamy przykładowy szablon Menedżera zasobów klastra maszyny Wirtualnej pięciu o konfiguracji diagnostyki dodane tooit jako część nasze przykłady szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="069be-143">We provide a sample five-VM cluster Resource Manager template with Diagnostics configuration added tooit as part of our Resource Manager template samples.</span></span> <span data-ttu-id="069be-144">Można to sprawdzić w tej lokalizacji w galerii Azure przykładów hello: [pięcioma węzłami klastra z przykładowy szablon Menedżera zasobów diagnostyki](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span><span class="sxs-lookup"><span data-stu-id="069be-144">You can see it at this location in hello Azure Samples gallery: [Five-node cluster with Diagnostics Resource Manager template sample](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype-wad).</span></span>

<span data-ttu-id="069be-145">ustawienia diagnostyki hello toosee hello szablonu usługi Resource Manager, hello Otwórz plik azuredeploy.json i wyszukaj **IaaSDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="069be-145">toosee hello Diagnostics setting in hello Resource Manager template, open hello azuredeploy.json file and search for **IaaSDiagnostics**.</span></span> <span data-ttu-id="069be-146">toocreate klastra przy użyciu tego szablonu, wybierz opcję hello **wdrażanie tooAzure** przycisk dostępne pod adresem hello poprzedniej konsolidacji.</span><span class="sxs-lookup"><span data-stu-id="069be-146">toocreate a cluster by using this template, select hello **Deploy tooAzure** button available at hello previous link.</span></span>

<span data-ttu-id="069be-147">Alternatywnie można pobrać hello próbki Menedżera zasobów, wprowadzić zmiany tooit i utworzyć klaster przy użyciu szablonu modyfikacji hello przy użyciu hello `New-AzureRmResourceGroupDeployment` polecenie w oknie programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="069be-147">Alternatively, you can download hello Resource Manager sample, make changes tooit, and create a cluster with hello modified template by using hello `New-AzureRmResourceGroupDeployment` command in an Azure PowerShell window.</span></span> <span data-ttu-id="069be-148">Zobacz hello następującego kodu dla parametrów hello, które przekazujesz w poleceniu toohello.</span><span class="sxs-lookup"><span data-stu-id="069be-148">See hello following code for hello parameters that you pass in toohello command.</span></span> <span data-ttu-id="069be-149">Aby uzyskać szczegółowe informacje dotyczące sposobu toodeploy zasób grupy przy użyciu programu PowerShell, zobacz artykuł hello [wdrażanie grupy zasobów z szablonem usługi Azure Resource Manager hello](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="069be-149">For detailed information on how toodeploy a resource group by using PowerShell, see hello article [Deploy a resource group with hello Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

### <a name="deploy-hello-diagnostics-extension-tooan-existing-cluster"></a><span data-ttu-id="069be-150">Wdrażanie hello diagnostyki rozszerzenia tooan istniejącego klastra</span><span class="sxs-lookup"><span data-stu-id="069be-150">Deploy hello Diagnostics extension tooan existing cluster</span></span>
<span data-ttu-id="069be-151">Jeśli masz istniejący klaster nie ma wdrożonych diagnostyki lub jeśli chcesz toomodify istniejącej konfiguracji, można dodać lub zaktualizować.</span><span class="sxs-lookup"><span data-stu-id="069be-151">If you have an existing cluster that doesn't have Diagnostics deployed, or if you want toomodify an existing configuration, you can add or update it.</span></span> <span data-ttu-id="069be-152">Zmodyfikuj szablon Menedżera zasobów hello, która jest używana toocreate hello istniejącego klastra lub pobrać hello szablonu z portalu hello zgodnie z wcześniejszym opisem.</span><span class="sxs-lookup"><span data-stu-id="069be-152">Modify hello Resource Manager template that's used toocreate hello existing cluster or download hello template from hello portal as described earlier.</span></span> <span data-ttu-id="069be-153">Zmodyfikuj plik template.json hello, wykonując następujące zadania hello.</span><span class="sxs-lookup"><span data-stu-id="069be-153">Modify hello template.json file by performing hello following tasks.</span></span>

<span data-ttu-id="069be-154">Dodaj nowy szablon toohello zasobów magazynu przez dodanie toohello sekcja zasobów.</span><span class="sxs-lookup"><span data-stu-id="069be-154">Add a new storage resource toohello template by adding toohello resources section.</span></span>

```json
{
  "apiVersion": "2015-05-01-preview",
  "type": "Microsoft.Storage/storageAccounts",
  "name": "[parameters('applicationDiagnosticsStorageAccountName')]",
  "location": "[parameters('computeLocation')]",
  "properties": {
    "accountType": "[parameters('applicationDiagnosticsStorageAccountType')]"
  },
  "tags": {
    "resourceType": "Service Fabric",
    "clusterName": "[parameters('clusterName')]"
  }
},
```

 <span data-ttu-id="069be-155">Następnie dodaj parametry toohello sekcji zaraz po definicji konta magazynu hello, między `supportLogStorageAccountName` i `vmNodeType0Name`.</span><span class="sxs-lookup"><span data-stu-id="069be-155">Next, add toohello parameters section just after hello storage account definitions, between `supportLogStorageAccountName` and `vmNodeType0Name`.</span></span> <span data-ttu-id="069be-156">Zastąp tekst zastępczy hello *nazwy konta magazynu tu* o nazwie hello hello konta magazynu.</span><span class="sxs-lookup"><span data-stu-id="069be-156">Replace hello placeholder text *storage account name goes here* with hello name of hello storage account.</span></span>

```json
    "applicationDiagnosticsStorageAccountType": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "Replication option for hello application diagnostics storage account"
      }
    },
    "applicationDiagnosticsStorageAccountName": {
      "type": "string",
      "defaultValue": "storage account name goes here",
      "metadata": {
        "description": "Name for hello storage account that contains application diagnostics data from hello cluster"
      }
    },
```
<span data-ttu-id="069be-157">Następnie zaktualizuj hello `VirtualMachineProfile` sekcji pliku template.json hello przez dodanie hello następującego kodu w ramach hello tablica rozszerzeń.</span><span class="sxs-lookup"><span data-stu-id="069be-157">Then, update hello `VirtualMachineProfile` section of hello template.json file by adding hello following code within hello extensions array.</span></span> <span data-ttu-id="069be-158">Należy się tooadd przecinkami hello początek lub koniec hello, w zależności od tego, gdzie jest wstawiana.</span><span class="sxs-lookup"><span data-stu-id="069be-158">Be sure tooadd a comma at hello beginning or hello end, depending on where it's inserted.</span></span>

```json
{
    "name": "[concat(parameters('vmNodeType0Name'),'_Microsoft.Insights.VMDiagnosticsSettings')]",
    "properties": {
        "type": "IaaSDiagnostics",
        "autoUpgradeMinorVersion": true,
        "protectedSettings": {
        "storageAccountName": "[parameters('applicationDiagnosticsStorageAccountName')]",
        "storageAccountKey": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName')),'2015-05-01-preview').key1]",
        "storageAccountEndPoint": "https://core.windows.net/"
        },
        "publisher": "Microsoft.Azure.Diagnostics",
        "settings": {
        "WadCfg": {
            "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": "50000",
            "EtwProviders": {
                "EtwEventSourceProviderConfiguration": [
                {
                    "provider": "Microsoft-ServiceFabric-Actors",
                    "scheduledTransferKeywordFilter": "1",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableActorEventTable"
                    }
                },
                {
                    "provider": "Microsoft-ServiceFabric-Services",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricReliableServiceEventTable"
                    }
                }
                ],
                "EtwManifestProviderConfiguration": [
                {
                    "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
                    "scheduledTransferLogLevelFilter": "Information",
                    "scheduledTransferKeywordFilter": "4611686018427387904",
                    "scheduledTransferPeriod": "PT5M",
                    "DefaultEvents": {
                    "eventDestination": "ServiceFabricSystemEventTable"
                    }
                }
                ]
            }
            }
        },
        "StorageAccount": "[parameters('applicationDiagnosticsStorageAccountName')]"
        },
        "typeHandlerVersion": "1.5"
    }
}
```

<span data-ttu-id="069be-159">Po zmodyfikowaniu pliku template.json hello zgodnie z opisem ponownie opublikować hello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="069be-159">After you modify hello template.json file as described, republish hello Resource Manager template.</span></span> <span data-ttu-id="069be-160">Jeśli został wyeksportowany szablon hello, uruchamianie pliku deploy.ps1 hello je opublikuje hello szablonu.</span><span class="sxs-lookup"><span data-stu-id="069be-160">If hello template was exported, running hello deploy.ps1 file republishes hello template.</span></span> <span data-ttu-id="069be-161">Po wdrożeniu, upewnij się, że **ProvisioningState** jest **zakończyło się pomyślnie**.</span><span class="sxs-lookup"><span data-stu-id="069be-161">After you deploy, ensure that **ProvisioningState** is **Succeeded**.</span></span>

## <a name="collect-health-and-load-events"></a><span data-ttu-id="069be-162">Zbieranie kondycji i załadować zdarzenia</span><span class="sxs-lookup"><span data-stu-id="069be-162">Collect health and load events</span></span>

<span data-ttu-id="069be-163">Począwszy od wersji platformy Service Fabric hello 5.4 metryki zdarzenia kondycji i obciążenia są dostępne dla kolekcji.</span><span class="sxs-lookup"><span data-stu-id="069be-163">Starting with hello 5.4 release of Service Fabric, health and load metric events are available for collection.</span></span> <span data-ttu-id="069be-164">Te zdarzenia odzwierciedlają zdarzeń generowanych przez hello system lub kodu za pomocą kondycji hello lub załadować API raportowania, takie jak [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) lub [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span><span class="sxs-lookup"><span data-stu-id="069be-164">These events reflect events generated by hello system or your code by using hello health or load reporting APIs such as [ReportPartitionHealth](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportpartitionhealth.aspx) or [ReportLoad](https://msdn.microsoft.com/library/azure/system.fabric.iservicepartition.reportload.aspx).</span></span> <span data-ttu-id="069be-165">Dzięki temu agregowanie i wyświetlanie stanu systemu wraz z upływem czasu oraz alerty na podstawie kondycji lub obciążenia zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="069be-165">This allows for aggregating and viewing system health over time and for alerting based on health or load events.</span></span> <span data-ttu-id="069be-166">tooview dodać tych zdarzeń w Podglądzie zdarzeń diagnostycznych programu Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000008" toohello listy dostawców ETW.</span><span class="sxs-lookup"><span data-stu-id="069be-166">tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000008" toohello list of ETW providers.</span></span>

<span data-ttu-id="069be-167">zdarzenia hello toocollect, zmodyfikuj tooinclude szablonu usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="069be-167">toocollect hello events, modify hello Resource Manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387912",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

## <a name="collect-reverse-proxy-events"></a><span data-ttu-id="069be-168">Zbieranie zdarzeń zwrotnego serwera proxy</span><span class="sxs-lookup"><span data-stu-id="069be-168">Collect reverse proxy events</span></span>

<span data-ttu-id="069be-169">Począwszy od wersji hello 5.7 usługi sieci szkieletowej, [odwrotny serwer proxy](service-fabric-reverseproxy.md) zdarzenia są dostępne dla kolekcji.</span><span class="sxs-lookup"><span data-stu-id="069be-169">Starting with hello 5.7 release of Service Fabric, [reverse proxy](service-fabric-reverseproxy.md) events are available for collection.</span></span>
<span data-ttu-id="069be-170">Zwrotny serwer proxy emituje zdarzenia do dwa kanały, jeden błąd zawierający zdarzenia w czasie wykonywania odbicia błędów przetwarzania żądań i hello drugi zawierający pełne zdarzenia dotyczące wszystkich żądań hello przetwarzane w hello zwrotnego serwera proxy.</span><span class="sxs-lookup"><span data-stu-id="069be-170">Reverse proxy emits events into two channels, one containing error events reflecting request processing failures and hello other one containing verbose events about all hello requests processed at hello reverse proxy.</span></span> 

1. <span data-ttu-id="069be-171">Zbieranie zdarzeń błędu: tooview dodać tych zdarzeń w Podglądzie zdarzeń diagnostycznych programu Visual Studio "Microsoft-ServiceFabric:4:0x4000000000000010" toohello listy dostawców ETW.</span><span class="sxs-lookup"><span data-stu-id="069be-171">Collect error events: tooview these events in Visual Studio's Diagnostic Event Viewer add "Microsoft-ServiceFabric:4:0x4000000000000010" toohello list of ETW providers.</span></span>
<span data-ttu-id="069be-172">zdarzenia hello toocollect z klastrami platformy Azure, zmodyfikuj tooinclude szablonu usługi Resource Manager hello</span><span class="sxs-lookup"><span data-stu-id="069be-172">toocollect hello events from Azure clusters, modify hello Resource Manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387920",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```

2. <span data-ttu-id="069be-173">Zbieranie wszystkie żądania przetwarzania zdarzeń: W programie Visual Studio diagnostycznych podglądu zdarzeń wpisu hello ServiceFabric programu Microsoft update w hello zbyt listy dostawców ETW "Microsoft-ServiceFabric:4:0x4000000000000020".</span><span class="sxs-lookup"><span data-stu-id="069be-173">Collect all request processing events: In Visual Studio's Diagnostic Event Viewer, update hello Microsoft-ServiceFabric entry in hello ETW provider list too"Microsoft-ServiceFabric:4:0x4000000000000020".</span></span>
<span data-ttu-id="069be-174">W przypadku klastrów sieci szkieletowej usług Azure zmodyfikuj tooinclude szablon Menedżera zasobów hello</span><span class="sxs-lookup"><span data-stu-id="069be-174">For Azure Service Fabric clusters, modify hello resource manager template tooinclude</span></span>

```json
  "EtwManifestProviderConfiguration": [
    {
      "provider": "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8",
      "scheduledTransferLogLevelFilter": "Information",
      "scheduledTransferKeywordFilter": "4611686018427387936",
      "scheduledTransferPeriod": "PT5M",
      "DefaultEvents": {
        "eventDestination": "ServiceFabricSystemEventTable"
      }
    }
```
> <span data-ttu-id="069be-175">To zbiera cały ruch przez zwrotny serwer proxy hello i może wymagać pojemności zaleca się toojudiciously Włącz zbieranie zdarzeń z tego kanału.</span><span class="sxs-lookup"><span data-stu-id="069be-175">It is recommended toojudiciously enable collecting events from this channel as this collects all traffic through hello reverse proxy and can quickly consume storage capacity.</span></span>

<span data-ttu-id="069be-176">W przypadku klastrów sieci szkieletowej usług Azure hello zdarzenia ze wszystkich węzłów hello są gromadzone i zagregowane w hello SystemEventTable.</span><span class="sxs-lookup"><span data-stu-id="069be-176">For Azure Service Fabric clusters, hello events from all hello nodes are collected and aggregated in hello SystemEventTable.</span></span>
<span data-ttu-id="069be-177">Szczegółowe Rozwiązywanie problemów z hello zdarzeń zwrotnego serwera proxy, zobacz hello [przewodnik diagnostyki zwrotnego serwera proxy](service-fabric-reverse-proxy-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="069be-177">For detailed troubleshooting of hello reverse proxy events, refer hello [reverse proxy diagnostics guide](service-fabric-reverse-proxy-diagnostics.md).</span></span>

## <a name="collect-from-new-eventsource-channels"></a><span data-ttu-id="069be-178">Zbierać z nowych kanałów źródła zdarzeń</span><span class="sxs-lookup"><span data-stu-id="069be-178">Collect from new EventSource channels</span></span>

<span data-ttu-id="069be-179">Dzienniki toocollect diagnostyki tooupdate nowych kanałów EventSource reprezentujących nowej aplikacji, który zajmie około toodeploy, wykonuje hello te same czynności jak opisano wcześniej hello ustawienia diagnostyki dla istniejącego klastra.</span><span class="sxs-lookup"><span data-stu-id="069be-179">tooupdate Diagnostics toocollect logs from new EventSource channels that represent a new application that you're about toodeploy, perform hello same steps as previously described for hello setup of Diagnostics for an existing cluster.</span></span>

<span data-ttu-id="069be-180">Zaktualizuj hello `EtwEventSourceProviderConfiguration` sekcji hello template.json wpisy tooadd hello nowych kanałów EventSource przed zastosowaniem konfiguracji hello aktualizacji przy użyciu hello `New-AzureRmResourceGroupDeployment` polecenia programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="069be-180">Update hello `EtwEventSourceProviderConfiguration` section in hello template.json file tooadd entries for hello new EventSource channels before you apply hello configuration update by using hello `New-AzureRmResourceGroupDeployment` PowerShell command.</span></span> <span data-ttu-id="069be-181">Nazwa Hello źródła zdarzeń hello jest zdefiniowany jako części kodu w pliku generowanych przez program Visual Studio ServiceEventSource.cs hello.</span><span class="sxs-lookup"><span data-stu-id="069be-181">hello name of hello event source is defined as part of your code in hello Visual Studio-generated ServiceEventSource.cs file.</span></span>

<span data-ttu-id="069be-182">Na przykład źródło zdarzenia jest o nazwie Mój Eventsource, dodać hello następujące zdarzenia hello tooplace kodu z Moje Eventsource do tabeli o nazwie MyDestinationTableName.</span><span class="sxs-lookup"><span data-stu-id="069be-182">For example, if your event source is named My-Eventsource, add hello following code tooplace hello events from My-Eventsource into a table named MyDestinationTableName.</span></span>

```json
        {
            "provider": "My-Eventsource",
            "scheduledTransferPeriod": "PT5M",
            "DefaultEvents": {
            "eventDestination": "MyDestinationTableName"
            }
        }
```

<span data-ttu-id="069be-183">liczniki wydajności toocollect lub dzienniki zdarzeń, modyfikować szablonu usługi Resource Manager hello za pomocą hello przykłady podane w [Utwórz maszynę wirtualną systemu Windows z monitorowania i diagnostyki za pomocą szablonu usługi Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="069be-183">toocollect performance counters or event logs, modify hello Resource Manager template by using hello examples provided in [Create a Windows virtual machine with monitoring and diagnostics by using an Azure Resource Manager template](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="069be-184">Następnie należy ponownie opublikować hello szablonu usługi Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="069be-184">Then, republish hello Resource Manager template.</span></span>

## <a name="collect-performance-counters"></a><span data-ttu-id="069be-185">Zebrać liczników wydajności</span><span class="sxs-lookup"><span data-stu-id="069be-185">Collect Performance Counters</span></span>

<span data-ttu-id="069be-186">metryki wydajności toocollect z klastra, Dodaj tooyour liczniki wydajności hello "WadCfg > DiagnosticMonitorConfiguration" w szablonie usługi Resource Manager powitania dla klastra.</span><span class="sxs-lookup"><span data-stu-id="069be-186">toocollect performance metrics from your cluster, add hello performance counters tooyour "WadCfg > DiagnosticMonitorConfiguration" in hello Resource Manager template for your cluster.</span></span> <span data-ttu-id="069be-187">Zobacz [liczniki wydajności sieci szkieletowej usług](service-fabric-diagnostics-event-generation-perf.md) dla liczników wydajności zalecamy zbierania.</span><span class="sxs-lookup"><span data-stu-id="069be-187">See [Service Fabric Performance Counters](service-fabric-diagnostics-event-generation-perf.md) for performance counters that we recommend collecting.</span></span>

<span data-ttu-id="069be-188">Na przykład, w tym miejscu możemy ustawić jeden licznik wydajności, próbkowany co 15 s (można zmienić tę wartość i sposób hello format "PT\<czasu >\<jednostki >", na przykład PT3M czy przykładowe co trzy minut), a przekazywane toohello Tabela magazynu odpowiednie co minutę.</span><span class="sxs-lookup"><span data-stu-id="069be-188">For example, here we set one performance counter, sampled every 15 seconds (this can be changed and follows hello format of "PT\<time>\<unit>", for example, PT3M would sample at three minute intervals), and transferred toohello appropriate storage table every one minute.</span></span>

  ```json
  "PerformanceCounters": {
      "scheduledTransferPeriod": "PT1M",
      "PerformanceCounterConfiguration": [
          {
              "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
              "sampleRate": "PT15S",
              "unit": "Percent",
              "annotation": [
              ],
              "sinks": ""
          }
      ]
  }
  ```
  
<span data-ttu-id="069be-189">Jeśli używasz zbiornika usługi Application Insights zgodnie z opisem w poniższej sekcji hello i mają te metryki tooshow się w usłudze Application Insights, upewnij się, że nazwa obiektu sink hello tooadd w sekcji "sink" hello, jak pokazano powyżej.</span><span class="sxs-lookup"><span data-stu-id="069be-189">If you are using an Application Insights sink, as described in hello section below, and want these metrics tooshow up in Application Insights, then make sure tooadd hello sink name in hello "sinks" section as shown above.</span></span> <span data-ttu-id="069be-190">Ponadto należy rozważyć utworzenie toosend osobnej tabeli liczniki wydajności, więc ich nie tłumu limit hello dane pochodzące z hello innych kanałów rejestrowania została włączona.</span><span class="sxs-lookup"><span data-stu-id="069be-190">Additionally, consider creating a separate table toosend your Performance Counters to, so they don't crowd out hello data coming from hello other logging channels you have enabled.</span></span>


## <a name="send-logs-tooapplication-insights"></a><span data-ttu-id="069be-191">Wyślij dzienniki tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="069be-191">Send logs tooApplication Insights</span></span>

<span data-ttu-id="069be-192">Wysyłanie tooApplication danych monitorowania i diagnostyki Insights (AI) może zostać wykonane jako część konfiguracji WAD hello.</span><span class="sxs-lookup"><span data-stu-id="069be-192">Sending monitoring and diagnostics data tooApplication Insights (AI) can be done as part of hello WAD configuration.</span></span> <span data-ttu-id="069be-193">Jeśli zdecydujesz toouse AI analizy zdarzeń i wizualizacji odczytu [analiza zdarzeń i wizualizacji z usługą Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset się zbiornika AI jako część programu "WadCfg".</span><span class="sxs-lookup"><span data-stu-id="069be-193">If you decide toouse AI for event analysis and visualization, read [Event Analysis and Visualization with Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) tooset up an AI Sink as part of your "WadCfg".</span></span>

## <a name="next-steps"></a><span data-ttu-id="069be-194">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="069be-194">Next steps</span></span>

<span data-ttu-id="069be-195">Po diagnostyki Azure zostały prawidłowo skonfigurowane, zostanie wyświetlona dane w tabelach magazynu z hello ETW i dzienniki EventSource.</span><span class="sxs-lookup"><span data-stu-id="069be-195">Once you have correctly configured Azure diagnostics, you will see data in your Storage tables from hello ETW and EventSource logs.</span></span> <span data-ttu-id="069be-196">Jeśli wybierzesz toouse OMS Kibana, lub wszelkie inne dane analizy i wizualizacji platformy, które nie skonfigurowano bezpośrednio w szablonie usługi Resource Manager hello, upewnij się, że tooset się hello platforma tooread Twojego wybór hello danych z tych tabel do przechowywania.</span><span class="sxs-lookup"><span data-stu-id="069be-196">If you choose toouse OMS, Kibana, or any other data analytics and visualization platform that is not directly configured in hello Resource Manager template, make sure tooset up hello platform of your choice tooread in hello data from these storage tables.</span></span> <span data-ttu-id="069be-197">W ten sposób dla OMS jest względnie proste i zostało wyjaśnione w dokumencie [zdarzeń i dziennika analizy za pośrednictwem OMS](service-fabric-diagnostics-event-analysis-oms.md).</span><span class="sxs-lookup"><span data-stu-id="069be-197">Doing this for OMS is relatively trivial, and is explained in [Event and log analysis through OMS](service-fabric-diagnostics-event-analysis-oms.md).</span></span> <span data-ttu-id="069be-198">Usługa Application Insights jest nieco szczególnych przypadkach, w tym sensie, ponieważ może być skonfigurowana jako część konfiguracji rozszerzenia diagnostyki hello, dlatego można znaleźć toohello [odpowiedniego artykułu](service-fabric-diagnostics-event-analysis-appinsights.md) po wybraniu toouse AI.</span><span class="sxs-lookup"><span data-stu-id="069be-198">Application Insights is a bit of a special case in this sense, since it can be configured as part of hello Diagnostics extension configuration, so refer toohello [appropriate article](service-fabric-diagnostics-event-analysis-appinsights.md) if you choose toouse AI.</span></span>

>[!NOTE]
><span data-ttu-id="069be-199">Nie ma żadnych sposób toofilter lub Oczyść hello zdarzenia, które są wysyłane toohello tabeli.</span><span class="sxs-lookup"><span data-stu-id="069be-199">There is currently no way toofilter or groom hello events that are sent toohello table.</span></span> <span data-ttu-id="069be-200">Jeśli nie implementują zdarzenia tooremove procesu z tabeli hello, hello tabeli będzie toogrow.</span><span class="sxs-lookup"><span data-stu-id="069be-200">If you don't implement a process tooremove events from hello table, hello table will continue toogrow.</span></span> <span data-ttu-id="069be-201">Obecnie jest przykładem usługi pielęgnacji danych działa w hello [próbki programu alarmowego](https://github.com/Azure-Samples/service-fabric-watchdog-service), i zaleca zapisu jedną dla siebie również, chyba że powody dla Ciebie dzienniki toostore poza przedział czasu dnia 30 lub 90.</span><span class="sxs-lookup"><span data-stu-id="069be-201">Currently, there is an example of a data grooming service running in hello [Watchdog sample](https://github.com/Azure-Samples/service-fabric-watchdog-service), and it is recommended that you write one for yourself as well, unless there is a good reason for you toostore logs beyond a 30 or 90 day timeframe.</span></span>

* [<span data-ttu-id="069be-202">Dowiedz się, jak toocollect liczników wydajności lub dzienniki przy użyciu hello rozszerzenia diagnostyki</span><span class="sxs-lookup"><span data-stu-id="069be-202">Learn how toocollect performance counters or logs by using hello Diagnostics extension</span></span>](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [<span data-ttu-id="069be-203">Analiza zdarzeń i wizualizacji z usługą Application Insights</span><span class="sxs-lookup"><span data-stu-id="069be-203">Event Analysis and Visualization with Application Insights</span></span>](service-fabric-diagnostics-event-analysis-appinsights.md)
* [<span data-ttu-id="069be-204">Analiza zdarzeń i wizualizacji z OMS</span><span class="sxs-lookup"><span data-stu-id="069be-204">Event Analysis and Visualization with OMS</span></span>](service-fabric-diagnostics-event-analysis-oms.md)