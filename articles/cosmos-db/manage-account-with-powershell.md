---
title: "aaaAzure automatyzacji DB rozwiązania Cosmos — zarządzanie za pomocą programu Powershell | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 3239fb815918a0e47bff69fcd1ab6562519e429b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-cosmos-db-account-using-powershell"></a>Tworzenie konta bazy danych rozwiązania Cosmos Azure przy użyciu programu PowerShell

Witaj następujący przewodnik zawiera opis zarządzania tooautomate poleceń Azure DB rozwiązania Cosmos konta bazy danych przy użyciu programu Azure Powershell. Zawiera także klucze konta toomanage poleceń i priorytetów trybu failover w [konta bazy danych w przypadku][scaling-globally]. Aktualizacja konta bazy danych pozwala toomodify spójności zasad, Dodaj lub usuń regionów. Do zarządzania i platform konta bazy danych rozwiązania Cosmos platformy Azure, możesz użyć dowolnej [interfejsu wiersza polecenia Azure](cli-samples.md), hello [interfejsu API REST dostawcy zasobów][rp-rest-api], lub hello [Azure Portal](create-documentdb-dotnet.md#create-account).

## <a name="getting-started"></a>Wprowadzenie

Postępuj zgodnie z instrukcjami hello [jak tooinstall i konfigurowanie programu Azure PowerShell] [ powershell-install-configure] tooinstall i zaloguj się tooyour usługi Azure Resource Manager konta w programie Powershell.

### <a name="notes"></a>Uwagi

* Jeśli chcesz hello tooexecute następujące polecenia, bez konieczności potwierdzenie dołączenia hello `-Force` Flaga toohello polecenia.
* Wszystkie hello następujące polecenia są synchroniczne.

## <a id="create-documentdb-account-powershell"></a>Tworzenie konta usługi Azure rozwiązania Cosmos bazy danych

To polecenie umożliwia toocreate konto bazy danych Azure DB rozwiązania Cosmos. Konfigurowanie nowego konta bazy danych jako albo jednym regionie lub [w przypadku] [ scaling-globally] niektóre [spójności zasad](consistency-levels.md).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name>  -Location "<resource-group-location>" -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`Nazwa lokalizacji Hello hello zapisu region hello konta bazy danych. Ta lokalizacja jest wymagana toohave wartość priorytetu trybu failover 0. Musi istnieć dokładnie jeden region zapisu na konto bazy danych.
* `<read-region-location>`Nazwa lokalizacji Hello hello odczytać region hello konta bazy danych. Ta lokalizacja jest wymagana toohave większa niż 0. wartość priorytetu trybu failover. Może istnieć więcej niż jeden odczytu regiony dla danego konta bazy danych.
* `<ip-range-filter>`Określa hello zbiór adresów IP i zakresów adresów IP CIDR formularza toobe uwzględnione jako hello białej listy adresów IP klienta, konto bazy danych. Zakresy adresów IP musi być przecinkami oddzielone i nie może zawierać spacji. Aby uzyskać więcej informacji, zobacz [Obsługa zapory DB rozwiązania Cosmos Azure](firewall-support.md)
* `<default-consistency-level>`Witaj poziom spójności domyślne hello konta bazy danych Azure rozwiązania Cosmos. Aby uzyskać więcej informacji, zobacz [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).
* `<max-interval>`W przypadku użycia z ograniczonym nieaktualności, ta wartość oznacza hello czasu ilość nieaktualności (w sekundach) dopuszczalne. Dopuszczalnego zakresu dla tej wartości to 1-100.
* `<max-staleness-prefix>`W przypadku użycia z ograniczonym nieaktualności, ta wartość przedstawia hello liczbę żądań starych dopuszczalne. Dopuszczalnego zakresu dla tej wartości to 1 – 2 147 483 647.
* `<resource-group-name>`Nazwa Hello hello [grupy zasobów platformy Azure] [ azure-resource-groups] toowhich hello nowej bazy danych Azure rozwiązania Cosmos bazy danych należy do.
* `<resource-group-location>`Lokalizacja Hello hello grupy zasobów platformy Azure toowhich hello nowej bazy danych Azure rozwiązania Cosmos konto bazy danych należy.
* `<database-account-name>`Nazwa Hello hello Azure DB rozwiązania Cosmos bazy danych konta toobe utworzony. Można używać tylko małe litery, cyfry, hello '-' znaków i musi zawierać od 3 do 50 znaków.

Przykład: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    New-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Location "West US" -Name "docdb-test" -Properties $CosmosDBProperties

### <a name="notes"></a>Uwagi
* Witaj poprzednim przykładzie tworzy konto bazy danych z dwóch regionach. Możliwe jest również możliwe toocreate konta bazy danych z jednego regionu (który jest oznaczony jako hello zapisu regionu i ma wartość priorytetu trybu failover, 0) lub więcej niż dwóch regionach. Aby uzyskać więcej informacji, zobacz [konta bazy danych w przypadku][scaling-globally].
* lokalizacje Hello musi być regionów, w których bazy danych Azure rozwiązania Cosmos jest ogólnie dostępna. Witaj bieżącą listę regionów znajduje się na powitania [strony regiony platformy Azure](https://azure.microsoft.com/regions/#services).

## <a id="update-documentdb-account-powershell"></a>Aktualizacja konta bazy danych usługi DocumentDB

To polecenie umożliwia tooupdate właściwości konta bazy danych z bazy danych Azure rozwiązania Cosmos. Obejmuje to hello spójności zasad i lokalizacje hello istnieje konto bazy danych, które hello w.

> [!NOTE]
> To polecenie umożliwia tooadd i Usuń regionów, ale nie zezwala toomodify priorytetów trybu failover. toomodify priorytetów trybu failover, zobacz [poniżej](#modify-failover-priority-powershell).

    $locations = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0}, @{"locationName"="<read-region-location>"; "failoverPriority"=1})
    $iprangefilter = "<ip-range-filter>"
    $consistencyPolicy = @{"defaultConsistencyLevel"="<default-consistency-level>"; "maxIntervalInSeconds"="<max-interval>"; "maxStalenessPrefix"="<max-staleness-prefix>"}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName <resource-group-name> -Name <database-account-name> -Properties $CosmosDBProperties
    
* `<write-region-location>`Nazwa lokalizacji Hello hello zapisu region hello konta bazy danych. Ta lokalizacja jest wymagana toohave wartość priorytetu trybu failover 0. Musi istnieć dokładnie jeden region zapisu na konto bazy danych.
* `<read-region-location>`Nazwa lokalizacji Hello hello odczytać region hello konta bazy danych. Ta lokalizacja jest wymagana toohave większa niż 0. wartość priorytetu trybu failover. Może istnieć więcej niż jeden odczytu regiony dla danego konta bazy danych.
* `<default-consistency-level>`Witaj poziom spójności domyślne hello konta bazy danych Azure rozwiązania Cosmos. Aby uzyskać więcej informacji, zobacz [poziomów spójności w usłudze Azure DB rozwiązania Cosmos](consistency-levels.md).
* `<ip-range-filter>`Określa hello zbiór adresów IP i zakresów adresów IP CIDR formularza toobe uwzględnione jako hello białej listy adresów IP klienta, konto bazy danych. Zakresy adresów IP musi być przecinkami oddzielone i nie może zawierać spacji. Aby uzyskać więcej informacji, zobacz [Obsługa zapory DB rozwiązania Cosmos Azure](firewall-support.md)
* `<max-interval>`W przypadku użycia z ograniczonym nieaktualności, ta wartość oznacza hello czasu ilość nieaktualności (w sekundach) dopuszczalne. Dopuszczalnego zakresu dla tej wartości to 1-100.
* `<max-staleness-prefix>`W przypadku użycia z ograniczonym nieaktualności, ta wartość przedstawia hello liczbę żądań starych dopuszczalne. Dopuszczalnego zakresu dla tej wartości to 1 – 2 147 483 647.
* `<resource-group-name>`Nazwa Hello hello [grupy zasobów platformy Azure] [ azure-resource-groups] toowhich hello nowej bazy danych Azure rozwiązania Cosmos bazy danych należy do.
* `<resource-group-location>`Lokalizacja Hello hello grupy zasobów platformy Azure toowhich hello nowej bazy danych Azure rozwiązania Cosmos konto bazy danych należy.
* `<database-account-name>`Nazwa Hello hello Azure DB rozwiązania Cosmos bazy danych konta toobe aktualizacji.

Przykład: 

    $locations = @(@{"locationName"="West US"; "failoverPriority"=0}, @{"locationName"="East US"; "failoverPriority"=1})
    $iprangefilter = ""
    $consistencyPolicy = @{"defaultConsistencyLevel"="BoundedStaleness"; "maxIntervalInSeconds"=5; "maxStalenessPrefix"=100}
    $CosmosDBProperties = @{"databaseAccountOfferType"="Standard"; "locations"=$locations; "consistencyPolicy"=$consistencyPolicy; "ipRangeFilter"=$iprangefilter}
    Set-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Properties $CosmosDBProperties

## <a id="delete-documentdb-account-powershell"></a>Usunięcie konta bazy danych usługi DocumentDB

To polecenie umożliwia toodelete istniejącego konta bazy danych Azure DB rozwiązania Cosmos.

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"
    
* `<resource-group-name>`Nazwa Hello hello [grupy zasobów platformy Azure] [ azure-resource-groups] toowhich hello nowej bazy danych Azure rozwiązania Cosmos bazy danych należy do.
* `<database-account-name>`Nazwa Hello hello Azure DB rozwiązania Cosmos bazy danych konta toobe usunięte.

Przykład:

    Remove-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="get-documentdb-properties-powershell"></a>Pobierz właściwości konta bazy danych usługi DocumentDB

To polecenie umożliwia tooget hello właściwości istniejącego konta bazy danych Azure DB rozwiązania Cosmos.

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Nazwa Hello hello [grupy zasobów platformy Azure] [ azure-resource-groups] toowhich hello nowej bazy danych Azure rozwiązania Cosmos bazy danych należy do.
* `<database-account-name>`Nazwa Hello hello Azure DB rozwiązania Cosmos konta bazy danych.

Przykład:

    Get-AzureRmResource -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="update-tags-powershell"></a>Tagi aktualizacja konta bazy danych Azure rozwiązania Cosmos bazy danych

Witaj poniższy przykład zawiera opis sposobu tooset [tagi zasobów Azure] [ azure-resource-tags] dla Twojej bazy danych rozwiązania Cosmos Azure bazy danych konta.

> [!NOTE]
> To polecenie może być łączone z hello Utwórz lub zaktualizuj polecenia przez dołączenie hello `-Tags` flagę hello odpowiadającego mu parametru.

Przykład:

    $tags = @{"dept" = "Finance”; environment = “Production”}
    Set-AzureRmResource -ResourceType “Microsoft.DocumentDB/databaseAccounts”  -ResourceGroupName "rg-test" -Name "docdb-test" -Tags $tags

## <a id="list-account-keys-powershell"></a>Lista kluczy konta

Podczas tworzenia konta bazy danych Azure rozwiązania Cosmos usługi hello generuje dwa klucze dostępu do głównego, które mogą być używane do uwierzytelniania podczas uzyskiwania dostępu do hello konta bazy danych Azure rozwiązania Cosmos. Zapewniając dwa klucze dostępu do bazy danych Azure rozwiązania Cosmos umożliwia tooregenerate hello klucze z nie przeszkód tooyour konta bazy danych Azure rozwiązania Cosmos. Dostępne są tylko do odczytu klucze do uwierzytelniania operacji tylko do odczytu. Istnieją dwa klucze odczytu i zapisu (podstawowych i pomocniczych) i dwa klucze tylko do odczytu (podstawowych i pomocniczych).

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Nazwa Hello hello [grupy zasobów platformy Azure] [ azure-resource-groups] toowhich hello nowej bazy danych Azure rozwiązania Cosmos bazy danych należy do.
* `<database-account-name>`Nazwa Hello hello Azure DB rozwiązania Cosmos konta bazy danych.

Przykład:

    $keys = Invoke-AzureRmResourceAction -Action listKeys -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="list-connection-strings-powershell"></a>Lista parametrów połączenia

W przypadku bazy danych MongoDB kont hello tooconnect ciąg połączenia, który można pobrać konta bazy danych MongoDB toohello aplikacji za pomocą następującego polecenia hello.

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>"

* `<resource-group-name>`Nazwa Hello hello [grupy zasobów platformy Azure] [ azure-resource-groups] toowhich hello nowej bazy danych Azure rozwiązania Cosmos bazy danych należy do.
* `<database-account-name>`Nazwa Hello hello Azure DB rozwiązania Cosmos konta bazy danych.

Przykład:

    $keys = Invoke-AzureRmResourceAction -Action listConnectionStrings -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test"

## <a id="regenerate-account-key-powershell"></a>Ponowne wygenerowanie klucza konta

Należy zmienić hello dostępu do kluczy tooyour bazy danych Azure rozwiązania Cosmos konta okresowo toohelp zabezpieczania połączeń. Dwa klucze dostępu są przypisane tooenable możesz toomaintain połączeń toohello konta bazy danych Azure rozwiązania Cosmos przy użyciu jednego klucza dostępu, jednocześnie ponownie generując hello drugi klucz dostępu.

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"keyKind"="<key-kind>"}

* `<resource-group-name>`Nazwa Hello hello [grupy zasobów platformy Azure] [ azure-resource-groups] toowhich hello nowej bazy danych Azure rozwiązania Cosmos bazy danych należy do.
* `<database-account-name>`Nazwa Hello hello Azure DB rozwiązania Cosmos konta bazy danych.
* `<key-kind>`Jeden z typów hello czterech kluczy: ["Primary" | " Pomocniczy "|" PrimaryReadonly "|" SecondaryReadonly"] ma tooregenerate.

Przykład:

    Invoke-AzureRmResourceAction -Action regenerateKey -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"keyKind"="Primary"}

## <a id="modify-failover-priority-powershell"></a>Modyfikowanie priorytetów trybu Failover konta bazy danych Azure rozwiązania Cosmos bazy danych

Dla konta w przypadku bazy danych można zmienić priorytet trybu failover hello hello w różnych regionach, które hello Azure DB rozwiązania Cosmos bazy danych konta istnieje w. Aby uzyskać więcej informacji na tryb failover w konta bazy danych DB rozwiązania Cosmos Azure, zobacz [dystrybucji danych globalnie z bazy danych Azure rozwiązania Cosmos][distribute-data-globally].

    $failoverPolicies = @(@{"locationName"="<write-region-location>"; "failoverPriority"=0},@{"locationName"="<read-region-location>"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "<resource-group-name>" -Name "<database-account-name>" -Parameters @{"failoverPolicies"=$failoverPolicies}

* `<write-region-location>`Nazwa lokalizacji Hello hello zapisu region hello konta bazy danych. Ta lokalizacja jest wymagana toohave wartość priorytetu trybu failover 0. Musi istnieć dokładnie jeden region zapisu na konto bazy danych.
* `<read-region-location>`Nazwa lokalizacji Hello hello odczytać region hello konta bazy danych. Ta lokalizacja jest wymagana toohave większa niż 0. wartość priorytetu trybu failover. Może istnieć więcej niż jeden odczytu regiony dla danego konta bazy danych.
* `<resource-group-name>`Nazwa Hello hello [grupy zasobów platformy Azure] [ azure-resource-groups] toowhich hello nowej bazy danych Azure rozwiązania Cosmos bazy danych należy do.
* `<database-account-name>`Nazwa Hello hello Azure DB rozwiązania Cosmos konta bazy danych.

Przykład:

    $failoverPolicies = @(@{"locationName"="East US"; "failoverPriority"=0},@{"locationName"="West US"; "failoverPriority"=1})
    Invoke-AzureRmResourceAction -Action failoverPriorityChange -ResourceType "Microsoft.DocumentDb/databaseAccounts" -ApiVersion "2015-04-08" -ResourceGroupName "rg-test" -Name "docdb-test" -Parameters @{"failoverPolicies"=$failoverPolicies}

## <a name="next-steps"></a>Następne kroki

* tooconnect przy użyciu platformy .NET, zobacz [Connect i zapytania z platformą .NET](create-documentdb-dotnet.md).
* tooconnect przy użyciu platformy .NET Core, zobacz [Connect i zapytania z platformą .NET Core](create-documentdb-dotnet-core.md).
* tooconnect przy użyciu środowiska Node.js, zobacz [Connect i zapytania przy użyciu środowiska Node.js i aplikacji bazy danych MongoDB](create-mongodb-nodejs.md).

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[powershell-install-configure]: https://docs.microsoft.com/azure/powershell-install-configure
[scaling-globally]: distribute-data-globally.md#EnableGlobalDistribution
[distribute-data-globally]: distribute-data-globally.md
[azure-resource-groups]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups
[azure-resource-tags]: https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags
[rp-rest-api]: https://docs.microsoft.com/rest/api/documentdbresourceprovider/
