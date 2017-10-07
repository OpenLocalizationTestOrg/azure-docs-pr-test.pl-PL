---
title: "aaaManage Azure CDN przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toouse hello toomanage poleceń cmdlet programu Azure PowerShell usługi Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: fb6f57a5-6e26-4847-8fd9-b51fb05a79eb
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 269373136d4ef018e4d31f147456b4be2253b463
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-cdn-with-powershell"></a>Zarządzanie Azure CDN przy użyciu programu PowerShell
PowerShell zawiera jedną z najbardziej elastycznym toomanage metody hello punktów końcowych i profile usługi Azure CDN.  Można użyć programu PowerShell, interakcyjnego lub pisząc skrypty tooautomate zadań zarządzania.  W tym samouczku przedstawiono kilka najbardziej typowych zadań hello można wykonać za pomocą programu PowerShell toomanage punktów końcowych i profile usługi Azure CDN.

## <a name="prerequisites"></a>Wymagania wstępne
toouse toomanage środowiska PowerShell usługi Azure CDN profile i punkty końcowe musi mieć zainstalowany moduł Azure PowerShell hello.  toolearn jak tooinstall programu Azure PowerShell i nawiąż połączenie przy użyciu hello tooAzure `Login-AzureRmAccount` polecenia cmdlet, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).

> [!IMPORTANT]
> Należy zalogować się przy użyciu `Login-AzureRmAccount` przed wykonaniem poleceń cmdlet programu Azure PowerShell.
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a>Wyświetlanie listy poleceń cmdlet usługi Azure CDN hello
Możesz wyświetlić listę wszystkich hello Azure CDN poleceń cmdlet zawierają hello `Get-Command` polecenia cmdlet.

```text
PS C:\> Get-Command -Module AzureRM.Cdn

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Cmdlet          Get-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnEndpointNameAvailability             2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Get-AzureRmCdnProfileSsoUrl                        2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnCustomDomain                         2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          New-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Publish-AzureRmCdnEndpointContent                  2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnCustomDomain                      2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnEndpoint                          2.0.0      AzureRm.Cdn
Cmdlet          Remove-AzureRmCdnProfile                           2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnEndpoint                             2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnOrigin                               2.0.0      AzureRm.Cdn
Cmdlet          Set-AzureRmCdnProfile                              2.0.0      AzureRm.Cdn
Cmdlet          Start-AzureRmCdnEndpoint                           2.0.0      AzureRm.Cdn
Cmdlet          Stop-AzureRmCdnEndpoint                            2.0.0      AzureRm.Cdn
Cmdlet          Test-AzureRmCdnCustomDomain                        2.0.0      AzureRm.Cdn
Cmdlet          Unpublish-AzureRmCdnEndpointContent                2.0.0      AzureRm.Cdn
```

## <a name="getting-help"></a>Uzyskiwanie pomocy
Pomoc można uzyskać za pomocą dowolnego z tych poleceń cmdlet, za pomocą hello `Get-Help` polecenia cmdlet.  `Get-Help`Umożliwia użycie i składni oraz opcjonalnie przedstawiono przykłady.

```text
PS C:\> Get-Help Get-AzureRmCdnProfile

NAME
    Get-AzureRmCdnProfile

SYNOPSIS
    Gets an Azure CDN profile.


SYNTAX
    Get-AzureRmCdnProfile [-ProfileName <String>] [-ResourceGroupName <String>] [-InformationAction
    <ActionPreference>] [-InformationVariable <String>] [<CommonParameters>]


DESCRIPTION
    Gets an Azure CDN profile and all related information.


RELATED LINKS

REMARKS
    toosee hello examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a>Lista istniejących profilów usługi Azure CDN
Witaj `Get-AzureRmCdnProfile` polecenie cmdlet bez parametrów pobiera wszystkich istniejących profilów CDN.

```powershell
Get-AzureRmCdnProfile
```

Te dane wyjściowe można gazociągami toocmdlets wyliczenia.

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

Można także wrócić jeden profil, określając hello profilu nazwy i grupie zasobów.

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> Jest możliwe toohave CDN wielu profili z hello takie same nazwy, pod warunkiem, znajdują się w różnych grupach zasobów.  Pominięcie hello `ResourceGroupName` parametr zwraca wszystkie profile o pasującej nazwie.
> 
> 

## <a name="listing-existing-cdn-endpoints"></a>Lista istniejących punktów końcowych usługi CDN
`Get-AzureRmCdnEndpoint`można pobrać punktu końcowego poszczególnych lub wszystkich hello punktów końcowych dla profilu.  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of hello endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of hello endpoints on all of hello profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of hello endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a>Tworzenie profilów sieci CDN i punkty końcowe
`New-AzureRmCdnProfile`i `New-AzureRmCdnEndpoint` są profile CDN toocreate używane i punktów końcowych.

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a>Sprawdzanie dostępności nazwy punktu końcowego
`Get-AzureRmCdnEndpointNameAvailability`Zwraca obiekt wskazującą, czy nazwa punktu końcowego jest dostępna.

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a>Dodawanie domeny niestandardowej
`New-AzureRmCdnCustomDomain`Dodaje domenę niestandardową nazwę tooan istniejącego punktu końcowego.

> [!IMPORTANT]
> Należy zdefiniować hello CNAME przy pomocy dostawcy usługi DNS zgodnie z opisem w [jak toomap domeny niestandardowe tooContent Delivery Network (CDN) w punkcie końcowym](cdn-map-content-to-custom-domain.md).  Można przetestować mapowania hello przed zmodyfikowaniem przy użyciu punktu końcowego `Test-AzureRmCdnCustomDomain`.
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check hello mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create hello custom domain on hello endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a>Modyfikowanie punktu końcowego
`Set-AzureRmCdnEndpoint`Modyfikuje istniejący punkt końcowy.

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a>Przeczyszczanie/wstępnie przygotowany-loading CDN zasoby
`Unpublish-AzureRmCdnEndpointContent`powoduje usunięcie buforowanych zasobów, podczas gdy `Publish-AzureRmCdnEndpointContent` wstępnie ładuje zasoby na obsługiwanych punktów końcowych.

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a>Punktów końcowych uruchamiania/zatrzymywania usługi CDN
`Start-AzureRmCdnEndpoint`i `Stop-AzureRmCdnEndpoint` można toostart używane i Zatrzymaj poszczególnych punktów końcowych lub grupy punktów końcowych.

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a>Usuwanie zasobów w sieci CDN
`Remove-AzureRmCdnProfile`i `Remove-AzureRmCdnEndpoint` mogą być używane tooremove profilów i punktów końcowych.

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a>Następne kroki
Dowiedz się, jak tooautomate Azure CDN z [.NET](cdn-app-dev-net.md) lub [Node.js](cdn-app-dev-node.md).

toolearn o funkcjach usługi CDN, zobacz [Omówienie usługi CDN](cdn-overview.md).

