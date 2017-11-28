---
title: "pamięć podręczna Redis Azure za pomocą interfejsu wiersza polecenia Azure aaaManage | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooinstall hello Azure CLI na dowolnej platformie, jak toouse go tooyour tooconnect konto platformy Azure i w jaki sposób toocreate oraz zarządzania nimi pamięci podręcznej Redis z hello wiersza polecenia platformy Azure."
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 964ff245-859d-4bc1-bccf-62e4b3c1169f
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: e8ee30090133e6b4edea93dcd13fd171e75989bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-azure-redis-cache-using-hello-azure-command-line-interface-azure-cli"></a><span data-ttu-id="f33ef-103">Jak toocreate i zarządzania pamięcią podręczną Redis Azure za pomocą hello interfejsu wiersza polecenia platformy Azure (Azure CLI)</span><span class="sxs-lookup"><span data-stu-id="f33ef-103">How toocreate and manage Azure Redis Cache using hello Azure Command-Line Interface (Azure CLI)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f33ef-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f33ef-104">PowerShell</span></span>](cache-howto-manage-redis-cache-powershell.md)
> * [<span data-ttu-id="f33ef-105">Interfejs wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="f33ef-105">Azure CLI</span></span>](cache-manage-cli.md)
>
>

<span data-ttu-id="f33ef-106">Hello Azure CLI jest toomanage doskonały sposób infrastruktury platformy Azure z dowolną platformą.</span><span class="sxs-lookup"><span data-stu-id="f33ef-106">hello Azure CLI is a great way toomanage your Azure infrastructure from any platform.</span></span> <span data-ttu-id="f33ef-107">W tym artykule opisano sposób toocreate i zarządzanie nimi z wystąpień pamięci podręcznej Redis Azure za pomocą hello wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f33ef-107">This article shows you how toocreate and manage your Azure Redis Cache instances using hello Azure CLI.</span></span>

