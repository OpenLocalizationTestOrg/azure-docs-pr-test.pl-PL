---
title: "Zarządzanie pamięć podręczna Azure Redis przy użyciu programu Azure PowerShell | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak wykonywać zadania administracyjne dla pamięci podręcznej Redis Azure za pomocą programu Azure PowerShell."
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
ms.openlocfilehash: 0a5c95eab3fd01f611fc049e80c5c506857e0b81
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/03/2017
---
# <a name="manage-azure-redis-cache-with-azure-powershell"></a><span data-ttu-id="564a3-103">Zarządzanie przy użyciu programu Azure PowerShell pamięć podręczna Azure Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-103">Manage Azure Redis Cache with Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="564a3-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="564a3-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="564a3-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="564a3-105">Azure CLI</span></span>](cache-manage-cli.md)
> 
> 

<span data-ttu-id="564a3-106">W tym temacie przedstawiono sposób typowych zadań do wykonywania takich jak tworzenie, aktualizacją, a skalowania swoich wystąpień w pamięci podręcznej Redis Azure, jak można ponownie wygenerować klucze dostępu i sposób wyświetlania informacji o pamięci podręczne.</span><span class="sxs-lookup"><span data-stu-id="564a3-106">This topic shows you how to perform common tasks such as create, update, and scale your Azure Redis Cache instances, how to regenerate access keys, and how to view information about your caches.</span></span> <span data-ttu-id="564a3-107">Aby uzyskać pełną listę poleceń cmdlet programu PowerShell pamięci podręcznej Redis Azure, zobacz [poleceń cmdlet pamięć podręczna Redis Azure](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span><span class="sxs-lookup"><span data-stu-id="564a3-107">For a complete list of Azure Redis Cache PowerShell cmdlets, see [Azure Redis Cache cmdlets](https://msdn.microsoft.com/library/azure/mt634513.aspx).</span></span>

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="564a3-108">Aby uzyskać więcej informacji na temat klasycznym modelu wdrażania, zobacz [usługi Azure Resource Manager, a wdrożenie klasyczne: zrozumienie modele wdrażania i stan zasobów](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span><span class="sxs-lookup"><span data-stu-id="564a3-108">For more information about the classic deployment model, see [Azure Resource Manager vs. classic deployment: Understand deployment models and the state of your resources](../azure-resource-manager/resource-manager-deployment-model.md#classic-deployment-characteristics).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="564a3-109">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="564a3-109">Prerequisites</span></span>
<span data-ttu-id="564a3-110">Jeśli użytkownik zainstalował już programu Azure PowerShell, musi mieć program Azure PowerShell w wersji 1.0.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="564a3-110">If you have already installed Azure PowerShell, you must have Azure PowerShell version 1.0.0 or later.</span></span> <span data-ttu-id="564a3-111">Można sprawdzić wersji programu Azure PowerShell, zainstalowanym za pomocą tego polecenia w wierszu polecenia programu PowerShell systemu Azure.</span><span class="sxs-lookup"><span data-stu-id="564a3-111">You can check the version of Azure PowerShell that you have installed with this command at the Azure PowerShell command prompt.</span></span>

    Get-Module azure | format-table version


<span data-ttu-id="564a3-112">Najpierw należy logujesz się na platformie Azure za pomocą tego polecenia.</span><span class="sxs-lookup"><span data-stu-id="564a3-112">First, you must log in to Azure with this command.</span></span>

    Login-AzureRmAccount

<span data-ttu-id="564a3-113">Określ adres e-mail konta platformy Azure i jego hasło w oknie dialogowym logowania Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="564a3-113">Specify the email address of your Azure account and its password in the Microsoft Azure sign-in dialog.</span></span>

<span data-ttu-id="564a3-114">Następnie Jeśli masz wiele subskrypcji Azure, należy ustawić subskrypcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="564a3-114">Next, if you have multiple Azure subscriptions, you need to set your Azure subscription.</span></span> <span data-ttu-id="564a3-115">Aby wyświetlić listę bieżące subskrypcje, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-115">To see a list of your current subscriptions, run this command.</span></span>

    Get-AzureRmSubscription | sort SubscriptionName | Select SubscriptionName

<span data-ttu-id="564a3-116">Aby określić subskrypcję, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-116">To specify the subscription, run the following command.</span></span> <span data-ttu-id="564a3-117">W poniższym przykładzie Nazwa subskrypcji jest `ContosoSubscription`.</span><span class="sxs-lookup"><span data-stu-id="564a3-117">In the following example, the subscription name is `ContosoSubscription`.</span></span>

    Select-AzureRmSubscription -SubscriptionName ContosoSubscription

<span data-ttu-id="564a3-118">Przed użyciem programu Windows PowerShell z usługą Azure Resource Manager, potrzebne są następujące elementy:</span><span class="sxs-lookup"><span data-stu-id="564a3-118">Before you can use Windows PowerShell with Azure Resource Manager, you need the following:</span></span>

* <span data-ttu-id="564a3-119">Środowiska Windows PowerShell w wersji 3.0 lub 4.0.</span><span class="sxs-lookup"><span data-stu-id="564a3-119">Windows PowerShell, Version 3.0 or 4.0.</span></span> <span data-ttu-id="564a3-120">Aby znaleźć wersję środowiska Windows PowerShell, wpisz:`$PSVersionTable` i sprawdź wartość `PSVersion` jest 3.0 lub 4.0.</span><span class="sxs-lookup"><span data-stu-id="564a3-120">To find the version of Windows PowerShell, type:`$PSVersionTable` and verify the value of `PSVersion` is 3.0 or 4.0.</span></span> <span data-ttu-id="564a3-121">Aby zainstalować zgodną wersję, zobacz [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) lub [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span><span class="sxs-lookup"><span data-stu-id="564a3-121">To install a compatible version, see [Windows Management Framework 3.0](http://www.microsoft.com/download/details.aspx?id=34595) or [Windows Management Framework 4.0](http://www.microsoft.com/download/details.aspx?id=40855).</span></span>

<span data-ttu-id="564a3-122">Aby uzyskać szczegółową pomoc dla każdego polecenia cmdlet, które są widoczne w tym samouczku, użyj polecenia cmdlet Get-Help.</span><span class="sxs-lookup"><span data-stu-id="564a3-122">To get detailed help for any cmdlet you see in this tutorial, use the Get-Help cmdlet.</span></span>

    Get-Help <cmdlet-name> -Detailed

<span data-ttu-id="564a3-123">Na przykład, aby uzyskać pomoc dotyczącą `New-AzureRmRedisCache` polecenia cmdlet, wpisz:</span><span class="sxs-lookup"><span data-stu-id="564a3-123">For example, to get help for the `New-AzureRmRedisCache` cmdlet, type:</span></span>

    Get-Help New-AzureRmRedisCache -Detailed

### <a name="how-to-connect-to-other-clouds"></a><span data-ttu-id="564a3-124">Łączenie z innych chmur</span><span class="sxs-lookup"><span data-stu-id="564a3-124">How to connect to other clouds</span></span>
<span data-ttu-id="564a3-125">Domyślnie platformy Azure to środowisko `AzureCloud`, reprezentuje wystąpienie globalne chmury Azure.</span><span class="sxs-lookup"><span data-stu-id="564a3-125">By default the Azure environment is `AzureCloud`, which represents the global Azure cloud instance.</span></span> <span data-ttu-id="564a3-126">Aby nawiązać połączenie z innym wystąpieniem, użyj `Add-AzureRmAccount` z `-Environment` lub -`EnvironmentName` przełącznik wiersza polecenia o nazwie środowiska lub wymagane środowisko.</span><span class="sxs-lookup"><span data-stu-id="564a3-126">To connect to a different instance, use the `Add-AzureRmAccount` command with the `-Environment` or -`EnvironmentName` command line switch with the desired environment or environment name.</span></span>

<span data-ttu-id="564a3-127">Aby wyświetlić listę dostępnych środowisk, należy uruchomić `Get-AzureRmEnvironment` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-127">To see the list of available environments, run the `Get-AzureRmEnvironment` cmdlet.</span></span>

### <a name="to-connect-to-the-azure-government-cloud"></a><span data-ttu-id="564a3-128">Do nawiązania połączenia chmury Azure dla instytucji rządowych</span><span class="sxs-lookup"><span data-stu-id="564a3-128">To connect to the Azure Government Cloud</span></span>
<span data-ttu-id="564a3-129">Aby połączyć do chmury Azure dla instytucji rządowych, użyj jednej z następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="564a3-129">To connect to the Azure Government Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureUSGovernment

<span data-ttu-id="564a3-130">lub</span><span class="sxs-lookup"><span data-stu-id="564a3-130">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureUSGovernment)

<span data-ttu-id="564a3-131">Aby utworzyć pamięć podręczną w chmurze Azure dla instytucji rządowych, użyj jednej z następujących lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="564a3-131">To create a cache in the Azure Government Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="564a3-132">USGov Virginia</span><span class="sxs-lookup"><span data-stu-id="564a3-132">USGov Virginia</span></span>
* <span data-ttu-id="564a3-133">USGov Iowa</span><span class="sxs-lookup"><span data-stu-id="564a3-133">USGov Iowa</span></span>

<span data-ttu-id="564a3-134">Aby uzyskać więcej informacji o chmurze platformy Azure dla instytucji rządowych, zobacz [Microsoft Azure dla instytucji rządowych](https://azure.microsoft.com/features/gov/) i [Podręczniku dewelopera programu Microsoft Azure dla instytucji rządowych](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="564a3-134">For more information about the Azure Government Cloud, see [Microsoft Azure Government](https://azure.microsoft.com/features/gov/) and [Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>

### <a name="to-connect-to-the-azure-china-cloud"></a><span data-ttu-id="564a3-135">Do nawiązania połączenia chmury Azure w Chinach</span><span class="sxs-lookup"><span data-stu-id="564a3-135">To connect to the Azure China Cloud</span></span>
<span data-ttu-id="564a3-136">Aby połączyć się z chmury Azure w Chinach, użyj jednej z następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="564a3-136">To connect to the Azure China Cloud, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureChinaCloud

<span data-ttu-id="564a3-137">lub</span><span class="sxs-lookup"><span data-stu-id="564a3-137">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureChinaCloud)

<span data-ttu-id="564a3-138">Aby utworzyć pamięć podręczną w chmurze platformy Azure w Chinach, użyj jednej z następujących lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="564a3-138">To create a cache in the Azure China Cloud, use one of the following locations.</span></span>

* <span data-ttu-id="564a3-139">Chiny Wschodnie</span><span class="sxs-lookup"><span data-stu-id="564a3-139">China East</span></span>
* <span data-ttu-id="564a3-140">Chiny Północne</span><span class="sxs-lookup"><span data-stu-id="564a3-140">China North</span></span>

<span data-ttu-id="564a3-141">Aby uzyskać więcej informacji o chmurze Chin platformy Azure, zobacz [AzureChinaCloud dla platformy Azure obsługiwane przez 21Vianet w Chinach](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="564a3-141">For more information about the Azure China Cloud, see [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span>

### <a name="to-connect-to-microsoft-azure-germany"></a><span data-ttu-id="564a3-142">Do nawiązania połączenia platformy Azure w Niemczech firmy Microsoft</span><span class="sxs-lookup"><span data-stu-id="564a3-142">To connect to Microsoft Azure Germany</span></span>
<span data-ttu-id="564a3-143">Aby połączyć się Microsoft platformy Azure w Niemczech, użyj jednej z następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="564a3-143">To connect to Microsoft Azure Germany, use one of the following commands.</span></span>

    Add-AzureRMAccount -EnvironmentName AzureGermanCloud


<span data-ttu-id="564a3-144">lub</span><span class="sxs-lookup"><span data-stu-id="564a3-144">or</span></span>

    Add-AzureRmAccount -Environment (Get-AzureRmEnvironment -Name AzureGermanCloud)

<span data-ttu-id="564a3-145">Aby utworzyć pamięć podręczną w Microsoft Azure Niemczech, użyj jednej z następujących lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="564a3-145">To create a cache in Microsoft Azure Germany, use one of the following locations.</span></span>

* <span data-ttu-id="564a3-146">Niemcy Środkowe</span><span class="sxs-lookup"><span data-stu-id="564a3-146">Germany Central</span></span>
* <span data-ttu-id="564a3-147">Niemcy Północno-Wschodnie</span><span class="sxs-lookup"><span data-stu-id="564a3-147">Germany Northeast</span></span>

<span data-ttu-id="564a3-148">Aby uzyskać więcej informacji o Microsoft platformy Azure w Niemczech, zobacz [Microsoft Azure Niemcy](https://azure.microsoft.com/overview/clouds/germany/).</span><span class="sxs-lookup"><span data-stu-id="564a3-148">For more information about Microsoft Azure Germany, see [Microsoft Azure Germany](https://azure.microsoft.com/overview/clouds/germany/).</span></span>

### <a name="properties-used-for-azure-redis-cache-powershell"></a><span data-ttu-id="564a3-149">Właściwości używanej do pamięci podręcznej Redis Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="564a3-149">Properties used for Azure Redis Cache PowerShell</span></span>
<span data-ttu-id="564a3-150">Poniższa tabela zawiera właściwości i opisy parametrów często używane podczas tworzenia i zarządzania nimi z wystąpień pamięci podręcznej Redis Azure za pomocą programu Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="564a3-150">The following table contains properties and descriptions for commonly used parameters when creating and managing your Azure Redis Cache instances using Azure PowerShell.</span></span>

| <span data-ttu-id="564a3-151">Parametr</span><span class="sxs-lookup"><span data-stu-id="564a3-151">Parameter</span></span> | <span data-ttu-id="564a3-152">Opis</span><span class="sxs-lookup"><span data-stu-id="564a3-152">Description</span></span> | <span data-ttu-id="564a3-153">Domyślne</span><span class="sxs-lookup"><span data-stu-id="564a3-153">Default</span></span> |
| --- | --- | --- |
| <span data-ttu-id="564a3-154">Nazwa</span><span class="sxs-lookup"><span data-stu-id="564a3-154">Name</span></span> |<span data-ttu-id="564a3-155">Nazwa pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="564a3-155">Name of the cache</span></span> | |
| <span data-ttu-id="564a3-156">Lokalizacja</span><span class="sxs-lookup"><span data-stu-id="564a3-156">Location</span></span> |<span data-ttu-id="564a3-157">Lokalizacja pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="564a3-157">Location of the cache</span></span> | |
| <span data-ttu-id="564a3-158">Grupy zasobów o nazwie</span><span class="sxs-lookup"><span data-stu-id="564a3-158">ResourceGroupName</span></span> |<span data-ttu-id="564a3-159">Nazwa grupy zasobów, w której chcesz utworzyć pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="564a3-159">Resource group name in which to create the cache</span></span> | |
| <span data-ttu-id="564a3-160">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="564a3-160">Size</span></span> |<span data-ttu-id="564a3-161">Rozmiar pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-161">The size of the cache.</span></span> <span data-ttu-id="564a3-162">Prawidłowe wartości to: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2,5 GB, 6 GB, 13 GB, 26 GB, 53 GB</span><span class="sxs-lookup"><span data-stu-id="564a3-162">Valid values are: P1, P2, P3, P4, C0, C1, C2, C3, C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB</span></span> |<span data-ttu-id="564a3-163">1 GB</span><span class="sxs-lookup"><span data-stu-id="564a3-163">1GB</span></span> |
| <span data-ttu-id="564a3-164">ShardCount</span><span class="sxs-lookup"><span data-stu-id="564a3-164">ShardCount</span></span> |<span data-ttu-id="564a3-165">Liczba fragmentów, aby utworzyć podczas tworzenia usługi pamięć podręczna premium z włączoną funkcją klastrowania.</span><span class="sxs-lookup"><span data-stu-id="564a3-165">The number of shards to create when creating a premium cache with clustering enabled.</span></span> <span data-ttu-id="564a3-166">Prawidłowe wartości to: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span><span class="sxs-lookup"><span data-stu-id="564a3-166">Valid values are: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10</span></span> | |
| <span data-ttu-id="564a3-167">SKU</span><span class="sxs-lookup"><span data-stu-id="564a3-167">SKU</span></span> |<span data-ttu-id="564a3-168">Określa numer pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-168">Specifies the SKU of the cache.</span></span> <span data-ttu-id="564a3-169">Prawidłowe wartości to: Basic, Standard, Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-169">Valid values are: Basic, Standard, Premium</span></span> |<span data-ttu-id="564a3-170">Standardowa</span><span class="sxs-lookup"><span data-stu-id="564a3-170">Standard</span></span> |
| <span data-ttu-id="564a3-171">RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="564a3-171">RedisConfiguration</span></span> |<span data-ttu-id="564a3-172">Określa ustawienia konfiguracji pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="564a3-172">Specifies Redis configuration settings.</span></span> <span data-ttu-id="564a3-173">Aby uzyskać szczegółowe informacje o każdym ustawieniu, zobacz następujące tematy [RedisConfiguration właściwości](#redisconfiguration-properties) tabeli.</span><span class="sxs-lookup"><span data-stu-id="564a3-173">For details on each setting, see the following [RedisConfiguration properties](#redisconfiguration-properties) table.</span></span> | |
| <span data-ttu-id="564a3-174">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="564a3-174">EnableNonSslPort</span></span> |<span data-ttu-id="564a3-175">Wskazuje, czy włączono port bez protokołu SSL.</span><span class="sxs-lookup"><span data-stu-id="564a3-175">Indicates whether the non-SSL port is enabled.</span></span> |<span data-ttu-id="564a3-176">False</span><span class="sxs-lookup"><span data-stu-id="564a3-176">False</span></span> |
| <span data-ttu-id="564a3-177">MaxMemoryPolicy</span><span class="sxs-lookup"><span data-stu-id="564a3-177">MaxMemoryPolicy</span></span> |<span data-ttu-id="564a3-178">Ten parametr jest przestarzały — zamiast tego użyj RedisConfiguration.</span><span class="sxs-lookup"><span data-stu-id="564a3-178">This parameter has been deprecated - use RedisConfiguration instead.</span></span> | |
| <span data-ttu-id="564a3-179">StaticIP</span><span class="sxs-lookup"><span data-stu-id="564a3-179">StaticIP</span></span> |<span data-ttu-id="564a3-180">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa unikatowy adres IP w podsieci dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-180">When hosting your cache in a VNET, specifies a unique IP address in the subnet for the cache.</span></span> <span data-ttu-id="564a3-181">Jeśli nie zostanie podana, co zostanie wybrany dla Ciebie podsieci.</span><span class="sxs-lookup"><span data-stu-id="564a3-181">If not provided, one is chosen for you from the subnet.</span></span> | |
| <span data-ttu-id="564a3-182">Podsieć</span><span class="sxs-lookup"><span data-stu-id="564a3-182">Subnet</span></span> |<span data-ttu-id="564a3-183">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa nazwę podsieci, w której chcesz wdrożyć w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-183">When hosting your cache in a VNET, specifies the name of the subnet in which to deploy the cache.</span></span> | |
| <span data-ttu-id="564a3-184">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="564a3-184">VirtualNetwork</span></span> |<span data-ttu-id="564a3-185">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa identyfikator zasobu sieci wirtualnej, w której chcesz wdrożyć w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-185">When hosting your cache in a VNET, specifies the resource ID of the VNET in which to deploy the cache.</span></span> | |
| <span data-ttu-id="564a3-186">Właściwość KeyType</span><span class="sxs-lookup"><span data-stu-id="564a3-186">KeyType</span></span> |<span data-ttu-id="564a3-187">Określa klucz, do którego dostęp można ponownie wygenerować podczas odnawiania klucze dostępu.</span><span class="sxs-lookup"><span data-stu-id="564a3-187">Specifies which access key to regenerate when renewing access keys.</span></span> <span data-ttu-id="564a3-188">Prawidłowe wartości to: podstawowej, dodatkowej</span><span class="sxs-lookup"><span data-stu-id="564a3-188">Valid values are: Primary, Secondary</span></span> | |

### <a name="redisconfiguration-properties"></a><span data-ttu-id="564a3-189">Właściwości RedisConfiguration</span><span class="sxs-lookup"><span data-stu-id="564a3-189">RedisConfiguration properties</span></span>
| <span data-ttu-id="564a3-190">Właściwość</span><span class="sxs-lookup"><span data-stu-id="564a3-190">Property</span></span> | <span data-ttu-id="564a3-191">Opis</span><span class="sxs-lookup"><span data-stu-id="564a3-191">Description</span></span> | <span data-ttu-id="564a3-192">Warstwy cenowe</span><span class="sxs-lookup"><span data-stu-id="564a3-192">Pricing tiers</span></span> |
| --- | --- | --- |
| <span data-ttu-id="564a3-193">włączone kopii zapasowej RDB</span><span class="sxs-lookup"><span data-stu-id="564a3-193">rdb-backup-enabled</span></span> |<span data-ttu-id="564a3-194">Czy [trwałość danych Redis](cache-how-to-premium-persistence.md) jest włączone</span><span class="sxs-lookup"><span data-stu-id="564a3-194">Whether [Redis data persistence](cache-how-to-premium-persistence.md) is enabled</span></span> |<span data-ttu-id="564a3-195">Tylko w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-195">Premium only</span></span> |
| <span data-ttu-id="564a3-196">RDB magazynu-— parametry połączenia</span><span class="sxs-lookup"><span data-stu-id="564a3-196">rdb-storage-connection-string</span></span> |<span data-ttu-id="564a3-197">Parametry połączenia z kontem magazynu dla [trwałość danych Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="564a3-197">The connection string to the storage account for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="564a3-198">Tylko w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-198">Premium only</span></span> |
| <span data-ttu-id="564a3-199">częstotliwość w przypadku wykonywania kopii zapasowych RDB</span><span class="sxs-lookup"><span data-stu-id="564a3-199">rdb-backup-frequency</span></span> |<span data-ttu-id="564a3-200">Częstotliwość wykonywania kopii zapasowych dla [trwałość danych Redis](cache-how-to-premium-persistence.md)</span><span class="sxs-lookup"><span data-stu-id="564a3-200">The backup frequency for [Redis data persistence](cache-how-to-premium-persistence.md)</span></span> |<span data-ttu-id="564a3-201">Tylko w warstwie Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-201">Premium only</span></span> |
| <span data-ttu-id="564a3-202">zastrzeżone maxmemory</span><span class="sxs-lookup"><span data-stu-id="564a3-202">maxmemory-reserved</span></span> |<span data-ttu-id="564a3-203">Konfiguruje [pamięci zarezerwowanej](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) -cache procesów</span><span class="sxs-lookup"><span data-stu-id="564a3-203">Configures the [memory reserved](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for non-cache processes</span></span> |<span data-ttu-id="564a3-204">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-204">Standard and Premium</span></span> |
| <span data-ttu-id="564a3-205">maxmemory-policy.</span><span class="sxs-lookup"><span data-stu-id="564a3-205">maxmemory-policy</span></span> |<span data-ttu-id="564a3-206">Konfiguruje [zasad eksmisji](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) dla pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="564a3-206">Configures the [eviction policy](cache-configure.md#maxmemory-policy-and-maxmemory-reserved) for the cache</span></span> |<span data-ttu-id="564a3-207">Wszystkie warstwy cenowe</span><span class="sxs-lookup"><span data-stu-id="564a3-207">All pricing tiers</span></span> |
| <span data-ttu-id="564a3-208">powiadomienia przestrzeni kluczy zdarzenia</span><span class="sxs-lookup"><span data-stu-id="564a3-208">notify-keyspace-events</span></span> |<span data-ttu-id="564a3-209">Konfiguruje [powiadomienia przestrzeni kluczy](cache-configure.md#keyspace-notifications-advanced-settings)</span><span class="sxs-lookup"><span data-stu-id="564a3-209">Configures [keyspace notifications](cache-configure.md#keyspace-notifications-advanced-settings)</span></span> |<span data-ttu-id="564a3-210">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-210">Standard and Premium</span></span> |
| <span data-ttu-id="564a3-211">Skrót max-ziplist — wpisów</span><span class="sxs-lookup"><span data-stu-id="564a3-211">hash-max-ziplist-entries</span></span> |<span data-ttu-id="564a3-212">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="564a3-212">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="564a3-213">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-213">Standard and Premium</span></span> |
| <span data-ttu-id="564a3-214">max-ziplist — wartość skrótu</span><span class="sxs-lookup"><span data-stu-id="564a3-214">hash-max-ziplist-value</span></span> |<span data-ttu-id="564a3-215">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="564a3-215">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="564a3-216">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-216">Standard and Premium</span></span> |
| <span data-ttu-id="564a3-217">zestaw max-intset wpisów</span><span class="sxs-lookup"><span data-stu-id="564a3-217">set-max-intset-entries</span></span> |<span data-ttu-id="564a3-218">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="564a3-218">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="564a3-219">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-219">Standard and Premium</span></span> |
| <span data-ttu-id="564a3-220">zset-max-ziplist wpisów</span><span class="sxs-lookup"><span data-stu-id="564a3-220">zset-max-ziplist-entries</span></span> |<span data-ttu-id="564a3-221">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="564a3-221">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="564a3-222">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-222">Standard and Premium</span></span> |
| <span data-ttu-id="564a3-223">zset-max-ziplist-value</span><span class="sxs-lookup"><span data-stu-id="564a3-223">zset-max-ziplist-value</span></span> |<span data-ttu-id="564a3-224">Konfiguruje [optymalizacji pamięci](http://redis.io/topics/memory-optimization) dla typów małych agregowanie danych</span><span class="sxs-lookup"><span data-stu-id="564a3-224">Configures [memory optimization](http://redis.io/topics/memory-optimization) for small aggregate data types</span></span> |<span data-ttu-id="564a3-225">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-225">Standard and Premium</span></span> |
| <span data-ttu-id="564a3-226">bazy danych</span><span class="sxs-lookup"><span data-stu-id="564a3-226">databases</span></span> |<span data-ttu-id="564a3-227">Konfiguruje liczbę baz danych.</span><span class="sxs-lookup"><span data-stu-id="564a3-227">Configures the number of databases.</span></span> <span data-ttu-id="564a3-228">Tej właściwości można skonfigurować tylko na tworzenie pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-228">This property can be configured only at cache creation.</span></span> |<span data-ttu-id="564a3-229">Standardowa i Premium</span><span class="sxs-lookup"><span data-stu-id="564a3-229">Standard and Premium</span></span> |

## <a name="to-create-a-redis-cache"></a><span data-ttu-id="564a3-230">Aby utworzyć pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-230">To create a Redis Cache</span></span>
<span data-ttu-id="564a3-231">Nowe wystąpienia pamięci podręcznej Redis Azure są tworzone przy użyciu [AzureRmRedisCache nowy](https://msdn.microsoft.com/library/azure/mt634517.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-231">New Azure Redis Cache instances are created using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="564a3-232">Tworzenie pamięci podręcznej Redis w ramach subskrypcji przy użyciu portalu Azure po raz pierwszy portalu rejestruje `Microsoft.Cache` przestrzeni nazw dla tej subskrypcji.</span><span class="sxs-lookup"><span data-stu-id="564a3-232">The first time you create a Redis cache in a subscription using the Azure portal, the portal registers the `Microsoft.Cache` namespace for that subscription.</span></span> <span data-ttu-id="564a3-233">Przy próbie utworzenia pierwszej pamięci podręcznej Redis w ramach subskrypcji przy użyciu programu PowerShell, najpierw należy zarejestrować tej przestrzeni nazw przy użyciu następującego polecenia; w przeciwnym razie poleceń cmdlet, takich jak `New-AzureRmRedisCache` i `Get-AzureRmRedisCache` się nie powieść.</span><span class="sxs-lookup"><span data-stu-id="564a3-233">If you attempt to create the first Redis cache in a subscription using PowerShell, you must first register that namespace using the following command; otherwise cmdlets such as `New-AzureRmRedisCache` and `Get-AzureRmRedisCache` fail.</span></span>
> 
> `Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.Cache"`
> 
> 

<span data-ttu-id="564a3-234">Aby wyświetlić listę dostępnych parametrów i ich opisy `New-AzureRmRedisCache`, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-234">To see a list of available parameters and their descriptions for `New-AzureRmRedisCache`, run the following command.</span></span>

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
        The New-AzureRmRedisCache cmdlet creates a new redis cache.


    PARAMETERS
        -Name <String>
            Name of the redis cache to create.

        -ResourceGroupName <String>
            Name of resource group in which to create the redis cache.

        -Location <String>
            Location in which to create the redis cache.

        -RedisVersion <String>
            RedisVersion is deprecated and will be removed in future release.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value, databases.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. If no value is provided, the default value is false and the
            non-SSL port will be disabled. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        -VirtualNetwork <String>
            The exact ARM resource ID of the virtual network to deploy the redis cache in. Example format: /subscriptions/{
            subid}/resourceGroups/{resourceGroupName}/providers/Microsoft.ClassicNetwork/VirtualNetworks/{vnetName}

        -Subnet <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        -StaticIP <String>
            Required when deploying a redis cache inside an existing Azure Virtual Network.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="564a3-235">Aby utworzyć pamięć podręczną z domyślnych parametrów, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-235">To create a cache with default parameters, run the following command.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US"

<span data-ttu-id="564a3-236">`ResourceGroupName`, `Name`, i `Location` są wymagane parametry, ale pozostałe są opcjonalne i mają przypisane wartości domyślne.</span><span class="sxs-lookup"><span data-stu-id="564a3-236">`ResourceGroupName`, `Name`, and `Location` are required parameters, but the rest are optional and have default values.</span></span> <span data-ttu-id="564a3-237">Poprzednie polecenia tworzy wystąpienie standardowy SKU pamięć podręczna Redis Azure z określoną nazwą, lokalizacji i grupy zasobów o rozmiarze z portu bez protokołu SSL, wyłączona 1 GB.</span><span class="sxs-lookup"><span data-stu-id="564a3-237">Running the previous command creates a Standard SKU Azure Redis Cache instance with the specified name, location, and resource group, that is 1 GB in size with the non-SSL port disabled.</span></span>

<span data-ttu-id="564a3-238">Aby utworzyć pamięć podręczną premium, określ rozmiar P1 (6 GB — 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), lub P4 (53 GB - 530 GB).</span><span class="sxs-lookup"><span data-stu-id="564a3-238">To create a premium cache, specify a size of P1 (6 GB - 60 GB), P2 (13 GB - 130 GB), P3 (26 GB - 260 GB), or P4 (53 GB - 530 GB).</span></span> <span data-ttu-id="564a3-239">Aby włączyć klastra, określ liczby niezależnych za pomocą `ShardCount` parametru.</span><span class="sxs-lookup"><span data-stu-id="564a3-239">To enable clustering, specify a shard count using the `ShardCount` parameter.</span></span> <span data-ttu-id="564a3-240">Poniższy przykład tworzy pamięć podręczna premium P1 z odłamków 3.</span><span class="sxs-lookup"><span data-stu-id="564a3-240">The following example creates a P1 premium cache with 3 shards.</span></span> <span data-ttu-id="564a3-241">Pamięć podręczna premium P1 w rozmiar 6 GB, a ponieważ firma Microsoft określone trzy odłamków całkowity rozmiar jest 18 GB (3 x 6 GB).</span><span class="sxs-lookup"><span data-stu-id="564a3-241">A P1 premium cache is 6 GB in size, and since we specified three shards the total size is 18 GB (3 x 6 GB).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P1 -ShardCount 3

<span data-ttu-id="564a3-242">Aby określić wartości dla `RedisConfiguration` parametru, ujmij wartości wewnątrz `{}` jako klucza i wartości, takich jak pary `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span><span class="sxs-lookup"><span data-stu-id="564a3-242">To specify values for the `RedisConfiguration` parameter, enclose the values inside `{}` as key/value pairs like `@{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}`.</span></span> <span data-ttu-id="564a3-243">Poniższy przykład tworzy standardowe 1 GB pamięci podręcznej z `allkeys-random` maxmemory zasad i przestrzeni kluczy powiadomienia skonfigurowane z `KEA`.</span><span class="sxs-lookup"><span data-stu-id="564a3-243">The following example creates a standard 1 GB cache with `allkeys-random` maxmemory policy and keyspace notifications configured with `KEA`.</span></span> <span data-ttu-id="564a3-244">Aby uzyskać więcej informacji, zobacz [powiadomienia przestrzeni kluczy (Zaawansowane ustawienia)](cache-configure.md#keyspace-notifications-advanced-settings) i [zasady pamięci](cache-configure.md#memory-policies).</span><span class="sxs-lookup"><span data-stu-id="564a3-244">For more information, see [Keyspace notifications (advanced settings)](cache-configure.md#keyspace-notifications-advanced-settings) and [Memory policies](cache-configure.md#memory-policies).</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random", "notify-keyspace-events" = "KEA"}

<a name="databases"></a>

## <a name="to-configure-the-databases-setting-during-cache-creation"></a><span data-ttu-id="564a3-245">Aby skonfigurować ustawienie podczas tworzenia pamięci podręcznej bazy danych</span><span class="sxs-lookup"><span data-stu-id="564a3-245">To configure the databases setting during cache creation</span></span>
<span data-ttu-id="564a3-246">`databases` Ustawienie można skonfigurować tylko podczas tworzenia pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-246">The `databases` setting can be configured only during cache creation.</span></span> <span data-ttu-id="564a3-247">Poniższy przykład tworzy — warstwa premium P3 (26 GB) pamięci podręcznej z 48 baz danych przy użyciu [AzureRmRedisCache nowy](https://msdn.microsoft.com/library/azure/mt634517.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-247">The following example creates a premium P3 (26 GB) cache with 48 databases using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet.</span></span>

    New-AzureRmRedisCache -ResourceGroupName myGroup -Name mycache -Location "North Central US" -Sku Premium -Size P3 -RedisConfiguration @{"databases" = "48"}

<span data-ttu-id="564a3-248">Aby uzyskać więcej informacji na temat `databases` właściwości, zobacz [konfiguracji serwera domyślna pamięci podręcznej Redis Azure](cache-configure.md#default-redis-server-configuration).</span><span class="sxs-lookup"><span data-stu-id="564a3-248">For more information on the `databases` property, see [Default Azure Redis Cache server configuration](cache-configure.md#default-redis-server-configuration).</span></span> <span data-ttu-id="564a3-249">Aby uzyskać więcej informacji na temat tworzenia pamięci podręcznej z użyciem [AzureRmRedisCache nowy](https://msdn.microsoft.com/library/azure/mt634517.aspx) polecenia cmdlet, zobacz poprzedni [do utworzenia pamięci podręcznej Redis](#to-create-a-redis-cache) sekcji.</span><span class="sxs-lookup"><span data-stu-id="564a3-249">For more information on creating a cache using the [New-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634517.aspx) cmdlet, see the previous [To create a Redis Cache](#to-create-a-redis-cache) section.</span></span>

## <a name="to-update-a-redis-cache"></a><span data-ttu-id="564a3-250">Aby zaktualizować pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-250">To update a Redis cache</span></span>
<span data-ttu-id="564a3-251">Wystąpienia pamięci podręcznej Redis Azure są aktualizowane przy użyciu [AzureRmRedisCache zestaw](https://msdn.microsoft.com/library/azure/mt634518.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-251">Azure Redis Cache instances are updated using the [Set-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634518.aspx) cmdlet.</span></span>

<span data-ttu-id="564a3-252">Aby wyświetlić listę dostępnych parametrów i ich opisy `Set-AzureRmRedisCache`, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-252">To see a list of available parameters and their descriptions for `Set-AzureRmRedisCache`, run the following command.</span></span>

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
        The Set-AzureRmRedisCache cmdlet sets redis cache parameters.

    PARAMETERS
        -Name <String>
            Name of the redis cache to update.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -Size <String>
            Size of the redis cache. The default value is 1GB or C1. Possible values are P1, P2, P3, P4, C0, C1, C2, C3,
            C4, C5, C6, 250MB, 1GB, 2.5GB, 6GB, 13GB, 26GB, 53GB.

        -Sku <String>
            Sku of redis cache. The default value is Standard. Possible values are Basic, Standard and Premium.

        -MaxMemoryPolicy <String>
            The 'MaxMemoryPolicy' setting has been deprecated. Please use 'RedisConfiguration' setting to set
            MaxMemoryPolicy. e.g. -RedisConfiguration @{"maxmemory-policy" = "allkeys-lru"}

        -RedisConfiguration <Hashtable>
            All Redis Configuration Settings. Few possible keys: rdb-backup-enabled, rdb-storage-connection-string,
            rdb-backup-frequency, maxmemory-reserved, maxmemory-policy, notify-keyspace-events, hash-max-ziplist-entries,
            hash-max-ziplist-value, set-max-intset-entries, zset-max-ziplist-entries, zset-max-ziplist-value.

        -EnableNonSslPort <Boolean>
            EnableNonSslPort is used by Azure Redis Cache. The default value is null and no change will be made to the
            currently configured value. Possible values are true and false.

        -ShardCount <Integer>
            The number of shards to create on a Premium Cluster Cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="564a3-253">`Set-AzureRmRedisCache` Polecenia cmdlet można używać do aktualizowania właściwości, takie jak `Size`, `Sku`, `EnableNonSslPort`i `RedisConfiguration` wartości.</span><span class="sxs-lookup"><span data-stu-id="564a3-253">The `Set-AzureRmRedisCache` cmdlet can be used to update properties such as `Size`, `Sku`, `EnableNonSslPort`, and the `RedisConfiguration` values.</span></span> 

<span data-ttu-id="564a3-254">Polecenie aktualizacji pamięci podręcznej Redis, o nazwie myCache maxmemory-policy.</span><span class="sxs-lookup"><span data-stu-id="564a3-254">The following command updates the maxmemory-policy for the Redis Cache named myCache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName "myGroup" -Name "myCache" -RedisConfiguration @{"maxmemory-policy" = "allkeys-random"}

<a name="scale"></a>

## <a name="to-scale-a-redis-cache"></a><span data-ttu-id="564a3-255">Aby skalować pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-255">To scale a Redis cache</span></span>
<span data-ttu-id="564a3-256">`Set-AzureRmRedisCache`może służyć do skalowania pamięci podręcznej Azure Redis wystąpienia, kiedy `Size`, `Sku`, lub `ShardCount` są modyfikowane właściwości.</span><span class="sxs-lookup"><span data-stu-id="564a3-256">`Set-AzureRmRedisCache` can be used to scale an Azure Redis cache instance when the `Size`, `Sku`, or `ShardCount` properties are modified.</span></span> 

> [!NOTE]
> <span data-ttu-id="564a3-257">Skalowanie pamięci podręcznej przy użyciu programu PowerShell podlega tego samego ograniczenia i wytyczne jako skalowanie pamięci podręcznej z portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="564a3-257">Scaling a cache using PowerShell is subject to the same limits and guidelines as scaling a cache from the Azure portal.</span></span> <span data-ttu-id="564a3-258">Można skalować do innej warstwy cenowej z następującymi ograniczeniami.</span><span class="sxs-lookup"><span data-stu-id="564a3-258">You can scale to a different pricing tier with the following restrictions.</span></span>
> 
> * <span data-ttu-id="564a3-259">Nie można skalować z wyższej warstwy cenowej do dolnej warstwy cenowej.</span><span class="sxs-lookup"><span data-stu-id="564a3-259">You can't scale from a higher pricing tier to a lower pricing tier.</span></span>
> * <span data-ttu-id="564a3-260">Nie można skalować z **Premium** pamięci podręcznej w dół do **standardowe** lub **podstawowe** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-260">You can't scale from a **Premium** cache down to a **Standard** or a **Basic** cache.</span></span>
> * <span data-ttu-id="564a3-261">Nie można skalować z **standardowe** pamięci podręcznej w dół do **podstawowe** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-261">You can't scale from a **Standard** cache down to a **Basic** cache.</span></span>
> * <span data-ttu-id="564a3-262">Możesz skalować z **podstawowe** pamięci podręcznej do **standardowe** pamięci podręcznej, ale nie można zmienić rozmiar w tym samym czasie.</span><span class="sxs-lookup"><span data-stu-id="564a3-262">You can scale from a **Basic** cache to a **Standard** cache but you can't change the size at the same time.</span></span> <span data-ttu-id="564a3-263">Jeśli potrzebujesz zmienić rozmiar, należy na żądany rozmiar kolejnych operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="564a3-263">If you need a different size, you can do a subsequent scaling operation to the desired size.</span></span>
> * <span data-ttu-id="564a3-264">Nie można skalować z **podstawowe** bezpośrednio do pamięci podręcznej **Premium** pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-264">You can't scale from a **Basic** cache directly to a **Premium** cache.</span></span> <span data-ttu-id="564a3-265">Należy skalować z **podstawowe** do **standardowe** w jednej operacji skalowania, a następnie z **standardowe** do **Premium** w kolejnych operacji skalowania.</span><span class="sxs-lookup"><span data-stu-id="564a3-265">You must scale from **Basic** to **Standard** in one scaling operation, and then from **Standard** to **Premium** in a subsequent scaling operation.</span></span>
> * <span data-ttu-id="564a3-266">Nie można skalować z większego rozmiaru w dół do **C0 (250 MB)** rozmiar.</span><span class="sxs-lookup"><span data-stu-id="564a3-266">You can't scale from a larger size down to the **C0 (250 MB)** size.</span></span>
> 
> <span data-ttu-id="564a3-267">Aby uzyskać więcej informacji, zobacz [jak pamięć podręczna Redis Azure skali](cache-how-to-scale.md).</span><span class="sxs-lookup"><span data-stu-id="564a3-267">For more information, see [How to Scale Azure Redis Cache](cache-how-to-scale.md).</span></span>
> 
> 

<span data-ttu-id="564a3-268">Poniższy przykład przedstawia sposób skalowania pamięci podręcznej o nazwie `myCache` do 2,5 GB pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-268">The following example shows how to scale a cache named `myCache` to a 2.5 GB cache.</span></span> <span data-ttu-id="564a3-269">Należy pamiętać, że to polecenie działa zarówno Basic lub Standard pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-269">Note that this command works for both a Basic or a Standard cache.</span></span>

    Set-AzureRmRedisCache -ResourceGroupName myGroup -Name myCache -Size 2.5GB

<span data-ttu-id="564a3-270">Po uruchomieniu tego polecenia, zwracany jest stan pamięci podręcznej (podobny do wywoływania `Get-AzureRmRedisCache`).</span><span class="sxs-lookup"><span data-stu-id="564a3-270">After this command is issued, the status of the cache is returned (similar to calling `Get-AzureRmRedisCache`).</span></span> <span data-ttu-id="564a3-271">Należy pamiętać, że `ProvisioningState` jest `Scaling`.</span><span class="sxs-lookup"><span data-stu-id="564a3-271">Note that the `ProvisioningState` is `Scaling`.</span></span>

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

<span data-ttu-id="564a3-272">Po zakończeniu operacji skalowania, `ProvisioningState` zmienia się na `Succeeded`.</span><span class="sxs-lookup"><span data-stu-id="564a3-272">When the scaling operation is complete, the `ProvisioningState` changes to `Succeeded`.</span></span> <span data-ttu-id="564a3-273">Jeśli konieczne jest wprowadzenie kolejnych operacji skalowania, takich jak zmiana z podstawowego na standardowy, a następnie zmienić rozmiar, należy zaczekać, aż poprzednia operacja została ukończona lub komunikat o błędzie podobny do następującego.</span><span class="sxs-lookup"><span data-stu-id="564a3-273">If you need to make a subsequent scaling operation, such as changing from Basic to Standard and then changing the size, you must wait until the previous operation is complete or you receive an error similar to the following.</span></span>

    Set-AzureRmRedisCache : Conflict: The resource '...' is not in a stable state, and is currently unable to accept the update request.

## <a name="to-get-information-about-a-redis-cache"></a><span data-ttu-id="564a3-274">Aby uzyskać informacje o pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-274">To get information about a Redis cache</span></span>
<span data-ttu-id="564a3-275">Można pobrać informacji o pamięci podręcznej z użyciem [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-275">You can retrieve information about a cache using the [Get-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634514.aspx) cmdlet.</span></span>

<span data-ttu-id="564a3-276">Aby wyświetlić listę dostępnych parametrów i ich opisy `Get-AzureRmRedisCache`, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-276">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCache -detailed

    NAME
        Get-AzureRmRedisCache

    SYNOPSIS
        Gets details about a single cache or all caches in the specified resource group or all caches in the current
        subscription.

    SYNTAX
        Get-AzureRmRedisCache [-Name <String>] [-ResourceGroupName <String>] [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCache cmdlet gets the details about a cache or caches depending on input parameters. If both
        ResourceGroupName and Name parameters are provided then Get-AzureRmRedisCache will return details about the
        specific cache name provided.

        If only ResourceGroupName is provided than it will return details about all caches in the specified resource group.

        If no parameters are given than it will return details about all caches the current subscription.

    PARAMETERS
        -Name <String>
            The name of the cache. When this parameter is provided along with ResourceGroupName, Get-AzureRmRedisCache
            returns the details for the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache or caches. If ResourceGroupName is provided with Name
            then Get-AzureRmRedisCache returns the details of the cache specified by Name. If only the ResourceGroup
            parameter is provided, then details for all caches in the resource group are returned.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="564a3-277">Zwraca informacje dotyczące wszystkich usług pamięć podręczna w bieżącej subskrypcji, uruchom `Get-AzureRmRedisCache` bez żadnych parametrów.</span><span class="sxs-lookup"><span data-stu-id="564a3-277">To return information about all caches in the current subscription, run `Get-AzureRmRedisCache` without any parameters.</span></span>

    Get-AzureRmRedisCache

<span data-ttu-id="564a3-278">Zwraca informacje dotyczące wszystkich usług pamięć podręczna w określonej grupy zasobów, uruchom `Get-AzureRmRedisCache` z `ResourceGroupName` parametru.</span><span class="sxs-lookup"><span data-stu-id="564a3-278">To return information about all caches in a specific resource group, run `Get-AzureRmRedisCache` with the `ResourceGroupName` parameter.</span></span>

    Get-AzureRmRedisCache -ResourceGroupName myGroup

<span data-ttu-id="564a3-279">Zwraca informacje dotyczące określonego pamięci podręcznej, uruchom `Get-AzureRmRedisCache` z `Name` parametr zawierający nazwę pamięci podręcznej i `ResourceGroupName` parametru z grupą zasobów, zawierającą tej pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-279">To return information about a specific cache, run `Get-AzureRmRedisCache` with the `Name` parameter containing the name of the cache, and the `ResourceGroupName` parameter with the resource group containing that cache.</span></span>

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

## <a name="to-retrieve-the-access-keys-for-a-redis-cache"></a><span data-ttu-id="564a3-280">Aby pobrać klucze dostępu pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-280">To retrieve the access keys for a Redis cache</span></span>
<span data-ttu-id="564a3-281">Aby pobrać klucze dostępu pamięci podręcznej, można użyć [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-281">To retrieve the access keys for your cache, you can use the [Get-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634516.aspx) cmdlet.</span></span>

<span data-ttu-id="564a3-282">Aby wyświetlić listę dostępnych parametrów i ich opisy `Get-AzureRmRedisCacheKey`, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-282">To see a list of available parameters and their descriptions for `Get-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help Get-AzureRmRedisCacheKey -detailed

    NAME
        Get-AzureRmRedisCacheKey

    SYNOPSIS
        Gets the accesskeys for the specified redis cache.


    SYNTAX
        Get-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> [<CommonParameters>]

    DESCRIPTION
        The Get-AzureRmRedisCacheKey cmdlet gets the access keys for the specified cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="564a3-283">Aby uzyskać dostęp do kluczy dla pamięci podręcznej, należy wywołać `Get-AzureRmRedisCacheKey` polecenia cmdlet i przekaż nazwę pamięci podręcznej Nazwa grupy zasobów, która zawiera pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-283">To retrieve the keys for your cache, call the `Get-AzureRmRedisCacheKey` cmdlet and pass in the name of your cache the name of the resource group that contains the cache.</span></span>

    PS C:\> Get-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup

    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : ABhfB757JgjIgt785JgKH9865eifmekfnn649303JKL=

## <a name="to-regenerate-access-keys-for-your-redis-cache"></a><span data-ttu-id="564a3-284">Można ponownie wygenerować klucze dostępu pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-284">To regenerate access keys for your Redis cache</span></span>
<span data-ttu-id="564a3-285">Aby ponownie wygenerować klucze dostępu pamięci podręcznej, można użyć [AzureRmRedisCacheKey nowy](https://msdn.microsoft.com/library/azure/mt634512.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-285">To regenerate the access keys for your cache, you can use the [New-AzureRmRedisCacheKey](https://msdn.microsoft.com/library/azure/mt634512.aspx) cmdlet.</span></span>

<span data-ttu-id="564a3-286">Aby wyświetlić listę dostępnych parametrów i ich opisy `New-AzureRmRedisCacheKey`, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-286">To see a list of available parameters and their descriptions for `New-AzureRmRedisCacheKey`, run the following command.</span></span>

    PS C:\> Get-Help New-AzureRmRedisCacheKey -detailed

    NAME
        New-AzureRmRedisCacheKey

    SYNOPSIS
        Regenerates the access key of a redis cache.

    SYNTAX
        New-AzureRmRedisCacheKey -Name <String> -ResourceGroupName <String> -KeyType <String> [-Force] [<CommonParameters>]

    DESCRIPTION
        The New-AzureRmRedisCacheKey cmdlet regenerate the access key of a redis cache.

    PARAMETERS
        -Name <String>
            Name of the redis cache.

        -ResourceGroupName <String>
            Name of the resource group for the cache.

        -KeyType <String>
            Specifies whether to regenerate the primary or secondary access key. Possible values are Primary or Secondary.

        -Force
            When the Force parameter is provided, the specified access key is regenerated without any confirmation prompts.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="564a3-287">Aby ponownie wygenerować klucz podstawowy lub pomocniczy dla pamięci podręcznej, należy wywołać `New-AzureRmRedisCacheKey` polecenia cmdlet i podaj nazwę grupy zasobów oraz określ `Primary` lub `Secondary` dla `KeyType` parametru.</span><span class="sxs-lookup"><span data-stu-id="564a3-287">To regenerate the primary or secondary key for your cache, call the `New-AzureRmRedisCacheKey` cmdlet and pass in the name, resource group, and specify either `Primary` or `Secondary` for the `KeyType` parameter.</span></span> <span data-ttu-id="564a3-288">W poniższym przykładzie jest ponownie wygenerować pomocniczy klucz dostępu dla pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-288">In the following example, the secondary access key for a cache is regenerated.</span></span>

    PS C:\> New-AzureRmRedisCacheKey -Name myCache -ResourceGroupName myGroup -KeyType Secondary

    Confirm
    Are you sure you want to regenerate Secondary key for redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


    PrimaryKey   : b2wdt43sfetlju4hfbryfnregrd9wgIcc6IA3zAO1lY=
    SecondaryKey : c53hj3kh4jhHjPJk8l0jji785JgKH9865eifmekfnn6=

## <a name="to-delete-a-redis-cache"></a><span data-ttu-id="564a3-289">Aby usunąć pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-289">To delete a Redis cache</span></span>
<span data-ttu-id="564a3-290">Aby usunąć pamięci podręcznej Redis, użyj [AzureRmRedisCache Usuń](https://msdn.microsoft.com/library/azure/mt634515.aspx) polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-290">To delete a Redis cache, use the [Remove-AzureRmRedisCache](https://msdn.microsoft.com/library/azure/mt634515.aspx) cmdlet.</span></span>

<span data-ttu-id="564a3-291">Aby wyświetlić listę dostępnych parametrów i ich opisy `Remove-AzureRmRedisCache`, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-291">To see a list of available parameters and their descriptions for `Remove-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Remove-AzureRmRedisCache -detailed

    NAME
        Remove-AzureRmRedisCache

    SYNOPSIS
        Remove redis cache if exists.

    SYNTAX
        Remove-AzureRmRedisCache -Name <String> -ResourceGroupName <String> [-Force] [-PassThru] [<CommonParameters>

    DESCRIPTION
        The Remove-AzureRmRedisCache cmdlet removes a redis cache if it exists.

    PARAMETERS
        -Name <String>
            Name of the redis cache to remove.

        -ResourceGroupName <String>
            Name of the resource group of the cache to remove.

        -Force
            When the Force parameter is provided, the cache is removed without any confirmation prompts.

        -PassThru
            By default Remove-AzureRmRedisCache removes the cache and does not return any value. If the PassThru par
            is provided then Remove-AzureRmRedisCache returns a boolean value indicating the success of the operatio

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).

<span data-ttu-id="564a3-292">W poniższym przykładzie pamięci podręcznej o nazwie `myCache` zostanie usunięta.</span><span class="sxs-lookup"><span data-stu-id="564a3-292">In the following example, the cache named `myCache` is removed.</span></span>

    PS C:\> Remove-AzureRmRedisCache -Name myCache -ResourceGroupName myGroup

    Confirm
    Are you sure you want to remove redis cache 'myCache'?
    [Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): Y


## <a name="to-import-a-redis-cache"></a><span data-ttu-id="564a3-293">Aby zaimportować pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-293">To import a Redis cache</span></span>
<span data-ttu-id="564a3-294">Można zaimportować danych do wystąpienia pamięci podręcznej Redis Azure za pomocą `Import-AzureRmRedisCache` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-294">You can import data into an Azure Redis Cache instance using the `Import-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="564a3-295">Narzędzie importu/eksportu jest dostępna tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-295">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="564a3-296">Aby uzyskać więcej informacji na temat importowania i eksportowania, zobacz [importować i eksportować dane w pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="564a3-296">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="564a3-297">Aby wyświetlić listę dostępnych parametrów i ich opisy `Import-AzureRmRedisCache`, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-297">To see a list of available parameters and their descriptions for `Import-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Import-AzureRmRedisCache -detailed

    NAME
        Import-AzureRmRedisCache

    SYNOPSIS
        Import data from blobs to Azure Redis Cache.


    SYNTAX
        Import-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Files <String[]> [-Format <String>] [-Force]
        [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Import-AzureRmRedisCache cmdlet imports data from the specified blobs into Azure Redis Cache.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Files <String[]>
            SAS urls of blobs whose content should be imported into the cache.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -Force
            When the Force parameter is provided, import will be performed without any confirmation prompts.

        -PassThru
            By default Import-AzureRmRedisCache imports data in cache and does not return any value. If the PassThru
            parameter is provided then Import-AzureRmRedisCache returns a boolean value indicating the success of the
            operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="564a3-298">Następujące polecenie importuje dane z obiektu blob, określony przez identyfikator uri sygnatury dostępu Współdzielonego w pamięci podręcznej Redis Azure.</span><span class="sxs-lookup"><span data-stu-id="564a3-298">The following command imports data from the blob specified by the SAS uri into Azure Redis Cache.</span></span>

    PS C:\>Import-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Files @("https://mystorageaccount.blob.core.windows.net/mycontainername/blobname?sv=2015-04-05&sr=b&sig=caIwutG2uDa0NZ8mjdNJdgOY8%2F8mhwRuGNdICU%2B0pI4%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwd") -Force

## <a name="to-export-a-redis-cache"></a><span data-ttu-id="564a3-299">Aby wyeksportować pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-299">To export a Redis cache</span></span>
<span data-ttu-id="564a3-300">Można eksportować dane z wystąpienia pamięci podręcznej Redis Azure za pomocą `Export-AzureRmRedisCache` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-300">You can export data from an Azure Redis Cache instance using the `Export-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="564a3-301">Narzędzie importu/eksportu jest dostępna tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-301">Import/Export is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="564a3-302">Aby uzyskać więcej informacji na temat importowania i eksportowania, zobacz [importować i eksportować dane w pamięci podręcznej Redis Azure](cache-how-to-import-export-data.md).</span><span class="sxs-lookup"><span data-stu-id="564a3-302">For more information about Import/Export, see [Import and Export data in Azure Redis Cache](cache-how-to-import-export-data.md).</span></span>
> 
> 

<span data-ttu-id="564a3-303">Aby wyświetlić listę dostępnych parametrów i ich opisy `Export-AzureRmRedisCache`, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-303">To see a list of available parameters and their descriptions for `Export-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Export-AzureRmRedisCache -detailed

    NAME
        Export-AzureRmRedisCache

    SYNOPSIS
        Exports data from Azure Redis Cache to a specified container.


    SYNTAX
        Export-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -Prefix <String> -Container <String> [-Format
        <String>] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Export-AzureRmRedisCache cmdlet exports data from Azure Redis Cache to a specified container.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -Prefix <String>
            Prefix to use for blob names.

        -Container <String>
            SAS url of container where data should be exported.

        -Format <String>
            Format for the blob.  Currently "rdb" is the only supported, with other formats expected in the future.

        -PassThru
            By default Export-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Export-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="564a3-304">Polecenie eksportuje dane z wystąpienia pamięci podręcznej Redis Azure do kontenera określony przez identyfikator uri sygnatury dostępu Współdzielonego.</span><span class="sxs-lookup"><span data-stu-id="564a3-304">The following command exports data from an Azure Redis Cache instance into the container specified by the SAS uri.</span></span>

        PS C:\>Export-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -Prefix "blobprefix"
        -Container "https://mystorageaccount.blob.core.windows.net/mycontainer?sv=2015-04-05&sr=c&sig=HezZtBZ3DURmEGDduauE7
        pvETY4kqlPI8JCNa8ATmaw%3D&st=2016-05-27T00%3A00%3A00Z&se=2016-05-28T00%3A00%3A00Z&sp=rwdl"

## <a name="to-reboot-a-redis-cache"></a><span data-ttu-id="564a3-305">Ponowne uruchomienie z pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="564a3-305">To reboot a Redis cache</span></span>
<span data-ttu-id="564a3-306">Możesz ponownie, używając wystąpienia pamięci podręcznej Redis Azure `Reset-AzureRmRedisCache` polecenia cmdlet.</span><span class="sxs-lookup"><span data-stu-id="564a3-306">You can reboot your Azure Redis Cache instance using the `Reset-AzureRmRedisCache` cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="564a3-307">Ponowne uruchomienie jest dostępna tylko dla [warstwy premium](cache-premium-tier-intro.md) przechowuje w pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-307">Reboot is only available for [premium tier](cache-premium-tier-intro.md) caches.</span></span> <span data-ttu-id="564a3-308">Aby uzyskać więcej informacji o ponowne uruchomienie z pamięci podręcznej, zobacz [pamięci podręcznej administracji — ponowny rozruch](cache-administration.md#reboot).</span><span class="sxs-lookup"><span data-stu-id="564a3-308">For more information about rebooting your cache, see [Cache administration - reboot](cache-administration.md#reboot).</span></span>
> 
> 

<span data-ttu-id="564a3-309">Aby wyświetlić listę dostępnych parametrów i ich opisy `Reset-AzureRmRedisCache`, uruchom następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="564a3-309">To see a list of available parameters and their descriptions for `Reset-AzureRmRedisCache`, run the following command.</span></span>

    PS C:\> Get-Help Reset-AzureRmRedisCache -detailed

    NAME
        Reset-AzureRmRedisCache

    SYNOPSIS
        Reboot specified node(s) of an Azure Redis Cache instance.


    SYNTAX
        Reset-AzureRmRedisCache -Name <String> -ResourceGroupName <String> -RebootType <String> [-ShardId <Integer>]
        [-Force] [-PassThru] [<CommonParameters>]


    DESCRIPTION
        The Reset-AzureRmRedisCache cmdlet reboots the specified node(s) of an Azure Redis Cache instance.


    PARAMETERS
        -Name <String>
            The name of the cache.

        -ResourceGroupName <String>
            The name of the resource group that contains the cache.

        -RebootType <String>
            Which node to reboot. Possible values are "PrimaryNode", "SecondaryNode", "AllNodes".

        -ShardId <Integer>
            Which shard to reboot when rebooting a premium cache with clustering enabled.

        -Force
            When the Force parameter is provided, reset will be performed without any confirmation prompts.

        -PassThru
            By default Reset-AzureRmRedisCache does not return any value. If the PassThru parameter is provided
            then Reset-AzureRmRedisCache returns a boolean value indicating the success of the operation.

        <CommonParameters>
            This cmdlet supports the common parameters: Verbose, Debug,
            ErrorAction, ErrorVariable, WarningAction, WarningVariable,
            OutBuffer, PipelineVariable, and OutVariable. For more information, see
            about_CommonParameters (http://go.microsoft.com/fwlink/?LinkID=113216).


<span data-ttu-id="564a3-310">Polecenie wykonuje ponowny rozruch oba węzły określonego pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="564a3-310">The following command reboots both nodes of the specified cache.</span></span>

        PS C:\>Reset-AzureRmRedisCache -ResourceGroupName "resourceGroupName" -Name "cacheName" -RebootType "AllNodes"
        -Force


## <a name="next-steps"></a><span data-ttu-id="564a3-311">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="564a3-311">Next steps</span></span>
<span data-ttu-id="564a3-312">Aby dowiedzieć się więcej na temat korzystania z platformy Azure, programu Windows PowerShell, zobacz następujące zasoby:</span><span class="sxs-lookup"><span data-stu-id="564a3-312">To learn more about using Windows PowerShell with Azure, see the following resources:</span></span>

* [<span data-ttu-id="564a3-313">Azure dokumentację poleceń cmdlet pamięci podręcznej Redis w witrynie MSDN</span><span class="sxs-lookup"><span data-stu-id="564a3-313">Azure Redis Cache cmdlet documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/mt634513.aspx)
* <span data-ttu-id="564a3-314">[Polecenia cmdlet Menedżera zasobów systemu Azure](http://go.microsoft.com/fwlink/?LinkID=394765): Dowiedz się, jak używać poleceń cmdlet w module usługi Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="564a3-314">[Azure Resource Manager Cmdlets](http://go.microsoft.com/fwlink/?LinkID=394765): Learn to use the cmdlets in the Azure Resource Manager module.</span></span>
* <span data-ttu-id="564a3-315">[Używanie grup zasobów do zarządzania zasobami Azure](../azure-resource-manager/resource-group-template-deploy-portal.md): informacje o sposobie tworzenia i obsługi grup zasobów w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="564a3-315">[Using Resource groups to manage your Azure resources](../azure-resource-manager/resource-group-template-deploy-portal.md): Learn how to create and manage resource groups in the Azure portal.</span></span>
* <span data-ttu-id="564a3-316">[Azure blog](http://blogs.msdn.com/windowsazure): więcej informacji na temat nowych funkcji w systemie Azure.</span><span class="sxs-lookup"><span data-stu-id="564a3-316">[Azure blog](http://blogs.msdn.com/windowsazure): Learn about new features in Azure.</span></span>
* <span data-ttu-id="564a3-317">[Blog dotyczący programu Windows PowerShell](http://blogs.msdn.com/powershell): więcej informacji na temat nowych funkcji w programie Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="564a3-317">[Windows PowerShell blog](http://blogs.msdn.com/powershell): Learn about new features in Windows PowerShell.</span></span>
* <span data-ttu-id="564a3-318">["Witaj, Twórco skryptów!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Pobierz rzeczywistych porady i wskazówki związane z społeczności programu Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="564a3-318">["Hey, Scripting Guy!" Blog](http://blogs.technet.com/b/heyscriptingguy/): Get real-world tips and tricks from the Windows PowerShell community.</span></span>

