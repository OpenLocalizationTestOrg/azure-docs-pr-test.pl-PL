---
title: "aaaManage pamięci podręcznej Redis Azure przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooperform zadania administracyjne dla pamięci podręcznej Redis Azure za pomocą programu Azure PowerShell."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 1136efe5-1e33-4d91-bb49-c8e2a6dca475
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: sdanie
ms.openlocfilehash: 1d526ce65c4bc05345cd6c3ff370211ed562cab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="316e0-103">Zarządzanie przy użyciu programu Azure PowerShell pamięć podręczna Azure Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="316e0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="316e0-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="316e0-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="316e0-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="316e0-106">W tym temacie pokazano, jak tooperform typowych zadań, takich jak tworzenie, aktualizowanie i jak skalować swoich wystąpień pamięci podręcznej Redis Azure tooregenerate klucze dostępu, jak i tooview informacji o pamięci podręczne.</span><span class="sxs-lookup"><span data-stu-id="316e0-106">This topic shows you how tooperform common tasks such as create, update, and scale your Azure Redis Cache instances, how tooregenerate access keys, and how tooview information about your caches.</span></span> <span data-ttu-id="316e0-107">Aby uzyskać pełną listę poleceń cmdlet programu PowerShell pamięci podręcznej Redis Azure, zobacz [poleceń cmdlet pamięć podręczna Redis Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="316e0-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="316e0-108">Aby uzyskać więcej informacji na temat hello klasycznego modelu wdrażania, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów hello](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="316e0-108">For more information about hello classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and hello state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="316e0-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="316e0-109">Prerequisites</span></span>
<span data-ttu-id="316e0-110">Jeśli użytkownik zainstalował już programu Azure PowerShell, musi mieć program Azure PowerShell w wersji 1.0.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="316e0-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="316e0-111">Można sprawdzić wersji hello programu Azure PowerShell, zainstalowanym za pomocą tego polecenia w wierszu polecenia programu Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-111">You can check hello version of Azure PowerShell that you have installed with this command at hello Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="316e0-112">Po pierwsze należy zalogować się tooAzure za pomocą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-112">First, you must log in tooAzure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="316e0-113">Określ adres e-mail hello konta platformy Azure i jego hasło w oknie dialogowym hello logowania Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="316e0-113">Specify hello email address of your Azure account and its password in hello Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="316e0-114">Następnie Jeśli masz wiele subskrypcji Azure, należy tooset subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="316e0-114">Next, if you have multiple Azure subscriptions, you need tooset your Azure subscription.</span></span> <span data-ttu-id="316e0-115">toosee listę bieżących subskrypcji, należy uruchomić to polecenie.</span><span class="sxs-lookup"><span data-stu-id="316e0-115">toosee a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="316e0-116">toospecify hello subskrypcji, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-116">toospecify hello subscription, run hello following command.</span></span> <span data-ttu-id="316e0-117">Poniższy przykład hello, Nazwa subskrypcji hello jest `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="316e0-117">In hello following example, hello subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="316e0-118">Przed użyciem programu Windows PowerShell z usługą Azure Resource Manager, potrzebne są następujące hello:</span><span class="sxs-lookup"><span data-stu-id="316e0-118">Before you can use Windows PowerShell with Azure Resource Manager, you need hello following:</span></span>

* <span data-ttu-id="316e0-119">Środowiska Windows PowerShell w wersji 3.0 lub 4.0.</span><span class="sxs-lookup"><span data-stu-id="316e0-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="316e0-120">toofind hello wersji programu Windows PowerShell, wpisz:`$PSVersionTable` i sprawdź wartość hello `PSVersion` 3.0 lub 4.0.</span><span class="sxs-lookup"><span data-stu-id="316e0-120">toofind hello version of Windows PowerShell, type:`$PSVersionTable` and verify hello value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="316e0-121">tooinstall zgodnej wersji, zobacz [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) lub [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="316e0-121">tooinstall a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="316e0-122">tooget szczegółową pomoc dla każdego polecenia cmdlet widocznej w tym samouczku, polecenia cmdlet Get-Help hello użycia.</span><span class="sxs-lookup"><span data-stu-id="316e0-122">tooget detailed help for any cmdlet you see in this tutorial, use hello Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="316e0-123">Na przykład tooget pomocy hello `New-AzureRmRedisCache` polecenia cmdlet, wpisz:</span><span class="sxs-lookup"><span data-stu-id="316e0-123">For example, tooget help for hello `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-tooconnect-tooother-clouds"></a><span data-ttu-id="316e0-124">Jak tooconnect tooother chmur</span><span class="sxs-lookup"><span data-stu-id="316e0-124">How tooconnect tooother clouds</span></span>
<span data-ttu-id="316e0-125">Domyślne hello Azure to środowisko `AzureCloud`, która reprezentuje hello wystąpienia globalne chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="316e0-125">By default hello Azure environment is `AzureCloud`, which represents hello global Azure cloud instance.</span></span> <span data-ttu-id="316e0-126">tooconnect tooa inne wystąpienie, użyj hello `Add-AzureRmAccount` z hello `-Environment` lub -`EnvironmentName` przełącznik wiersza polecenia o nazwie środowiska lub hello wymagane środowisko.</span><span class="sxs-lookup"><span data-stu-id="316e0-126">tooconnect tooa different instance, use hello `Add-AzureRmAccount` command with hello `-Environment` or -`EnvironmentName` command line switch with hello desired environment or environment name.</span></span>

<span data-ttu-id="316e0-127">toosee hello listę dostępnych środowisk, uruchom hello `Get-AzureRmEnvironment` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-127">toosee hello list of available environments, run hello `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="tooconnect-toohello-azure-government-cloud"></a><span data-ttu-id="316e0-128">toohello tooconnect chmury Azure dla instytucji rządowych</span><span class="sxs-lookup"><span data-stu-id="316e0-128">tooconnect toohello Azure Government Cloud</span></span>
<span data-ttu-id="316e0-129">toohello tooconnect Azure dla instytucji rządowych chmury, użyj następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-129">tooconnect toohello Azure Government Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="316e0-130">lub</span><span class="sxs-lookup"><span data-stu-id="316e0-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="316e0-131">toocreate pamięci podręcznej w hello Azure dla instytucji rządowych chmury, użyj jednej z następujących lokalizacji hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-131">toocreate a cache in hello Azure Government Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="316e0-132">USGov Virginia</span><span class="sxs-lookup"><span data-stu-id="316e0-132">USGov Virginia</span></span>
* <span data-ttu-id="316e0-133">USGov Iowa</span><span class="sxs-lookup"><span data-stu-id="316e0-133">USGov Iowa</span></span>

<span data-ttu-id="316e0-134">Aby uzyskać więcej informacji na temat hello Azure dla instytucji rządowych chmury zobacz [Microsoft Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/) i [Podręczniku dewelopera programu Microsoft Azure dla instytucji rządowych](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="316e0-134">For more information about hello Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="tooconnect-toohello-azure-china-cloud"></a><span data-ttu-id="316e0-135">toohello tooconnect Azure Chin chmury</span><span class="sxs-lookup"><span data-stu-id="316e0-135">tooconnect toohello Azure China Cloud</span></span>
<span data-ttu-id="316e0-136">toohello tooconnect chmury Chin Azure, użyj następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-136">tooconnect toohello Azure China Cloud, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="316e0-137">lub</span><span class="sxs-lookup"><span data-stu-id="316e0-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="316e0-138">toocreate pamięci podręcznej w hello Azure Chin chmury, użyj jednej z następujących lokalizacji hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-138">toocreate a cache in hello Azure China Cloud, use one of hello following locations.</span></span>

* <span data-ttu-id="316e0-139">Chiny Wschodnie</span><span class="sxs-lookup"><span data-stu-id="316e0-139">China East</span></span>
* <span data-ttu-id="316e0-140">Chiny Północne</span><span class="sxs-lookup"><span data-stu-id="316e0-140">China North</span></span>

<span data-ttu-id="316e0-141">Aby uzyskać więcej informacji na temat hello Azure Chin chmury zobacz [AzureChinaCloud dla platformy Azure obsługiwane przez 21Vianet w Chinach](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="316e0-141">For more information about hello Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="tooconnect-toomicrosoft-azure-germany"></a><span data-ttu-id="316e0-142">tooMicrosoft tooconnect platformy Azure w Niemczech</span><span class="sxs-lookup"><span data-stu-id="316e0-142">tooconnect tooMicrosoft Azure Germany</span></span>
<span data-ttu-id="316e0-143">tooMicrosoft tooconnect platformy Azure w Niemczech, użyj następującego polecenia hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-143">tooconnect tooMicrosoft Azure Germany, use one of hello following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="316e0-144">lub</span><span class="sxs-lookup"><span data-stu-id="316e0-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="316e0-145">toocreate pamięci podręcznej w Microsoft Azure Niemczech, użyj jednej z następujących lokalizacji hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-145">toocreate a cache in Microsoft Azure Germany, use one of hello following locations.</span></span>

* <span data-ttu-id="316e0-146">Niemcy Środkowe</span><span class="sxs-lookup"><span data-stu-id="316e0-146">Germany Central</span></span>
* <span data-ttu-id="316e0-147">Niemcy Północno-Wschodnie</span><span class="sxs-lookup"><span data-stu-id="316e0-147">Germany Northeast</span></span>

<span data-ttu-id="316e0-148">Aby uzyskać więcej informacji o Microsoft platformy Azure w Niemczech, zobacz [Microsoft Azure Niemcy](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="316e0-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="316e0-149">Właściwości używanej do pamięci podręcznej Redis Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="316e0-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="316e0-150">w poniższej tabeli Hello zawiera właściwości i opisy parametrów często używane podczas tworzenia i zarządzania nimi z wystąpień pamięci podręcznej Redis Azure za pomocą programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="316e0-150">hello following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="316e0-151">Parametr</span><span class="sxs-lookup"><span data-stu-id="316e0-151">Parameter</span></span> | <span data-ttu-id="316e0-152">Opis</span><span class="sxs-lookup"><span data-stu-id="316e0-152">Description</span></span> | <span data-ttu-id="316e0-153">Domyślne</span><span class="sxs-lookup"><span data-stu-id="316e0-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="316e0-154">Nazwa</span><span class="sxs-lookup"><span data-stu-id="316e0-154">Name</span></span> |<span data-ttu-id="316e0-155">Nazwa hello pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="316e0-155">Name of hello cache</span></span> | |
| <span data-ttu-id="316e0-156">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="316e0-156">Location</span></span> |<span data-ttu-id="316e0-157">Lokalizacja pamięci podręcznej hello</span><span class="sxs-lookup"><span data-stu-id="316e0-157">Location of hello cache</span></span> | |
| <span data-ttu-id="316e0-158">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="316e0-158">ResourceGroupName</span></span> |<span data-ttu-id="316e0-159">Nazwa grupy zasobów, w których pamięci podręcznej hello toocreate</span><span class="sxs-lookup"><span data-stu-id="316e0-159">Resource group name in which toocreate hello cache</span></span> | |
| <span data-ttu-id="316e0-160">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="316e0-160">Size</span></span> |<span data-ttu-id="316e0-161">rozmiar Hello hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-161">hello size of hello cache.</span></span> <span data-ttu-id="316e0-162">Prawidłowe wartości to: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB</span><span class="sxs-lookup"><span data-stu-id="316e0-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="316e0-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="316e0-163">1GB</span></span> |
| <span data-ttu-id="316e0-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="316e0-164">ShardCount</span></span> |<span data-ttu-id="316e0-165">Liczba Hello toocreate odłamków podczas tworzenia usługi pamięć podręczna premium z włączoną funkcją klastrowania.</span><span class="sxs-lookup"><span data-stu-id="316e0-165">hello number of shards toocreate when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="316e0-166">Prawidłowe wartości to: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="316e0-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="316e0-167">SKU</span><span class="sxs-lookup"><span data-stu-id="316e0-167">SKU</span></span> |<span data-ttu-id="316e0-168">Określa hello SKU hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-168">Specifies hello SKU of hello cache.</span></span> <span data-ttu-id="316e0-169">Prawidłowe wartości to: Basic, Standard, Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="316e0-170">Standardowa</span><span class="sxs-lookup"><span data-stu-id="316e0-170">Standard</span></span> |
| <span data-ttu-id="316e0-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="316e0-171">RedisConfiguration</span></span> |<span data-ttu-id="316e0-172">Określa ustawienia konfiguracji pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="316e0-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="316e0-173">Aby uzyskać szczegółowe informacje o każdym ustawieniu, zobacz następujące hello [RedisConfiguration właściwości](#redisconfiguration-properties) tabeli.</span><span class="sxs-lookup"><span data-stu-id="316e0-173">For details on each setting, see hello following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="316e0-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="316e0-174">EnableNonSslPort</span></span> |<span data-ttu-id="316e0-175">Wskazuje, czy włączono port bez protokołu SSL hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-175">Indicates whether hello non-SSL port is enabled.</span></span> |<span data-ttu-id="316e0-176">False</span><span class="sxs-lookup"><span data-stu-id="316e0-176">False</span></span> |
| <span data-ttu-id="316e0-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="316e0-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="316e0-178">Ten parametr jest przestarzały — zamiast tego użyj RedisConfiguration.</span><span class="sxs-lookup"><span data-stu-id="316e0-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="316e0-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="316e0-179">StaticIP</span></span> |<span data-ttu-id="316e0-180">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa unikatowy adres IP w podsieci hello hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-180">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="316e0-181">Jeśli nie zostanie podana, co jest wybrany dla Ciebie z hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="316e0-181">If not provided, one is chosen for you from hello subnet.</span></span> | |
| <span data-ttu-id="316e0-182">Podsieć</span><span class="sxs-lookup"><span data-stu-id="316e0-182">Subnet</span></span> |<span data-ttu-id="316e0-183">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa nazwę hello hello podsieci, w których pamięci podręcznej hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="316e0-183">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="316e0-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="316e0-184">VirtualNetwork</span></span> |<span data-ttu-id="316e0-185">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa identyfikator zasobu hello hello sieci Wirtualnej, w których pamięci podręcznej hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="316e0-185">When hosting your cache in a VNET, specifies hello resource ID of hello VNET in which toodeploy hello cache.</span></span> | |
| <span data-ttu-id="316e0-186">Właściwość KeyType</span><span class="sxs-lookup"><span data-stu-id="316e0-186">KeyType</span></span> |<span data-ttu-id="316e0-187">Określa klucz dostępu, do którego tooregenerate podczas odnawiania klucze dostępu.</span><span class="sxs-lookup"><span data-stu-id="316e0-187">Specifies which access key tooregenerate when renewing access keys.</span></span> <span data-ttu-id="316e0-188">Prawidłowe wartości to: podstawowej, dodatkowej</span><span class="sxs-lookup"><span data-stu-id="316e0-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="316e0-189">Właściwości RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="316e0-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="316e0-190">Właściwość</span><span class="sxs-lookup"><span data-stu-id="316e0-190">Property</span></span> | <span data-ttu-id="316e0-191">Opis</span><span class="sxs-lookup"><span data-stu-id="316e0-191">Description</span></span> | <span data-ttu-id="316e0-192">Warstwy cenowe</span><span class="sxs-lookup"><span data-stu-id="316e0-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="316e0-193">włączone kopii zapasowej RDB</span><span class="sxs-lookup"><span data-stu-id="316e0-193">rdb-backup-enabled</span></span> |<span data-ttu-id="316e0-194">Czy [trwałość danych Redis](cache-how-to-premium-persistence.md) jest włączone</span><span class="sxs-lookup"><span data-stu-id="316e0-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="316e0-195">Tylko w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-195">Premium only</span></span> |
| <span data-ttu-id="316e0-196">RDB magazynu-— parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="316e0-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="316e0-197">Witaj konto magazynu toohello ciągu połączenia dla [trwałość danych Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="316e0-197">hello connection string toohello storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="316e0-198">Tylko w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-198">Premium only</span></span> |
| <span data-ttu-id="316e0-199">częstotliwość w przypadku wykonywania kopii zapasowych RDB</span><span class="sxs-lookup"><span data-stu-id="316e0-199">rdb-backup-frequency</span></span> |<span data-ttu-id="316e0-200">Częstotliwość wykonywania kopii zapasowych dla Hello [trwałość danych Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="316e0-200">hello backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="316e0-201">Tylko w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-201">Premium only</span></span> |
| <span data-ttu-id="316e0-202">zastrzeżone maxmemory</span><span class="sxs-lookup"><span data-stu-id="316e0-202">maxmemory-reserved</span></span> |<span data-ttu-id="316e0-203">Konfiguruje hello [pamięci zarezerwowanej](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) -cache procesów</span><span class="sxs-lookup"><span data-stu-id="316e0-203">Configures hello [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="316e0-204">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-204">Standard and Premium</span></span> |
| <span data-ttu-id="316e0-205">maxmemory-policy.</span><span class="sxs-lookup"><span data-stu-id="316e0-205">maxmemory-policy</span></span> |<span data-ttu-id="316e0-206">Konfiguruje hello [zasady wykluczania](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) hello pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="316e0-206">Configures hello [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for hello cache</span></span> |<span data-ttu-id="316e0-207">Wszystkie warstwy cenowe</span><span class="sxs-lookup"><span data-stu-id="316e0-207">All pricing tiers</span></span> |
| <span data-ttu-id="316e0-208">powiadomienia przestrzeni kluczy zdarzenia</span><span class="sxs-lookup"><span data-stu-id="316e0-208">notify-keyspace-events</span></span> |<span data-ttu-id="316e0-209">Konfiguruje [powiadomienia przestrzeni kluczy](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="316e0-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="316e0-210">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-210">Standard and Premium</span></span> |
| <span data-ttu-id="316e0-211">Skrót max-ziplist — wpisów</span><span class="sxs-lookup"><span data-stu-id="316e0-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="316e0-212">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="316e0-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="316e0-213">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-213">Standard and Premium</span></span> |
| <span data-ttu-id="316e0-214">max-ziplist — wartość skrótu</span><span class="sxs-lookup"><span data-stu-id="316e0-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="316e0-215">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="316e0-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="316e0-216">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-216">Standard and Premium</span></span> |
| <span data-ttu-id="316e0-217">zestaw max-intset wpisów</span><span class="sxs-lookup"><span data-stu-id="316e0-217">set-max-intset-entries</span></span> |<span data-ttu-id="316e0-218">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="316e0-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="316e0-219">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-219">Standard and Premium</span></span> |
| <span data-ttu-id="316e0-220">zset-max-ziplist wpisów</span><span class="sxs-lookup"><span data-stu-id="316e0-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="316e0-221">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="316e0-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="316e0-222">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-222">Standard and Premium</span></span> |
| <span data-ttu-id="316e0-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="316e0-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="316e0-224">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="316e0-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="316e0-225">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-225">Standard and Premium</span></span> |
| <span data-ttu-id="316e0-226">bazy danych</span><span class="sxs-lookup"><span data-stu-id="316e0-226">databases</span></span> |<span data-ttu-id="316e0-227">Konfiguruje hello liczbę baz danych.</span><span class="sxs-lookup"><span data-stu-id="316e0-227">Configures hello number of databases.</span></span> <span data-ttu-id="316e0-228">Tej właściwości można skonfigurować tylko na tworzenie pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="316e0-229">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="316e0-229">Standard and Premium</span></span> |

## <a name="toocreate-a-redis-cache"></a><span data-ttu-id="316e0-230">toocreate pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-230">toocreate a Redis Cache</span></span>
<span data-ttu-id="316e0-231">Nowe wystąpienia pamięci podręcznej Redis Azure są tworzone przy użyciu hello [AzureRmRedisCache nowy](https://msdn.microsoft.com/library/azure/mt634517.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-231">New Azure Redis Cache instances are created using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="316e0-232">Witaj tworzenia pamięci podręcznej Redis w ramach subskrypcji przy użyciu hello portalu Azure po raz pierwszy hello portalu rejestruje hello `Microsoft.Cache` przestrzeni nazw dla tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="316e0-232">hello first time you create a Redis cache in a subscription using hello Azure portal, hello portal registers hello `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="316e0-233">Jeśli podjęto toocreate hello najpierw Redis pamięci podręcznej w ramach subskrypcji przy użyciu programu PowerShell, najpierw należy zarejestrować tej przestrzeni nazw przy użyciu następującego polecenia; hello w przeciwnym razie poleceń cmdlet, takich jak `New-AzureRmRedisCache` i `Get-AzureRmRedisCache` się nie powieść.</span><span class="sxs-lookup"><span data-stu-id="316e0-233">If you attempt toocreate hello first Redis cache in a subscription using PowerShell, you must first register that namespace using hello following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="316e0-234">toosee listę dostępnych parametrów i ich opisy `New-AzureRmRedisCache`Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-234">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCache -detailed

    NAME
        New-AzureRmRedisCache

    SYNOPSIS
        Creates a new redis cache.


    SYNTAX
        New-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Location <String> [-RedisVersion <String>]
        [-Size <String>] [-Sku <String>] [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort
        <Boolean>] [-ShardCount <Integer>] [-VirtualNetwork <String>] [-Subnet <String>] [-StaticIP <String>]
        [<CommonParameters>]


    DESCRIPTION
        hello New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of hello redis cache toocreate.

        -ResourceGroupName <String>
            Name of resource group in which toocreate hello redis cache.

        -Location <String>
            Location in which toocreate hello redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, hello default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        -VirtualNetwork <String>
            hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="316e0-235">toocreate pamięci podręcznej z parametrów domyślnych, uruchom następujące polecenie hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-235">toocreate a cache with default parameters, run hello following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="316e0-236">`ResourceGroupName`, `Name`, i `Location` są wymagane parametry, ale pozostałe hello są opcjonalne i mają przypisane wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="316e0-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but hello rest are optional and have default values.</span></span> <span data-ttu-id="316e0-237">Uruchamianie hello poprzednie polecenie tworzy wystąpienie standardowy SKU pamięć podręczna Redis Azure hello określonej nazwy, lokalizacji i grupy zasobów o rozmiarze z portu bez protokołu SSL hello wyłączone 1 GB.</span><span class="sxs-lookup"><span data-stu-id="316e0-237">Running hello previous command creates a Standard SKU Azure Redis Cache instance with hello specified name, location, and resource group, that is 1 GB in size with hello non-SSL port disabled.</span></span>

<span data-ttu-id="316e0-238">toocreate pamięć podręczna premium, określ rozmiar P1 (6 GB — 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), lub P4 (53 GB - 530 GB).</span><span class="sxs-lookup"><span data-stu-id="316e0-238">toocreate a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="316e0-239">tooenable klaster, określić liczbę niezależnych przy użyciu hello `ShardCount` parametru.</span><span class="sxs-lookup"><span data-stu-id="316e0-239">tooenable clustering, specify a shard count using hello `ShardCount` parameter.</span></span> <span data-ttu-id="316e0-240">Witaj poniższy przykład tworzy pamięć podręczna premium P1 z odłamków 3.</span><span class="sxs-lookup"><span data-stu-id="316e0-240">hello following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="316e0-241">Pamięć podręczna premium P1 6 GB ma rozmiar, a ponieważ możemy określić trzy odłamków hello całkowity rozmiar jest 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="316e0-241">A P1 premium cache is 6 GB in size, and since we specified three shards hello total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="316e0-242">wartości toospecify hello `RedisConfiguration` parametru, ujmij wartości hello wewnątrz `{}` jako klucza i wartości, takich jak pary `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="316e0-242">toospecify values for hello `RedisConfiguration` parameter, enclose hello values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="316e0-243">Witaj poniższy przykład tworzy standardowe 1 GB pamięci podręcznej z `allkeys-random` maxmemory zasad i przestrzeni kluczy powiadomienia skonfigurowane z `KEA`.</span><span class="sxs-lookup"><span data-stu-id="316e0-243">hello following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="316e0-244">Aby uzyskać więcej informacji, zobacz [powiadomienia przestrzeni kluczy (Zaawansowane ustawienia)](cache-configure.md#keyspace-notifications-advanced-settings) i [zasady pamięci](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="316e0-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="tooconfigure-hello-databases-setting-during-cache-creation"></a><span data-ttu-id="316e0-245">bazy danych hello tooconfigure ustawienie podczas tworzenia pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="316e0-245">tooconfigure hello databases setting during cache creation</span></span>
<span data-ttu-id="316e0-246">Witaj `databases` ustawienie można skonfigurować tylko podczas tworzenia pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-246">hello `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="316e0-247">Witaj poniższy przykład tworzy — warstwa premium P3 (26 GB) pamięci podręcznej z 48 baz danych przy użyciu hello [AzureRmRedisCache nowy](https://msdn.microsoft.com/library/azure/mt634517.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-247">hello following example creates a premium P3 (26 GB) cache with 48 databases using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="316e0-248">Aby uzyskać więcej informacji na temat hello `databases` właściwości, zobacz [konfiguracji serwera domyślna pamięci podręcznej Redis Azure](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="316e0-248">For more information on hello `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="316e0-249">Aby uzyskać więcej informacji na temat tworzenia pamięci podręcznej przy użyciu hello [AzureRmRedisCache nowy](https://msdn.microsoft.com/library/azure/mt634517.aspx) polecenia cmdlet, zobacz poprzednie hello [toocreate pamięci podręcznej Redis](#to-create-a-redis-cache) sekcji.</span><span class="sxs-lookup"><span data-stu-id="316e0-249">For more information on creating a cache using hello [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see hello previous [toocreate a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="tooupdate-a-redis-cache"></a><span data-ttu-id="316e0-250">tooupdate pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-250">tooupdate a Redis cache</span></span>
<span data-ttu-id="316e0-251">Wystąpienia pamięci podręcznej Redis Azure są aktualizowane przy użyciu hello [AzureRmRedisCache zestaw](https://msdn.microsoft.com/library/azure/mt634518.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-251">Azure Redis Cache instances are updated using hello [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="316e0-252">toosee listę dostępnych parametrów i ich opisy `Set-AzureRmRedisCache`Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-252">toosee a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Set-AzureRmRedisCache -detailed

    NAME
        Set-AzureRmRedisCache

    SYNOPSIS
        Set redis cache updatable parameters.

    SYNTAX
        Set-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Size <String>] [-Sku <String>]
        [-MaxMemoryPolicy <String>] [-RedisConfiguration <Hashtable>] [-EnableNonSslPort <Boolean>] [-ShardCount
        <Integer>] [<CommonParameters>]

    DESCRIPTION
        hello Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooupdate.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -Size <String>
            Size of hello redis cache. hello default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. hello default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            hello 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting tooset
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. hello default value is null and no change will be made toothe
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            hello number of shards toocreate on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="316e0-253">Witaj `Set-AzureRmRedisCache` polecenia cmdlet mogą być używane tooupdate właściwości, takie jak `Size`, `Sku`, `EnableNonSslPort`i hello `RedisConfiguration` wartości.</span><span class="sxs-lookup"><span data-stu-id="316e0-253">hello `Set-AzureRmRedisCache` cmdlet can be used tooupdate properties such as `Size`, `Sku`, `EnableNonSslPort`, and hello `RedisConfiguration` values.</span></span> 

<span data-ttu-id="316e0-254">Witaj następujące polecenia, które aktualizacje hello maxmemory-policy dla pamięci podręcznej Redis hello o nazwie myCache.</span><span class="sxs-lookup"><span data-stu-id="316e0-254">hello following command updates hello maxmemory-policy for hello Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="tooscale-a-redis-cache"></a><span data-ttu-id="316e0-255">tooscale pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-255">tooscale a Redis cache</span></span>
<span data-ttu-id="316e0-256">`Set-AzureRmRedisCache`może być używane tooscale wystąpienia pamięci podręcznej Azure Redis podczas hello `Size`, `Sku`, lub `ShardCount` są modyfikowane właściwości.</span><span class="sxs-lookup"><span data-stu-id="316e0-256">`Set-AzureRmRedisCache` can be used tooscale an Azure Redis cache instance when hello `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="316e0-257">Skalowanie pamięci podręcznej przy użyciu programu PowerShell jest toohello podmiotu takie same ograniczenia i wytyczne jako skalowanie pamięci podręcznej z hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="316e0-257">Scaling a cache using PowerShell is subject toohello same limits and guidelines as scaling a cache from hello Azure portal.</span></span> <span data-ttu-id="316e0-258">Możesz skalować tooa inną warstwa cenowa z hello następujące ograniczenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-258">You can scale tooa different pricing tier with hello following restrictions.</span></span>
> 
> * <span data-ttu-id="316e0-259">Nie można skalować z wyższej cenową warstwy tooa dolnej warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="316e0-259">You can't scale from a higher pricing tier tooa lower pricing tier.</span></span>
> * <span data-ttu-id="316e0-260">Nie można skalować z **Premium** pamięci podręcznej w dół tooa **standardowe** lub **podstawowe** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-260">You can't scale from a **Premium** cache down tooa **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="316e0-261">Nie można skalować z **standardowe** pamięci podręcznej w dół tooa **podstawowe** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-261">You can't scale from a **Standard** cache down tooa **Basic** cache.</span></span>
> * <span data-ttu-id="316e0-262">Możesz skalować z **podstawowe** pamięci podręcznej tooa **standardowe** pamięci podręcznej, ale nie można zmienić rozmiaru hello na powitania tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="316e0-262">You can scale from a **Basic** cache tooa **Standard** cache but you can't change hello size at hello same time.</span></span> <span data-ttu-id="316e0-263">Jeśli potrzebujesz zmienić rozmiar należy kolejnych skalowania rozmiar toohello żądaną operację.</span><span class="sxs-lookup"><span data-stu-id="316e0-263">If you need a different size, you can do a subsequent scaling operation toohello desired size.</span></span>
> * <span data-ttu-id="316e0-264">Nie można skalować z **podstawowe** pamięci podręcznej bezpośrednio tooa **Premium** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-264">You can't scale from a **Basic** cache directly tooa **Premium** cache.</span></span> <span data-ttu-id="316e0-265">Należy skalować z **podstawowe** za**standardowe** w jednej operacji skalowania, a następnie z **standardowe** za**Premium** kolejnych skalowania Operacja.</span><span class="sxs-lookup"><span data-stu-id="316e0-265">You must scale from **Basic** too**Standard** in one scaling operation, and then from **Standard** too**Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="316e0-266">Nie można skalować z większego rozmiaru dół toohello **C0 (250 MB)** rozmiar.</span><span class="sxs-lookup"><span data-stu-id="316e0-266">You can't scale from a larger size down toohello **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="316e0-267">Aby uzyskać więcej informacji, zobacz [jak tooScale Azure pamięci podręcznej Redis](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="316e0-267">For more information, see [How tooScale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="316e0-268">Witaj poniższy przykład przedstawia sposób tooscale pamięci podręcznej o nazwie `myCache` tooa 2,5 GB w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-268">hello following example shows how tooscale a cache named `myCache` tooa 2.5 GB cache.</span></span> <span data-ttu-id="316e0-269">Należy pamiętać, że to polecenie działa zarówno Basic lub Standard pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="316e0-270">Po uruchomieniu tego polecenia, zwracany jest stan hello hello pamięci podręcznej (podobne toocalling `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="316e0-270">After this command is issued, hello status of hello cache is returned (similar toocalling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="316e0-271">Należy pamiętać, że hello `ProvisioningState` jest `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="316e0-271">Note that hello `ProvisioningState` is `Scaling`.</span></span>

    PS C:\> Set-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup -Size 2.5GB


    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/mygroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Scaling
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 150], [notify-keyspace-events, KEA],
                         [maxmemory-delta, 150]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : mygroup
    PrimaryKey         : ....
    SecondaryKey       : ....
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

<span data-ttu-id="316e0-272">Po zakończeniu operacji skalowania hello hello `ProvisioningState` zmiany zbyt`Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="316e0-272">When hello scaling operation is complete, hello `ProvisioningState` changes too`Succeeded`.</span></span> <span data-ttu-id="316e0-273">Jeśli potrzebujesz toomake kolejnych operacji skalowania, takich jak zmiana z tooStandard podstawowych, a następnie zmienić rozmiar hello, należy zaczekać, aż hello Poprzednia operacja została ukończona lub jest wyświetlany następujący błąd podobny toohello.</span><span class="sxs-lookup"><span data-stu-id="316e0-273">If you need toomake a subsequent scaling operation, such as changing from Basic tooStandard and then changing hello size, you must wait until hello previous operation is complete or you receive an error similar toohello following.</span></span>

    Set-AzureRmRedisCache : Conflict: hello resource '...' is not in a stable state, and is currently unable tooaccept hello update request.

## <a name="tooget-information-about-a-redis-cache"></a><span data-ttu-id="316e0-274">tooget informacji o pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-274">tooget information about a Redis cache</span></span>
<span data-ttu-id="316e0-275">Można pobrać informacji o pamięci podręcznej przy użyciu hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-275">You can retrieve information about a cache using hello [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="316e0-276">toosee listę dostępnych parametrów i ich opisy `Get-AzureRmRedisCache`Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-276">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in hello specified resource group or all caches in hello current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCache cmdlet gets hello details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in hello specified resource group.

        If no parameters are given than it will return details about all caches hello current subscription.

    PARAMETERS
        -Name <String>
            hello name of hello cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns hello details for hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns hello details of hello cache specified by Name. If only hello ResourceGroup
            parameter is provided, then details for all caches in hello resource group are returned.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="316e0-277">Uruchom tooreturn informacji na temat wszystkich usług pamięć podręczna w bieżącej subskrypcji hello `Get-AzureRmRedisCache` bez żadnych parametrów.</span><span class="sxs-lookup"><span data-stu-id="316e0-277">tooreturn information about all caches in hello current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="316e0-278">Uruchom tooreturn informacji na temat wszystkich usług pamięć podręczna w grupie zasobów specyficznych `Get-AzureRmRedisCache` z hello `ResourceGroupName` parametru.</span><span class="sxs-lookup"><span data-stu-id="316e0-278">tooreturn information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with hello `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="316e0-279">Uruchom tooreturn informacji na temat określonych pamięci podręcznej, `Get-AzureRmRedisCache` z hello `Name` parametr zawierający nazwę hello hello pamięci podręcznej i hello `ResourceGroupName` parametru z grupą zasobów hello zawierającą tej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-279">tooreturn information about a specific cache, run `Get-AzureRmRedisCache` with hello `Name` parameter containing hello name of hello cache, and hello `ResourceGroupName` parameter with hello resource group containing that cache.</span></span>

    PS C:\> Get-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Name               : mycache
    Id                 : /subscriptions/12ad12bd-abdc-2231-a2ed-a2b8b246bbad4/resourceGroups/myGroup/providers/Mi
                         crosoft.Cache/Redis/mycache
    Location           : South Central US
    Type               : Microsoft.Cache/Redis
    HostName           : mycache.redis.cache.windows.net
    Port               : 6379
    ProvisioningState  : Succeeded
    SslPort            : 6380
    RedisConfiguration : {[maxmemory-policy, volatile-lru], [maxmemory-reserved, 62], [notify-keyspace-events, KEA],
                         [maxclients, 1000]...}
    EnableNonSslPort   : False
    RedisVersion       : 3.0
    Size               : 1GB
    Sku                : Standard
    ResourceGroupName  : myGroup
    VirtualNetwork     :
    Subnet             :
    StaticIP           :
    TenantSettings     : {}
    ShardCount         :

## <a name="tooretrieve-hello-access-keys-for-a-redis-cache"></a><span data-ttu-id="316e0-280">tooretrieve hello klucze dostępu pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-280">tooretrieve hello access keys for a Redis cache</span></span>
<span data-ttu-id="316e0-281">tooretrieve hello klucze dostępu dla pamięci podręcznej, można użyć hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-281">tooretrieve hello access keys for your cache, you can use hello [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="316e0-282">toosee listę dostępnych parametrów i ich opisy `Get-AzureRmRedisCacheKey`Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-282">toosee a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets hello accesskeys for hello specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        hello Get-AzureRmRedisCacheKey cmdlet gets hello access keys for hello specified cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="316e0-283">tooretrieve hello kluczy dla pamięci podręcznej, wywołanie hello `Get-AzureRmRedisCacheKey` polecenia cmdlet i przekaż nazwę hello pamięć podręczną hello nazwę grupy zasobów hello, która zawiera hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-283">tooretrieve hello keys for your cache, call hello `Get-AzureRmRedisCacheKey` cmdlet and pass in hello name of your cache hello name of hello resource group that contains hello cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="tooregenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="316e0-284">tooregenerate klucze dostępu pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-284">tooregenerate access keys for your Redis cache</span></span>
<span data-ttu-id="316e0-285">tooregenerate hello klucze dostępu dla pamięci podręcznej, można użyć hello [AzureRmRedisCacheKey nowy](https://msdn.microsoft.com/library/azure/mt634512.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-285">tooregenerate hello access keys for your cache, you can use hello [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="316e0-286">toosee listę dostępnych parametrów i ich opisy `New-AzureRmRedisCacheKey`Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-286">toosee a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run hello following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates hello access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        hello New-AzureRmRedisCacheKey cmdlet regenerate hello access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of hello redis cache.

        -ResourceGroupName <String>
            Name of hello resource group for hello cache.

        -KeyType <String>
            Specifies whether tooregenerate hello primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When hello Force parameter is provided, hello specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="316e0-287">tooregenerate klucz podstawowy lub pomocniczy hello pamięci podręcznej, wywołanie hello `New-AzureRmRedisCacheKey` polecenia cmdlet i przekaż hello Nazwa grupy zasobów oraz określ `Primary` lub `Secondary` dla hello `KeyType` parametru.</span><span class="sxs-lookup"><span data-stu-id="316e0-287">tooregenerate hello primary or secondary key for your cache, call hello `New-AzureRmRedisCacheKey` cmdlet and pass in hello name, resource group, and specify either `Primary` or `Secondary` for hello `KeyType` parameter.</span></span> <span data-ttu-id="316e0-288">W hello poniższy przykład hello pomocniczy klucz dostępu dla pamięci podręcznej zostanie ponownie wygenerowany.</span><span class="sxs-lookup"><span data-stu-id="316e0-288">In hello following example, hello secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want tooregenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="toodelete-a-redis-cache"></a><span data-ttu-id="316e0-289">toodelete pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-289">toodelete a Redis cache</span></span>
<span data-ttu-id="316e0-290">toodelete pamięci podręcznej Redis, użyj hello [AzureRmRedisCache Usuń](https://msdn.microsoft.com/library/azure/mt634515.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-290">toodelete a Redis cache, use hello [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="316e0-291">toosee listę dostępnych parametrów i ich opisy `Remove-AzureRmRedisCache`Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-291">toosee a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        hello Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of hello redis cache tooremove.

        -ResourceGroupName <String>
            Name of hello resource group of hello cache tooremove.

        -Force
            When hello Force parameter is provided, hello cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes hello cache and does not return any value. If hello PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating hello success of hello operatio

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="316e0-292">W hello poniższy przykład, hello pamięci podręcznej o nazwie `myCache` zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="316e0-292">In hello following example, hello cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want tooremove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="tooimport-a-redis-cache"></a><span data-ttu-id="316e0-293">tooimport pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-293">tooimport a Redis cache</span></span>
<span data-ttu-id="316e0-294">Dane można importować do wystąpienia pamięci podręcznej Redis Azure za pomocą hello `Import-AzureRmRedisCache` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-294">You can import data into an Azure Redis Cache instance using hello `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="316e0-295">Narzędzie importu/eksportu jest dostępna tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="316e0-296">Aby uzyskać więcej informacji na temat importowania i eksportowania, zobacz [importować i eksportować dane w pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="316e0-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="316e0-297">toosee listę dostępnych parametrów i ich opisy `Import-AzureRmRedisCache`Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-297">toosee a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs tooAzure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Import-AzureRmRedisCache cmdlet imports data from hello specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into hello cache.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -Force
            When hello Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If hello PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating hello success of the
            operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="316e0-298">Witaj następujące polecenie importuje dane z obiektu blob hello określonego przez identyfikator uri sygnatury dostępu Współdzielonego hello do pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="316e0-298">hello following command imports data from hello blob specified by hello SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="tooexport-a-redis-cache"></a><span data-ttu-id="316e0-299">tooexport pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-299">tooexport a Redis cache</span></span>
<span data-ttu-id="316e0-300">Można eksportować dane z wystąpienia pamięci podręcznej Redis Azure za pomocą hello `Export-AzureRmRedisCache` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-300">You can export data from an Azure Redis Cache instance using hello `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="316e0-301">Narzędzie importu/eksportu jest dostępna tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="316e0-302">Aby uzyskać więcej informacji na temat importowania i eksportowania, zobacz [importować i eksportować dane w pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="316e0-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="316e0-303">toosee listę dostępnych parametrów i ich opisy `Export-AzureRmRedisCache`Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-303">toosee a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache tooa specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache tooa specified container.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -Prefix <String>
            Prefix toouse for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for hello blob.  Currently "rdb" is hello only supported, with other formats expected in hello future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="316e0-304">Witaj następujące polecenie eksportuje dane z wystąpienia pamięci podręcznej Redis Azure do kontenera hello określony przez identyfikator uri sygnatury dostępu Współdzielonego hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-304">hello following command exports data from an Azure Redis Cache instance into hello container specified by hello SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="tooreboot-a-redis-cache"></a><span data-ttu-id="316e0-305">tooreboot pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="316e0-305">tooreboot a Redis cache</span></span>
<span data-ttu-id="316e0-306">Ponowne uruchomienie wystąpienia pamięci podręcznej Redis Azure za pomocą hello `Reset-AzureRmRedisCache` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="316e0-306">You can reboot your Azure Redis Cache instance using hello `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="316e0-307">Ponowne uruchomienie jest dostępna tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="316e0-308">Aby uzyskać więcej informacji o ponowne uruchomienie z pamięci podręcznej, zobacz [pamięci podręcznej administracji — ponowny rozruch](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="316e0-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="316e0-309">toosee listę dostępnych parametrów i ich opisy `Reset-AzureRmRedisCache`Uruchom hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="316e0-309">toosee a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run hello following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        hello Reset-AzureRmRedisCache cmdlet reboots hello specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            hello name of hello cache.

        -ResourceGroupName <String>
            hello name of hello resource group that contains hello cache.

        -RebootType <String>
            Which node tooreboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard tooreboot when rebooting a premium cache with clustering enabled.

        -Force
            When hello Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If hello PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating hello success of hello operation.

        <CommonParameters>
            This cmdlet supports hello common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="316e0-310">Hello następujące polecenie ponownego uruchamiania obu węzłów hello określono pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="316e0-310">hello following command reboots both nodes of hello specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="316e0-311">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="316e0-311">Next steps</span></span>
<span data-ttu-id="316e0-312">toolearn więcej informacji na temat przy użyciu programu Windows PowerShell przy użyciu platformy Azure, zobacz następujące zasoby hello:</span><span class="sxs-lookup"><span data-stu-id="316e0-312">toolearn more about using Windows PowerShell with Azure, see hello following resources:</span></span>

* [<span data-ttu-id="316e0-313">Azure dokumentację poleceń cmdlet pamięci podręcznej Redis w witrynie MSDN</span><span class="sxs-lookup"><span data-stu-id="316e0-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="316e0-314">[Polecenia cmdlet Menedżera zasobów systemu Azure](http://go.microsoft.com/fwlink/?LinkID=394765): Omówienie poleceń cmdlet hello toouse w module usługi Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="316e0-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn toouse hello cmdlets in hello Azure Resource Manager module.</span></span>
* <span data-ttu-id="316e0-315">[Toomanage przy użyciu zasobów grup zasobów platformy Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): Dowiedz się, jak toocreate grup zasobów w hello portalu Azure i zarządzanie nimi.</span><span class="sxs-lookup"><span data-stu-id="316e0-315">[Using Resource groups toomanage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how toocreate and manage resource groups in hello Azure portal.</span></span>
* <span data-ttu-id="316e0-316">[Azure blog](http://blogs.msdn.com/windowsazure): więcej informacji na temat nowych funkcji w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="316e0-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="316e0-317">[Blog dotyczący programu Windows PowerShell](http://blogs.msdn.com/powershell): więcej informacji na temat nowych funkcji w programie Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="316e0-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="316e0-318">["Witaj, Twórco skryptów!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Pobierz rzeczywistych porady i wskazówki związane z hello społeczności programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="316e0-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from hello Windows PowerShell community.</span></span>

