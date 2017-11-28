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
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="eacee-103">Zarządzanie Azure CDN przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="eacee-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="eacee-104">PowerShell zawiera jedną z najbardziej elastycznym toomanage metody hello punktów końcowych i profile usługi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="eacee-104">PowerShell provides one of hello most flexible methods toomanage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="eacee-105">Można użyć programu PowerShell, interakcyjnego lub pisząc skrypty tooautomate zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="eacee-105">You can use PowerShell interactively or by writing scripts tooautomate management tasks.</span></span>  <span data-ttu-id="eacee-106">W tym samouczku przedstawiono kilka najbardziej typowych zadań hello można wykonać za pomocą programu PowerShell toomanage punktów końcowych i profile usługi Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="eacee-106">This tutorial demonstrates several of hello most common tasks you can accomplish with PowerShell toomanage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eacee-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="eacee-107">Prerequisites</span></span>
<span data-ttu-id="eacee-108">toouse toomanage środowiska PowerShell usługi Azure CDN profile i punkty końcowe musi mieć zainstalowany moduł Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="eacee-108">toouse PowerShell toomanage your Azure CDN profiles and endpoints, you must have hello Azure PowerShell module installed.</span></span>  <span data-ttu-id="eacee-109">toolearn jak tooinstall programu Azure PowerShell i nawiąż połączenie przy użyciu hello tooAzure `Login-AzureRmAccount` polecenia cmdlet, zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eacee-109">toolearn how tooinstall Azure PowerShell and connect tooAzure using hello `Login-AzureRmAccount` cmdlet, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eacee-110">Należy zalogować się przy użyciu `Login-AzureRmAccount` przed wykonaniem poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eacee-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-hello-azure-cdn-cmdlets"></a><span data-ttu-id="eacee-111">Wyświetlanie listy poleceń cmdlet usługi Azure CDN hello</span><span class="sxs-lookup"><span data-stu-id="eacee-111">Listing hello Azure CDN cmdlets</span></span>
<span data-ttu-id="eacee-112">Możesz wyświetlić listę wszystkich hello Azure CDN poleceń cmdlet zawierają hello `Get-Command` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eacee-112">You can list all hello Azure CDN cmdlets using hello `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="eacee-113">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="eacee-113">Getting help</span></span>
<span data-ttu-id="eacee-114">Pomoc można uzyskać za pomocą dowolnego z tych poleceń cmdlet, za pomocą hello `Get-Help` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="eacee-114">You can get help with any of these cmdlets using hello `Get-Help` cmdlet.</span></span>  <span data-ttu-id="eacee-115">`Get-Help`Umożliwia użycie i składni oraz opcjonalnie przedstawiono przykłady.</span><span class="sxs-lookup"><span data-stu-id="eacee-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="eacee-116">Lista istniejących profilów usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="eacee-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="eacee-117">Witaj `Get-AzureRmCdnProfile` polecenie cmdlet bez parametrów pobiera wszystkich istniejących profilów CDN.</span><span class="sxs-lookup"><span data-stu-id="eacee-117">hello `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="eacee-118">Te dane wyjściowe można gazociągami toocmdlets wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="eacee-118">This output can be piped toocmdlets for enumeration.</span></span>

```powershell
# Output hello name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="eacee-119">Można także wrócić jeden profil, określając hello profilu nazwy i grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="eacee-119">You can also return a single profile by specifying hello profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="eacee-120">Jest możliwe toohave CDN wielu profili z hello takie same nazwy, pod warunkiem, znajdują się w różnych grupach zasobów.</span><span class="sxs-lookup"><span data-stu-id="eacee-120">It is possible toohave multiple CDN profiles with hello same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="eacee-121">Pominięcie hello `ResourceGroupName` parametr zwraca wszystkie profile o pasującej nazwie.</span><span class="sxs-lookup"><span data-stu-id="eacee-121">Omitting hello `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="eacee-122">Lista istniejących punktów końcowych usługi CDN</span><span class="sxs-lookup"><span data-stu-id="eacee-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="eacee-123">`Get-AzureRmCdnEndpoint`można pobrać punktu końcowego poszczególnych lub wszystkich hello punktów końcowych dla profilu.</span><span class="sxs-lookup"><span data-stu-id="eacee-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all hello endpoints on a profile.</span></span>  

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

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="eacee-124">Tworzenie profilów sieci CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="eacee-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="eacee-125">`New-AzureRmCdnProfile`i `New-AzureRmCdnEndpoint` są profile CDN toocreate używane i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="eacee-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used toocreate CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="eacee-126">Sprawdzanie dostępności nazwy punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="eacee-126">Checking endpoint name availability</span></span>
<span data-ttu-id="eacee-127">`Get-AzureRmCdnEndpointNameAvailability`Zwraca obiekt wskazującą, czy nazwa punktu końcowego jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="eacee-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message toohello console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="eacee-128">Dodawanie domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="eacee-128">Adding a custom domain</span></span>
<span data-ttu-id="eacee-129">`New-AzureRmCdnCustomDomain`Dodaje domenę niestandardową nazwę tooan istniejącego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="eacee-129">`New-AzureRmCdnCustomDomain` adds a custom domain name tooan existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eacee-130">Należy zdefiniować hello CNAME przy pomocy dostawcy usługi DNS zgodnie z opisem w [jak toomap domeny niestandardowe tooContent Delivery Network (CDN) w punkcie końcowym](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="eacee-130">You must set up hello CNAME with your DNS provider as described in [How toomap Custom Domain tooContent Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="eacee-131">Można przetestować mapowania hello przed zmodyfikowaniem przy użyciu punktu końcowego `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="eacee-131">You can test hello mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
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

## <a name="modifying-an-endpoint"></a><span data-ttu-id="eacee-132">Modyfikowanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="eacee-132">Modifying an endpoint</span></span>
<span data-ttu-id="eacee-133">`Set-AzureRmCdnEndpoint`Modyfikuje istniejący punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="eacee-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save hello changed endpoint and apply hello changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="eacee-134">Przeczyszczanie/wstępnie przygotowany-loading CDN zasoby</span><span class="sxs-lookup"><span data-stu-id="eacee-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="eacee-135">`Unpublish-AzureRmCdnEndpointContent`powoduje usunięcie buforowanych zasobów, podczas gdy `Publish-AzureRmCdnEndpointContent` wstępnie ładuje zasoby na obsługiwanych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="eacee-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="eacee-136">Punktów końcowych uruchamiania/zatrzymywania usługi CDN</span><span class="sxs-lookup"><span data-stu-id="eacee-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="eacee-137">`Start-AzureRmCdnEndpoint`i `Stop-AzureRmCdnEndpoint` można toostart używane i Zatrzymaj poszczególnych punktów końcowych lub grupy punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="eacee-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used toostart and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop hello cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="eacee-138">Usuwanie zasobów w sieci CDN</span><span class="sxs-lookup"><span data-stu-id="eacee-138">Deleting CDN resources</span></span>
<span data-ttu-id="eacee-139">`Remove-AzureRmCdnProfile`i `Remove-AzureRmCdnEndpoint` mogą być używane tooremove profilów i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="eacee-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used tooremove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all hello endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="eacee-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="eacee-140">Next Steps</span></span>
<span data-ttu-id="eacee-141">Dowiedz się, jak tooautomate Azure CDN z [.NET](cdn-app-dev-net.md) lub [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="eacee-141">Learn how tooautomate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="eacee-142">toolearn o funkcjach usługi CDN, zobacz [Omówienie usługi CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eacee-142">toolearn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

