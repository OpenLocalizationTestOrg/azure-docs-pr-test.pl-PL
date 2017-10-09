---
title: "zasoby usługi Azure Service Bus toomanage PowerShell aaaUse | Dokumentacja firmy Microsoft"
description: "Użyj toocreate modułu programu PowerShell i zarządzanie zasobami usługi Service Bus"
services: service-bus-messaging
documentationcenter: .NET
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/06/2017
ms.author: sethm
ms.openlocfilehash: 737044def913c5798e7e05fc4f1aeece76c8f4dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomanage-service-bus-resources"></a>Korzystanie z zasobów usługi Service Bus toomanage środowiska PowerShell

Microsoft Azure PowerShell jest środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania usługami Azure. W tym artykule opisano sposób toouse hello [modułu programu PowerShell dla Menedżera zasobów usługi magistrali](/powershell/module/azurerm.servicebus) tooprovision i zarządzanie nimi jednostek usługi Service Bus (przestrzeni nazw, kolejki, tematy i subskrypcje) przy użyciu lokalnej konsoli programu Azure PowerShell lub skrypt.

Można również zarządzać jednostek usługi Service Bus przy użyciu szablonów usługi Azure Resource Manager. Aby uzyskać więcej informacji, zobacz artykuł hello [zasobów usługi Service Bus utworzyć przy użyciu szablonów usługi Azure Resource Manager](service-bus-resource-manager-overview.md).

## <a name="prerequisites"></a>Wymagania wstępne

Przed rozpoczęciem, potrzebne są następujące hello:

* Subskrypcja platformy Azure. Aby uzyskać więcej informacji na temat uzyskiwania subskrypcji, zobacz [opcji zakupu][purchase options], [oferty Członkowskie][member offers], lub [bezpłatne konto][free account].
* Komputer z programem Azure PowerShell. Aby uzyskać instrukcje, zobacz [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/get-started-azureps).
* Ogólny opis skryptów programu PowerShell, pakietami NuGet i hello .NET Framework.

## <a name="get-started"></a>Rozpoczęcie pracy

Witaj pierwszym krokiem jest toouse toolog programu PowerShell w tooyour konto platformy Azure i subskrypcji platformy Azure. Postępuj zgodnie z instrukcjami hello [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/get-started-azureps) toolog tooyour konto platformy Azure i pobieranie oraz dostęp do zasobów hello w Twojej subskrypcji platformy Azure.

## <a name="provision-a-service-bus-namespace"></a>Zainicjuj obsługę przestrzeni nazw usługi Service Bus

Podczas pracy z przestrzeni nazw usługi Service Bus, można użyć hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [AzureRmServiceBusNamespace nowy](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), i [AzureRmServiceBusNamespace zestaw](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) polecenia cmdlet.

W tym przykładzie powoduje utworzenie kilku zmiennych lokalnych w skrypcie hello; `$Namespace` i `$Location`.

* `$Namespace`to nazwa hello hello nazw usługi Service Bus, z którą chcemy toowork.
* `$Location`identyfikuje hello centrum danych, w którym będzie możemy udostępnić hello przestrzeni nazw.
* `$CurrentNamespace`przechowuje nazw odwołania hello możemy pobrać (lub Utwórz).

W skrypcie rzeczywiste `$Namespace` i `$Location` mogą być przekazywane jako parametry.

Ta część skryptu hello hello następujące:

1. Tooretrieve prób przestrzeni nazw usługi Service Bus z hello określono nazwę.
2. Przestrzeń nazw hello zostanie znaleziony, raporty, co znaleziono.
3. Jeśli przestrzeń nazw hello nie zostanie znaleziony, tworzy hello przestrzeni nazw i następnie pobiera hello nowo utworzonego obszaru nazw.
   
    ``` powershell
    # Query toosee if hello namespace currently exists
    $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
   
    # Check if hello namespace already exists or needs toobe created
    if ($CurrentNamespace)
    {
        Write-Host "hello namespace $Namespace already exists in hello $Location region:"
        # Report what was found
        Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
    }
    else
    {
        Write-Host "hello $Namespace namespace does not exist."
        Write-Host "Creating hello $Namespace namespace in hello $Location region..."
        New-AzureRmServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace -Location $Location
        $CurrentNamespace = Get-AzureRMServiceBusNamespace -ResourceGroup $ResGrpName -NamespaceName $Namespace
        Write-Host "hello $Namespace namespace in Resource Group $ResGrpName in hello $Location region has been successfully created."
                
    }
    ```

