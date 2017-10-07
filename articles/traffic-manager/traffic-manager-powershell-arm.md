---
title: "aaaUsing toomanage programu PowerShell Menedżera ruchu na platformie Azure | Dokumentacja firmy Microsoft"
description: "Przy użyciu programu PowerShell dla Menedżera ruchu z usługi Azure Resource Manager"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a><span data-ttu-id="d706d-103">Przy użyciu programu PowerShell toomanage Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-103">Using PowerShell toomanage Traffic Manager</span></span>

<span data-ttu-id="d706d-104">Usługa Azure Resource Manager to hello preferowane interfejs dla usług Azure.</span><span class="sxs-lookup"><span data-stu-id="d706d-104">Azure Resource Manager is hello preferred management interface for services in Azure.</span></span> <span data-ttu-id="d706d-105">Azure profilów usługi Traffic Manager mogą być zarządzane przy użyciu usługi Azure Resource Manager na podstawie interfejsów API i narzędzia.</span><span class="sxs-lookup"><span data-stu-id="d706d-105">Azure Traffic Manager profiles can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="resource-model"></a><span data-ttu-id="d706d-106">Model zasobów</span><span class="sxs-lookup"><span data-stu-id="d706d-106">Resource model</span></span>

<span data-ttu-id="d706d-107">Menedżer ruchu Azure jest konfigurowane przy użyciu kolekcję ustawień o nazwie profilu usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d706d-107">Azure Traffic Manager is configured using a collection of settings called a Traffic Manager profile.</span></span> <span data-ttu-id="d706d-108">Ten profil zawiera ustawienia DNS, ustawienia kierowania ruchu, ustawienia monitorowania punktu końcowego, a jest kierowany listę ruch toowhich punktów końcowych usługi.</span><span class="sxs-lookup"><span data-stu-id="d706d-108">This profile contains DNS settings, traffic routing settings, endpoint monitoring settings, and a list of service endpoints toowhich traffic is routed.</span></span>

<span data-ttu-id="d706d-109">Każdy profil Menedżera ruchu jest reprezentowana przez zasób typu "TrafficManagerProfiles".</span><span class="sxs-lookup"><span data-stu-id="d706d-109">Each Traffic Manager profile is represented by a resource of type 'TrafficManagerProfiles'.</span></span> <span data-ttu-id="d706d-110">Na powitania poziom interfejsu API REST hello identyfikatora URI dla każdego profilu jest następujący:</span><span class="sxs-lookup"><span data-stu-id="d706d-110">At hello REST API level, hello URI for each profile is as follows:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a><span data-ttu-id="d706d-111">Konfigurowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d706d-111">Setting up Azure PowerShell</span></span>

<span data-ttu-id="d706d-112">Poniższe instrukcje korzystają z programu Microsoft Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d706d-112">These instructions use Microsoft Azure PowerShell.</span></span> <span data-ttu-id="d706d-113">Witaj artykule wyjaśniono, jak tooinstall i konfigurowanie programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d706d-113">hello following article explains how tooinstall and configure Azure PowerShell.</span></span>

