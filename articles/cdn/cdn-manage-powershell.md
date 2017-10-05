---
title: "Zarządzanie Azure CDN przy użyciu programu PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak używać poleceń cmdlet programu Azure PowerShell do zarządzania usługi Azure CDN."
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
ms.openlocfilehash: 5bd2eed7b34cafa43e8f38279890405d4ae55568
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-azure-cdn-with-powershell"></a><span data-ttu-id="47487-103">Zarządzanie Azure CDN przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="47487-103">Manage Azure CDN with PowerShell</span></span>
<span data-ttu-id="47487-104">PowerShell zawiera jedną z najbardziej elastycznym metod do zarządzania profilami usługi Azure CDN i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="47487-104">PowerShell provides one of the most flexible methods to manage your Azure CDN profiles and endpoints.</span></span>  <span data-ttu-id="47487-105">Można użyć programu PowerShell interakcyjnego lub pisanie skryptów do automatyzacji zadań zarządzania.</span><span class="sxs-lookup"><span data-stu-id="47487-105">You can use PowerShell interactively or by writing scripts to automate management tasks.</span></span>  <span data-ttu-id="47487-106">W tym samouczku przedstawiono kilka najbardziej typowych zadań, można wykonać za pomocą programu PowerShell do zarządzania profilami usługi Azure CDN i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="47487-106">This tutorial demonstrates several of the most common tasks you can accomplish with PowerShell to manage your Azure CDN profiles and endpoints.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47487-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="47487-107">Prerequisites</span></span>
<span data-ttu-id="47487-108">Zarządzanie profilami usługi Azure CDN i punktów końcowych przy użyciu programu PowerShell, musi mieć zainstalowany moduł Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47487-108">To use PowerShell to manage your Azure CDN profiles and endpoints, you must have the Azure PowerShell module installed.</span></span>  <span data-ttu-id="47487-109">Aby dowiedzieć się, jak zainstalować program Azure PowerShell i nawiązania połączenia platformy Azure przy użyciu `Login-AzureRmAccount` polecenia cmdlet, zobacz [jak instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="47487-109">To learn how to install Azure PowerShell and connect to Azure using the `Login-AzureRmAccount` cmdlet, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47487-110">Należy zalogować się przy użyciu `Login-AzureRmAccount` przed wykonaniem poleceń cmdlet programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47487-110">You must log in with `Login-AzureRmAccount` before you can execute Azure PowerShell cmdlets.</span></span>
> 
> 

## <a name="listing-the-azure-cdn-cmdlets"></a><span data-ttu-id="47487-111">Wyświetlanie listy poleceń cmdlet usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="47487-111">Listing the Azure CDN cmdlets</span></span>
<span data-ttu-id="47487-112">Możesz wyświetlić listę wszystkich poleceń cmdlet usługi Azure CDN przy użyciu `Get-Command` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="47487-112">You can list all the Azure CDN cmdlets using the `Get-Command` cmdlet.</span></span>

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

## <a name="getting-help"></a><span data-ttu-id="47487-113">Uzyskiwanie pomocy</span><span class="sxs-lookup"><span data-stu-id="47487-113">Getting help</span></span>
<span data-ttu-id="47487-114">Pomoc można uzyskać za pomocą dowolnego z tych poleceń cmdlet, za pomocą `Get-Help` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="47487-114">You can get help with any of these cmdlets using the `Get-Help` cmdlet.</span></span>  <span data-ttu-id="47487-115">`Get-Help`Umożliwia użycie i składni oraz opcjonalnie przedstawiono przykłady.</span><span class="sxs-lookup"><span data-stu-id="47487-115">`Get-Help` provides usage and syntax, and optionally shows examples.</span></span>

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
    To see the examples, type: "get-help Get-AzureRmCdnProfile -examples".
    For more information, type: "get-help Get-AzureRmCdnProfile -detailed".
    For technical information, type: "get-help Get-AzureRmCdnProfile -full".

```

## <a name="listing-existing-azure-cdn-profiles"></a><span data-ttu-id="47487-116">Lista istniejących profilów usługi Azure CDN</span><span class="sxs-lookup"><span data-stu-id="47487-116">Listing existing Azure CDN profiles</span></span>
<span data-ttu-id="47487-117">`Get-AzureRmCdnProfile` Polecenie cmdlet bez parametrów pobiera wszystkich istniejących profilów CDN.</span><span class="sxs-lookup"><span data-stu-id="47487-117">The `Get-AzureRmCdnProfile` cmdlet without any parameters retrieves all your existing CDN profiles.</span></span>

```powershell
Get-AzureRmCdnProfile
```

<span data-ttu-id="47487-118">Te dane wyjściowe mogą być przetwarzane potokowo do polecenia cmdlet dla wyliczenia.</span><span class="sxs-lookup"><span data-stu-id="47487-118">This output can be piped to cmdlets for enumeration.</span></span>

```powershell
# Output the name of all profiles on this subscription.
Get-AzureRmCdnProfile | ForEach-Object { Write-Host $_.Name }

