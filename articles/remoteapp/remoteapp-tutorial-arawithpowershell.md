---
title: "aaaUse poleceń cmdlet programu PowerShell z usługą Azure RemoteApp | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse poleceń cmdlet programu Windows PowerShell w usłudze Azure RemoteApp."
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
ms.openlocfilehash: a09cae2093e2c3a4a2ed673b5d148a22ceb935f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-windows-powershell-cmdlets-with-azure-remoteapp"></a>Użyj polecenia cmdlet programu Windows PowerShell z usługą Azure RemoteApp
> [!IMPORTANT]
> Usługa Azure RemoteApp nie będzie obsługiwana od 31 sierpnia 2017 r. Witaj odczytu [anonsu](https://go.microsoft.com/fwlink/?linkid=821148) szczegółowe informacje.
> 
> 

 Można użyć tooadminister poleceń cmdlet środowiska PowerShell usługi Azure RemoteApp hello i obsługa kolekcji. Użyj hello następujące informacje tooget uruchomiona.

## <a name="get-hello-cmdlets"></a>Pobierz hello poleceń cmdlet
- - -
Należy najpierw pobrać poleceń cmdlet programu Azure Powershell hello [tutaj](http://go.microsoft.com/?linkid=9811175), poleceń cmdlet funkcji RemoteApp hello znajdują się w nim. 

Zapoznaj się z hello [pomocy polecenia cmdlet usługi Azure RemoteApp](/powershell/module/azure?view=azuresmps-3.7.0).

## <a name="configure-azure-cmdlets-toouse-your-subscription"></a>Skonfiguruj subskrypcję toouse poleceń cmdlet systemu Azure
- - -
Postępuj zgodnie z [w tym przewodniku](/powershell/azure/overview) dzięki czemu można użyć poleceń cmdlet hello względem subskrypcji platformy Azure.

Możesz użyć tych tooget kroki szybko rozpocząć:

1. Pobierz i zainstaluj hello [poleceń cmdlet programu Azure PowerShell](http://go.microsoft.com/?linkid=9811175).
2. Uruchom program PowerShell platformy Microsoft Azure.
3. Uruchom **Add-AzureAccount** tooyour tooauthenticate subskrypcji platformy Azure. Po wyświetleniu monitu wprowadź hello tej samej nazwy użytkownika i hasła, użyj toosign w portalu tooAzure.  
4. Uruchom **Get-AzureSubscription** toolist hello subskrypcji skojarzonych z Twoim kontem użytkownika. 
5. Uruchom **AzureSubscription wybierz — Nazwa subskrypcji &lt;Nazwa subskrypcji&gt;**  lub **AzureSubscription wybierz - SubscriptionId &lt;identyfikator subskrypcji&gt;**  toospecify hello subskrypcji toouse.

Gratulacje, konsola programu Azure PowerShell jest skonfigurowany i gotowy toouse. Należy pamiętać, że musisz mieć toorepeate kroki od 2 do 5 w każdym uruchomieniu konsoli programu Azure PowerShell hello hello.  


## <a name="list-all-collections"></a>Wyświetl listę wszystkich kolekcji
- - -
     Get-AzureRemoteAppCollection

## <a name="delete-a-collection"></a>Usuwanie kolekcji
- - -
    Usuń AzureRemoteAppCollection<enter collection name>

Przykład: `Remove-AzureRemoteAppCollection ContosoProduction`.

## <a name="create-a-cloud-collection"></a>Tworzenie kolekcji w chmurze
- - -
To proste, uruchom następujące polecenie hello:

    New-AzureRemoteAppCollection -Collectionname RAppO365Col1 -ImageName "Office 365 ProPlus (Subscription required)" -Plan Basic -Location "West US" - Description "Office 365 Collection."

Witaj powyżej polecenie automatycznie publikuje aplikacje Microsoft Office 365 (Excel, OneNote, Outlook, PowerPoint, Visio i Word).

Tworzenie kolekcji może potrwać 30 minut lub dłużej toocomplete. Dlatego to polecenie zwraca identyfikator śledzenia, w którym można w następujący sposób:

    Get-AzureRemoteAppOperationResult -TrackingId xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

Po wykonaniu czynności hello kolekcji można dodać kolekcji toohello użytkowników z hello następujące polecenie:

    Add-AzureRemoteAppUser -CollectionName RAppO365Col1 -Type microsoftAccount -UserUpn someone@domain.com

I gotowe! Ten użytkownik powinien być stanie tooconnect toohello aplikacji za pomocą klienta usługi Azure RemoteApp hello znaleziono [tutaj](https://www.remoteapp.windowsazure.com/).

## <a name="available-cmdlets"></a>Dostępne polecenia cmdlet
Istnieje wiele innych poleceń mamy, zostanie udostępniona wkrótce hello dokumentacji dla nich:

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

