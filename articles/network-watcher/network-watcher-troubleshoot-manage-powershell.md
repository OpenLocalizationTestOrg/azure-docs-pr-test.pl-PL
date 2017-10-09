---
title: "aaaTroubleshoot Brama sieci wirtualnej platformy Azure i połączeń - PowerShell | Dokumentacja firmy Microsoft"
description: "Ta strona wyjaśniono, jak toouse hello Azure obserwatora sieciowego Rozwiązywanie problemów z polecenia cmdlet programu PowerShell"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: f6f0a813-38b6-4a1f-8cfc-1dfdf979f595
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/19/2017
ms.author: gwallace
ms.openlocfilehash: b7dbe6e44e0fa1ea0481223a84098d7a57c068a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-virtual-network-gateway-and-connections-using-azure-network-watcher-powershell"></a>Rozwiązywanie problemów z Brama sieci wirtualnej i połączeń przy użyciu programu PowerShell obserwatora sieci platformy Azure

> [!div class="op_single_selector"]
> - [Portal](network-watcher-troubleshoot-manage-portal.md)
> - [PowerShell](network-watcher-troubleshoot-manage-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-troubleshoot-manage-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-troubleshoot-manage-cli.md)
> - [Interfejs API REST](network-watcher-troubleshoot-manage-rest.md)

Obserwatora sieciowego zawiera wiele funkcji, co wiąże toounderstanding zasobów sieciowych na platformie Azure. Jeden z tych funkcji jest zasobem rozwiązywania problemów. Rozwiązywanie problemów z zasobów można wywołać za pomocą portalu hello, programu PowerShell, interfejsu wiersza polecenia lub interfejsu API REST. Po wywołaniu, obserwatora sieciowego sprawdza kondycję hello Brama sieci wirtualnej lub połączenie i zwraca jego wyniki.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego.

Lista odwiedziny typy obsługiwanych bramy [bramy obsługiwane typy](network-watcher-troubleshoot-overview.md#supported-gateway-types).

## <a name="overview"></a>Omówienie

Rozwiązywanie problemów z zasobów umożliwia określenie hello rozwiązywania problemów, które wynikają z bramy sieci wirtualnej i połączenia. Po wysłaniu żądania jest rozwiązywanie problemów z tooresource, dzienniki są proszeni i inspekcji. Po zakończeniu kontroli hello są zwracane. Zasób, którego rozwiązywania problemów z żądania to długo działające żądania, może to potrwać kilka minut tooreturn wynik. Dzienniki Hello z Rozwiązywanie problemów z są przechowywane w kontenerze na koncie magazynu, który jest określony.

## <a name="retrieve-network-watcher"></a>Pobrać obserwatora sieciowego

pierwszym krokiem Hello jest tooretrieve hello obserwatora sieciowego wystąpienia. Witaj `$networkWatcher` zmienna jest przekazywana toohello `Start-AzureRmNetworkWatcherResourceTroubleshooting` polecenia cmdlet w kroku 4.

```powershell
$nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq "WestCentralUS" } 
$networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName 
```

## <a name="retrieve-a-virtual-network-gateway-connection"></a>Pobieranie połączenia bramy sieci wirtualnej

W tym przykładzie Rozwiązywanie problemów z zasobów jest są uruchomione na połączenie. Można również przekazać go Brama sieci wirtualnej.

```powershell
$connection = Get-AzureRmVirtualNetworkGatewayConnection -Name "2to3" -ResourceGroupName "testrg"
```

## <a name="create-a-storage-account"></a>Tworzenie konta magazynu

Rozwiązywanie problemów z zasobów zwraca dane dotyczące kondycji hello hello zasobu, zapisuje dzienniki tooa magazynu konta toobe sprawdzone. W tym kroku utworzymy konta magazynu, jeśli istnieje już konto magazynu można go.

```powershell
$sa = New-AzureRmStorageAccount -Name "contosoexamplesa" -SKU "Standard_LRS" -ResourceGroupName "testrg" -Location "WestCentralUS"
Set-AzureRmCurrentStorageAccount -ResourceGroupName $sa.ResourceGroupName -Name $sa.StorageAccountName
$sc = New-AzureStorageContainer -Name logs
```

## <a name="run-network-watcher-resource-troubleshooting"></a>Uruchom Rozwiązywanie problemów z zasobów obserwatora sieciowego

Rozwiązywanie problemów z zasobami za pomocą hello `Start-AzureRmNetworkWatcherResourceTroubleshooting` polecenia cmdlet. Jest przekazywana hello polecenia cmdlet hello obserwatora sieciowego obiektu, hello identyfikator hello połączenia lub brama sieci wirtualnej, identyfikator konta magazynu hello i hello ścieżki toostore hello wyników.

> [!NOTE]
> Witaj `Start-AzureRmNetworkWatcherResourceTroubleshooting` jest długo działające i może potrwać kilka minut toocomplete polecenia cmdlet.

```powershell
Start-AzureRmNetworkWatcherResourceTroubleshooting -NetworkWatcher $networkWatcher -TargetResourceId $connection.Id -StorageId $sa.Id -StoragePath "$($sa.PrimaryEndpoints.Blob)$($sc.name)"
```

Po uruchomieniu polecenia cmdlet hello obserwatora sieciowego przegląda hello zasobów tooverify hello kondycji. Zwraca wyniki hello toohello powłoki, a są przechowywane dzienniki hello wyników na koncie magazynu hello określony.

## <a name="understanding-hello-results"></a>Opis wyników hello

tekst akcji Hello zawiera ogólne wskazówki dotyczące sposobu tooresolve hello problem. Jeśli hello problemu można podjąć akcję, link jest dostarczany z dodatkowych wskazówek. W przypadku hello w przypadku, gdy nie ma żadnych dodatkowych wskazówek, odpowiedź hello zapewnia tooopen adres url hello sprawy pomocy technicznej.  Aby uzyskać więcej informacji o właściwościach hello hello odpowiedzi i dostępnych, odwiedź stronę [Rozwiązywanie problemów z obserwatora sieciowego — omówienie](network-watcher-troubleshoot-overview.md)

Aby uzyskać instrukcje dotyczące pobierania plików z kontami magazynu azure, zobacz zbyt[Rozpoczynanie pracy z magazynem obiektów Blob platformy Azure przy użyciu platformy .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Kolejnym narzędziem, który może służyć jest Eksploratora usługi Storage. Więcej informacji na temat Eksploratora usługi Storage można znaleźć tutaj na powitania następującego łącza: [Eksploratora usługi Storage](http://storageexplorer.com/)

## <a name="next-steps"></a>Następne kroki

Jeśli ustawienia zostały zmienione które zatrzymania połączenia sieci VPN, zobacz [Zarządzaj grupami zabezpieczeń sieci](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack dół hello reguły zabezpieczeń sieciowych grupy i zabezpieczeń, które mogą być zagrożona.
