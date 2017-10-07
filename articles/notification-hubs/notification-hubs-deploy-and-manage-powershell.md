---
title: "aaaDeploy i zarządzanie Notification Hubs przy użyciu programu PowerShell"
description: "Jak tooCreate i zarządzanie Notification Hubs przy użyciu programu PowerShell automatyzacji"
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 7c58f2c8-0399-42bc-9e1e-a7f073426451
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8835bdefa0d360354263eab8040259ad08281771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a><span data-ttu-id="59e48-103">Wdrażanie usługi Notification Hubs i zarządzanie nią przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="59e48-103">Deploy and Manage Notification Hubs using PowerShell</span></span>
## <a name="overview"></a><span data-ttu-id="59e48-104">Omówienie</span><span class="sxs-lookup"><span data-stu-id="59e48-104">Overview</span></span>
<span data-ttu-id="59e48-105">W tym artykule opisano sposób tworzenia toouse oraz zarządzania usługi Azure Notification Hubs przy użyciu programu PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59e48-105">This article shows you how toouse Create and Manage Azure Notification Hubs using PowerShell.</span></span> <span data-ttu-id="59e48-106">następujące typowe zadania dotyczące automatyzacji Hello są wyświetlane w tym temacie.</span><span class="sxs-lookup"><span data-stu-id="59e48-106">hello following common automation tasks are shown in this topic.</span></span>

* <span data-ttu-id="59e48-107">Tworzenie Centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="59e48-107">Create a Notification Hub</span></span>
* <span data-ttu-id="59e48-108">Ustawianie poświadczeń</span><span class="sxs-lookup"><span data-stu-id="59e48-108">Set Credentials</span></span>