### <a name="create-a-namespace-authorization-rule"></a>Utwórz regułę autoryzacji przestrzeni nazw

Witaj poniższy przykład przedstawia sposób hello toomanage reguł autoryzacji dla przestrzeni nazw przy użyciu [AzureRmServiceBusNamespaceAuthorizationRule nowy](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [AzureRmServiceBusNamespaceAuthorizationRule zestaw](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), i [polecenia cmdlet Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).

```powershell
# Query toosee if rule exists
$CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

# Check if hello rule already exists or needs toobe created
if ($CurrentRule)
{
    Write-Host "hello $AuthRule rule already exists for hello namespace $Namespace."
}
else
{
    Write-Host "hello $AuthRule rule does not exist."
    Write-Host "Creating hello $AuthRule rule for hello $Namespace namespace..."
    New-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule -Rights @("Listen","Send")
    $CurrentRule = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
    Write-Host "hello $AuthRule rule for hello $Namespace namespace has been successfully created."

    Write-Host "Setting rights on hello namespace"
    $authRuleObj = Get-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule

    Write-Host "Remove Send rights"
    $authRuleObj.Rights.Remove("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Add Send and Manage rights toohello namespace"
    $authRuleObj.Rights.Add("Send")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj
    $authRuleObj.Rights.Add("Manage")
    Set-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthRuleObj $authRuleObj

    Write-Host "Show value of primary key"
    $CurrentKey = Get-AzureRmServiceBusNamespaceKey -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
        
    Write-Host "Remove this authorization rule"
    Remove-AzureRmServiceBusNamespaceAuthorizationRule -ResourceGroup $ResGrpName -NamespaceName $Namespace -AuthorizationRuleName $AuthRule
}
```

## <a name="create-a-queue"></a>Tworzenie kolejki

toocreate kolejka lub temat, należy przeprowadzić przy użyciu skryptu hello w poprzedniej sekcji hello sprawdzania przestrzeni nazw. Następnie utwórz kolejkę hello:

```powershell
# Check if queue already exists
$CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName

if($CurrentQ)
{
    Write-Host "hello queue $QueueName already exists in hello $Location region:"
}
else
{
    Write-Host "hello $QueueName queue does not exist."
    Write-Host "Creating hello $QueueName queue in hello $Location region..."
    New-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -EnablePartitioning $True
    $CurrentQ = Get-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName
    Write-Host "hello $QueueName queue in Resource Group $ResGrpName in hello $Location region has been successfully created."
}
```

### <a name="modify-queue-properties"></a>Modyfikowanie właściwości kolejki

Po wykonaniu skryptu hello w powyższej sekcji hello, można użyć hello [AzureRmServiceBusQueue zestaw](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) polecenia cmdlet tooupdate hello właściwości kolejki, tak jak hello poniższy przykład:

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a>Inicjowanie obsługi innych jednostek usługi Service Bus

Można użyć hello [modułu programu PowerShell usługi Service Bus](/powershell/module/azurerm.servicebus) tooprovision inne jednostki, na przykład tematów i subskrypcji. Te polecenia cmdlet są podobne składniowo toohello kolejki Tworzenie polecenia cmdlet przedstawiona w poprzedniej sekcji hello.

## <a name="next-steps"></a>Następne kroki

- Zobacz pełną dokumentację modułu programu PowerShell Menedżera zasobów usługi magistrali hello [tutaj](/powershell/module/azurerm.servicebus). Ta strona zawiera listę wszystkich dostępnych poleceń cmdlet.
- Aby uzyskać informacje dotyczące korzystania z szablonów usługi Azure Resource Manager, zobacz artykuł hello [zasobów usługi Service Bus utworzyć przy użyciu szablonów usługi Azure Resource Manager](service-bus-resource-manager-overview.md).
- Informacje o [biblioteki zarządzania .NET magistrali usługi](service-bus-management-libraries.md).

Istnieje kilka metod alternatywnych toomanage jednostek usługi Service Bus, zgodnie z opisem w wpisy na blogu:

* [Jak toocreate usługi Service Bus kolejki, tematy i subskrypcje za pomocą skryptu programu PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Jak toocreate a Namespace magistrali usługi i Centrum zdarzeń za pomocą skryptu programu PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [Skrypty programu PowerShell usługi Service Bus](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
