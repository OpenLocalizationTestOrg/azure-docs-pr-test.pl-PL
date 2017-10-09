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
# <a name="use-powershell-toomanage-service-bus-resources"></a><span data-ttu-id="71044-103">Korzystanie z zasobów usługi Service Bus toomanage środowiska PowerShell</span><span class="sxs-lookup"><span data-stu-id="71044-103">Use PowerShell toomanage Service Bus resources</span></span>

<span data-ttu-id="71044-104">Microsoft Azure PowerShell jest środowisko obsługi skryptów, można użyć toocontrol i zautomatyzować hello wdrażania i zarządzania usługami Azure.</span><span class="sxs-lookup"><span data-stu-id="71044-104">Microsoft Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of Azure services.</span></span> <span data-ttu-id="71044-105">W tym artykule opisano sposób toouse hello [modułu programu PowerShell dla Menedżera zasobów usługi magistrali](/powershell/module/azurerm.servicebus) tooprovision i zarządzanie nimi jednostek usługi Service Bus (przestrzeni nazw, kolejki, tematy i subskrypcje) przy użyciu lokalnej konsoli programu Azure PowerShell lub skrypt.</span><span class="sxs-lookup"><span data-stu-id="71044-105">This article describes how toouse hello [Service Bus Resource Manager PowerShell module](/powershell/module/azurerm.servicebus) tooprovision and manage Service Bus entities (namespaces, queues, topics, and subscriptions) using a local Azure PowerShell console or script.</span></span>

