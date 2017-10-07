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
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>Wdrażanie usługi Notification Hubs i zarządzanie nią przy użyciu programu PowerShell
## <a name="overview"></a>Omówienie
W tym artykule opisano sposób tworzenia toouse oraz zarządzania usługi Azure Notification Hubs przy użyciu programu PowerShell. następujące typowe zadania dotyczące automatyzacji Hello są wyświetlane w tym temacie.

* Tworzenie Centrum powiadomień
* Ustawianie poświadczeń

Jeśli potrzebujesz również toocreate nowego przestrzeń nazw magistrali usług dla Twojej usługi notification hubs, zobacz [zarządzania usługi Service Bus przy użyciu programu PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).

Zarządzanie centra powiadomień nie jest obsługiwane bezpośrednio przez polecenia cmdlet hello dołączone do programu Azure PowerShell. najlepsze rozwiązania Hello ze środowiska PowerShell jest tooreference hello Microsoft.Azure.NotificationHubs.dll zestawu. zestaw Hello jest dystrybuowane z hello [pakietu NuGet platformy Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem tego artykułu, musi mieć następujące hello:

* Subskrypcja platformy Azure. Azure to platforma subskrypcji. Aby uzyskać więcej informacji na temat uzyskiwania subskrypcji, zobacz [opcje zakupu], [oferty Członkowskie], lub [bezpłatnej wersji próbnej].
* Komputer z programem Azure PowerShell. Aby uzyskać instrukcje, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell].
* Ogólny opis skryptów programu PowerShell, pakietami NuGet i hello .NET Framework.

## <a name="including-a-reference-toohello-net-assembly-for-service-bus"></a>W tym zestaw .NET toohello odwołania dla usługi Service Bus
Zarządzanie usługą Azure Notification Hubs nie jest jeszcze dołączony hello poleceń cmdlet programu PowerShell w programie Azure PowerShell. centra powiadomień tooprovision, można użyć w powitania klienta .NET hello [pakietu NuGet platformy Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Najpierw upewnij się, skrypt może zlokalizować hello **Microsoft.Azure.NotificationHubs.dll** zestawu, który jest instalowany jako pakietu NuGet w projekcie programu Visual Studio. W kolejności toobe elastyczne skrypt hello wykonuje następujące czynności:

1. Określa ścieżkę hello jaką został wywołany.
2. Traverses hello ścieżki, aż do znalezienia folder o nazwie `packages`. Ten folder jest tworzony podczas instalowania pakietów NuGet dla projektów programu Visual Studio.
3. Rekursywnie wyszukuje hello `packages` folder dla zestawu o nazwie **Microsoft.Azure.NotificationHubs.dll**.
4. Odwołania hello zestawu, dzięki czemu hello typy są dostępne do późniejszego użycia.

Oto implementowania skrypt programu PowerShell następujące kroki:

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

## <a name="create-hello-namespacemanager-class"></a>Utwórz klasę NamespaceManager hello
tooprovision Notification Hubs, Utwórz wystąpienie hello [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) klasy z hello zestawu SDK. 

Można użyć hello [Get-AzureSBAuthorizationRule] polecenia cmdlet dołączone do programu Azure PowerShell tooretrieve reguły autoryzacji, która została użyta tooprovide ciąg połączenia. Firma Microsoft będzie przechowywać toohello odwołanie `NamespaceManager` wystąpienie w hello `$NamespaceManager` zmiennej. Używamy `$NamespaceManager` tooprovision Centrum powiadomień.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create hello NamespaceManager object toocreate hello hub
Write-Output "Creating a NamespaceManager object for hello [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for hello [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>Inicjowanie obsługi nowego centrum powiadomień
tooprovision nowego centrum powiadomień, użyj hello [interfejs API .NET dla usługi Notification Hubs].

W tej części skryptu hello skonfigurowaniu czterech zmiennych lokalnych. 

1. `$Namespace`: Ta toohello Nazwa zestawu hello przestrzeni nazw, w którym ma toocreate Centrum powiadomień.
2. `$Path`: Ustaw ten toohello ścieżka hello nowego centrum powiadomień.  Na przykład "MyHub".    
3. `$WnsPackageSid`: Zestaw identyfikator SID pakietu toohello aplikacji systemu Windows z hello [Centrum deweloperów systemu Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).
4. `$WnsSecretkey`: Ustaw ten klucz tajny toohello dla Ciebie aplikacji systemu Windows z hello [Centrum deweloperów systemu Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).

Te zmienne są używane tooconnect tooyour w przestrzeni nazw i Utwórz nowe toohandle Centrum powiadomień skonfigurowane powiadomienia usługi WNS (Windows Notification) przy użyciu poświadczeń usługi WNS aplikacji systemu Windows. Aby uzyskać informacje dotyczące hello pakietu identyfikator SID i tajnego klucza, zobacz temat hello [wprowadzenie do korzystania z usługi Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) samouczka. 

* fragment kodu skryptu Hello używa hello `NamespaceManager` obiekt toocheck toosee, zostanie oznaczona hello Centrum powiadomień `$Path` istnieje.
* Jeśli nie istnieje, zostanie utworzona skryptu hello `NotificationHubDescription` z usługą WNS poświadczenia, a następnie przekaż tego toohello `NamespaceManager` klasy `CreateNotificationHub` metody.

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




## <a name="additional-resources"></a>Dodatkowe zasoby
* [Zarządzanie usługi Service Bus przy użyciu programu PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [Jak toocreate usługi Service Bus kolejki, tematy i subskrypcje za pomocą skryptu programu PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Jak toocreate a Namespace magistrali usługi i Centrum zdarzeń za pomocą skryptu programu PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

Niektóre skrypty gotowe są także dostępne do pobrania:

* [Skrypty programu PowerShell usługi Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-PowerShell-a46b7059)

[opcje zakupu]: http://azure.microsoft.com/pricing/purchase-options/
[oferty Członkowskie]: http://azure.microsoft.com/pricing/member-offers/
[bezpłatnej wersji próbnej]: http://azure.microsoft.com/pricing/free-trial/
[Instalowanie i konfigurowanie programu Azure PowerShell]: /powershell/azureps-cmdlets-docs
[interfejs API .NET dla usługi Notification Hubs]: https://msdn.microsoft.com/library/azure/mt414893.aspx
[Get-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495122.aspx
[New-AzureSBNamespace]: https://msdn.microsoft.com/library/azure/dn495165.aspx
[Get-AzureSBAuthorizationRule]: https://msdn.microsoft.com/library/azure/dn495113.aspx