* [<span data-ttu-id="d706d-114">Jak tooinstall i konfigurowanie programu Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d706d-114">How tooinstall and configure Azure PowerShell</span></span>](/powershell/azure/overview)

<span data-ttu-id="d706d-115">Hello przykłady w tym artykule założono, że masz istniejącą grupę zasobów.</span><span class="sxs-lookup"><span data-stu-id="d706d-115">hello examples in this article assume that you have an existing resource group.</span></span> <span data-ttu-id="d706d-116">Można utworzyć grupy zasobów przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="d706d-116">You can create a resource group using hello following command:</span></span>

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> <span data-ttu-id="d706d-117">Usługa Azure Resource Manager wymaga, aby wszystkie grupy zasobów miały miejsce.</span><span class="sxs-lookup"><span data-stu-id="d706d-117">Azure Resource Manager requires that all resource groups have a location.</span></span> <span data-ttu-id="d706d-118">Ta lokalizacja jest używana jako domyślna hello zasoby utworzone w tej grupie zasobów.</span><span class="sxs-lookup"><span data-stu-id="d706d-118">This location is used as hello default for resources created in that resource group.</span></span> <span data-ttu-id="d706d-119">Jednak ponieważ zasoby profilu Menedżera ruchu są globalne, a nie regionalne, hello wybór lokalizacji grupy zasobów nie ma wpływu na usługi Azure Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d706d-119">However, since Traffic Manager profile resources are global, not regional, hello choice of resource group location has no impact on Azure Traffic Manager.</span></span>

## <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="d706d-120">Tworzenie profilu Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-120">Create a Traffic Manager Profile</span></span>

<span data-ttu-id="d706d-121">toocreate profilu usługi Traffic Manager, użyj hello `New-AzureRmTrafficManagerProfile` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d706d-121">toocreate a Traffic Manager profile, use hello `New-AzureRmTrafficManagerProfile` cmdlet:</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

<span data-ttu-id="d706d-122">Witaj w poniższej tabeli opisano parametry hello:</span><span class="sxs-lookup"><span data-stu-id="d706d-122">hello following table describes hello parameters:</span></span>

| <span data-ttu-id="d706d-123">Parametr</span><span class="sxs-lookup"><span data-stu-id="d706d-123">Parameter</span></span> | <span data-ttu-id="d706d-124">Opis</span><span class="sxs-lookup"><span data-stu-id="d706d-124">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d706d-125">Nazwa</span><span class="sxs-lookup"><span data-stu-id="d706d-125">Name</span></span> |<span data-ttu-id="d706d-126">Nazwa zasobu Hello hello zasobów profilu Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="d706d-126">hello resource name for hello Traffic Manager profile resource.</span></span> <span data-ttu-id="d706d-127">Profile w hello sama grupa zasobów muszą mieć unikatowe nazwy.</span><span class="sxs-lookup"><span data-stu-id="d706d-127">Profiles in hello same resource group must have unique names.</span></span> <span data-ttu-id="d706d-128">Ta nazwa jest oddzielony od hello DNS nazwę używaną dla zapytań DNS.</span><span class="sxs-lookup"><span data-stu-id="d706d-128">This name is separate from hello DNS name used for DNS queries.</span></span> |
| <span data-ttu-id="d706d-129">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="d706d-129">ResourceGroupName</span></span> |<span data-ttu-id="d706d-130">Nazwa Hello hello zasobu zawierającego hello profilu zasób grupy.</span><span class="sxs-lookup"><span data-stu-id="d706d-130">hello name of hello resource group containing hello profile resource.</span></span> |
| <span data-ttu-id="d706d-131">TrafficRoutingMethod</span><span class="sxs-lookup"><span data-stu-id="d706d-131">TrafficRoutingMethod</span></span> |<span data-ttu-id="d706d-132">Określa hello routingu ruchu metodę toodetermine który punkt końcowy jest zwracany w odpowiedzi do zapytania DNS.</span><span class="sxs-lookup"><span data-stu-id="d706d-132">Specifies hello traffic-routing method used toodetermine which endpoint is returned in response a DNS query.</span></span> <span data-ttu-id="d706d-133">Możliwe wartości to "Performance", 'Ważone' lub 'Priority'.</span><span class="sxs-lookup"><span data-stu-id="d706d-133">Possible values are 'Performance', 'Weighted' or 'Priority'.</span></span> |
| <span data-ttu-id="d706d-134">RelativeDnsName</span><span class="sxs-lookup"><span data-stu-id="d706d-134">RelativeDnsName</span></span> |<span data-ttu-id="d706d-135">Określa hello hostname część nazwy DNS hello udostępniane przez ten profil Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="d706d-135">Specifies hello hostname portion of hello DNS name provided by this Traffic Manager profile.</span></span> <span data-ttu-id="d706d-136">Ta wartość jest połączona z nazwą domeny DNS hello używane przez usługi Azure Traffic Manager tooform hello pełni kwalifikowaną nazwę domeny (FQDN) hello profilu.</span><span class="sxs-lookup"><span data-stu-id="d706d-136">This value is combined with hello DNS domain name used by Azure Traffic Manager tooform hello fully qualified domain name (FQDN) of hello profile.</span></span> <span data-ttu-id="d706d-137">Na przykład ustawienie wartości hello "contoso" staje się "contoso.trafficmanager.net."</span><span class="sxs-lookup"><span data-stu-id="d706d-137">For example, setting hello value of 'contoso' becomes 'contoso.trafficmanager.net.'</span></span> |
| <span data-ttu-id="d706d-138">CZAS WYGAŚNIĘCIA</span><span class="sxs-lookup"><span data-stu-id="d706d-138">TTL</span></span> |<span data-ttu-id="d706d-139">Witaj DNS Time-to-Live (TTL) określa w sekundach.</span><span class="sxs-lookup"><span data-stu-id="d706d-139">Specifies hello DNS Time-to-Live (TTL), in seconds.</span></span> <span data-ttu-id="d706d-140">Ten czas wygaśnięcia informuje rozpoznawania nazw DNS lokalne powitania i klientów DNS, jak długo toocache odpowiedzi DNS dla tego profilu usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d706d-140">This TTL informs hello Local DNS resolvers and DNS clients how long toocache DNS responses for this Traffic Manager profile.</span></span> |
| <span data-ttu-id="d706d-141">MonitorProtocol</span><span class="sxs-lookup"><span data-stu-id="d706d-141">MonitorProtocol</span></span> |<span data-ttu-id="d706d-142">Określa hello protokołu toouse toomonitor punktu końcowego kondycji.</span><span class="sxs-lookup"><span data-stu-id="d706d-142">Specifies hello protocol toouse toomonitor endpoint health.</span></span> <span data-ttu-id="d706d-143">Możliwe wartości to "HTTP" i "HTTPS".</span><span class="sxs-lookup"><span data-stu-id="d706d-143">Possible values are 'HTTP' and 'HTTPS'.</span></span> |
| <span data-ttu-id="d706d-144">MonitorPort</span><span class="sxs-lookup"><span data-stu-id="d706d-144">MonitorPort</span></span> |<span data-ttu-id="d706d-145">Określa, że hello TCP port używany toomonitor kondycji punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d706d-145">Specifies hello TCP port used toomonitor endpoint health.</span></span> |
| <span data-ttu-id="d706d-146">MonitorPath</span><span class="sxs-lookup"><span data-stu-id="d706d-146">MonitorPath</span></span> |<span data-ttu-id="d706d-147">Określa, że nazwa domeny hello ścieżki względnej toohello punktu końcowego używane tooprobe kondycji punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d706d-147">Specifies hello path relative toohello endpoint domain name used tooprobe for endpoint health.</span></span> |

<span data-ttu-id="d706d-148">polecenia cmdlet Hello tworzy profil Menedżera ruchu na platformie Azure i zwraca odpowiednie tooPowerShell obiektu profilu.</span><span class="sxs-lookup"><span data-stu-id="d706d-148">hello cmdlet creates a Traffic Manager profile in Azure and returns a corresponding profile object tooPowerShell.</span></span> <span data-ttu-id="d706d-149">W tym momencie hello profil zastępczy nie zawiera żadnych punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="d706d-149">At this point, hello profile does not contain any endpoints.</span></span> <span data-ttu-id="d706d-150">Aby uzyskać więcej informacji na temat dodawania profilu usługi Traffic Manager tooa punktów końcowych, zobacz [Dodawanie punktów końcowych usługi Traffic Manager](#adding-traffic-manager-endpoints).</span><span class="sxs-lookup"><span data-stu-id="d706d-150">For more information about adding endpoints tooa Traffic Manager profile, see [Adding Traffic Manager Endpoints](#adding-traffic-manager-endpoints).</span></span>

## <a name="get-a-traffic-manager-profile"></a><span data-ttu-id="d706d-151">Pobierz profil Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-151">Get a Traffic Manager Profile</span></span>

<span data-ttu-id="d706d-152">tooretrieve istniejącego obiektu profilu usługi Traffic Manager, użyj hello `Get-AzureRmTrafficManagerProfle` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d706d-152">tooretrieve an existing Traffic Manager profile object, use hello `Get-AzureRmTrafficManagerProfle` cmdlet:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="d706d-153">To polecenie cmdlet zwraca obiekt profilu Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="d706d-153">This cmdlet returns a Traffic Manager profile object.</span></span>

## <a name="update-a-traffic-manager-profile"></a><span data-ttu-id="d706d-154">Zaktualizuj profil Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-154">Update a Traffic Manager Profile</span></span>

<span data-ttu-id="d706d-155">Modyfikowanie profilów usługi Traffic Manager następujący proces krok 3:</span><span class="sxs-lookup"><span data-stu-id="d706d-155">Modifying Traffic Manager profiles follows a 3-step process:</span></span>

1. <span data-ttu-id="d706d-156">Przy użyciu profilu hello pobrać `Get-AzureRmTrafficManagerProfile` lub Użyj profilu hello zwrócony przez `New-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="d706d-156">Retrieve hello profile using `Get-AzureRmTrafficManagerProfile` or use hello profile returned by `New-AzureRmTrafficManagerProfile`.</span></span>
2. <span data-ttu-id="d706d-157">Modyfikowanie hello profilu.</span><span class="sxs-lookup"><span data-stu-id="d706d-157">Modify hello profile.</span></span> <span data-ttu-id="d706d-158">Można dodać i usunąć punkty końcowe lub zmień parametry punktu końcowego lub profil.</span><span class="sxs-lookup"><span data-stu-id="d706d-158">You can add and remove endpoints or change endpoint or profile parameters.</span></span> <span data-ttu-id="d706d-159">Te zmiany są operacji w trybie offline.</span><span class="sxs-lookup"><span data-stu-id="d706d-159">These changes are off-line operations.</span></span> <span data-ttu-id="d706d-160">Zmieniasz hello lokalnego obiektu w pamięci, która reprezentuje hello profilu.</span><span class="sxs-lookup"><span data-stu-id="d706d-160">You are only changing hello local object in memory that represents hello profile.</span></span>
3. <span data-ttu-id="d706d-161">Zatwierdź zmiany przy użyciu hello `Set-AzureRmTrafficManagerProfile` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d706d-161">Commit your changes using hello `Set-AzureRmTrafficManagerProfile` cmdlet.</span></span>

<span data-ttu-id="d706d-162">Wszystkie właściwości profilu można zmienić z wyjątkiem RelativeDnsName hello profilu.</span><span class="sxs-lookup"><span data-stu-id="d706d-162">All profile properties can be changed except hello profile's RelativeDnsName.</span></span> <span data-ttu-id="d706d-163">toochange hello RelativeDnsName, należy usunąć profil i nowy profil z nową nazwą.</span><span class="sxs-lookup"><span data-stu-id="d706d-163">toochange hello RelativeDnsName, you must delete profile and a new profile with a new name.</span></span>

<span data-ttu-id="d706d-164">Witaj poniższy przykład pokazuje, jak toochange hello TTL profilu:</span><span class="sxs-lookup"><span data-stu-id="d706d-164">hello following example demonstrates how toochange hello profile's TTL:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="d706d-165">Istnieją trzy typy punktów końcowych usługi Traffic Manager:</span><span class="sxs-lookup"><span data-stu-id="d706d-165">There are three types of Traffic Manager endpoints:</span></span>

1. <span data-ttu-id="d706d-166">**Punkty końcowe systemu Azure** są usługi hostowanej na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="d706d-166">**Azure endpoints** are services hosted in Azure</span></span>
2. <span data-ttu-id="d706d-167">**Zewnętrzne punkty końcowe** usług hostowanych poza platformą Azure</span><span class="sxs-lookup"><span data-stu-id="d706d-167">**External endpoints** are services hosted outside of Azure</span></span>
3. <span data-ttu-id="d706d-168">**Zagnieżdżone punkty końcowe** są używane tooconstruct zagnieżdżone hierarchie profilów usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d706d-168">**Nested endpoints** are used tooconstruct nested hierarchies of Traffic Manager profiles.</span></span> <span data-ttu-id="d706d-169">Punkty końcowe zagnieżdżonych Włącz zaawansowane konfiguracje routingu ruchu w kontekście aplikacji złożonych.</span><span class="sxs-lookup"><span data-stu-id="d706d-169">Nested endpoints enable advanced traffic-routing configurations for complex applications.</span></span>

<span data-ttu-id="d706d-170">We wszystkich przypadkach trzy punkty końcowe mogą być dodawane na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="d706d-170">In all three cases, endpoints can be added in two ways:</span></span>

1. <span data-ttu-id="d706d-171">Przy użyciu kroku 3 procedury opisane wcześniej.</span><span class="sxs-lookup"><span data-stu-id="d706d-171">Using a 3-step process described previously.</span></span> <span data-ttu-id="d706d-172">Hello zaletą tej metody jest, że wiele zmian punktu końcowego można podjąć w pojedynczej aktualizacji.</span><span class="sxs-lookup"><span data-stu-id="d706d-172">hello advantage of this method is that several endpoint changes can be made in a single update.</span></span>
2. <span data-ttu-id="d706d-173">Za pomocą polecenia cmdlet New-AzureRmTrafficManagerEndpoint hello.</span><span class="sxs-lookup"><span data-stu-id="d706d-173">Using hello New-AzureRmTrafficManagerEndpoint cmdlet.</span></span> <span data-ttu-id="d706d-174">To polecenie cmdlet dodaje istniejący profil usługi Traffic Manager punktu końcowego tooan w ramach jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="d706d-174">This cmdlet adds an endpoint tooan existing Traffic Manager profile in a single operation.</span></span>

## <a name="adding-azure-endpoints"></a><span data-ttu-id="d706d-175">Dodawanie punkty końcowe systemu Azure</span><span class="sxs-lookup"><span data-stu-id="d706d-175">Adding Azure Endpoints</span></span>

<span data-ttu-id="d706d-176">Punkty końcowe systemu Azure odwoływać się do usług hostowanych na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="d706d-176">Azure endpoints reference services hosted in Azure.</span></span> <span data-ttu-id="d706d-177">Obsługiwane są dwa typy punkty końcowe systemu Azure:</span><span class="sxs-lookup"><span data-stu-id="d706d-177">Two types of Azure endpoints are supported:</span></span>

1. <span data-ttu-id="d706d-178">Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="d706d-178">Azure Web Apps</span></span>
2. <span data-ttu-id="d706d-179">Azure zasoby publicznego adresu IP (które może być dołączone tooa modułu równoważenia obciążenia lub maszyny wirtualnej karty Sieciowej).</span><span class="sxs-lookup"><span data-stu-id="d706d-179">Azure PublicIpAddress resources (which can be attached tooa load-balancer or a virtual machine NIC).</span></span> <span data-ttu-id="d706d-180">Witaj publicznego adresu IP musi mieć nazwę DNS przypisane toobe używane w usłudze Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d706d-180">hello PublicIpAddress must have a DNS name assigned toobe used in Traffic Manager.</span></span>

<span data-ttu-id="d706d-181">W każdym przypadku:</span><span class="sxs-lookup"><span data-stu-id="d706d-181">In each case:</span></span>

* <span data-ttu-id="d706d-182">Usługa Hello jest określona za pomocą parametru "element targetResourceId" hello `Add-AzureRmTrafficManagerEndpointConfig` lub `New-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="d706d-182">hello service is specified using hello 'targetResourceId' parameter of `Add-AzureRmTrafficManagerEndpointConfig` or `New-AzureRmTrafficManagerEndpoint`.</span></span>
* <span data-ttu-id="d706d-183">Witaj "Target" i "EndpointLocation" są implikowana przez element TargetResourceId hello.</span><span class="sxs-lookup"><span data-stu-id="d706d-183">hello 'Target' and 'EndpointLocation' are implied by hello TargetResourceId.</span></span>
* <span data-ttu-id="d706d-184">Określenie hello "Waga" jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="d706d-184">Specifying hello 'Weight' is optional.</span></span> <span data-ttu-id="d706d-185">Wagi są używane tylko w przypadku profilu hello skonfigurowanego toouse metody routingu ruchu "Ważone" hello.</span><span class="sxs-lookup"><span data-stu-id="d706d-185">Weights are only used if hello profile is configured toouse hello 'Weighted' traffic-routing method.</span></span> <span data-ttu-id="d706d-186">W przeciwnym razie są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="d706d-186">Otherwise, they are ignored.</span></span> <span data-ttu-id="d706d-187">Jeśli jest określony, wartość hello musi być liczbą z zakresu od 1 do 1000.</span><span class="sxs-lookup"><span data-stu-id="d706d-187">If specified, hello value must be a number between 1 and 1000.</span></span> <span data-ttu-id="d706d-188">Witaj, wartością domyślną jest "1".</span><span class="sxs-lookup"><span data-stu-id="d706d-188">hello default value is '1'.</span></span>
* <span data-ttu-id="d706d-189">Określanie hello 'Priority' jest opcjonalna.</span><span class="sxs-lookup"><span data-stu-id="d706d-189">Specifying hello 'Priority' is optional.</span></span> <span data-ttu-id="d706d-190">Priorytety są używane, jeśli profil hello jest skonfigurowany toouse hello 'Priority' metody routingu ruchu.</span><span class="sxs-lookup"><span data-stu-id="d706d-190">Priorities are only used if hello profile is configured toouse hello 'Priority' traffic-routing method.</span></span> <span data-ttu-id="d706d-191">W przeciwnym razie są ignorowane.</span><span class="sxs-lookup"><span data-stu-id="d706d-191">Otherwise, they are ignored.</span></span> <span data-ttu-id="d706d-192">Prawidłowe wartości to od 1 too1000 o niższych wartościach, wskazując wyższy priorytet.</span><span class="sxs-lookup"><span data-stu-id="d706d-192">Valid values are from 1 too1000 with lower values indicating a higher priority.</span></span> <span data-ttu-id="d706d-193">Jeśli określone dla punktów końcowych, musi być określona dla wszystkich punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="d706d-193">If specified for one endpoint, they must be specified for all endpoints.</span></span> <span data-ttu-id="d706d-194">Pominięcie wartości domyślne, zaczynając od "1" są stosowane w kolejności hello wymieniony hello punktów końcowych.</span><span class="sxs-lookup"><span data-stu-id="d706d-194">If omitted, default values starting from '1' are applied in hello order that hello endpoints are listed.</span></span>

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a><span data-ttu-id="d706d-195">Przykład 1: Dodawanie punktów końcowych aplikacji sieci Web przy użyciu`Add-AzureRmTrafficManagerEndpointConfig`</span><span class="sxs-lookup"><span data-stu-id="d706d-195">Example 1: Adding Web App endpoints using `Add-AzureRmTrafficManagerEndpointConfig`</span></span>

<span data-ttu-id="d706d-196">W tym przykładzie, możemy utworzyć profil Menedżera ruchu i dodaj dwa punkty końcowe aplikacji sieci Web, przy użyciu hello `Add-AzureRmTrafficManagerEndpointConfig` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d706d-196">In this example, we create a Traffic Manager profile and add two Web App endpoints using hello `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="d706d-197">Przykład 2: Dodawanie punktu końcowego publicznego adresu IP za pomocą`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="d706d-197">Example 2: Adding a publicIpAddress endpoint using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="d706d-198">W tym przykładzie zasób publiczny adres IP jest dodany toohello profilu usługi Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="d706d-198">In this example, a public IP address resource is added toohello Traffic Manager profile.</span></span> <span data-ttu-id="d706d-199">Hello publiczny adres IP musi mieć nazwę DNS skonfigurowane i może być powiązany albo toohello karty Sieciowej maszyny Wirtualnej lub tooa usługi równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="d706d-199">hello public IP address must have a DNS name configured, and can be bound either toohello NIC of a VM or tooa load balancer.</span></span>

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a><span data-ttu-id="d706d-200">Dodawanie zewnętrzne punkty końcowe</span><span class="sxs-lookup"><span data-stu-id="d706d-200">Adding External Endpoints</span></span>

<span data-ttu-id="d706d-201">Traffic Manager używa zewnętrzne punkty końcowe toodirect ruchu tooservices hostowanej poza platformą Azure.</span><span class="sxs-lookup"><span data-stu-id="d706d-201">Traffic Manager uses external endpoints toodirect traffic tooservices hosted outside of Azure.</span></span> <span data-ttu-id="d706d-202">Zgodnie z punkty końcowe systemu Azure, zewnętrzne punkty końcowe można dodać albo przy użyciu `Add-AzureRmTrafficManagerEndpointConfig` następuje `Set-AzureRmTrafficManagerProfile`, lub `New-AzureRMTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="d706d-202">As with Azure endpoints, external endpoints can be added either using `Add-AzureRmTrafficManagerEndpointConfig` followed by `Set-AzureRmTrafficManagerProfile`, or `New-AzureRMTrafficManagerEndpoint`.</span></span>

<span data-ttu-id="d706d-203">Podczas określania zewnętrzne punkty końcowe:</span><span class="sxs-lookup"><span data-stu-id="d706d-203">When specifying external endpoints:</span></span>

* <span data-ttu-id="d706d-204">należy podać nazwę domeny punktu końcowego Hello za pomocą parametru 'Target' hello</span><span class="sxs-lookup"><span data-stu-id="d706d-204">hello endpoint domain name must be specified using hello 'Target' parameter</span></span>
* <span data-ttu-id="d706d-205">Użycie hello metody routingu ruchu "Performance" hello "EndpointLocation" jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="d706d-205">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="d706d-206">W przeciwnym razie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="d706d-206">Otherwise it is optional.</span></span> <span data-ttu-id="d706d-207">Witaj, wartość musi być [Nazwa Nieprawidłowa regionu Azure](https://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="d706d-207">hello value must be a [valid Azure region name](https://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="d706d-208">Witaj, 'Wagi' i 'Priority' są opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="d706d-208">hello 'Weight' and 'Priority' are optional.</span></span>

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="d706d-209">Przykład 1: Dodawanie zewnętrzne punkty końcowe przy użyciu `Add-AzureRmTrafficManagerEndpointConfig` i`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="d706d-209">Example 1: Adding external endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="d706d-210">W tym przykładzie możemy utworzyć profil Menedżera ruchu, dodaj dwa zewnętrzne punkty końcowe i zatwierdź zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="d706d-210">In this example, we create a Traffic Manager profile, add two external endpoints, and commit hello changes.</span></span>

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="d706d-211">Przykład 2: Dodawanie zewnętrzne punkty końcowe przy użyciu`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="d706d-211">Example 2: Adding external endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="d706d-212">W tym przykładzie dodamy istniejący profil tooan zewnętrznego punktu końcowego.</span><span class="sxs-lookup"><span data-stu-id="d706d-212">In this example, we add an external endpoint tooan existing profile.</span></span> <span data-ttu-id="d706d-213">Profil Hello jest określona za pomocą nazwy grupy hello profilu i zasobów.</span><span class="sxs-lookup"><span data-stu-id="d706d-213">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a><span data-ttu-id="d706d-214">Dodawanie punktów końcowych 'Nested'</span><span class="sxs-lookup"><span data-stu-id="d706d-214">Adding 'Nested' endpoints</span></span>

<span data-ttu-id="d706d-215">Każdy profil usługi Traffic Manager określa pojedynczej metody routingu ruchu.</span><span class="sxs-lookup"><span data-stu-id="d706d-215">Each Traffic Manager profile specifies a single traffic-routing method.</span></span> <span data-ttu-id="d706d-216">Istnieją jednak scenariusze, które wymagają bardziej złożone routingu ruchu niż hello routingu udostępniane przez jeden profil Menedżera ruchu.</span><span class="sxs-lookup"><span data-stu-id="d706d-216">However, there are scenarios that require more sophisticated traffic routing than hello routing provided by a single Traffic Manager profile.</span></span> <span data-ttu-id="d706d-217">Można zagnieżdżać Traffic Manager profile toocombine hello korzyści z więcej niż jedna metoda routingu ruchu.</span><span class="sxs-lookup"><span data-stu-id="d706d-217">You can nest Traffic Manager profiles toocombine hello benefits of more than one traffic-routing method.</span></span> <span data-ttu-id="d706d-218">Zagnieżdżonych profilów pozwalają toooverride hello domyślnego menedżera ruchu zachowanie toosupport większych i bardziej złożone wdrożenia aplikacji.</span><span class="sxs-lookup"><span data-stu-id="d706d-218">Nested profiles allow you toooverride hello default Traffic Manager behavior toosupport larger and more complex application deployments.</span></span> <span data-ttu-id="d706d-219">Aby uzyskać bardziej szczegółowe przykłady, zobacz [profilów usługi Traffic Manager zagnieżdżone](traffic-manager-nested-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="d706d-219">For more detailed examples, see [Nested Traffic Manager profiles](traffic-manager-nested-profiles.md).</span></span>

<span data-ttu-id="d706d-220">Zagnieżdżone punkty końcowe zostały skonfigurowane w profilu nadrzędnego hello, przy użyciu typu określonego punktu końcowego "NestedEndpoints".</span><span class="sxs-lookup"><span data-stu-id="d706d-220">Nested endpoints are configured at hello parent profile, using a specific endpoint type, 'NestedEndpoints'.</span></span> <span data-ttu-id="d706d-221">Podczas określania zagnieżdżonych punktów końcowych:</span><span class="sxs-lookup"><span data-stu-id="d706d-221">When specifying nested endpoints:</span></span>

* <span data-ttu-id="d706d-222">Witaj punktu końcowego musi być określona za pomocą parametru "element targetResourceId" hello</span><span class="sxs-lookup"><span data-stu-id="d706d-222">hello endpoint must be specified using hello 'targetResourceId' parameter</span></span>
* <span data-ttu-id="d706d-223">Użycie hello metody routingu ruchu "Performance" hello "EndpointLocation" jest wymagana.</span><span class="sxs-lookup"><span data-stu-id="d706d-223">If hello 'Performance' traffic-routing method is used, hello 'EndpointLocation' is required.</span></span> <span data-ttu-id="d706d-224">W przeciwnym razie jest opcjonalne.</span><span class="sxs-lookup"><span data-stu-id="d706d-224">Otherwise it is optional.</span></span> <span data-ttu-id="d706d-225">Witaj, wartość musi być [Nazwa Nieprawidłowa regionu Azure](http://azure.microsoft.com/regions/).</span><span class="sxs-lookup"><span data-stu-id="d706d-225">hello value must be a [valid Azure region name](http://azure.microsoft.com/regions/).</span></span>
* <span data-ttu-id="d706d-226">Witaj, 'Wagi' i 'Priority' są opcjonalne, jak w przypadku punkty końcowe systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="d706d-226">hello 'Weight' and 'Priority' are optional, as for Azure endpoints.</span></span>
* <span data-ttu-id="d706d-227">Parametr "MinChildEndpoints" Hello jest opcjonalny.</span><span class="sxs-lookup"><span data-stu-id="d706d-227">hello 'MinChildEndpoints' parameter is optional.</span></span> <span data-ttu-id="d706d-228">Witaj, wartością domyślną jest "1".</span><span class="sxs-lookup"><span data-stu-id="d706d-228">hello default value is '1'.</span></span> <span data-ttu-id="d706d-229">Jeśli hello liczba dostępnych punktów końcowych spada poniżej tej wartości progowej, profilu nadrzędnego hello uwzględnia hello podrzędne profil "niższa" i odwracają toohello ruchu z innych punktów końcowych w profilu nadrzędnego hello.</span><span class="sxs-lookup"><span data-stu-id="d706d-229">If hello number of available endpoints falls below this threshold, hello parent profile considers hello child profile 'degraded' and diverts traffic toohello other endpoints in hello parent profile.</span></span>

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="d706d-230">Przykład 1: Dodawanie zagnieżdżonych punktów końcowych przy użyciu `Add-AzureRmTrafficManagerEndpointConfig` i`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="d706d-230">Example 1: Adding nested endpoints using `Add-AzureRmTrafficManagerEndpointConfig` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="d706d-231">W tym przykładzie firma Microsoft Tworzenie nowej usługi Traffic Manager nadrzędnym a podrzędnym profilów, Dodaj obiekt podrzędny hello jako element nadrzędny toohello zagnieżdżonych punktu końcowego i zatwierdź zmiany hello.</span><span class="sxs-lookup"><span data-stu-id="d706d-231">In this example, we create new Traffic Manager child and parent profiles, add hello child as a nested endpoint toohello parent, and commit hello changes.</span></span>

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

<span data-ttu-id="d706d-232">Jednak w tym przykładzie firma Microsoft nie dodano żadnych innych punktów końcowych toohello podrzędnej lub nadrzędnej profilów.</span><span class="sxs-lookup"><span data-stu-id="d706d-232">For brevity in this example, we did not add any other endpoints toohello child or parent profiles.</span></span>

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a><span data-ttu-id="d706d-233">Przykład 2: Dodawanie zagnieżdżonych punktów końcowych przy użyciu`New-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="d706d-233">Example 2: Adding nested endpoints using `New-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="d706d-234">W tym przykładzie dodamy istniejący profil podrzędnych jako zagnieżdżony punktu końcowego tooan istniejącego nadrzędnego profil.</span><span class="sxs-lookup"><span data-stu-id="d706d-234">In this example, we add an existing child profile as a nested endpoint tooan existing parent profile.</span></span> <span data-ttu-id="d706d-235">Profil Hello jest określona za pomocą nazwy grupy hello profilu i zasobów.</span><span class="sxs-lookup"><span data-stu-id="d706d-235">hello profile is specified using hello profile and resource group names.</span></span>

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a><span data-ttu-id="d706d-236">Aktualizowanie punktu końcowego Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-236">Update a Traffic Manager Endpoint</span></span>

<span data-ttu-id="d706d-237">Istnieją dwa sposoby tooupdate istniejący punkt końcowy Menedżera ruchu:</span><span class="sxs-lookup"><span data-stu-id="d706d-237">There are two ways tooupdate an existing Traffic Manager endpoint:</span></span>

1. <span data-ttu-id="d706d-238">Przy użyciu profilu Menedżera ruchu hello `Get-AzureRmTrafficManagerProfile`, zaktualizować właściwości punktu końcowego hello w profilu hello i zatwierdzić zmiany hello przy użyciu `Set-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="d706d-238">Get hello Traffic Manager profile using `Get-AzureRmTrafficManagerProfile`, update hello endpoint properties within hello profile, and commit hello changes using `Set-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="d706d-239">Ta metoda ma zaletą hello jest możliwe tooupdate więcej niż jeden punkt końcowy w ramach jednej operacji.</span><span class="sxs-lookup"><span data-stu-id="d706d-239">This method has hello advantage of being able tooupdate more than one endpoint in a single operation.</span></span>
2. <span data-ttu-id="d706d-240">Przy użyciu punktu końcowego Menedżera ruchu hello `Get-AzureRmTrafficManagerEndpoint`, zaktualizować właściwości punktu końcowego hello i zatwierdzić zmiany hello przy użyciu `Set-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="d706d-240">Get hello Traffic Manager endpoint using `Get-AzureRmTrafficManagerEndpoint`, update hello endpoint properties, and commit hello changes using `Set-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="d706d-241">Ta metoda jest prostsza, ponieważ nie jest wymagane, przeprowadzane jest indeksowanie do tablicy punkty końcowe hello hello profilu.</span><span class="sxs-lookup"><span data-stu-id="d706d-241">This method is simpler, since it does not require indexing into hello Endpoints array in hello profile.</span></span>

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a><span data-ttu-id="d706d-242">Przykład 1: Aktualizowanie punktów końcowych przy użyciu `Get-AzureRmTrafficManagerProfile` i`Set-AzureRmTrafficManagerProfile`</span><span class="sxs-lookup"><span data-stu-id="d706d-242">Example 1: Updating endpoints using `Get-AzureRmTrafficManagerProfile` and `Set-AzureRmTrafficManagerProfile`</span></span>

<span data-ttu-id="d706d-243">W tym przykładzie mamy zmodyfikować priorytet hello na dwa punkty końcowe w ramach istniejącego profilu.</span><span class="sxs-lookup"><span data-stu-id="d706d-243">In this example, we modify hello priority on two endpoints within an existing profile.</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a><span data-ttu-id="d706d-244">Przykład 2: Aktualizowanie punktu końcowego za pomocą `Get-AzureRmTrafficManagerEndpoint` i`Set-AzureRmTrafficManagerEndpoint`</span><span class="sxs-lookup"><span data-stu-id="d706d-244">Example 2: Updating an endpoint using `Get-AzureRmTrafficManagerEndpoint` and `Set-AzureRmTrafficManagerEndpoint`</span></span>

<span data-ttu-id="d706d-245">W tym przykładzie mamy zmodyfikować hello wagę jeden punkt końcowy w istniejącego profilu.</span><span class="sxs-lookup"><span data-stu-id="d706d-245">In this example, we modify hello weight of a single endpoint in an existing profile.</span></span>

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a><span data-ttu-id="d706d-246">Włączanie i wyłączanie punktów końcowych i profili</span><span class="sxs-lookup"><span data-stu-id="d706d-246">Enabling and Disabling Endpoints and Profiles</span></span>

<span data-ttu-id="d706d-247">Menedżer ruchu umożliwia toobe poszczególne punkty końcowe włączone i wyłączone, oraz umożliwiając Włączanie i wyłączanie całego profilów.</span><span class="sxs-lookup"><span data-stu-id="d706d-247">Traffic Manager allows individual endpoints toobe enabled and disabled, as well as allowing enabling and disabling of entire profiles.</span></span>
<span data-ttu-id="d706d-248">Tych zmian przez hello pobierania/aktualizowania/ustawienia punktu końcowego lub profilu zasobów.</span><span class="sxs-lookup"><span data-stu-id="d706d-248">These changes can be made by getting/updating/setting hello endpoint or profile resources.</span></span> <span data-ttu-id="d706d-249">toostreamline tych typowych operacji są również obsługiwane za pośrednictwem dedykowanej polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d706d-249">toostreamline these common operations, they are also supported via dedicated cmdlets.</span></span>

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a><span data-ttu-id="d706d-250">Przykład 1: Włączanie i wyłączanie profilu Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-250">Example 1: Enabling and disabling a Traffic Manager profile</span></span>

<span data-ttu-id="d706d-251">Użyj tooenable profil Menedżera ruchu `Enable-AzureRmTrafficManagerProfile`.</span><span class="sxs-lookup"><span data-stu-id="d706d-251">tooenable a Traffic Manager profile, use `Enable-AzureRmTrafficManagerProfile`.</span></span> <span data-ttu-id="d706d-252">Profil Hello można określić za pomocą obiektu profilu.</span><span class="sxs-lookup"><span data-stu-id="d706d-252">hello profile can be specified using a profile object.</span></span> <span data-ttu-id="d706d-253">Witaj obiektu profilu mogą zostać przekazane za pośrednictwem potoku hello lub za pomocą hello "-TrafficManagerProfile" parametru.</span><span class="sxs-lookup"><span data-stu-id="d706d-253">hello profile object can be passed via hello pipeline or by using hello '-TrafficManagerProfile' parameter.</span></span> <span data-ttu-id="d706d-254">W tym przykładzie określono profil hello hello nazwę grupy profilu i zasobów.</span><span class="sxs-lookup"><span data-stu-id="d706d-254">In this example, we specify hello profile by hello profile and resource group name.</span></span>

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="d706d-255">toodisable profilu usługi Traffic Manager:</span><span class="sxs-lookup"><span data-stu-id="d706d-255">toodisable a Traffic Manager profile:</span></span>

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

<span data-ttu-id="d706d-256">polecenie cmdlet Disable-AzureRmTrafficManagerProfile Hello monituje o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="d706d-256">hello Disable-AzureRmTrafficManagerProfile cmdlet prompts for confirmation.</span></span> <span data-ttu-id="d706d-257">Ten monit można pomijać przy użyciu hello '-Force "parametru.</span><span class="sxs-lookup"><span data-stu-id="d706d-257">This prompt can be suppressed using hello '-Force' parameter.</span></span>

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a><span data-ttu-id="d706d-258">Przykład 2: Włączanie i wyłączanie punktu końcowego Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-258">Example 2: Enabling and disabling a Traffic Manager endpoint</span></span>

<span data-ttu-id="d706d-259">Użyj tooenable punktu końcowego Menedżera ruchu `Enable-AzureRmTrafficManagerEndpoint`.</span><span class="sxs-lookup"><span data-stu-id="d706d-259">tooenable a Traffic Manager endpoint, use `Enable-AzureRmTrafficManagerEndpoint`.</span></span> <span data-ttu-id="d706d-260">Istnieją dwa sposoby toospecify hello punktu końcowego</span><span class="sxs-lookup"><span data-stu-id="d706d-260">There are two ways toospecify hello endpoint</span></span>

1. <span data-ttu-id="d706d-261">Przy użyciu obiektu TrafficManagerEndpoint przekazywane za pośrednictwem potoku hello lub hello "-TrafficManagerEndpoint" parametru</span><span class="sxs-lookup"><span data-stu-id="d706d-261">Using a TrafficManagerEndpoint object passed via hello pipeline or using hello '-TrafficManagerEndpoint' parameter</span></span>
2. <span data-ttu-id="d706d-262">Przy użyciu hello Nazwa punktu końcowego, typ punktu końcowego, nazwa profilu i nazwa grupy zasobów:</span><span class="sxs-lookup"><span data-stu-id="d706d-262">Using hello endpoint name, endpoint type, profile name, and resource group name:</span></span>

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="d706d-263">Podobnie toodisable punktu końcowego Menedżera ruchu:</span><span class="sxs-lookup"><span data-stu-id="d706d-263">Similarly, toodisable a Traffic Manager endpoint:</span></span>

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

<span data-ttu-id="d706d-264">Jak `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` polecenie cmdlet monituje o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="d706d-264">As with `Disable-AzureRmTrafficManagerProfile`, hello `Disable-AzureRmTrafficManagerEndpoint` cmdlet prompts for confirmation.</span></span> <span data-ttu-id="d706d-265">Ten monit można pomijać przy użyciu hello '-Force "parametru.</span><span class="sxs-lookup"><span data-stu-id="d706d-265">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-endpoint"></a><span data-ttu-id="d706d-266">Usuwanie punktu końcowego Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-266">Delete a Traffic Manager Endpoint</span></span>

<span data-ttu-id="d706d-267">poszczególne punkty końcowe tooremove, użyj hello `Remove-AzureRmTrafficManagerEndpoint` polecenia cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d706d-267">tooremove individual endpoints, use hello `Remove-AzureRmTrafficManagerEndpoint` cmdlet:</span></span>

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

<span data-ttu-id="d706d-268">To polecenie cmdlet wyświetli monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="d706d-268">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="d706d-269">Ten monit można pomijać przy użyciu hello '-Force "parametru.</span><span class="sxs-lookup"><span data-stu-id="d706d-269">This prompt can be suppressed using hello '-Force' parameter.</span></span>

## <a name="delete-a-traffic-manager-profile"></a><span data-ttu-id="d706d-270">Usuwanie profilu Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-270">Delete a Traffic Manager Profile</span></span>

<span data-ttu-id="d706d-271">toodelete profilu usługi Traffic Manager, użyj hello `Remove-AzureRmTrafficManagerProfile` polecenia cmdlet, określenie nazwy hello profilu oraz zasobów grupy:</span><span class="sxs-lookup"><span data-stu-id="d706d-271">toodelete a Traffic Manager profile, use hello `Remove-AzureRmTrafficManagerProfile` cmdlet, specifying hello profile and resource group names:</span></span>

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

<span data-ttu-id="d706d-272">To polecenie cmdlet wyświetli monit o potwierdzenie.</span><span class="sxs-lookup"><span data-stu-id="d706d-272">This cmdlet prompts for confirmation.</span></span> <span data-ttu-id="d706d-273">Ten monit można pomijać przy użyciu hello '-Force "parametru.</span><span class="sxs-lookup"><span data-stu-id="d706d-273">This prompt can be suppressed using hello '-Force' parameter.</span></span>

<span data-ttu-id="d706d-274">usunięte toobe profilu Hello można również określić za pomocą obiektu profilu:</span><span class="sxs-lookup"><span data-stu-id="d706d-274">hello profile toobe deleted can also be specified using a profile object:</span></span>

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

<span data-ttu-id="d706d-275">Ta sekwencja również mogą być przekazywane w potoku:</span><span class="sxs-lookup"><span data-stu-id="d706d-275">This sequence can also be piped:</span></span>

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a><span data-ttu-id="d706d-276">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="d706d-276">Next steps</span></span>

[<span data-ttu-id="d706d-277">Monitorowanie Menedżera ruchu</span><span class="sxs-lookup"><span data-stu-id="d706d-277">Traffic Manager monitoring</span></span>](traffic-manager-monitoring.md)

[<span data-ttu-id="d706d-278">Zagadnienia dotyczące wydajności usługi Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="d706d-278">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