<span data-ttu-id="59e48-109">Jeśli potrzebujesz również toocreate nowego przestrzeń nazw magistrali usług dla Twojej usługi notification hubs, zobacz [zarządzania usługi Service Bus przy użyciu programu PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span><span class="sxs-lookup"><span data-stu-id="59e48-109">If you also need toocreate a new service bus namespace for your notification hubs, see [Manage Service Bus with PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).</span></span>

<span data-ttu-id="59e48-110">Zarządzanie centra powiadomień nie jest obsługiwane bezpośrednio przez polecenia cmdlet hello dołączone do programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59e48-110">Managing Notifications Hubs is not supported directly by hello cmdlets included with Azure PowerShell.</span></span> <span data-ttu-id="59e48-111">najlepsze rozwiązania Hello ze środowiska PowerShell jest tooreference hello Microsoft.Azure.NotificationHubs.dll zestawu.</span><span class="sxs-lookup"><span data-stu-id="59e48-111">hello best approach from PowerShell is tooreference hello Microsoft.Azure.NotificationHubs.dll assembly.</span></span> <span data-ttu-id="59e48-112">zestaw Hello jest dystrybuowane z hello [pakietu NuGet platformy Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="59e48-112">hello assembly is distributed with hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59e48-113">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="59e48-113">Prerequisites</span></span>
<span data-ttu-id="59e48-114">Przed rozpoczęciem tego artykułu, musi mieć następujące hello:</span><span class="sxs-lookup"><span data-stu-id="59e48-114">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="59e48-115">Subskrypcja platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="59e48-115">An Azure subscription.</span></span> <span data-ttu-id="59e48-116">Azure to platforma subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="59e48-116">Azure is a subscription-based platform.</span></span> <span data-ttu-id="59e48-117">Aby uzyskać więcej informacji na temat uzyskiwania subskrypcji, zobacz [opcje zakupu], [oferty Członkowskie], lub [bezpłatnej wersji próbnej].</span><span class="sxs-lookup"><span data-stu-id="59e48-117">For more information about obtaining a subscription, see [Purchase Options], [Member Offers], or [Free Trial].</span></span>
* <span data-ttu-id="59e48-118">Komputer z programem Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59e48-118">A computer with Azure PowerShell.</span></span> <span data-ttu-id="59e48-119">Aby uzyskać instrukcje, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="59e48-119">For instructions, see [Install and configure Azure PowerShell].</span></span>
* <span data-ttu-id="59e48-120">Ogólny opis skryptów programu PowerShell, pakietami NuGet i hello .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="59e48-120">A general understanding of PowerShell scripts, NuGet packages, and hello .NET Framework.</span></span>

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a><span data-ttu-id="59e48-121">W tym zestaw .NET toohello odwołania dla usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="59e48-121">Including a reference toohello .NET assembly for Service Bus</span></span>
<span data-ttu-id="59e48-122">Zarządzanie usługą Azure Notification Hubs nie jest jeszcze dołączony hello poleceń cmdlet programu PowerShell w programie Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="59e48-122">Managing Azure Notification Hubs is not yet included with hello PowerShell cmdlets in Azure PowerShell.</span></span> <span data-ttu-id="59e48-123">centra powiadomień tooprovision, można użyć w powitania klienta .NET hello [pakietu NuGet platformy Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="59e48-123">tooprovision notification hubs, you can use hello .NET client provided in hello [Microsoft Azure Notification Hubs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>

<span data-ttu-id="59e48-124">Najpierw upewnij się, skrypt może zlokalizować hello **Microsoft.Azure.NotificationHubs.dll** zestawu, który jest instalowany jako pakietu NuGet w projekcie programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59e48-124">First, make sure your script can locate hello **Microsoft.Azure.NotificationHubs.dll** assembly, which is installed as a NuGet package in a Visual Studio project.</span></span> <span data-ttu-id="59e48-125">W kolejności toobe elastyczne skrypt hello wykonuje następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="59e48-125">In order toobe flexible, hello script performs these steps:</span></span>

1. <span data-ttu-id="59e48-126">Określa ścieżkę hello jaką został wywołany.</span><span class="sxs-lookup"><span data-stu-id="59e48-126">Determines hello path at which it was invoked.</span></span>
2. <span data-ttu-id="59e48-127">Traverses hello ścieżki, aż do znalezienia folder o nazwie `packages`.</span><span class="sxs-lookup"><span data-stu-id="59e48-127">Traverses hello path until it finds a folder named `packages`.</span></span> <span data-ttu-id="59e48-128">Ten folder jest tworzony podczas instalowania pakietów NuGet dla projektów programu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59e48-128">This folder is created when you install NuGet packages for Visual Studio projects.</span></span>
3. <span data-ttu-id="59e48-129">Rekursywnie wyszukuje hello `packages` folder dla zestawu o nazwie **Microsoft.Azure.NotificationHubs.dll**.</span><span class="sxs-lookup"><span data-stu-id="59e48-129">Recursively searches hello `packages` folder for an assembly named **Microsoft.Azure.NotificationHubs.dll**.</span></span>
4. <span data-ttu-id="59e48-130">Odwołania hello zestawu, dzięki czemu hello typy są dostępne do późniejszego użycia.</span><span class="sxs-lookup"><span data-stu-id="59e48-130">References hello assembly so that hello types are available for later use.</span></span>

<span data-ttu-id="59e48-131">Oto implementowania skrypt programu PowerShell następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="59e48-131">Here's how these steps are implemented in a PowerShell script:</span></span>

``` powershell

try
{
    # WARNING: Make sure tooreference hello latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding hello [Microsoft.Azure.NotificationHubs.dll] assembly toohello script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "hello [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added toohello script."
}

catch [System.Exception]
{
    Write-Error("Could not add hello Microsoft.Azure.NotificationHubs.dll assembly toohello script. Make sure you build hello solution before running hello provisioning script.")
}
```

## <a name="create-hello-namespacemanager-class"></a><span data-ttu-id="59e48-132">Utwórz klasę NamespaceManager hello</span><span class="sxs-lookup"><span data-stu-id="59e48-132">Create hello NamespaceManager class</span></span>
<span data-ttu-id="59e48-133">tooprovision Notification Hubs, Utwórz wystąpienie hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) klasy z hello zestawu SDK.</span><span class="sxs-lookup"><span data-stu-id="59e48-133">tooprovision Notification Hubs, create an instance of hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) class from hello SDK.</span></span> 

<span data-ttu-id="59e48-134">Można użyć hello [Get-AzureSBAuthorizationRule] polecenia cmdlet dołączone do programu Azure PowerShell tooretrieve reguły autoryzacji, która została użyta tooprovide ciąg połączenia.</span><span class="sxs-lookup"><span data-stu-id="59e48-134">You can use hello [Get-AzureSBAuthorizationRule] cmdlet included with Azure PowerShell tooretrieve an authorization rule that's used tooprovide a connection string.</span></span> <span data-ttu-id="59e48-135">Firma Microsoft będzie przechowywać toohello odwołanie `NamespaceManager` wystąpienie w hello `$NamespaceManager` zmiennej.</span><span class="sxs-lookup"><span data-stu-id="59e48-135">We'll store a reference toohello `NamespaceManager` instance in hello `$NamespaceManager` variable.</span></span> <span data-ttu-id="59e48-136">Używamy `$NamespaceManager` tooprovision Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="59e48-136">We will use `$NamespaceManager` tooprovision a notification hub.</span></span>

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a><span data-ttu-id="59e48-137">Inicjowanie obsługi nowego centrum powiadomień</span><span class="sxs-lookup"><span data-stu-id="59e48-137">Provisioning a new Notification Hub</span></span>
<span data-ttu-id="59e48-138">tooprovision nowego centrum powiadomień, użyj hello [interfejs API .NET dla usługi Notification Hubs].</span><span class="sxs-lookup"><span data-stu-id="59e48-138">tooprovision a new notification hub, use hello [.NET API for Notification Hubs].</span></span>

<span data-ttu-id="59e48-139">W tej części skryptu hello skonfigurowaniu czterech zmiennych lokalnych.</span><span class="sxs-lookup"><span data-stu-id="59e48-139">In this part of hello script you set up four local variables.</span></span> 

1. <span data-ttu-id="59e48-140">`$Namespace`: Ta toohello Nazwa zestawu hello przestrzeni nazw, w którym ma toocreate Centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="59e48-140">`$Namespace` : Set this toohello name of hello namespace where you want toocreate a notification hub.</span></span>
2. <span data-ttu-id="59e48-141">`$Path`: Ustaw ten toohello ścieżka hello nowego centrum powiadomień.</span><span class="sxs-lookup"><span data-stu-id="59e48-141">`$Path` : Set this path toohello name of hello new notification hub.</span></span>  <span data-ttu-id="59e48-142">Na przykład "MyHub".</span><span class="sxs-lookup"><span data-stu-id="59e48-142">For example, "MyHub".</span></span>    
3. <span data-ttu-id="59e48-143">`$WnsPackageSid`: Zestaw identyfikator SID pakietu toohello aplikacji systemu Windows z hello [Centrum deweloperów systemu Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="59e48-143">`$WnsPackageSid` : Set this toohello package SID for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>
4. <span data-ttu-id="59e48-144">`$WnsSecretkey`: Ustaw ten klucz tajny toohello dla Ciebie aplikacji systemu Windows z hello [Centrum deweloperów systemu Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="59e48-144">`$WnsSecretkey`: Set this toohello secret key for you Windows App from hello [Windows Dev Center](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).</span></span>

<span data-ttu-id="59e48-145">Te zmienne są używane tooconnect tooyour w przestrzeni nazw i Utwórz nowe toohandle Centrum powiadomień skonfigurowane powiadomienia usługi WNS (Windows Notification) przy użyciu poświadczeń usługi WNS aplikacji systemu Windows.</span><span class="sxs-lookup"><span data-stu-id="59e48-145">These variables are used tooconnect tooyour namespace and create a new Notification Hub configured toohandle Windows Notification Services (WNS) notifications with WNS credentials for a Windows App.</span></span> <span data-ttu-id="59e48-146">Aby uzyskać informacje dotyczące hello pakietu identyfikator SID i tajnego klucza, zobacz temat hello [wprowadzenie do korzystania z usługi Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) samouczka.</span><span class="sxs-lookup"><span data-stu-id="59e48-146">For information on obtaining hello package SID and secret key see, hello [Getting Started with Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) tutorial.</span></span> 

* <span data-ttu-id="59e48-147">fragment kodu skryptu Hello używa hello `NamespaceManager` obiekt toocheck toosee, zostanie oznaczona hello Centrum powiadomień `$Path` istnieje.</span><span class="sxs-lookup"><span data-stu-id="59e48-147">hello script snippet uses hello `NamespaceManager` object toocheck toosee if hello Notification Hub identified by `$Path` exists.</span></span>
* <span data-ttu-id="59e48-148">Jeśli nie istnieje, zostanie utworzona skryptu hello `NotificationHubDescription` z usługą WNS poświadczenia, a następnie przekaż tego toohello `NamespaceManager` klasy `CreateNotificationHub` metody.</span><span class="sxs-lookup"><span data-stu-id="59e48-148">If it does not exist, hello script will create an `NotificationHubDescription` with WNS credentials and pass that toohello `NamespaceManager` class `CreateNotificationHub` method.</span></span>

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query hello namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if hello namespace already exists
if ($CurrentNamespace)
{
    Write-Output "hello namespace [$Namespace] in hello [$($CurrentNamespace.Region)] region was found."

    # Create hello NamespaceManager object used toocreate a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."

    # Check toosee if hello Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "hello [$Path] notification hub already exists in hello [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating hello [$Path] notification hub in hello [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "hello [$Path] notification hub was created in hello [$Namespace] namespace."
    }
}
else
{
    Write-Host "hello [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a><span data-ttu-id="59e48-149">Dodatkowe zasoby</span><span class="sxs-lookup"><span data-stu-id="59e48-149">Additional Resources</span></span>
* [<span data-ttu-id="59e48-150">Zarządzanie usługi Service Bus przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="59e48-150">Manage Service Bus with PowerShell</span></span>](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="59e48-151">Jak toocreate usługi Service Bus kolejki, tematy i subskrypcje za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="59e48-151">How toocreate Service Bus queues, topics and subscriptions using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [<span data-ttu-id="59e48-152">Jak toocreate a Namespace magistrali usługi i Centrum zdarzeń za pomocą skryptu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="59e48-152">How toocreate a Service Bus Namespace and an Event Hub using a PowerShell script</span></span>](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

<span data-ttu-id="59e48-153">Niektóre skrypty gotowe są także dostępne do pobrania:</span><span class="sxs-lookup"><span data-stu-id="59e48-153">Some ready-made scripts are also available for download:</span></span>

* [<span data-ttu-id="59e48-154">Skrypty programu PowerShell usługi Service Bus</span><span class="sxs-lookup"><span data-stu-id="59e48-154">Service Bus PowerShell Scripts</span></span>](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[opcje zakupu]: http://azure.microsoft.com/pricing/purchase-options/
[oferty Członkowskie]: http://azure.microsoft.com/pricing/member-offers/
[bezpłatnej wersji próbnej]: http://azure.microsoft.com/pricing/free-trial/
[Instalowanie i konfigurowanie programu Azure PowerShell]: /powershell/azureps-cmdlets-docs
[interfejs API .NET dla usługi Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

