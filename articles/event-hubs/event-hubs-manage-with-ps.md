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
# <a name="use-powershell-toomanage-event-hubs-resources"></a>Korzystanie z zasobów usługi Event Hubs toomanage programu PowerShell

Microsoft Azure PowerShell jest środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania usługami Azure. W tym artykule opisano sposób toouse hello [modułu programu PowerShell Menedżera zasobów centrów zdarzeń](/powershell/module/azurerm.eventhub) tooprovision i zarządzanie nimi jednostek usługi Event Hubs (obszary nazw, centra zdarzeń w poszczególnych i grupy konsumentów) przy użyciu lokalnej konsoli programu Azure PowerShell lub skrypt.

Można również zarządzać zasobami usługi Event Hubs przy użyciu szablonów usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz artykuł hello [tworzenie przestrzeni nazw usługi Event Hubs z grupy koncentratora i odbiorców zdarzeń przy użyciu szablonu usługi Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem, potrzebne są następujące hello:

* Subskrypcja platformy Azure. Aby uzyskać więcej informacji na temat uzyskiwania subskrypcji, zobacz [opcji zakupu][purchase options], [oferty Członkowskie][member offers], lub [bezpłatne konto][free account].
* Komputer z programem Azure PowerShell. Aby uzyskać instrukcje, zobacz [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/get-started-azureps).
* Ogólny opis skryptów programu PowerShell, pakietami NuGet i hello .NET Framework.

## <a name="get-started"></a>Rozpoczęcie pracy

Witaj pierwszym krokiem jest toouse toolog programu PowerShell w tooyour konto platformy Azure i subskrypcji platformy Azure. Postępuj zgodnie z instrukcjami hello [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/get-started-azureps) toolog w tooyour konto platformy Azure, następnie pobrać i uzyskiwać dostęp do zasobów hello w Twojej subskrypcji platformy Azure.

## <a name="provision-an-event-hubs-namespace"></a>Należy do przestrzeni nazw usługi Event Hubs

Podczas pracy z przestrzeni nazw usługi Event Hubs, można użyć hello [Get-AzureRmEventHubNamespace](/powershell/module/azurerm.eventhub/get-azurermeventhubnamespace), [AzureRmEventHubNamespace nowy](/powershell/module/azurerm.eventhub/new-azurermeventhubnamespace), [AzureRmEventHubNamespace Usuń](/powershell/module/azurerm.eventhub/remove-azurermeventhubnamespace) , a [AzureRmEventHubNamespace zestaw](/powershell/module/azurerm.eventhub/set-azurermeventhubnamespace) polecenia cmdlet.

W tym przykładzie powoduje utworzenie kilku zmiennych lokalnych w skrypcie hello; `$Namespace` i `$Location`.

* `$Namespace`jest nazwą hello hello nazw centra zdarzeń, z którą chcemy toowork.
* `$Location`identyfikuje hello centrum danych, w którym będzie możemy udostępnić hello przestrzeni nazw.
* `$CurrentNamespace`przechowuje nazw odwołania hello możemy pobrać (lub Utwórz).

W skrypcie rzeczywiste `$Namespace` i `$Location` mogą być przekazywane jako parametry.

Ta część skryptu hello hello następujące:

1. Tooretrieve prób centra zdarzeń w obszarze nazw hello określono nazwę.
2. Przestrzeń nazw hello zostanie znaleziony, raporty, co znaleziono.
3. Jeśli przestrzeń nazw hello nie zostanie znaleziony, tworzy hello przestrzeni nazw i następnie pobiera hello nowo utworzonego obszaru nazw.

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

## <a name="create-an-event-hub"></a>Tworzenie centrum zdarzeń

Sprawdzanie przestrzeni nazw przy użyciu skryptu hello w poprzedniej sekcji hello przeprowadzić toocreate Centrum zdarzeń. Następnie należy użyć hello [AzureRmEventHub nowy](/powershell/module/azurerm.eventhub/new-azurermeventhub) Centrum zdarzeń hello toocreate polecenia cmdlet:

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

### <a name="create-a-consumer-group"></a>Tworzenie grupy odbiorców

toocreate grupy odbiorców w ramach Centrum zdarzeń, sprawdzana jest hello przestrzeni nazw i zdarzenia Centrum skryptów hello w poprzedniej sekcji hello. Następnie należy użyć hello [AzureRmEventHubConsumerGroup nowy](/powershell/module/azurerm.eventhub/new-azurermeventhubconsumergroup) grupy odbiorców hello toocreate polecenia cmdlet w ramach Centrum zdarzeń hello. Na przykład:

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

#### <a name="set-user-metadata"></a>Zestaw metadanych użytkownika

Po wykonaniu hello skryptów w powyższej sekcji hello, można użyć hello [AzureRmEventHubConsumerGroup zestaw](/powershell/module/azurerm.eventhub/set-azurermeventhubconsumergroup) polecenia cmdlet tooupdate hello właściwości grupy konsumentów, tak jak hello poniższy przykład:

```powershell
# Set some user metadata on hello CG
Write-Host "Setting hello UserMetadata field too'Testing'"
Set-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName -UserMetadata "Testing"
# Show result
Get-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
```

## <a name="remove-event-hub"></a>Usuń Centrum zdarzeń

centra zdarzeń hello tooremove został utworzony, można użyć hello `Remove-*` jak hello poniższy przykład polecenia cmdlet:

```powershell
# Clean up
Remove-AzureRmEventHubConsumerGroup -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName -ConsumerGroupName $ConsumerGroupName
Remove-AzureRmEventHub -ResourceGroupName $ResGrpName -NamespaceName $Namespace -EventHubName $EventHubName
Remove-AzureRmEventHubNamespace -ResourceGroupName $ResGrpName -NamespaceName $Namespace
```

## <a name="next-steps"></a>Następne kroki

- Zobacz pełną dokumentację modułu programu PowerShell Menedżera zasobów centrów zdarzeń hello [tutaj](/powershell/module/azurerm.eventhub). Ta strona zawiera listę wszystkich dostępnych poleceń cmdlet.
- Aby uzyskać informacje dotyczące korzystania z szablonów usługi Azure Resource Manager, zobacz artykuł hello [tworzenie przestrzeni nazw usługi Event Hubs z grupy koncentratora i odbiorców zdarzeń przy użyciu szablonu usługi Azure Resource Manager](event-hubs-resource-manager-namespace-event-hub.md).
- Informacje o [biblioteki zarządzania .NET centra zdarzeń](event-hubs-management-libraries.md).

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
