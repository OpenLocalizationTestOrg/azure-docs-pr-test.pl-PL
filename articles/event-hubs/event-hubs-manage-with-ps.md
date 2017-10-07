---
title: "zasoby usługi Azure Event Hubs toomanage PowerShell aaaUse | Dokumentacja firmy Microsoft"
description: "Użyj toocreate modułu programu PowerShell i zarządzanie nimi centra zdarzeń"
services: event-hubs
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: d79cb307c2b4a031d059ce6ca67117ffc0b4600b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-event-hubs-resources"></a><span data-ttu-id="9704f-103">Korzystanie z zasobów usługi Event Hubs toomanage programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="9704f-103">Use PowerShell toomanage Event Hubs resources</span></span>

<span data-ttu-id="9704f-104">Microsoft Azure PowerShell jest środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="9704f-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="9704f-105">W tym artykule opisano sposób toouse hello [modułu programu PowerShell Menedżera zasobów centrów zdarzeń](/powershell/module/azurerm.eventhub) tooprovision i zarządzanie nimi jednostek usługi Event Hubs (obszary nazw, centra zdarzeń w poszczególnych i grupy konsumentów) przy użyciu lokalnej konsoli programu Azure PowerShell lub skrypt.</span><span class="sxs-lookup"><span data-stu-id="9704f-105">This article describes how toouse hello [Event Hubs Resource Manager PowerShell module](/powershell/module/azurerm.eventhub) tooprovision and manage Event Hubs entities (namespaces, individual event hubs, and consumer groups) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="9704f-106">Można również zarządzać zasobami usługi Event Hubs przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9704f-106">You can also manage Event Hubs resources using Azure Resource Manager templates.</span></span> <span data-ttu-id="9704f-107">Aby uzyskać więcej informacji, zobacz artykuł hello [tworzenie przestrzeni nazw usługi Event Hubs z grupy koncentratora i odbiorców zdarzeń przy użyciu szablonu usługi Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9704f-107">For more information, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9704f-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="9704f-108">Prerequisites</span></span>

<span data-ttu-id="9704f-109">Przed rozpoczęciem, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="9704f-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="9704f-110">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9704f-110">An Azure subscription.</span></span> <span data-ttu-id="9704f-111">Aby uzyskać więcej informacji na temat uzyskiwania subskrypcji, zobacz [opcji zakupu][purchase options], [oferty Członkowskie][member offers], lub [bezpłatne konto][free account].</span><span class="sxs-lookup"><span data-stu-id="9704f-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="9704f-112">Komputer z programem Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9704f-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="9704f-113">Aby uzyskać instrukcje, zobacz [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="9704f-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="9704f-114">Ogólny opis skryptów programu PowerShell, pakietami NuGet i hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="9704f-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="9704f-115">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="9704f-115">Get started</span></span>

<span data-ttu-id="9704f-116">Witaj pierwszym krokiem jest toouse toolog programu PowerShell w tooyour konto platformy Azure i subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9704f-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="9704f-117">Postępuj zgodnie z instrukcjami hello [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/get-started-azureps) toolog w tooyour konto platformy Azure, następnie pobrać i uzyskiwać dostęp do zasobów hello w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9704f-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, then retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-an-event-hubs-namespace"></a><span data-ttu-id="9704f-118">Należy do przestrzeni nazw usługi Event Hubs</span><span class="sxs-lookup"><span data-stu-id="9704f-118">Provision an Event Hubs namespace</span></span>

<span data-ttu-id="9704f-119">Podczas pracy z przestrzeni nazw usługi Event Hubs, można użyć hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [AzureRmEventHubNamespace nowy](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [AzureRmEventHubNamespace Usuń](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , a [AzureRmEventHubNamespace zestaw](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9704f-119">When working with Event Hubs namespaces, you can use hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [New-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [Remove-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace), and [Set-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) cmdlets.</span></span>

<span data-ttu-id="9704f-120">W tym przykładzie powoduje utworzenie kilku zmiennych lokalnych w skrypcie hello; `$Namespace` i `$Location`.</span><span class="sxs-lookup"><span data-stu-id="9704f-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="9704f-121">`$Namespace`jest nazwą hello hello nazw centra zdarzeń, z którą chcemy toowork.</span><span class="sxs-lookup"><span data-stu-id="9704f-121">`$Namespace` is hello name of hello Event Hubs namespace with which we want toowork.</span></span>
* <span data-ttu-id="9704f-122">`$Location`identyfikuje hello centrum danych, w którym będzie możemy udostępnić hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="9704f-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="9704f-123">`$CurrentNamespace`przechowuje nazw odwołania hello możemy pobrać (lub Utwórz).</span><span class="sxs-lookup"><span data-stu-id="9704f-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="9704f-124">W skrypcie rzeczywiste `$Namespace` i `$Location` mogą być przekazywane jako parametry.</span><span class="sxs-lookup"><span data-stu-id="9704f-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="9704f-125">Ta część skryptu hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="9704f-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="9704f-126">Tooretrieve prób centra zdarzeń w obszarze nazw hello określono nazwę.</span><span class="sxs-lookup"><span data-stu-id="9704f-126">Attempts tooretrieve an Event Hubs namespace with hello specified name.</span></span>
2. <span data-ttu-id="9704f-127">Przestrzeń nazw hello zostanie znaleziony, raporty, co znaleziono.</span><span class="sxs-lookup"><span data-stu-id="9704f-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="9704f-128">Jeśli przestrzeń nazw hello nie zostanie znaleziony, tworzy hello przestrzeni nazw i następnie pobiera hello nowo utworzonego obszaru nazw.</span><span class="sxs-lookup"><span data-stu-id="9704f-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>

    ```powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
    }
    ```

## <a name="create-an-event-hub"></a><span data-ttu-id="9704f-129">Tworzenie centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="9704f-129">Create an event hub</span></span>

<span data-ttu-id="9704f-130">Sprawdzanie przestrzeni nazw przy użyciu skryptu hello w poprzedniej sekcji hello przeprowadzić toocreate Centrum zdarzeń.</span><span class="sxs-lookup"><span data-stu-id="9704f-130">toocreate an event hub, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="9704f-131">Następnie należy użyć hello [AzureRmEventHub nowy](/powershell/module/azurerm.eventhub/new-azurermeventhub) Centrum zdarzeń hello toocreate polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9704f-131">Then, use hello [New-AzureRmEventHub](/powershell/module/azurerm.eventhub/new-azurermeventhub) cmdlet toocreate hello event hub:</span></span>

```powershell
# Check if event hub already exists
$CurrentEH = Get-AzureRMEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName

if($CurrentEH)
{
    Write-Host "hello event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $EventHubName event hub does not exist."
    Write-Host "Creating hello $EventHubName event hub in hello $Location region..."
    New-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -Location $Location -MessageRetentionInDays 3
    $CurrentEH = Get-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $EventHubName event hub in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="create-a-consumer-group"></a><span data-ttu-id="9704f-132">Tworzenie grupy odbiorców</span><span class="sxs-lookup"><span data-stu-id="9704f-132">Create a consumer group</span></span>

<span data-ttu-id="9704f-133">toocreate grupy odbiorców w ramach Centrum zdarzeń, sprawdzana jest hello przestrzeni nazw i zdarzenia Centrum skryptów hello w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="9704f-133">toocreate a consumer group within an event hub, perform hello namespace and event hub checks using hello scripts in hello previous section.</span></span> <span data-ttu-id="9704f-134">Następnie należy użyć hello [AzureRmEventHubConsumerGroup nowy](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) grupy odbiorców hello toocreate polecenia cmdlet w ramach Centrum zdarzeń hello.</span><span class="sxs-lookup"><span data-stu-id="9704f-134">Then, use hello [New-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) cmdlet toocreate hello consumer group within hello event hub.</span></span> <span data-ttu-id="9704f-135">Na przykład:</span><span class="sxs-lookup"><span data-stu-id="9704f-135">For example:</span></span>

```powershell
# Check if consumer group already exists
$CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -ErrorAction Ignore

if($CurrentCG)
{
    Write-Host "hello consumer group $ConsumerGroupName in event hub $EventHubName already exists in hello $Location region:"
    # Report what was found
    Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
}
else
{
    Write-Host "hello $ConsumerGroupName consumer group does not exist."
    Write-Host "Creating hello $ConsumerGroupName consumer group in hello $Location region..."
    New-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
    $CurrentCG = Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
    Write-Host "hello $ConsumerGroupName consumer group in event hub $EventHubName in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

#### <a name="set-user-metadata"></a><span data-ttu-id="9704f-136">Zestaw metadanych użytkownika</span><span class="sxs-lookup"><span data-stu-id="9704f-136">Set user metadata</span></span>

<span data-ttu-id="9704f-137">Po wykonaniu hello skryptów w powyższej sekcji hello, można użyć hello [AzureRmEventHubConsumerGroup zestaw](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) polecenia cmdlet tooupdate hello właściwości grupy konsumentów, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="9704f-137">After executing hello scripts in hello preceding sections, you can use hello [Set-AzureRmEventHubConsumerGroup](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) cmdlet tooupdate hello properties of a consumer group, as in hello following example:</span></span>

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a><span data-ttu-id="9704f-138">Usuń Centrum zdarzeń</span><span class="sxs-lookup"><span data-stu-id="9704f-138">Remove event hub</span></span>

<span data-ttu-id="9704f-139">centra zdarzeń hello tooremove został utworzony, można użyć hello `Remove-*` jak hello poniższy przykład polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9704f-139">tooremove hello event hubs you created, you can use hello `Remove-*` cmdlets, as in hello following example:</span></span>

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a><span data-ttu-id="9704f-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9704f-140">Next steps</span></span>

- <span data-ttu-id="9704f-141">Zobacz pełną dokumentację modułu programu PowerShell Menedżera zasobów centrów zdarzeń hello [tutaj](/powershell/module/azurerm.eventhub).</span><span class="sxs-lookup"><span data-stu-id="9704f-141">See hello complete Event Hubs Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.eventhub).</span></span> <span data-ttu-id="9704f-142">Ta strona zawiera listę wszystkich dostępnych poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9704f-142">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="9704f-143">Aby uzyskać informacje dotyczące korzystania z szablonów usługi Azure Resource Manager, zobacz artykuł hello [tworzenie przestrzeni nazw usługi Event Hubs z grupy koncentratora i odbiorców zdarzeń przy użyciu szablonu usługi Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9704f-143">For information about using Azure Resource Manager templates, see hello article [Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template](event-hubs-resource-manager-namespace-event-hub.md).</span></span>
- <span data-ttu-id="9704f-144">Informacje o [biblioteki zarządzania .NET centra zdarzeń](event-hubs-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="9704f-144">Information about [Event Hubs .NET management libraries](event-hubs-management-libraries.md).</span></span>

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