# Return only **Azure CDN from Verizon** profiles.
Get-AzureRmCdnProfile | Where-Object { $_.Sku.Name -eq "StandardVerizon" }
```

<span data-ttu-id="47487-119">Można także wrócić jeden profil, określając nazwę i zasobów grupy profilów.</span><span class="sxs-lookup"><span data-stu-id="47487-119">You can also return a single profile by specifying the profile name and resource group.</span></span>

```powershell
Get-AzureRmCdnProfile -ProfileName CdnDemo -ResourceGroupName CdnDemoRG
```

> [!TIP]
> <span data-ttu-id="47487-120">Użytkownik może mieć wiele profilów CDN o takiej samej nazwie, tak długo, jak znajdują się w różnych grupach zasobów.</span><span class="sxs-lookup"><span data-stu-id="47487-120">It is possible to have multiple CDN profiles with the same name, so long as they are in different resource groups.</span></span>  <span data-ttu-id="47487-121">Pominięcie `ResourceGroupName` parametr zwraca wszystkie profile o pasującej nazwie.</span><span class="sxs-lookup"><span data-stu-id="47487-121">Omitting the `ResourceGroupName` parameter returns all profiles with a matching name.</span></span>
> 
> 

## <a name="listing-existing-cdn-endpoints"></a><span data-ttu-id="47487-122">Lista istniejących punktów końcowych usługi CDN</span><span class="sxs-lookup"><span data-stu-id="47487-122">Listing existing CDN endpoints</span></span>
<span data-ttu-id="47487-123">`Get-AzureRmCdnEndpoint`można pobrać punktu końcowego poszczególnych lub wszystkich punktów końcowych dla profilu.</span><span class="sxs-lookup"><span data-stu-id="47487-123">`Get-AzureRmCdnEndpoint` can retrieve an individual endpoint or all the endpoints on a profile.</span></span>  

```powershell
# Get a single endpoint.
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Get all of the endpoints on a given profile. 
Get-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG

# Return all of the endpoints on all of the profiles.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint

# Return all of the endpoints in this subscription that are currently running.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Where-Object { $_.ResourceState -eq "Running" }
```

## <a name="creating-cdn-profiles-and-endpoints"></a><span data-ttu-id="47487-124">Tworzenie profilów sieci CDN i punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="47487-124">Creating CDN profiles and endpoints</span></span>
<span data-ttu-id="47487-125">`New-AzureRmCdnProfile`i `New-AzureRmCdnEndpoint` są używane do tworzenia profilów sieci CDN i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="47487-125">`New-AzureRmCdnProfile` and `New-AzureRmCdnEndpoint` are used to create CDN profiles and endpoints.</span></span>

```powershell
# Create a new profile
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US"

# Create a new endpoint
New-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Location "Central US" -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

# Create a new profile and endpoint (same as above) in one line
New-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -Sku StandardAkamai -Location "Central US" | New-AzureRmCdnEndpoint -EndpointName cdnposhdoc -OriginName "Contoso" -OriginHostName "www.contoso.com"

```

## <a name="checking-endpoint-name-availability"></a><span data-ttu-id="47487-126">Sprawdzanie dostępności nazwy punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="47487-126">Checking endpoint name availability</span></span>
<span data-ttu-id="47487-127">`Get-AzureRmCdnEndpointNameAvailability`Zwraca obiekt wskazującą, czy nazwa punktu końcowego jest dostępna.</span><span class="sxs-lookup"><span data-stu-id="47487-127">`Get-AzureRmCdnEndpointNameAvailability` returns an object indicating if an endpoint name is available.</span></span>

```powershell
# Retrieve availability
$availability = Get-AzureRmCdnEndpointNameAvailability -EndpointName "cdnposhdoc"

# If available, write a message to the console.
If($availability.NameAvailable) { Write-Host "Yes, that endpoint name is available." }
Else { Write-Host "No, that endpoint name is not available." }
```

## <a name="adding-a-custom-domain"></a><span data-ttu-id="47487-128">Dodawanie domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="47487-128">Adding a custom domain</span></span>
<span data-ttu-id="47487-129">`New-AzureRmCdnCustomDomain`dodaje niestandardową nazwę domeny do istniejącego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="47487-129">`New-AzureRmCdnCustomDomain` adds a custom domain name to an existing endpoint.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="47487-130">Należy zdefiniować CNAME przy pomocy dostawcy usługi DNS zgodnie z opisem w [jak zamapować niestandardową domenę na punkt końcowy sieci dostarczania zawartości (CDN)](cdn-map-content-to-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="47487-130">You must set up the CNAME with your DNS provider as described in [How to map Custom Domain to Content Delivery Network (CDN) endpoint](cdn-map-content-to-custom-domain.md).</span></span>  <span data-ttu-id="47487-131">Można przetestować mapowania przed zmodyfikowaniem przy użyciu punktu końcowego `Test-AzureRmCdnCustomDomain`.</span><span class="sxs-lookup"><span data-stu-id="47487-131">You can test the mapping before modifying your endpoint using `Test-AzureRmCdnCustomDomain`.</span></span>
> 
> 

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Check the mapping
$result = Test-AzureRmCdnCustomDomain -CdnEndpoint $endpoint -CustomDomainHostName "cdn.contoso.com"

# Create the custom domain on the endpoint
If($result.CustomDomainValidated){ New-AzureRmCdnCustomDomain -CustomDomainName Contoso -HostName "cdn.contoso.com" -CdnEndpoint $endpoint }
```

