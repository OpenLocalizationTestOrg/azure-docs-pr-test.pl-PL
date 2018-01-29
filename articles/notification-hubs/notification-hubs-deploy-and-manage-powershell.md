---
title: "Wdrażanie usługi Notification Hubs i zarządzanie nią przy użyciu programu PowerShell"
description: "Jak tworzyć i zarządzać nimi przy użyciu programu PowerShell do automatyzacji centra powiadomień"
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
ms.openlocfilehash: 4db058e4bd91dc287b14e887abc6c378c65c4a2b
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/11/2017
---
# <a name="deploy-and-manage-notification-hubs-using-powershell"></a>Wdrażanie usługi Notification Hubs i zarządzanie nią przy użyciu programu PowerShell
## <a name="overview"></a>Omówienie
W tym artykule przedstawiono sposób tworzenia i zarządzania usługi Azure Notification Hubs przy użyciu programu PowerShell. Następujące typowe zadania automatyzacji są wyświetlane w tym temacie.

* Tworzenie Centrum powiadomień
* Ustawianie poświadczeń

Jeśli musisz również utworzyć nowy przestrzeń nazw magistrali usług, dla Twojej usługi notification hubs, zobacz [zarządzania usługi Service Bus przy użyciu programu PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md).

Zarządzanie centra powiadomień nie jest obsługiwane bezpośrednio przez poleceń cmdlet programu Azure PowerShell. Najlepszym rozwiązaniem z programu PowerShell jest odwołać się do zestawu Microsoft.Azure.NotificationHubs.dll. Zestaw jest dystrybuowane z [pakietu NuGet platformy Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

## <a name="prerequisites"></a>Wymagania wstępne
Przed rozpoczęciem korzystania z informacji zawartych w tym artykule należy dysponować następującymi elementami:

* Subskrypcja platformy Azure. Azure to platforma subskrypcji. Aby uzyskać więcej informacji na temat uzyskiwania subskrypcji, zobacz [opcje zakupu], [oferty Członkowskie], lub [bezpłatnej wersji próbnej].
* Komputer z programem Azure PowerShell. Aby uzyskać instrukcje, zobacz [Instalowanie i konfigurowanie programu Azure PowerShell].
* Ogólny opis skryptów programu PowerShell, pakietami NuGet i .NET Framework.

## <a name="including-a-reference-to-the-net-assembly-for-service-bus"></a>W tym odwołanie do zestawu .NET dla usługi Service Bus
Zarządzanie usługą Azure Notification Hubs nie jest jeszcze dołączony do poleceń cmdlet programu PowerShell w programie Azure PowerShell. Aby udostępnić usługi notification hubs, można użyć klienta programu .NET w [pakietu NuGet platformy Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).

Najpierw upewnij się, można znaleźć skryptu **Microsoft.Azure.NotificationHubs.dll** zestawu, który jest instalowany jako pakietu NuGet w projekcie programu Visual Studio. Aby mogła być elastyczne, skrypt wykonuje następujące czynności:

1. Określa ścieżkę, w którym został wywołany.
2. Ścieżka jest przesyłany do momentu znalezienia folder o nazwie `packages`. Ten folder jest tworzony podczas instalowania pakietów NuGet dla projektów programu Visual Studio.
3. Rekursywnie wyszukuje `packages` folder dla zestawu o nazwie **Microsoft.Azure.NotificationHubs.dll**.
4. Odwołuje się do zestawu, dzięki czemu typy są dostępne do późniejszego użycia.

Oto implementowania skrypt programu PowerShell następujące kroki:

``` powershell

try
{
    # WARNING: Make sure to reference the latest version of Microsoft.Azure.NotificationHubs.dll
    Write-Output "Adding the [Microsoft.Azure.NotificationHubs.dll] assembly to the script..."
    $scriptPath = Split-Path (Get-Variable MyInvocation -Scope 0).Value.MyCommand.Path
    $packagesFolder = (Split-Path $scriptPath -Parent) + "\packages"
    $assembly = Get-ChildItem $packagesFolder -Include "Microsoft.Azure.NotificationHubs.dll" -Recurse
    Add-Type -Path $assembly.FullName

    Write-Output "The [Microsoft.Azure.NotificationHubs.dll] assembly has been successfully added to the script."
}

catch [System.Exception]
{
    Write-Error("Could not add the Microsoft.Azure.NotificationHubs.dll assembly to the script. Make sure you build the solution before running the provisioning script.")
}
```

## <a name="create-the-namespacemanager-class"></a>Utwórz klasę NamespaceManager
Aby udostępnić usługi Notification Hubs, Utwórz wystąpienie [NamespaceManager](https://msdn.microsoft.com/library/azure/microsoft.azure.notificationhubs.namespacemanager.aspx) klasy z zestawu SDK. 

Można użyć [Get-AzureSBAuthorizationRule] polecenia cmdlet dołączone do programu Azure PowerShell można pobrać reguły autoryzacji, która służy do zapewnienia ciąg połączenia. Firma Microsoft będzie przechowywać odwołanie do `NamespaceManager` wystąpienia w `$NamespaceManager` zmiennej. Używamy `$NamespaceManager` do udostępnienia Centrum powiadomień.

``` powershell
$sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
# Create the NamespaceManager object to create the hub
Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
$NamespaceManager=[Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."
```


## <a name="provisioning-a-new-notification-hub"></a>Inicjowanie obsługi nowego centrum powiadomień
Aby udostępnić nowe Centrum powiadomień, należy użyć [interfejs API .NET dla usługi Notification Hubs].

Ta część skrypt służy do konfigurowania czterech zmiennych lokalnych. 

1. `$Namespace`: Ustaw na nazwę obszaru nazw, której chcesz utworzyć Centrum powiadomień.
2. `$Path`: Ustaw tę ścieżkę nazwę nowego centrum powiadomień.  Na przykład "MyHub".    
3. `$WnsPackageSid`: Ustaw tę wartość na identyfikator SID pakietu dla Ciebie aplikacji systemu Windows z [Centrum deweloperów systemu Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).
4. `$WnsSecretkey`: Ustaw tę wartość na klucz tajny dla Ciebie aplikacji systemu Windows z [Centrum deweloperów systemu Windows](http://go.microsoft.com/fwlink/p/?linkid=266582&clcid=0x409).

Te zmienne są używane do połączyć się z obszarem nazw i Utwórz nowe Centrum powiadomień skonfigurowane do obsługi powiadomienia usługi WNS (Windows Notification) przy użyciu poświadczeń usługi WNS aplikacji systemu Windows. Aby uzyskać informacje dotyczące pakietu identyfikator SID i tajnego klucza, zobacz temat [wprowadzenie do korzystania z usługi Notification Hubs](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) samouczka. 

* Fragment kodu skryptu używa `NamespaceManager` obiekt, aby sprawdzić, czy Centrum powiadomień jest identyfikowane przez `$Path` istnieje.
* Jeśli nie istnieje, zostanie utworzony skrypt `NotificationHubDescription` z usługą WNS poświadczenia i że w celu przekazania `NamespaceManager` klasy `CreateNotificationHub` metody.

``` powershell

$Namespace = "<Enter your namespace>"
$Path  = "<Enter a name for your notification hub>"
$WnsPackageSid = "<your package sid>"
$WnsSecretkey = "<enter your secret key>"

$WnsCredential = New-Object -TypeName Microsoft.Azure.NotificationHubs.WnsCredential -ArgumentList $WnsPackageSid,$WnsSecretkey

# Query the namespace
$CurrentNamespace = Get-AzureSBNamespace -Name $Namespace

# Check if the namespace already exists
if ($CurrentNamespace)
{
    Write-Output "The namespace [$Namespace] in the [$($CurrentNamespace.Region)] region was found."

    # Create the NamespaceManager object used to create a new notification hub
    $sbr = Get-AzureSBAuthorizationRule -Namespace $Namespace
    Write-Output "Creating a NamespaceManager object for the [$Namespace] namespace..."
    $NamespaceManager = [Microsoft.Azure.NotificationHubs.NamespaceManager]::CreateFromConnectionString($sbr.ConnectionString);
    Write-Output "NamespaceManager object for the [$Namespace] namespace has been successfully created."

    # Check to see if the Notification Hub already exists
    if ($NamespaceManager.NotificationHubExists($Path))
    {
        Write-Output "The [$Path] notification hub already exists in the [$Namespace] namespace."  
    }
    else
    {
        Write-Output "Creating the [$Path] notification hub in the [$Namespace] namespace."
        $NHDescription = New-Object -TypeName Microsoft.Azure.NotificationHubs.NotificationHubDescription -ArgumentList $Path;
        $NHDescription.WnsCredential = $WnsCredential;
        $NamespaceManager.CreateNotificationHub($NHDescription);
        Write-Output "The [$Path] notification hub was created in the [$Namespace] namespace."
    }
}
else
{
    Write-Host "The [$Namespace] namespace does not exist."
}
```




## <a name="additional-resources"></a>Dodatkowe zasoby
* [Zarządzanie usługi Service Bus przy użyciu programu PowerShell](../service-bus-messaging/service-bus-powershell-how-to-provision.md)
* [Tworzenie usługi Service Bus kolejki, tematy i subskrypcje, za pomocą skryptu programu PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/02/how-to-create-a-service-bus-queues-topics-and-subscriptions-using-a-powershell-script.aspx)
* [Jak utworzyć Namespace magistrali usługi i Centrum zdarzeń za pomocą skryptu programu PowerShell](http://blogs.msdn.com/b/paolos/archive/2014/12/01/how-to-create-a-service-bus-namespace-and-an-event-hub-using-a-powershell-script.aspx)

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

