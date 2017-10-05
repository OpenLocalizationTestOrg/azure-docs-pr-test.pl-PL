---
title: "Użyj polecenia cmdlet programu PowerShell z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać poleceń cmdlet programu Windows PowerShell w usłudze Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: guscatalano
manager: mbaldwin
editor: 
ms.assetid: 7d3d5ded-6f73-4de6-a8ac-c1d622e842a2
ms.service: remoteapp
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: compute
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 699b20a4dadd4ecaff57e2cc80355fe545360663
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Użyj polecenia cmdlet programu Windows PowerShell z usługą Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Szczegółowe informacje zawiera [powiadomienie](https://go.microsoft.com/fwlink/?linkid=821148).
> 
> 

 Do administrowania i obsługa kolekcji, można użyć poleceń cmdlet środowiska PowerShell usługi Azure RemoteApp. Skorzystaj z poniższych informacji, aby rozpocząć pracę.

## <a name="get-the-cmdlets"></a>Polecenia cmdlet Get
- - -
Polecenia cmdlet programu Azure Powershell należy najpierw pobrać [tutaj](http://go.microsoft.com/?linkid=9811175), poleceń cmdlet programu RemoteApp znajdują się w nim. 

Zapoznaj się z [pomocy polecenia cmdlet usługi Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-to-use-your-subscription"></a>Konfigurowanie polecenia cmdlet systemu Azure, aby korzystać z subskrypcji
- - -
Postępuj zgodnie z [w tym przewodniku](/powershell/azure/overview) dzięki czemu można użyć poleceń cmdlet dla Twojej subskrypcji platformy Azure.

Korzystania z tych kroków, aby szybko rozpocząć pracę:

1. Pobierz i zainstaluj [poleceń cmdlet programu Azure PowerShell](http://go.microsoft.com/?linkid=9811175).
2. Uruchom program PowerShell platformy Microsoft Azure.
3. Uruchom **Add-AzureAccount** do uwierzytelniania do subskrypcji platformy Azure. Po wyświetleniu monitu wprowadź tej samej nazwy użytkownika i hasło, którego używasz do logowania do portalu Azure.  
4. Uruchom **Get-AzureSubscription** na liście subskrypcji skojarzonych z Twoim kontem użytkownika. 
5. Uruchom **AzureSubscription wybierz — Nazwa subskrypcji &lt;Nazwa subskrypcji&gt;**  lub **AzureSubscription wybierz - SubscriptionId &lt;identyfikator subskrypcji&gt;**  Aby określić subskrypcję do użycia.

Gratulacje, konsola programu Azure PowerShell jest skonfigurowana i gotowa do użycia. Należy pamiętać, że konieczne będzie repeate kroki od 2 do 5 w każdym uruchomieniu konsoli programu Azure PowerShell.  


## <a name="list-all-collections"></a>Wyświetl listę wszystkich kolekcji
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Usuwanie kolekcji
- - -
    Usuń AzureRemoteAppCollection<enter collection name>

Przykład: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Tworzenie kolekcji w chmurze
- - -
To proste, uruchom następujące polecenie:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Powyższe polecenie automatycznie publikuje aplikacje Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio i Word).

Tworzenie kolekcji może potrwać 30 minut lub dłużej. Dlatego to polecenie zwraca identyfikator śledzenia, w którym można w następujący sposób:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Po zakończeniu kolekcji można dodać użytkowników do kolekcji przy użyciu następującego polecenia:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

I gotowe! Ten użytkownik powinien móc połączyć się z aplikacją za pomocą klienta usługi Azure RemoteApp, znaleziono [tutaj](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Dostępne polecenia cmdlet
Istnieje wiele innych poleceń mamy, zostanie wkrótce udostępniona w dokumentacji:

Podstawowe kolekcji usługi RemoteApp poleceń cmdlet: 

* New-AzureRemoteAppCollection
* Get-AzureRemoteAppCollection
* Set-AzureRemoteAppCollection
* Update-AzureRemoteAppCollection
* Remove-AzureRemoteAppCollection
* Add-AzureRemoteAppUser
* Get-AzureRemoteAppUser
* Remove-AzureRemoteAppUser
* Get-AzureRemoteAppSession
* Disconnect-AzureRemoteAppSession
* Invoke-AzureRemoteAppSessionLogoff
* Send-AzureRemoteAppSessionMessage
* Get-AzureRemoteAppProgram
* Get-AzureRemoteAppStartMenuProgram
* Publish-AzureRemoteAppProgram
* Unpublish-AzureRemoteAppProgram
* Get-AzureRemoteAppCollectionUsageDetails
* Get-AzureRemoteAppCollectionUsageSummary
* Get-AzureRemoteAppPlan

Polecenia cmdlet sieci wirtualnej usługi RemoteApp:

* New-AzureRemoteAppVNet
* Get-AzureRemoteAppVNet
* Set-AzureRemoteAppVNet
* Remove-AzureRemoteAppVNet
* Get-AzureRemoteAppVpnDevice
* Get - AzureRemoteAppVpnDeviceConfigScript
* Reset-AzureRemoteAppVpnSharedKey

Polecenia cmdlet obrazu szablonu usługi RemoteApp:

* New-AzureRemoteAppTemplateImage
* Get-AzureRemoteAppTemplateImage
* Rename-AzureRemoteAppTemplateImage
* Remove-AzureRemoteAppTemplateImage

Inne polecenia cmdlet usługi RemoteApp:

* Get-AzureRemoteAppLocation
* Get-AzureRemoteAppWorkspace
* Set-AzureRemoteAppWorkspace
* Get-AzureRemoteAppOperationResult

