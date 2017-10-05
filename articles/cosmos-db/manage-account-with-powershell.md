---
title: "Automatyzacja Azure rozwiązania Cosmos DB - zarządzania przy użyciu programu Powershell | Dokumentacja firmy Microsoft"
description: "Użyj programu Powershell Azure Zarządzanie konta bazy danych Azure rozwiązania Cosmos."
services: cosmos-db
author: dmakwana
manager: jhubbard
editor: 
tags: azure-resource-manager
documentationcenter: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/21/2017
ms.author: dimakwan
ms.openlocfilehash: 25c543528119410dff0684845a713dcb0d6151d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a><span data-ttu-id="60f95-103">Tworzenie konta bazy danych rozwiązania Cosmos Azure przy użyciu programu PowerShell</span><span class="sxs-lookup"><span data-stu-id="60f95-103">Create an Azure Cosmos DB account using PowerShell</span></span>

<span data-ttu-id="60f95-104">Następujący przewodnik zawiera opis polecenia do automatyzacji zarządzania konta bazy danych DB rozwiązania Cosmos Azure przy użyciu programu Azure Powershell.</span><span class="sxs-lookup"><span data-stu-id="60f95-104">The following guide describes commands to automate management of your Azure Cosmos DB database accounts using Azure Powershell.</span></span> <span data-ttu-id="60f95-105">Zawiera także polecenia do zarządzania klucze konta i priorytetów trybu failover w [konta bazy danych w przypadku][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="60f95-105">It also includes commands to manage account keys and failover priorities in [multi-region database accounts][scaling-globally].</span></span> <span data-ttu-id="60f95-106">Aktualizacja konta bazy danych służy do modyfikowania zasad zgodności i Dodaj lub usuń regionów.</span><span class="sxs-lookup"><span data-stu-id="60f95-106">Updating your database account allows you to modify consistency policies and add/remove regions.</span></span> <span data-ttu-id="60f95-107">Do zarządzania i platform konta bazy danych rozwiązania Cosmos platformy Azure, możesz użyć dowolnej [interfejsu wiersza polecenia Azure](cli-samples.md), [interfejsu API REST dostawcy zasobów][rp-rest-api], lub [portalu Azure ](create-documentdb-dotnet.md#create-account).</span><span class="sxs-lookup"><span data-stu-id="60f95-107">For cross-platform management of your Azure Cosmos DB account, you can use either [Azure CLI](cli-samples.md), the [Resource Provider REST API][rp-rest-api], or the [Azure portal](create-documentdb-dotnet.md#create-account).</span></span>

## <a name="getting-started"></a><span data-ttu-id="60f95-108">Wprowadzenie</span><span class="sxs-lookup"><span data-stu-id="60f95-108">Getting Started</span></span>

<span data-ttu-id="60f95-109">Postępuj zgodnie z instrukcjami [jak instalowanie i konfigurowanie programu Azure PowerShell] [ powershell-install-configure] do zainstalowania i zaloguj się do konta usługi Azure Resource Manager w programie Powershell.</span><span class="sxs-lookup"><span data-stu-id="60f95-109">Follow the instructions in [How to install and configure Azure PowerShell][powershell-install-configure] to install and log in to your Azure Resource Manager account in Powershell.</span></span>

### <a name="notes"></a><span data-ttu-id="60f95-110">Uwagi</span><span class="sxs-lookup"><span data-stu-id="60f95-110">Notes</span></span>

* <span data-ttu-id="60f95-111">Jeśli chcesz wykonać następujące polecenia, bez konieczności potwierdzenie przez użytkownika, dołącz `-Force` flagi do polecenia.</span><span class="sxs-lookup"><span data-stu-id="60f95-111">If you would like to execute the following commands without requiring user confirmation, append the `-Force` flag to the command.</span></span>
* <span data-ttu-id="60f95-112">Poniższe polecenia są synchroniczne.</span><span class="sxs-lookup"><span data-stu-id="60f95-112">All the following commands are synchronous.</span></span>

## <span data-ttu-id="60f95-113"><a id="create-documentdb-account-powershell"></a>Tworzenie konta usługi Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="60f95-113"><a id="create-documentdb-account-powershell"></a> Create an Azure Cosmos DB Account</span></span>

<span data-ttu-id="60f95-114">To polecenie umożliwia tworzenie konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-114">This command allows you to create an Azure Cosmos DB database account.</span></span> <span data-ttu-id="60f95-115">Konfigurowanie nowego konta bazy danych jako albo jednym regionie lub [w przypadku] [ scaling-globally] niektóre [spójności zasad](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="60f95-115">Configure your new database account as either single-region or [multi-region][scaling-globally] with a certain [consistency policy](consistency-levels.md).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="60f95-116">`<write-region-location>`Nazwa lokalizacji zapisu regionu konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-116">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="60f95-117">Ta lokalizacja musi mieć wartość 0 priorytet trybu failover.</span><span class="sxs-lookup"><span data-stu-id="60f95-117">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="60f95-118">Musi istnieć dokładnie jeden region zapisu na konto bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-118">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="60f95-119">`<read-region-location>`Nazwa lokalizacji obszaru odczytu konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-119">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="60f95-120">Ta lokalizacja musi być większa niż 0. wartość priorytetu trybu failover.</span><span class="sxs-lookup"><span data-stu-id="60f95-120">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="60f95-121">Może istnieć więcej niż jeden odczytu regiony dla danego konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-121">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="60f95-122">`<ip-range-filter>`Określa zbiór adresów IP i zakresów adresów IP w postaci CIDR do uwzględnienia jako lista dozwolonych adresów IP klienta, konto bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-122">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="60f95-123">Zakresy adresów IP musi być przecinkami oddzielone i nie może zawierać spacji.</span><span class="sxs-lookup"><span data-stu-id="60f95-123">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="60f95-124">Aby uzyskać więcej informacji, zobacz [Obsługa zapory DB rozwiązania Cosmos Azure](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="60f95-124">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="60f95-125">`<default-consistency-level>`Domyślny poziom spójności konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-125">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="60f95-126">Aby uzyskać więcej informacji, zobacz [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="60f95-126">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="60f95-127">`<max-interval>`W przypadku użycia z ograniczonym nieaktualności, ta wartość przedstawia ilość czasu nieaktualności (w sekundach), dopuszczalne.</span><span class="sxs-lookup"><span data-stu-id="60f95-127">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="60f95-128">Dopuszczalnego zakresu dla tej wartości to 1-100.</span><span class="sxs-lookup"><span data-stu-id="60f95-128">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="60f95-129">`<max-staleness-prefix>`W przypadku użycia z ograniczonym nieaktualności, ta wartość reprezentuje liczbę żądań starych dopuszczalne.</span><span class="sxs-lookup"><span data-stu-id="60f95-129">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="60f95-130">Dopuszczalnego zakresu dla tej wartości to 1 – 2 147 483 647.</span><span class="sxs-lookup"><span data-stu-id="60f95-130">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="60f95-131">`<resource-group-name>`Nazwa [grupy zasobów platformy Azure] [ azure-resource-groups] do której należy do nowego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-131">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-132">`<resource-group-location>`Lokalizacja grupy zasobów platformy Azure, do którego należy nowe konto bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-132">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-133">`<database-account-name>`Nazwa bazy danych Azure rozwiązania Cosmos konto bazy danych ma zostać utworzony.</span><span class="sxs-lookup"><span data-stu-id="60f95-133">`<database-account-name>` The name of the Azure Cosmos DB database account to be created.</span></span> <span data-ttu-id="60f95-134">Można używać tylko małe litery, cyfry, '-' znaków i musi zawierać od 3 do 50 znaków.</span><span class="sxs-lookup"><span data-stu-id="60f95-134">It can only use lowercase letters, numbers, the '-' character, and must be between 3 and 50 characters.</span></span>

<span data-ttu-id="60f95-135">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60f95-135">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a><span data-ttu-id="60f95-136">Uwagi</span><span class="sxs-lookup"><span data-stu-id="60f95-136">Notes</span></span>
* <span data-ttu-id="60f95-137">Powyższy przykład tworzy konto bazy danych z dwóch regionach.</span><span class="sxs-lookup"><span data-stu-id="60f95-137">The preceding example creates a database account with two regions.</span></span> <span data-ttu-id="60f95-138">Istnieje również możliwość utworzenia konta bazy danych z jednego regionu (który jest oznaczony jako regionu zapisu i ma wartość priorytetu trybu failover, 0) lub więcej niż dwóch regionach.</span><span class="sxs-lookup"><span data-stu-id="60f95-138">It is also possible to create a database account with either one region (which is designated as the write region and have a failover priority value of 0) or more than two regions.</span></span> <span data-ttu-id="60f95-139">Aby uzyskać więcej informacji, zobacz [konta bazy danych w przypadku][scaling-globally].</span><span class="sxs-lookup"><span data-stu-id="60f95-139">For more information, see [multi-region database accounts][scaling-globally].</span></span>
* <span data-ttu-id="60f95-140">Lokalizacje musi być regionów, w których bazy danych Azure rozwiązania Cosmos jest ogólnie dostępna.</span><span class="sxs-lookup"><span data-stu-id="60f95-140">The locations must be regions in which Azure Cosmos DB is generally available.</span></span> <span data-ttu-id="60f95-141">Bieżąca lista regionów znajduje się na [strony regiony platformy Azure](https://azure.microsoft.com/regions/#services).</span><span class="sxs-lookup"><span data-stu-id="60f95-141">The current list of regions is provided on the [Azure Regions page](https://azure.microsoft.com/regions/#services).</span></span>

## <span data-ttu-id="60f95-142"><a id="update-documentdb-account-powershell"></a>Aktualizacja konta bazy danych usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="60f95-142"><a id="update-documentdb-account-powershell"></a> Update a DocumentDB Database Account</span></span>

<span data-ttu-id="60f95-143">To polecenie umożliwia zaktualizowanie bazy danych Azure rozwiązania Cosmos właściwościach konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-143">This command allows you to update your Azure Cosmos DB database account properties.</span></span> <span data-ttu-id="60f95-144">W tym zasad zgodności i lokalizacje, w których istnieje konto bazy danych w.</span><span class="sxs-lookup"><span data-stu-id="60f95-144">This includes the consistency policy and the locations which the database account exists in.</span></span>

> [!NOTE]
> <span data-ttu-id="60f95-145">To polecenie umożliwia dodawanie i usuwanie regionów, ale nie zezwala na modyfikowanie priorytetów trybu failover.</span><span class="sxs-lookup"><span data-stu-id="60f95-145">This command allows you to add and remove regions but does not allow you to modify failover priorities.</span></span> <span data-ttu-id="60f95-146">Aby zmodyfikować priorytetów trybu failover, zobacz [poniżej](#modify-failover-priority-powershell).</span><span class="sxs-lookup"><span data-stu-id="60f95-146">To modify failover priorities, see [below](#modify-failover-priority-powershell).</span></span>

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* <span data-ttu-id="60f95-147">`<write-region-location>`Nazwa lokalizacji zapisu regionu konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-147">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="60f95-148">Ta lokalizacja musi mieć wartość 0 priorytet trybu failover.</span><span class="sxs-lookup"><span data-stu-id="60f95-148">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="60f95-149">Musi istnieć dokładnie jeden region zapisu na konto bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-149">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="60f95-150">`<read-region-location>`Nazwa lokalizacji obszaru odczytu konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-150">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="60f95-151">Ta lokalizacja musi być większa niż 0. wartość priorytetu trybu failover.</span><span class="sxs-lookup"><span data-stu-id="60f95-151">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="60f95-152">Może istnieć więcej niż jeden odczytu regiony dla danego konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-152">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="60f95-153">`<default-consistency-level>`Domyślny poziom spójności konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-153">`<default-consistency-level>` The default consistency level of the Azure Cosmos DB account.</span></span> <span data-ttu-id="60f95-154">Aby uzyskać więcej informacji, zobacz [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="60f95-154">For more information, see [Consistency Levels in Azure Cosmos DB](consistency-levels.md).</span></span>
* <span data-ttu-id="60f95-155">`<ip-range-filter>`Określa zbiór adresów IP i zakresów adresów IP w postaci CIDR do uwzględnienia jako lista dozwolonych adresów IP klienta, konto bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-155">`<ip-range-filter>` Specifies the set of IP addresses or IP address ranges in CIDR form to be included as the allowed list of client IPs for a given database account.</span></span> <span data-ttu-id="60f95-156">Zakresy adresów IP musi być przecinkami oddzielone i nie może zawierać spacji.</span><span class="sxs-lookup"><span data-stu-id="60f95-156">IP addresses/ranges must be comma separated and must not contain any spaces.</span></span> <span data-ttu-id="60f95-157">Aby uzyskać więcej informacji, zobacz [Obsługa zapory DB rozwiązania Cosmos Azure](firewall-support.md)</span><span class="sxs-lookup"><span data-stu-id="60f95-157">For more information, see [Azure Cosmos DB Firewall Support](firewall-support.md)</span></span>
* <span data-ttu-id="60f95-158">`<max-interval>`W przypadku użycia z ograniczonym nieaktualności, ta wartość przedstawia ilość czasu nieaktualności (w sekundach), dopuszczalne.</span><span class="sxs-lookup"><span data-stu-id="60f95-158">`<max-interval>` When used with Bounded Staleness consistency, this value represents the time amount of staleness (in seconds) tolerated.</span></span> <span data-ttu-id="60f95-159">Dopuszczalnego zakresu dla tej wartości to 1-100.</span><span class="sxs-lookup"><span data-stu-id="60f95-159">Accepted range for this value is 1 - 100.</span></span>
* <span data-ttu-id="60f95-160">`<max-staleness-prefix>`W przypadku użycia z ograniczonym nieaktualności, ta wartość reprezentuje liczbę żądań starych dopuszczalne.</span><span class="sxs-lookup"><span data-stu-id="60f95-160">`<max-staleness-prefix>` When used with Bounded Staleness consistency, this value represents the number of stale requests tolerated.</span></span> <span data-ttu-id="60f95-161">Dopuszczalnego zakresu dla tej wartości to 1 – 2 147 483 647.</span><span class="sxs-lookup"><span data-stu-id="60f95-161">Accepted range for this value is 1 – 2,147,483,647.</span></span>
* <span data-ttu-id="60f95-162">`<resource-group-name>`Nazwa [grupy zasobów platformy Azure] [ azure-resource-groups] do której należy do nowego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-162">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-163">`<resource-group-location>`Lokalizacja grupy zasobów platformy Azure, do którego należy nowe konto bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-163">`<resource-group-location>` The location of the Azure Resource Group to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-164">`<database-account-name>`Nazwa bazy danych Azure rozwiązania Cosmos konto bazy danych do zaktualizowania.</span><span class="sxs-lookup"><span data-stu-id="60f95-164">`<database-account-name>` The name of the Azure Cosmos DB database account to be updated.</span></span>

<span data-ttu-id="60f95-165">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60f95-165">Example:</span></span> 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <span data-ttu-id="60f95-166"><a id="delete-documentdb-account-powershell"></a>Usunięcie konta bazy danych usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="60f95-166"><a id="delete-documentdb-account-powershell"></a> Delete a DocumentDB Database Account</span></span>

<span data-ttu-id="60f95-167">To polecenie umożliwia usunięcie istniejącego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-167">This command allows you to delete an existing Azure Cosmos DB database account.</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* <span data-ttu-id="60f95-168">`<resource-group-name>`Nazwa [grupy zasobów platformy Azure] [ azure-resource-groups] do której należy do nowego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-168">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-169">`<database-account-name>`Nazwa bazy danych Azure rozwiązania Cosmos konto bazy danych do usunięcia.</span><span class="sxs-lookup"><span data-stu-id="60f95-169">`<database-account-name>` The name of the Azure Cosmos DB database account to be deleted.</span></span>

<span data-ttu-id="60f95-170">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60f95-170">Example:</span></span>

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="60f95-171"><a id="get-documentdb-properties-powershell"></a>Pobierz właściwości konta bazy danych usługi DocumentDB</span><span class="sxs-lookup"><span data-stu-id="60f95-171"><a id="get-documentdb-properties-powershell"></a> Get Properties of a DocumentDB Database Account</span></span>

<span data-ttu-id="60f95-172">To polecenie umożliwia uzyskiwanie właściwości istniejącego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-172">This command allows you to get the properties of an existing Azure Cosmos DB database account.</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="60f95-173">`<resource-group-name>`Nazwa [grupy zasobów platformy Azure] [ azure-resource-groups] do której należy do nowego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-173">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-174">`<database-account-name>`Nazwa bazy danych Azure rozwiązania Cosmos konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-174">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="60f95-175">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60f95-175">Example:</span></span>

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="60f95-176"><a id="update-tags-powershell"></a>Tagi aktualizacja konta bazy danych Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="60f95-176"><a id="update-tags-powershell"></a> Update Tags of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="60f95-177">Poniższy przykład zawiera opis sposobu ustawiania [tagi zasobów Azure] [ azure-resource-tags] dla Twojej bazy danych rozwiązania Cosmos Azure bazy danych konta.</span><span class="sxs-lookup"><span data-stu-id="60f95-177">The following example describes how to set [Azure resource tags][azure-resource-tags] for your Azure Cosmos DB database account.</span></span>

> [!NOTE]
> <span data-ttu-id="60f95-178">To polecenie może być łączone z poleceń create i update przez dołączenie `-Tags` flagę odpowiadającego mu parametru.</span><span class="sxs-lookup"><span data-stu-id="60f95-178">This command can be combined with the create or update commands by appending the `-Tags` flag with the corresponding parameter.</span></span>

<span data-ttu-id="60f95-179">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60f95-179">Example:</span></span>

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <span data-ttu-id="60f95-180"><a id="list-account-keys-powershell"></a>Lista kluczy konta</span><span class="sxs-lookup"><span data-stu-id="60f95-180"><a id="list-account-keys-powershell"></a> List Account Keys</span></span>

<span data-ttu-id="60f95-181">Podczas tworzenia konta bazy danych Azure rozwiązania Cosmos usługi generuje dwa klucze dostępu do głównego, które mogą być używane do uwierzytelniania podczas uzyskiwania dostępu do konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-181">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="60f95-182">Zapewniając dwa klucze dostępu do bazy danych rozwiązania Cosmos Azure umożliwia ponowne generowanie kluczy nie przeszkód do swojego konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-182">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> <span data-ttu-id="60f95-183">Dostępne są tylko do odczytu klucze do uwierzytelniania operacji tylko do odczytu.</span><span class="sxs-lookup"><span data-stu-id="60f95-183">Read-only keys for authenticating read-only operations are also available.</span></span> <span data-ttu-id="60f95-184">Istnieją dwa klucze odczytu i zapisu (podstawowych i pomocniczych) i dwa klucze tylko do odczytu (podstawowych i pomocniczych).</span><span class="sxs-lookup"><span data-stu-id="60f95-184">There are two read-write keys (primary and secondary) and two read-only keys (primary and secondary).</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="60f95-185">`<resource-group-name>`Nazwa [grupy zasobów platformy Azure] [ azure-resource-groups] do której należy do nowego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-185">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-186">`<database-account-name>`Nazwa bazy danych Azure rozwiązania Cosmos konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-186">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="60f95-187">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60f95-187">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="60f95-188"><a id="list-connection-strings-powershell"></a>Lista parametrów połączenia</span><span class="sxs-lookup"><span data-stu-id="60f95-188"><a id="list-connection-strings-powershell"></a> List Connection Strings</span></span>

<span data-ttu-id="60f95-189">Dla konta bazy danych MongoDB można pobrać parametry połączenia do łączenie aplikacji z bazy danych MongoDB konto bazy danych przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="60f95-189">For MongoDB accounts, the connection string to connect your MongoDB app to the database account can be retrieved using the following command.</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* <span data-ttu-id="60f95-190">`<resource-group-name>`Nazwa [grupy zasobów platformy Azure] [ azure-resource-groups] do której należy do nowego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-190">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-191">`<database-account-name>`Nazwa bazy danych Azure rozwiązania Cosmos konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-191">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="60f95-192">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60f95-192">Example:</span></span>

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <span data-ttu-id="60f95-193"><a id="regenerate-account-key-powershell"></a>Ponowne wygenerowanie klucza konta</span><span class="sxs-lookup"><span data-stu-id="60f95-193"><a id="regenerate-account-key-powershell"></a> Regenerate Account Key</span></span>

<span data-ttu-id="60f95-194">Należy zmienić klucze dostępu do konta bazy danych Azure rozwiązania Cosmos okresowo, aby zabezpieczyć połączenia.</span><span class="sxs-lookup"><span data-stu-id="60f95-194">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="60f95-195">Dwa klucze dostępu są przypisywane do utrzymania połączeń przy użyciu jednego klucza dostępu, jednocześnie ponownie generując drugi klucz dostępu konta bazy danych Azure rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-195">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* <span data-ttu-id="60f95-196">`<resource-group-name>`Nazwa [grupy zasobów platformy Azure] [ azure-resource-groups] do której należy do nowego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-196">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-197">`<database-account-name>`Nazwa bazy danych Azure rozwiązania Cosmos konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-197">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>
* <span data-ttu-id="60f95-198">`<key-kind>`Jeden z czterech typów kluczy: ["Primary" | " Pomocniczy "|" PrimaryReadonly "|" SecondaryReadonly"], który chcesz ponownie wygenerować.</span><span class="sxs-lookup"><span data-stu-id="60f95-198">`<key-kind>` One of the four types of keys: ["Primary"|"Secondary"|"PrimaryReadonly"|"SecondaryReadonly"] that you would like to regenerate.</span></span>

<span data-ttu-id="60f95-199">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60f95-199">Example:</span></span>

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <span data-ttu-id="60f95-200"><a id="modify-failover-priority-powershell"></a>Modyfikowanie priorytetów trybu Failover konta bazy danych Azure rozwiązania Cosmos bazy danych</span><span class="sxs-lookup"><span data-stu-id="60f95-200"><a id="modify-failover-priority-powershell"></a> Modify Failover Priority of an Azure Cosmos DB Database Account</span></span>

<span data-ttu-id="60f95-201">Dla konta w przypadku bazy danych można zmienić priorytet trybu failover różnych regionów, w których istnieje konto bazy danych Azure DB rozwiązania Cosmos w.</span><span class="sxs-lookup"><span data-stu-id="60f95-201">For multi-region database accounts, you can change the failover priority of the various regions which the Azure Cosmos DB database account exists in.</span></span> <span data-ttu-id="60f95-202">Aby uzyskać więcej informacji na tryb failover w konta bazy danych DB rozwiązania Cosmos Azure, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos][distribute-data-globally].</span><span class="sxs-lookup"><span data-stu-id="60f95-202">For more information on failover in your Azure Cosmos DB database account, see [Distribute data globally with Azure Cosmos DB][distribute-data-globally].</span></span>

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* <span data-ttu-id="60f95-203">`<write-region-location>`Nazwa lokalizacji zapisu regionu konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-203">`<write-region-location>` The location name of the write region of the database account.</span></span> <span data-ttu-id="60f95-204">Ta lokalizacja musi mieć wartość 0 priorytet trybu failover.</span><span class="sxs-lookup"><span data-stu-id="60f95-204">This location is required to have a failover priority value of 0.</span></span> <span data-ttu-id="60f95-205">Musi istnieć dokładnie jeden region zapisu na konto bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-205">There must be exactly one write region per database account.</span></span>
* <span data-ttu-id="60f95-206">`<read-region-location>`Nazwa lokalizacji obszaru odczytu konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-206">`<read-region-location>` The location name of the read region of the database account.</span></span> <span data-ttu-id="60f95-207">Ta lokalizacja musi być większa niż 0. wartość priorytetu trybu failover.</span><span class="sxs-lookup"><span data-stu-id="60f95-207">This location is required to have a failover priority value of greater than 0.</span></span> <span data-ttu-id="60f95-208">Może istnieć więcej niż jeden odczytu regiony dla danego konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-208">There can be more than one read regions per database account.</span></span>
* <span data-ttu-id="60f95-209">`<resource-group-name>`Nazwa [grupy zasobów platformy Azure] [ azure-resource-groups] do której należy do nowego konta bazy danych Azure DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="60f95-209">`<resource-group-name>` The name of the [Azure Resource Group][azure-resource-groups] to which the new Azure Cosmos DB database account belongs to.</span></span>
* <span data-ttu-id="60f95-210">`<database-account-name>`Nazwa bazy danych Azure rozwiązania Cosmos konta bazy danych.</span><span class="sxs-lookup"><span data-stu-id="60f95-210">`<database-account-name>` The name of the Azure Cosmos DB database account.</span></span>

<span data-ttu-id="60f95-211">Przykład:</span><span class="sxs-lookup"><span data-stu-id="60f95-211">Example:</span></span>

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a><span data-ttu-id="60f95-212">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="60f95-212">Next steps</span></span>

* <span data-ttu-id="60f95-213">Aby połączyć się przy użyciu platformy .NET, zobacz [Connect i zapytania z platformą .NET](create-documentdb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="60f95-213">To connect using .NET, see [Connect and query with .NET](create-documentdb-dotnet.md).</span></span>
* <span data-ttu-id="60f95-214">Nawiązywanie połączenia przy użyciu platformy .NET Core, zobacz [Connect i zapytania z platformą .NET Core](create-documentdb-dotnet-core.md).</span><span class="sxs-lookup"><span data-stu-id="60f95-214">To connect using .NET Core, see [Connect and query with .NET Core](create-documentdb-dotnet-core.md).</span></span>
* <span data-ttu-id="60f95-215">Nawiązywanie połączenia przy użyciu środowiska Node.js, zobacz [Connect i zapytania przy użyciu środowiska Node.js i aplikacji bazy danych MongoDB](create-mongodb-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="60f95-215">To connect using Node.js, see [Connect and query with Node.js and a MongoDB app](create-mongodb-nodejs.md).</span></span>

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