## <a name="modifying-an-endpoint"></a><span data-ttu-id="47487-132">Modyfikowanie punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="47487-132">Modifying an endpoint</span></span>
<span data-ttu-id="47487-133">`Set-AzureRmCdnEndpoint`Modyfikuje istniejący punkt końcowy.</span><span class="sxs-lookup"><span data-stu-id="47487-133">`Set-AzureRmCdnEndpoint` modifies an existing endpoint.</span></span>

```powershell
# Get an existing endpoint
$endpoint = Get-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Set up content compression
$endpoint.IsCompressionEnabled = $true
$endpoint.ContentTypesToCompress = "text/javascript","text/css","application/json"

# Save the changed endpoint and apply the changes
Set-AzureRmCdnEndpoint -CdnEndpoint $endpoint
```

## <a name="purgingpre-loading-cdn-assets"></a><span data-ttu-id="47487-134">Przeczyszczanie/wstępnie przygotowany-loading CDN zasoby</span><span class="sxs-lookup"><span data-stu-id="47487-134">Purging/Pre-loading CDN assets</span></span>
<span data-ttu-id="47487-135">`Unpublish-AzureRmCdnEndpointContent`powoduje usunięcie buforowanych zasobów, podczas gdy `Publish-AzureRmCdnEndpointContent` wstępnie ładuje zasoby na obsługiwanych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="47487-135">`Unpublish-AzureRmCdnEndpointContent` purges cached assets, while `Publish-AzureRmCdnEndpointContent` pre-loads assets on supported endpoints.</span></span>

```powershell
# Purge some assets.
Unpublish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -PurgeContent "/images/kitten.png","/video/rickroll.mp4"

# Pre-load some assets.
Publish-AzureRmCdnEndpointContent -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo -LoadContent "/images/kitten.png","/video/rickroll.mp4"

# Purge everything in /images/ on all endpoints.
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Unpublish-AzureRmCdnEndpointContent -PurgeContent "/images/*"
```

## <a name="startingstopping-cdn-endpoints"></a><span data-ttu-id="47487-136">Punktów końcowych uruchamiania/zatrzymywania usługi CDN</span><span class="sxs-lookup"><span data-stu-id="47487-136">Starting/Stopping CDN endpoints</span></span>
<span data-ttu-id="47487-137">`Start-AzureRmCdnEndpoint`i `Stop-AzureRmCdnEndpoint` może służyć do uruchamiania i zatrzymywania poszczególnych punktów końcowych lub grupy punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="47487-137">`Start-AzureRmCdnEndpoint` and `Stop-AzureRmCdnEndpoint` can be used to start and stop individual endpoints or groups of endpoints.</span></span>

```powershell
# Stop the cdndocdemo endpoint
Stop-AzureRmCdnEndpoint -ProfileName CdnDemo -ResourceGroupName CdnDemoRG -EndpointName cdndocdemo

# Stop all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Stop-AzureRmCdnEndpoint

# Start all endpoints
Get-AzureRmCdnProfile | Get-AzureRmCdnEndpoint | Start-AzureRmCdnEndpoint
```

## <a name="deleting-cdn-resources"></a><span data-ttu-id="47487-138">Usuwanie zasobów w sieci CDN</span><span class="sxs-lookup"><span data-stu-id="47487-138">Deleting CDN resources</span></span>
<span data-ttu-id="47487-139">`Remove-AzureRmCdnProfile`i `Remove-AzureRmCdnEndpoint` może służyć do usunięcia profilów i punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="47487-139">`Remove-AzureRmCdnProfile` and `Remove-AzureRmCdnEndpoint` can be used to remove profiles and endpoints.</span></span>

```powershell
# Remove a single endpoint
Remove-AzureRmCdnEndpoint -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG -EndpointName cdnposhdoc

# Remove all the endpoints on a profile and skip confirmation (-Force)
Get-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG | Get-AzureRmCdnEndpoint | Remove-AzureRmCdnEndpoint -Force

# Remove a single profile
Remove-AzureRmCdnProfile -ProfileName CdnPoshDemo -ResourceGroupName CdnDemoRG
```

## <a name="next-steps"></a><span data-ttu-id="47487-140">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="47487-140">Next Steps</span></span>
<span data-ttu-id="47487-141">Dowiedz się, jak zautomatyzować usługę Azure CDN przy użyciu platformy [.NET](cdn-app-dev-net.md) lub [Node.js](cdn-app-dev-node.md).</span><span class="sxs-lookup"><span data-stu-id="47487-141">Learn how to automate Azure CDN with [.NET](cdn-app-dev-net.md) or [Node.js](cdn-app-dev-node.md).</span></span>

<span data-ttu-id="47487-142">Aby dowiedzieć się więcej o funkcjach usługi CDN, zobacz [Omówienie usługi CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="47487-142">To learn about CDN features, see [CDN Overview](cdn-overview.md).</span></span>