<span data-ttu-id="71044-106">Można również zarządzać jednostek usługi Service Bus przy użyciu szablonów usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="71044-106">You can also manage Service Bus entities using Azure Resource Manager templates.</span></span> <span data-ttu-id="71044-107">Aby uzyskać więcej informacji, zobacz artykuł hello [zasobów usługi Service Bus utworzyć przy użyciu szablonów usługi Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71044-107">For more information, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71044-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="71044-108">Prerequisites</span></span>

<span data-ttu-id="71044-109">Przed rozpoczęciem, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="71044-109">Before you begin, you'll need hello following:</span></span>

* <span data-ttu-id="71044-110">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71044-110">An Azure subscription.</span></span> <span data-ttu-id="71044-111">Aby uzyskać więcej informacji na temat uzyskiwania subskrypcji, zobacz [opcji zakupu][purchase options], [oferty Członkowskie][member offers], lub [bezpłatne konto][free account].</span><span class="sxs-lookup"><span data-stu-id="71044-111">For more information about obtaining a subscription, see [purchase options][purchase options], [member offers][member offers], or [free account][free account].</span></span>
* <span data-ttu-id="71044-112">Komputer z programem Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="71044-112">A computer with Azure PowerShell.</span></span> <span data-ttu-id="71044-113">Aby uzyskać instrukcje, zobacz [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/get-started-azureps).</span><span class="sxs-lookup"><span data-stu-id="71044-113">For instructions, see [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps).</span></span>
* <span data-ttu-id="71044-114">Ogólny opis skryptów programu PowerShell, pakietami NuGet i hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="71044-114">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="get-started"></a><span data-ttu-id="71044-115">Rozpoczęcie pracy</span><span class="sxs-lookup"><span data-stu-id="71044-115">Get started</span></span>

<span data-ttu-id="71044-116">Witaj pierwszym krokiem jest toouse toolog programu PowerShell w tooyour konto platformy Azure i subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71044-116">hello first step is toouse PowerShell toolog in tooyour Azure account and Azure subscription.</span></span> <span data-ttu-id="71044-117">Postępuj zgodnie z instrukcjami hello [wprowadzenie do poleceń cmdlet programu Azure PowerShell](/powershell/azure/get-started-azureps) toolog tooyour konto platformy Azure i pobieranie oraz dostęp do zasobów hello w Twojej subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="71044-117">Follow hello instructions in [Get started with Azure PowerShell cmdlets](/powershell/azure/get-started-azureps) toolog in tooyour Azure account, and retrieve and access hello resources in your Azure subscription.</span></span>

## <a name="provision-a-service-bus-namespace"></a><span data-ttu-id="71044-118">Zainicjuj obsługę przestrzeni nazw usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="71044-118">Provision a Service Bus namespace</span></span>

<span data-ttu-id="71044-119">Podczas pracy z przestrzeni nazw usługi Service Bus, można użyć hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [AzureRmServiceBusNamespace nowy](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), i [AzureRmServiceBusNamespace zestaw](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71044-119">When working with Service Bus namespaces, you can use hello [Get-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespace), [New-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespace), [Remove-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespace), and [Set-AzureRmServiceBusNamespace](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespace) cmdlets.</span></span>

<span data-ttu-id="71044-120">W tym przykładzie powoduje utworzenie kilku zmiennych lokalnych w skrypcie hello; `$Namespace` i `$Location`.</span><span class="sxs-lookup"><span data-stu-id="71044-120">This example creates a few local variables in hello script; `$Namespace` and `$Location`.</span></span>

* <span data-ttu-id="71044-121">`$Namespace`to nazwa hello hello nazw usługi Service Bus, z którą chcemy toowork.</span><span class="sxs-lookup"><span data-stu-id="71044-121">`$Namespace` is hello name of hello Service Bus namespace with which we want toowork.</span></span>
* <span data-ttu-id="71044-122">`$Location`identyfikuje hello centrum danych, w którym będzie możemy udostępnić hello przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="71044-122">`$Location` identifies hello data center in which will we provision hello namespace.</span></span>
* <span data-ttu-id="71044-123">`$CurrentNamespace`przechowuje nazw odwołania hello możemy pobrać (lub Utwórz).</span><span class="sxs-lookup"><span data-stu-id="71044-123">`$CurrentNamespace` stores hello reference namespace that we retrieve (or create).</span></span>

<span data-ttu-id="71044-124">W skrypcie rzeczywiste `$Namespace` i `$Location` mogą być przekazywane jako parametry.</span><span class="sxs-lookup"><span data-stu-id="71044-124">In an actual script, `$Namespace` and `$Location` can be passed as parameters.</span></span>

<span data-ttu-id="71044-125">Ta część skryptu hello hello następujące:</span><span class="sxs-lookup"><span data-stu-id="71044-125">This part of hello script does hello following:</span></span>

1. <span data-ttu-id="71044-126">Tooretrieve prób przestrzeni nazw usługi Service Bus z hello określono nazwę.</span><span class="sxs-lookup"><span data-stu-id="71044-126">Attempts tooretrieve a Service Bus namespace with hello specified name.</span></span>
2. <span data-ttu-id="71044-127">Przestrzeń nazw hello zostanie znaleziony, raporty, co znaleziono.</span><span class="sxs-lookup"><span data-stu-id="71044-127">If hello namespace is found, it reports what was found.</span></span>
3. <span data-ttu-id="71044-128">Jeśli przestrzeń nazw hello nie zostanie znaleziony, tworzy hello przestrzeni nazw i następnie pobiera hello nowo utworzonego obszaru nazw.</span><span class="sxs-lookup"><span data-stu-id="71044-128">If hello namespace is not found, it creates hello namespace and then retrieves hello newly created namespace.</span></span>
   
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

### <a name="create-a-namespace-authorization-rule"></a><span data-ttu-id="71044-129">Utwórz regułę autoryzacji przestrzeni nazw</span><span class="sxs-lookup"><span data-stu-id="71044-129">Create a namespace authorization rule</span></span>

<span data-ttu-id="71044-130">Witaj poniższy przykład przedstawia sposób hello toomanage reguł autoryzacji dla przestrzeni nazw przy użyciu [AzureRmServiceBusNamespaceAuthorizationRule nowy](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [AzureRmServiceBusNamespaceAuthorizationRule zestaw](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), i [polecenia cmdlet Remove-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span><span class="sxs-lookup"><span data-stu-id="71044-130">hello following example shows how toomanage namespace authorization rules using hello [New-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/new-azurermservicebusnamespaceauthorizationrule), [Get-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/get-azurermservicebusnamespaceauthorizationrule), [Set-AzureRmServiceBusNamespaceAuthorizationRule](/powershell/module/azurerm.servicebus/set-azurermservicebusnamespaceauthorizationrule), and [Remove-AzureRmServiceBusNamespaceAuthorizationRule cmdlets](/powershell/module/azurerm.servicebus/remove-azurermservicebusnamespaceauthorizationrule).</span></span>

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

## <a name="create-a-queue"></a><span data-ttu-id="71044-131">Tworzenie kolejki</span><span class="sxs-lookup"><span data-stu-id="71044-131">Create a queue</span></span>

<span data-ttu-id="71044-132">toocreate kolejka lub temat, należy przeprowadzić przy użyciu skryptu hello w poprzedniej sekcji hello sprawdzania przestrzeni nazw.</span><span class="sxs-lookup"><span data-stu-id="71044-132">toocreate a queue or topic, perform a namespace check using hello script in hello previous section.</span></span> <span data-ttu-id="71044-133">Następnie utwórz kolejkę hello:</span><span class="sxs-lookup"><span data-stu-id="71044-133">Then, create hello queue:</span></span>

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

### <a name="modify-queue-properties"></a><span data-ttu-id="71044-134">Modyfikowanie właściwości kolejki</span><span class="sxs-lookup"><span data-stu-id="71044-134">Modify queue properties</span></span>

<span data-ttu-id="71044-135">Po wykonaniu skryptu hello w powyższej sekcji hello, można użyć hello [AzureRmServiceBusQueue zestaw](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) polecenia cmdlet tooupdate hello właściwości kolejki, tak jak hello poniższy przykład:</span><span class="sxs-lookup"><span data-stu-id="71044-135">After executing hello script in hello preceding section, you can use hello [Set-AzureRmServiceBusQueue](/powershell/module/azurerm.servicebus/set-azurermservicebusqueue) cmdlet tooupdate hello properties of a queue, as in hello following example:</span></span>

```powershell
$CurrentQ.DeadLetteringOnMessageExpiration = $True
$CurrentQ.MaxDeliveryCount = 7
$CurrentQ.MaxSizeInMegabytes = 2048
$CurrentQ.EnableExpress = $True

Set-AzureRmServiceBusQueue -ResourceGroup $ResGrpName -NamespaceName $Namespace -QueueName $QueueName -QueueObj $CurrentQ
```

## <a name="provisioning-other-service-bus-entities"></a><span data-ttu-id="71044-136">Inicjowanie obsługi innych jednostek usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="71044-136">Provisioning other Service Bus entities</span></span>

<span data-ttu-id="71044-137">Można użyć hello [modułu programu PowerShell usługi Service Bus](/powershell/module/azurerm.servicebus) tooprovision inne jednostki, na przykład tematów i subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="71044-137">You can use hello [Service Bus PowerShell module](/powershell/module/azurerm.servicebus) tooprovision other entities, such as topics and subscriptions.</span></span> <span data-ttu-id="71044-138">Te polecenia cmdlet są podobne składniowo toohello kolejki Tworzenie polecenia cmdlet przedstawiona w poprzedniej sekcji hello.</span><span class="sxs-lookup"><span data-stu-id="71044-138">These cmdlets are syntactically similar toohello queue creation cmdlets demonstrated in hello previous section.</span></span>

## <a name="next-steps"></a><span data-ttu-id="71044-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="71044-139">Next steps</span></span>

- <span data-ttu-id="71044-140">Zobacz pełną dokumentację modułu programu PowerShell Menedżera zasobów usługi magistrali hello [tutaj](/powershell/module/azurerm.servicebus).</span><span class="sxs-lookup"><span data-stu-id="71044-140">See hello complete Service Bus Resource Manager PowerShell module documentation [here](/powershell/module/azurerm.servicebus).</span></span> <span data-ttu-id="71044-141">Ta strona zawiera listę wszystkich dostępnych poleceń cmdlet.</span><span class="sxs-lookup"><span data-stu-id="71044-141">This page lists all available cmdlets.</span></span>
- <span data-ttu-id="71044-142">Aby uzyskać informacje dotyczące korzystania z szablonów usługi Azure Resource Manager, zobacz artykuł hello [zasobów usługi Service Bus utworzyć przy użyciu szablonów usługi Azure Resource Manager](service-bus-resource-manager-overview.md).</span><span class="sxs-lookup"><span data-stu-id="71044-142">For information about using Azure Resource Manager templates, see hello article [Create Service Bus resources using Azure Resource Manager templates](service-bus-resource-manager-overview.md).</span></span>
- <span data-ttu-id="71044-143">Informacje o [biblioteki zarządzania .NET magistrali usługi](service-bus-management-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="71044-143">Information about [Service Bus .NET management libraries](service-bus-management-libraries.md).</span></span>

<span data-ttu-id="71044-144">Istnieje kilka metod alternatywnych toomanage jednostek usługi Service Bus, zgodnie z opisem w wpisy na blogu:</span><span class="sxs-lookup"><span data-stu-id="71044-144">There are some alternate ways toomanage Service Bus entities, as described in these blog posts:</span></span>

* [<span data-ttu-id="71044-145">Jak toocreate usługi Service Bus kolejki, tematy i subskrypcje za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="71044-145">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="71044-146">Jak toocreate a Namespace magistrali usługi i Centrum zdarzeń za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="71044-146">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)
* [<span data-ttu-id="71044-147">Skrypty programu PowerShell usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="71044-147">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/Service-Bus-PowerShell-a46b7059)

<!--Anchors-->

[purchase options]: http://azure.microsoft.com/pricing/purchase-options/
[member offers]: http://azure.microsoft.com/pricing/member-offers/
[free account]: http://azure.microsoft.com/pricing/free-trial/