> [!NOTE]
> <span data-ttu-id="f33ef-108">Ten artykuł dotyczy tooa poprzedniej wersji interfejsu wiersza polecenia Azure.</span><span class="sxs-lookup"><span data-stu-id="f33ef-108">This article applies tooa previous version of Azure CLI.</span></span> <span data-ttu-id="f33ef-109">Dla hello najnowsze Azure CLI 2.0 przykładowe skrypty, zobacz [przykłady pamięci podręcznej Azure CLI Redis](cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f33ef-109">For hello latest Azure CLI 2.0 sample scripts, see [Azure CLI Redis cache samples](cli-samples.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="f33ef-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f33ef-110">Prerequisites</span></span>
<span data-ttu-id="f33ef-111">toocreate i Zarządzanie wystąpieniami usługi pamięć podręczna Redis Azure za pomocą interfejsu wiersza polecenia Azure, należy wykonać następujące kroki hello.</span><span class="sxs-lookup"><span data-stu-id="f33ef-111">toocreate and manage Azure Redis Cache instances using Azure CLI, you must complete hello following steps.</span></span>

* <span data-ttu-id="f33ef-112">Musi mieć konto platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f33ef-112">You must have an Azure account.</span></span> <span data-ttu-id="f33ef-113">Jeśli nie masz, możesz utworzyć [bezpłatne konto](https://azure.microsoft.com/pricing/free-trial/) za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="f33ef-113">If you don't have one, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a few moments.</span></span>
* <span data-ttu-id="f33ef-114">[Instalowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f33ef-114">[Install hello Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="f33ef-115">Połącz instalacji wiersza polecenia platformy Azure z osobistego konta Azure lub służbowy lub Azure konta służbowego i logowania z hello interfejsu wiersza polecenia platformy Azure przy użyciu hello `azure login` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-115">Connect your Azure CLI installation with a personal Azure account, or with a work or school Azure account, and log in from hello Azure CLI using hello `azure login` command.</span></span> <span data-ttu-id="f33ef-116">toounderstand hello różnic oraz wybrać, zobacz [połączyć tooan subskrypcji platformy Azure z hello interfejsu wiersza polecenia platformy Azure (Azure CLI)](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f33ef-116">toounderstand hello differences and choose, see [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="f33ef-117">Przed uruchomieniem żadnego hello następujące polecenia, Przełącz hello wiersza polecenia platformy Azure w trybie Menedżera zasobów, uruchamiając hello `azure config mode arm` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-117">Before running any of hello following commands, switch hello Azure CLI into Resource Manager mode by running hello `azure config mode arm` command.</span></span> <span data-ttu-id="f33ef-118">Aby uzyskać więcej informacji, zobacz [Użyj toomanage interfejsu wiersza polecenia Azure hello Azure zasobów i grup zasobów](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="f33ef-118">For more information, see [Use hello Azure CLI toomanage Azure resources and resource groups](../xplat-cli-azure-resource-manager.md).</span></span>

## <a name="redis-cache-properties"></a><span data-ttu-id="f33ef-119">Właściwości pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="f33ef-119">Redis Cache properties</span></span>
<span data-ttu-id="f33ef-120">Witaj następujące właściwości są używane podczas tworzenia i aktualizowania wystąpienia pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="f33ef-120">hello following properties are used when creating and updating Redis Cache instances.</span></span>

| <span data-ttu-id="f33ef-121">Właściwość</span><span class="sxs-lookup"><span data-stu-id="f33ef-121">Property</span></span> | <span data-ttu-id="f33ef-122">Przełącznik</span><span class="sxs-lookup"><span data-stu-id="f33ef-122">Switch</span></span> | <span data-ttu-id="f33ef-123">Opis</span><span class="sxs-lookup"><span data-stu-id="f33ef-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f33ef-124">name</span><span class="sxs-lookup"><span data-stu-id="f33ef-124">name</span></span> |<span data-ttu-id="f33ef-125">-n, — nazwa</span><span class="sxs-lookup"><span data-stu-id="f33ef-125">-n, --name</span></span> |<span data-ttu-id="f33ef-126">Nazwa hello pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="f33ef-126">Name of hello Redis Cache.</span></span> |
| <span data-ttu-id="f33ef-127">grupa zasobów</span><span class="sxs-lookup"><span data-stu-id="f33ef-127">resource group</span></span> |<span data-ttu-id="f33ef-128">-g,--grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="f33ef-128">-g, --resource-group</span></span> |<span data-ttu-id="f33ef-129">Nazwa hello grupy zasobów.</span><span class="sxs-lookup"><span data-stu-id="f33ef-129">Name of hello Resource Group.</span></span> |
| <span data-ttu-id="f33ef-130">location</span><span class="sxs-lookup"><span data-stu-id="f33ef-130">location</span></span> |<span data-ttu-id="f33ef-131">-l, — lokalizacja</span><span class="sxs-lookup"><span data-stu-id="f33ef-131">-l, --location</span></span> |<span data-ttu-id="f33ef-132">Pamięć podręczna toocreate lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="f33ef-132">Location toocreate cache.</span></span> |
| <span data-ttu-id="f33ef-133">Rozmiar</span><span class="sxs-lookup"><span data-stu-id="f33ef-133">size</span></span> |<span data-ttu-id="f33ef-134">-z, — rozmiar</span><span class="sxs-lookup"><span data-stu-id="f33ef-134">-z, --size</span></span> |<span data-ttu-id="f33ef-135">Rozmiar hello pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="f33ef-135">Size of hello Redis Cache.</span></span> <span data-ttu-id="f33ef-136">Prawidłowe wartości: [C0 C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span><span class="sxs-lookup"><span data-stu-id="f33ef-136">Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]</span></span> |
| <span data-ttu-id="f33ef-137">Jednostka SKU</span><span class="sxs-lookup"><span data-stu-id="f33ef-137">sku</span></span> |<span data-ttu-id="f33ef-138">-x - sku</span><span class="sxs-lookup"><span data-stu-id="f33ef-138">-x, --sku</span></span> |<span data-ttu-id="f33ef-139">W pamięci podręcznej redis jednostki SKU.</span><span class="sxs-lookup"><span data-stu-id="f33ef-139">Redis SKU.</span></span> <span data-ttu-id="f33ef-140">Powinien być jednym z: [Basic, Standard, Premium]</span><span class="sxs-lookup"><span data-stu-id="f33ef-140">Should be one of : [Basic, Standard, Premium]</span></span> |
| <span data-ttu-id="f33ef-141">EnableNonSslPort</span><span class="sxs-lookup"><span data-stu-id="f33ef-141">EnableNonSslPort</span></span> |<span data-ttu-id="f33ef-142">-e, - enable bez protokołu ssl portu</span><span class="sxs-lookup"><span data-stu-id="f33ef-142">-e, --enable-non-ssl-port</span></span> |<span data-ttu-id="f33ef-143">Właściwość EnableNonSslPort hello pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="f33ef-143">EnableNonSslPort property of hello Redis Cache.</span></span> <span data-ttu-id="f33ef-144">Dodać tę flagę Port SSL nie hello tooenable dla pamięci podręcznej</span><span class="sxs-lookup"><span data-stu-id="f33ef-144">Add this flag if you want tooenable hello Non SSL Port for your cache</span></span> |
| <span data-ttu-id="f33ef-145">Redis konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f33ef-145">Redis Configuration</span></span> |<span data-ttu-id="f33ef-146">-c,--konfiguracja pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="f33ef-146">-c, --redis-configuration</span></span> |<span data-ttu-id="f33ef-147">W pamięci podręcznej redis konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f33ef-147">Redis Configuration.</span></span> <span data-ttu-id="f33ef-148">Wprowadź ciąg w formacie JSON konfiguracji kluczy i wartości w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="f33ef-148">Enter a JSON formatted string of configuration keys and values here.</span></span> <span data-ttu-id="f33ef-149">Format: "{" ":""," ":" "}"</span><span class="sxs-lookup"><span data-stu-id="f33ef-149">Format:"{"":"","":""}"</span></span> |
| <span data-ttu-id="f33ef-150">Redis konfiguracji</span><span class="sxs-lookup"><span data-stu-id="f33ef-150">Redis Configuration</span></span> |<span data-ttu-id="f33ef-151">-f, — plik w przypadku konfiguracji pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="f33ef-151">-f, --redis-configuration-file</span></span> |<span data-ttu-id="f33ef-152">W pamięci podręcznej redis konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f33ef-152">Redis Configuration.</span></span> <span data-ttu-id="f33ef-153">Wprowadź ścieżkę hello plik zawierający konfigurację kluczy i wartości w tym miejscu.</span><span class="sxs-lookup"><span data-stu-id="f33ef-153">Enter hello path of a file containing configuration keys and values here.</span></span> <span data-ttu-id="f33ef-154">Format wpis pliku hello: {"": "","": ""}</span><span class="sxs-lookup"><span data-stu-id="f33ef-154">Format for hello file entry: {"":"","":""}</span></span> |
| <span data-ttu-id="f33ef-155">Liczba niezależnych</span><span class="sxs-lookup"><span data-stu-id="f33ef-155">Shard Count</span></span> |<span data-ttu-id="f33ef-156">-r--niezależnego fragmentu-, count, liczba</span><span class="sxs-lookup"><span data-stu-id="f33ef-156">-r, --shard-count</span></span> |<span data-ttu-id="f33ef-157">Liczba fragmentów toocreate na pamięć podręczna Premium klastrowania z klastra.</span><span class="sxs-lookup"><span data-stu-id="f33ef-157">Number of Shards toocreate on a Premium Cluster Cache with clustering.</span></span> |
| <span data-ttu-id="f33ef-158">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="f33ef-158">Virtual Network</span></span> |<span data-ttu-id="f33ef-159">-v, — sieci wirtualnej</span><span class="sxs-lookup"><span data-stu-id="f33ef-159">-v, --virtual-network</span></span> |<span data-ttu-id="f33ef-160">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa pamięci podręcznej w redis hello dokładnie ARM identyfikator zasobu Witaj Witaj toodeploy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f33ef-160">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="f33ef-161">Przykładowy format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="f33ef-161">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="f33ef-162">Typ klucza</span><span class="sxs-lookup"><span data-stu-id="f33ef-162">key type</span></span> |<span data-ttu-id="f33ef-163">-t, — typ klucza</span><span class="sxs-lookup"><span data-stu-id="f33ef-163">-t, --key-type</span></span> |<span data-ttu-id="f33ef-164">Typ klucza toorenew.</span><span class="sxs-lookup"><span data-stu-id="f33ef-164">Type of key toorenew.</span></span> <span data-ttu-id="f33ef-165">Prawidłowe wartości: [podstawową, dodatkowej]</span><span class="sxs-lookup"><span data-stu-id="f33ef-165">Valid values: [Primary, Secondary]</span></span> |
| <span data-ttu-id="f33ef-166">StaticIP</span><span class="sxs-lookup"><span data-stu-id="f33ef-166">StaticIP</span></span> |<span data-ttu-id="f33ef-167">-p,--static ip < static ip ></span><span class="sxs-lookup"><span data-stu-id="f33ef-167">-p, --static-ip <static-ip></span></span> |<span data-ttu-id="f33ef-168">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa unikatowy adres IP w podsieci hello hello pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="f33ef-168">When hosting your cache in a VNET, specifies a unique IP address in hello subnet for hello cache.</span></span> <span data-ttu-id="f33ef-169">Jeśli nie zostanie podana, co jest wybrany dla Ciebie z hello podsieci.</span><span class="sxs-lookup"><span data-stu-id="f33ef-169">If not provided, one is chosen for you from hello subnet.</span></span> |
| <span data-ttu-id="f33ef-170">Podsieć</span><span class="sxs-lookup"><span data-stu-id="f33ef-170">Subnet</span></span> |<span data-ttu-id="f33ef-171">t,--podsieci<subnet></span><span class="sxs-lookup"><span data-stu-id="f33ef-171">t, --subnet <subnet></span></span> |<span data-ttu-id="f33ef-172">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa nazwę hello hello podsieci, w których pamięci podręcznej hello toodeploy.</span><span class="sxs-lookup"><span data-stu-id="f33ef-172">When hosting your cache in a VNET, specifies hello name of hello subnet in which toodeploy hello cache.</span></span> |
| <span data-ttu-id="f33ef-173">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="f33ef-173">VirtualNetwork</span></span> |<span data-ttu-id="f33ef-174">-v, — sieci wirtualnej <-sieci wirtualnej ></span><span class="sxs-lookup"><span data-stu-id="f33ef-174">-v, --virtual-network <virtual-network></span></span> |<span data-ttu-id="f33ef-175">Podczas obsługi pamięci podręcznej w sieci Wirtualnej, określa pamięci podręcznej w redis hello dokładnie ARM identyfikator zasobu Witaj Witaj toodeploy sieci wirtualnej.</span><span class="sxs-lookup"><span data-stu-id="f33ef-175">When hosting your cache in a VNET, specifies hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in.</span></span> <span data-ttu-id="f33ef-176">Przykładowy format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span><span class="sxs-lookup"><span data-stu-id="f33ef-176">Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1</span></span> |
| <span data-ttu-id="f33ef-177">Subskrypcja</span><span class="sxs-lookup"><span data-stu-id="f33ef-177">Subscription</span></span> |<span data-ttu-id="f33ef-178">-s, - subskrypcji</span><span class="sxs-lookup"><span data-stu-id="f33ef-178">-s, --subscription</span></span> |<span data-ttu-id="f33ef-179">Identyfikator subskrypcji Hello.</span><span class="sxs-lookup"><span data-stu-id="f33ef-179">hello subscription identifier.</span></span> |

## <a name="see-all-redis-cache-commands"></a><span data-ttu-id="f33ef-180">Zobacz wszystkie polecenia pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="f33ef-180">See all Redis Cache commands</span></span>
<span data-ttu-id="f33ef-181">toosee wszystkie polecenia pamięci podręcznej Redis i ich parametry, użyj hello `azure rediscache -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-181">toosee all Redis Cache commands and their parameters, use hello `azure rediscache -h` command.</span></span>

    C:\>azure rediscache -h
    help:    Commands toomanage your Azure Redis Cache(s)
    help:
    help:    Create a Redis Cache
    help:      rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Delete an existing Redis Cache
    help:      rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    List all Redis Caches within your Subscription or Resource Group
    help:      rediscache list [options]
    help:
    help:    Show properties of an existing Redis Cache
    help:      rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Change settings of an existing Redis Cache
    help:      rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Renew hello authentication key for an existing Redis Cache
    help:      rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:      rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help  output usage information
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="create-a-redis-cache"></a><span data-ttu-id="f33ef-182">Tworzenie pamięci podręcznej Redis Cache</span><span class="sxs-lookup"><span data-stu-id="f33ef-182">Create a Redis Cache</span></span>
<span data-ttu-id="f33ef-183">toocreate pamięci podręcznej Redis, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f33ef-183">toocreate a Redis Cache, use hello following command:</span></span>

    azure rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]

<span data-ttu-id="f33ef-184">Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache create -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-184">For more information about this command, run hello `azure rediscache create -h` command.</span></span>

    C:\>azure rediscache create -h
    help:    Create a Redis Cache
    help:
    help:    Usage: rediscache create [--name <name> --resource-group <resource-group> --location <location> [options]]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -l, --location <location>                                Location toocreate cache.
    help:      -z, --size <size>                                        Size of hello Redis Cache. Valid values: [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]
    help:      -x, --sku <sku>                                          Redis SKU. Should be one of : [Basic, Standard, Premium]
    help:      -e, --enable-non-ssl-port                                EnableNonSslPort property of hello Redis Cache. Add this flag if you want tooenable hello Non SSL Port for your cache
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here. Format:"{"<key1>":"<value1>","<key2>":"<value2>"}"
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here. Format for hello file entry: {"<key1>":"<value1>","<key2>":"<value2>"}
    help:      -r, --shard-count <shard-count>                          Number of Shards toocreate on a Premium Cluster Cache
    help:      -v, --virtual-network <virtual-network>                  hello exact ARM resource ID of hello virtual network toodeploy hello redis cache in. Example format: /subscriptions/{subid}/resourceGroups/{resourceGroupName}/Microsoft.ClassicNetwork/VirtualNetworks/vnet1
    help:      -t, --subnet <subnet>                                    Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -p, --static-ip <static-ip>                              Required when deploying a redis cache inside an existing Azure Virtual Network
    help:      -s, --subscription <id>                                  hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="delete-an-existing-redis-cache"></a><span data-ttu-id="f33ef-185">Usuń istniejące pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="f33ef-185">Delete an existing Redis Cache</span></span>
<span data-ttu-id="f33ef-186">toodelete pamięci podręcznej Redis, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f33ef-186">toodelete a Redis Cache, use hello following command:</span></span>

    azure rediscache delete [--name <name> --resource-group <resource-group> ]

<span data-ttu-id="f33ef-187">Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache delete -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-187">For more information about this command, run hello `azure rediscache delete -h` command.</span></span>

    C:\>azure rediscache delete -h
    help:    Delete an existing Redis Cache
    help:
    help:    Usage: rediscache delete [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which hello cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-all-redis-caches-within-your-subscription-or-resource-group"></a><span data-ttu-id="f33ef-188">Wyświetl listę wszystkich pamięci podręczne Redis w ramach Twojej subskrypcji lub grupy zasobów</span><span class="sxs-lookup"><span data-stu-id="f33ef-188">List all Redis Caches within your Subscription or Resource Group</span></span>
<span data-ttu-id="f33ef-189">Użyj wszystkich pamięci podręczne Redis w ramach Twojej subskrypcji lub grupy zasobów, toolist hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="f33ef-189">toolist all Redis Caches within your Subscription or Resource Group, use hello following command:</span></span>

    azure rediscache list [options]

<span data-ttu-id="f33ef-190">Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache list -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-190">For more information about this command, run hello `azure rediscache list -h` command.</span></span>

    C:\>azure rediscache list -h
    help:    List all Redis Caches within your Subscription or Resource Group
    help:
    help:    Usage: rediscache list [options]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="show-properties-of-an-existing-redis-cache"></a><span data-ttu-id="f33ef-191">Pokaż właściwości istniejącej pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="f33ef-191">Show properties of an existing Redis Cache</span></span>
<span data-ttu-id="f33ef-192">właściwości tooshow istniejącej pamięci podręcznej Redis, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f33ef-192">tooshow properties of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache show [--name <name> --resource-group <resource-group>]

<span data-ttu-id="f33ef-193">Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache show -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-193">For more information about this command, run hello `azure rediscache show -h` command.</span></span>

    C:\>azure rediscache show -h
    help:    Show properties of an existing Redis Cache
    help:
    help:    Usage: rediscache show [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

<a name="scale"></a>

## <a name="change-settings-of-an-existing-redis-cache"></a><span data-ttu-id="f33ef-194">Zmień ustawienia istniejących pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="f33ef-194">Change settings of an existing Redis Cache</span></span>
<span data-ttu-id="f33ef-195">Ustawienia toochange istniejącej pamięci podręcznej Redis, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f33ef-195">toochange settings of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]

<span data-ttu-id="f33ef-196">Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache set -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-196">For more information about this command, run hello `azure rediscache set -h` command.</span></span>

    C:\>azure rediscache set -h
    help:    Change settings of an existing Redis Cache
    help:
    help:    Usage: rediscache set [--name <name> --resource-group <resource-group> --redis-configuration <redis-configuration>/--redis-configuration-file <redisConfigurationFile>]
    help:
    help:    Options:
    help:      -h, --help                                               output usage information
    help:      -v, --verbose                                            use verbose output
    help:      -vv                                                      more verbose with debug output
    help:      --json                                                   use json output
    help:      -n, --name <name>                                        Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>                    Name of hello Resource Group
    help:      -c, --redis-configuration <redis-configuration>          Redis Configuration. Enter a JSON formatted string of configuration keys and values here.
    help:      -f, --redis-configuration-file <redisConfigurationFile>  Redis Configuration. Enter hello path of a file containing configuration keys and values here.
    help:      -s, --subscription <subscription>                        hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="renew-hello-authentication-key-for-an-existing-redis-cache"></a><span data-ttu-id="f33ef-197">Odnawianie klucz uwierzytelniania powitania dla istniejącej pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="f33ef-197">Renew hello authentication key for an existing Redis Cache</span></span>
<span data-ttu-id="f33ef-198">klucz uwierzytelniania hello toorenew dla istniejącej pamięci podręcznej Redis, hello Użyj następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="f33ef-198">toorenew hello authentication key for an existing Redis Cache, use hello following command:</span></span>

    azure rediscache renew-key [--name <name> --resource-group <resource-group> --key-type <key-type>]

<span data-ttu-id="f33ef-199">Określ `Primary` lub `Secondary` dla `key-type`.</span><span class="sxs-lookup"><span data-stu-id="f33ef-199">Specify `Primary` or `Secondary` for `key-type`.</span></span>

<span data-ttu-id="f33ef-200">Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache renew-key -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-200">For more information about this command, run hello `azure rediscache renew-key -h` command.</span></span>

    C:\>azure rediscache renew-key -h
    help:    Renew hello authentication key for an existing Redis Cache
    help:
    help:    Usage: rediscache renew-key [--name <name> --resource-group <resource-group> ]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which cache exists
    help:      -t, --key-type <key-type>              type of key toorenew. Valid values are: 'Primary', 'Secondary'.
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)

## <a name="list-primary-and-secondary-keys-of-an-existing-redis-cache"></a><span data-ttu-id="f33ef-201">Lista podstawowe i pomocnicze klucze istniejącej pamięci podręcznej Redis</span><span class="sxs-lookup"><span data-stu-id="f33ef-201">List Primary and Secondary keys of an existing Redis Cache</span></span>
<span data-ttu-id="f33ef-202">klucze podstawowe i pomocnicze toolist istniejącej pamięci podręcznej Redis, użyj następującego polecenia hello:</span><span class="sxs-lookup"><span data-stu-id="f33ef-202">toolist Primary and Secondary keys of an existing Redis Cache, use hello following command:</span></span>

    azure rediscache list-keys [--name <name> --resource-group <resource-group>]

<span data-ttu-id="f33ef-203">Aby uzyskać więcej informacji na temat tego polecenia, uruchom hello `azure rediscache list-keys -h` polecenia.</span><span class="sxs-lookup"><span data-stu-id="f33ef-203">For more information about this command, run hello `azure rediscache list-keys -h` command.</span></span>

    C:\>azure rediscache list-keys -h
    help:    Lists Primary and Secondary key of an existing Redis Cache
    help:
    help:    Usage: rediscache list-keys [--name <name> --resource-group <resource-group>]
    help:
    help:    Options:
    help:      -h, --help                             output usage information
    help:      -v, --verbose                          use verbose output
    help:      -vv                                    more verbose with debug output
    help:      --json                                 use json output
    help:      -n, --name <name>                      Name of hello Redis Cache.
    help:      -g, --resource-group <resource-group>  Name of hello Resource Group under which Cache exists
    help:      -s, --subscription <subscription>      hello subscription identifier
    help:
    help:    Current Mode: arm (Azure Resource Management)
