---
title: "aaaManage usługi Azure Search za pomocą skryptów programu Powershell | Dokumentacja firmy Microsoft"
description: "Zarządzanie za pomocą skryptów środowiska PowerShell usługi Azure Search. Tworzenie lub aktualizowanie usługi Azure Search i zarządzania kluczami administratora usługi Azure Search"
services: search
documentationcenter: 
author: seansaleh
manager: mblythe
editor: 
tags: azure-resource-manager
ms.assetid: 9b3dc1f2-3619-4235-ba1f-d2d6f5c45dd5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: powershell
ms.date: 08/15/2016
ms.author: seasa
ms.openlocfilehash: fc7fb4b025340c77717601e0aaee938be3e9230f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-search-service-with-powershell"></a>Zarządzanie usługą Azure Search przy użyciu programu PowerShell
> [!div class="op_single_selector"]
> * [Portal](search-manage.md)
> * [PowerShell](search-manage-powershell.md)
> 
> 

W tym temacie opisano tooperform poleceń programu PowerShell hello wiele hello zadania zarządzania dla usługi Azure Search. Firma Microsoft przeprowadzi tworzenia usługi wyszukiwania, jej skalowania i zarządzania jego kluczy interfejsu API.
Te polecenia równoległe hello opcji zarządzania dostępnych w hello [interfejsu API REST usługi Azure Search zarządzania](http://msdn.microsoft.com/library/dn832684.aspx).

## <a name="prerequisites"></a>Wymagania wstępne
* Musi mieć programu Azure PowerShell 1.0 lub nowszego. Aby uzyskać instrukcje, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).
* Należy być zalogowanym tooyour subskrypcji platformy Azure w programie PowerShell, zgodnie z poniższym opisem.

Najpierw należy tooAzure logowania za pomocą tego polecenia:

    Login-AzureRmAccount

Określ adres e-mail hello konta platformy Azure i jego hasło w oknie dialogowym logowania Microsoft Azure hello.

Alternatywnie możesz [logowania nieinteraktywnie przy użyciu nazwy głównej usługi](../azure-resource-manager/resource-group-authenticate-service-principal.md).

Jeśli masz wiele subskrypcji Azure, należy tooset subskrypcji platformy Azure. toosee listę bieżących subskrypcji, należy uruchomić to polecenie.

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

toospecify hello subskrypcji, uruchom następujące polecenie hello. Poniższy przykład hello, Nazwa subskrypcji hello jest `ContosoSubscription`.

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

## <a name="commands-toohelp-you-get-started"></a>Toohelp poleceń, które rozpoczęcie pracy
    $serviceName = "your-service-name-lowercase-with-dashes"
    $sku = "free" # or "basic" or "standard" for paid services
    $location = "West US"
    # You can get a list of potential locations with
    # (Get-AzureRmResourceProvider -ListAvailable | Where-Object {$_.ProviderNamespace -eq 'Microsoft.Search'}).Locations
    $resourceGroupName = "YourResourceGroup" 
    # If you don't already have this resource group, you can create it with 
    # New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Register hello ARM provider idempotently. This must be done once per subscription
    Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Search"

    # Create a new search service
    # This command will return once hello service is fully created
    New-AzureRmResourceGroupDeployment `
        -ResourceGroupName $resourceGroupName `
        -TemplateUri "https://gallery.azure.com/artifact/20151001/Microsoft.Search.1.0.9/DeploymentTemplates/searchServiceDefaultTemplate.json" `
        -NameFromTemplate $serviceName `
        -Sku $sku `
        -Location $location `
        -PartitionCount 1 `
        -ReplicaCount 1

    # Get information about your new service and store it in $resource
    $resource = Get-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # View your resource
    $resource

    # Get hello primary admin API key
    $primaryKey = (Invoke-AzureRmResourceAction `
        -Action listAdminKeys `
        -ResourceId $resource.ResourceId `
        -ApiVersion 2015-08-19).PrimaryKey

    # Regenerate hello secondary admin API Key
    $secondaryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/regenerateAdminKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action secondary).SecondaryKey

    # Create a query key for read only access tooyour indexes
    $queryKeyDescription = "query-key-created-from-powershell"
    $queryKey = (Invoke-AzureRmResourceAction `
        -ResourceType "Microsoft.Search/searchServices/createQueryKey" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19 `
        -Action $queryKeyDescription).Key

    # View your query key
    $queryKey

    # Delete query key
    Remove-AzureRmResource `
        -ResourceType "Microsoft.Search/searchServices/deleteQueryKey/$($queryKey)" `
        -ResourceGroupName $resourceGroupName `
        -ResourceName $serviceName `
        -ApiVersion 2015-08-19

    # Scale your service up
    # Note that this will only work if you made a non "free" service
    # This command will not return until hello operation is finished
    # It can take 15 minutes or more tooprovision hello additional resources
    $resource.Properties.ReplicaCount = 2
    $resource | Set-AzureRmResource

    # Delete your service
    # Deleting your service will delete all indexes and data in hello service
    $resource | Remove-AzureRmResource

## <a name="next-steps"></a>Następne kroki
Teraz, gdy usługa jest tworzony, można wykonać kolejne kroki hello: tworzenie [indeksu](search-what-is-an-index.md), [tworzenie zapytań względem indeksu](search-query-overview.md), a na koniec tworzenie i zarządzanie nimi własnych aplikacji wyszukiwania, która używa usługi Azure Search.

* [Tworzenie indeksu usługi Azure Search w portalu Azure hello](search-create-index-portal.md)
* [Zapytanie indeksu usługi Azure Search przy użyciu Eksploratora wyszukiwania w hello portalu Azure](search-explorer.md)
* [Ustawienia danych tooload indeksatora z innych usług](search-indexer-overview.md)
* [Jak toouse Azure wyszukiwania w .NET](search-howto-dotnet-sdk.md)
* [Analiza ruchu w sieci usługi Azure Search](search-traffic-analytics.md)

