---
title: "aaaAzure wspólnej metryki automatycznego skalowania Monitor | Dokumentacja firmy Microsoft"
description: "Dowiedz się, metryk, które są często używane do skalowania automatycznego usługi w chmurze, maszyn wirtualnych i aplikacji sieci Web."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 189b2a13-01c8-4aca-afd5-90711903ca59
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/6/2016
ms.author: ancav
ms.openlocfilehash: 372a40d72d7a6c22c5ff854b1460ec8a3b7ed1d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor-autoscaling-common-metrics"></a>Azure metryki wspólnej Skalowanie automatyczne monitora
Azure Monitor Skalowanie automatyczne pozwala tooscale hello liczba uruchomionych wystąpień w górę lub w dół, na podstawie danych telemetrycznych (metryk). W tym dokumencie opisano typowe metryki można toouse. W hello portalu Azure dla farmy serwerów i usług w chmurze można wybrać metryki hello hello tooscale zasobów przez. Jednak możesz również wszystkie metryki z różnych zasobów tooscale przez.

Azure Monitor skalowania automatycznego ma zastosowanie tylko zbyt[zestawy skalowania maszyny wirtualnej](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [usługi w chmurze](https://azure.microsoft.com/services/cloud-services/), i [usługi aplikacji — aplikacje sieci Web](https://azure.microsoft.com/services/app-service/web/). Innymi usługami Azure, użyj metod skalowania.

## <a name="compute-metrics-for-resource-manager-based-vms"></a>Obliczanie metryki dla maszyn wirtualnych w Menedżerze zasobów
Domyślnie maszyn wirtualnych z systemem Resource Manager i zestawy skalowania maszyny wirtualnej Emituj podstawowe metryki (poziomie hosta). Ponadto podczas konfigurowania funkcji zbierania danych diagnostycznych dla maszyny Wirtualnej platformy Azure i VMSS hello rozszerzenie diagnostyki Azure również emituje liczników wydajności systemu operacyjnego gościa (często nazywana "Systemu operacyjnego gościa metryki").  Za pomocą tych metryk w reguł skalowania automatycznego.

Można użyć hello `Get MetricDefinitions` dostępnych dla zasobu VMSS metryk hello tooview interfejsu API/PoSH/interfejsu wiersza polecenia.

Jeśli używasz zestawy skalowania maszyny Wirtualnej i nie widzisz określonej metryki na liście, a następnie prawdopodobnie *wyłączone* Twojego rozszerzenia diagnostyki.

Jeśli w określonej metryki nie jest częstotliwość próbki lub przeniesione na powitania, należy zaktualizować hello konfiguracji diagnostyki.

W przypadku obu powyższych przypadkach ma wartość true, następnie przejrzyj [tooenable Użyj programu PowerShell diagnostyki Azure na maszynie wirtualnej z systemem Windows](../virtual-machines/windows/ps-extensions-diagnostics.md) o tooconfigure środowiska PowerShell i aktualizacja Twojego tooenable rozszerzenia diagnostyki maszyny Wirtualnej Azure hello metryki. Ten artykuł zawiera także przykładowy plik konfiguracyjny diagnostyki.

### <a name="host-metrics-for-resource-manager-based-windows-and-linux-vms"></a>Metryki hosta dla Menedżera zasobów systemu Windows i maszyn wirtualnych systemu Linux
Witaj następujące metryki na poziomie hosta są emitowane domyślnie dla maszyny Wirtualnej platformy Azure i VMSS w systemach Windows i Linux wystąpień. Te metryki pokazują maszyny Wirtualnej Azure, ale są zbierane z hosta maszyny Wirtualnej Azure hello, a nie za pomocą agenta zainstalowanego na powitania gościa maszyny Wirtualnej. Możesz użyć tych metryk w regułach Skalowanie automatyczne.

- [Metryki hosta dla Menedżera zasobów systemu Windows i maszyn wirtualnych systemu Linux](monitoring-supported-metrics.md#microsoftcomputevirtualmachines)
- [Metryki hosta dla Menedżera zasobów systemu Windows i zestawy skalowania maszyny Wirtualnej systemu Linux](monitoring-supported-metrics.md#microsoftcomputevirtualmachinescalesets)

### <a name="guest-os-metrics-resource-manager-based-windows-vms"></a>Metryki systemu operacyjnego gościa maszyn wirtualnych Menedżera zasobów systemu Windows
Po utworzeniu maszyny Wirtualnej na platformie Azure diagnostics jest włączona przy użyciu rozszerzenia diagnostyki hello. rozszerzenia diagnostyki Hello emituje zestawu metryki pobranych z wewnątrz hello maszyny Wirtualnej. Oznacza to, że skalowanie automatyczne wylogowuje metryki, które nie są emitowane przez domyślny.

Za pomocą następującego polecenia programu PowerShell hello można wygenerować listy hello metryki.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Można utworzyć alertu dotyczącego hello następujące metryki:

| Nazwa metryki | Jednostka |
| --- | --- |
| \Processor(_Total)\% Processor Time |Procent |
| \Processor(_Total)\% czas uprzywilejowany |Procent |
| \Processor(_Total)\% czas użytkownika |Procent |
| Częstotliwość \Processor informacji (_Total) \Processor |Licznik |
| \System\Processes |Licznik |
| Liczba \Thread \Process (_Total) |Licznik |
| Liczba \Handle \Process (_Total) |Licznik |
| \Memory\% Zadeklarowane bajty w użyciu |Procent |
| \Memory\Available Bytes |Bajty |
| \Memory\Committed bajtów |Bajty |
| \Memory\Commit limit |Bajty |
| \Memory\Pool stronicowanej |Bajty |
| \Memory\Pool puli niestronicowanej |Bajty |
| \PhysicalDisk(_Total)\% czas na dysku |Procent |
| \PhysicalDisk(_Total)\% czas odczytu z dysku |Procent |
| \PhysicalDisk(_Total)\% czas zapisu na dysku |Procent |
| Transfery \Disk \PhysicalDisk (_Total) na sekundę |CountPerSecond |
| Odczyty \Disk \PhysicalDisk (_Total) na sekundę |CountPerSecond |
| Zapisy \Disk \PhysicalDisk (_Total) na sekundę |CountPerSecond |
| \Disk \PhysicalDisk (_Total) bajty/s |BytesPerSecond |
| Bajty odczytane/s \Disk \PhysicalDisk (_Total) |BytesPerSecond |
| Bajty zapisu \Disk \PhysicalDisk (_Total) / s |BytesPerSecond |
| \Avg \PhysicalDisk (_Total) Długość kolejki dysku |Licznik |
| \Avg \PhysicalDisk (_Total) Długość kolejki odczytu dysku |Licznik |
| \Avg \PhysicalDisk (_Total) Długość kolejki dysku zapisu |Licznik |
| \LogicalDisk(_Total)\% wolnego miejsca |Procent |
| Megabajtów \Free \LogicalDisk (_Total) |Licznik |

### <a name="guest-os-metrics-linux-vms"></a>Metryki systemu operacyjnego gościa maszyn wirtualnych systemu Linux
Po utworzeniu maszyny Wirtualnej na platformie Azure diagnostics jest domyślnie włączona przy użyciu rozszerzenia diagnostyki.

Za pomocą następującego polecenia programu PowerShell hello można wygenerować listy hello metryki.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

 Można utworzyć alertu dotyczącego hello następujące metryki:

| Nazwa metryki | Jednostka |
| --- | --- |
| \Memory\AvailableMemory |Bajty |
| \Memory\PercentAvailableMemory |Procent |
| \Memory\UsedMemory |Bajty |
| \Memory\PercentUsedMemory |Procent |
| \Memory\PercentUsedByCache |Procent |
| \Memory\PagesPerSec |CountPerSecond |
| \Memory\PagesReadPerSec |CountPerSecond |
| \Memory\PagesWrittenPerSec |CountPerSecond |
| \Memory\AvailableSwap |Bajty |
| \Memory\PercentAvailableSwap |Procent |
| \Memory\UsedSwap |Bajty |
| \Memory\PercentUsedSwap |Procent |
| \Processor\PercentIdleTime |Procent |
| \Processor\PercentUserTime |Procent |
| \Processor\PercentNiceTime |Procent |
| \Processor\PercentPrivilegedTime |Procent |
| \Processor\PercentInterruptTime |Procent |
| \Processor\PercentDPCTime |Procent |
| \Processor\PercentProcessorTime |Procent |
| \Processor\PercentIOWaitTime |Procent |
| \PhysicalDisk\BytesPerSecond |BytesPerSecond |
| \PhysicalDisk\ReadBytesPerSecond |BytesPerSecond |
| \PhysicalDisk\WriteBytesPerSecond |BytesPerSecond |
| \PhysicalDisk\TransfersPerSecond |CountPerSecond |
| \PhysicalDisk\ReadsPerSecond |CountPerSecond |
| \PhysicalDisk\WritesPerSecond |CountPerSecond |
| \PhysicalDisk\AverageReadTime |Sekundy |
| \PhysicalDisk\AverageWriteTime |Sekundy |
| \PhysicalDisk\AverageTransferTime |Sekundy |
| \PhysicalDisk\AverageDiskQueueLength |Licznik |
| \NetworkInterface\BytesTransmitted |Bajty |
| \NetworkInterface\BytesReceived |Bajty |
| \NetworkInterface\PacketsTransmitted |Licznik |
| \NetworkInterface\PacketsReceived |Licznik |
| \NetworkInterface\BytesTotal |Bajty |
| \NetworkInterface\TotalRxErrors |Licznik |
| \NetworkInterface\TotalTxErrors |Licznik |
| \NetworkInterface\TotalCollisions |Licznik |

## <a name="commonly-used-web-server-farm-metrics"></a>Często używane metryki sieci Web (farmy serwerów)
Można także przeprowadzić automatycznego skalowania w oparciu o wspólne metryki serwera sieci web, takich jak hello długość kolejki Http. Nazwa metryki jego jest **HttpQueueLength**.  powitania po sekcji listy dostępnego serwera w farmie (aplikacje sieci Web) metryki.

### <a name="web-apps-metrics"></a>Metryki aplikacji sieci Web
Za pomocą następującego polecenia programu PowerShell hello można wygenerować listy hello metryki aplikacji sieci Web.

```
Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit
```

Możesz alert po wystąpieniu lub skalowania przez te metryki.

| Nazwa metryki | Jednostka |
| --- | --- |
| CpuPercentage |Procent |
| MemoryPercentage |Procent |
| DiskQueueLength |Licznik |
| HttpQueueLength |Licznik |
| BytesReceived |Bajty |
| Żądania |Bajty |

## <a name="commonly-used-storage-metrics"></a>Często używane metryki magazynu
Możesz skalować długości kolejki magazynu, czyli hello liczba wiadomości w kolejce magazynu hello. Długość kolejki magazynu to specjalne metryki i próg hello jest hello liczbę komunikatów dla każdego wystąpienia. Na przykład jeśli istnieją dwa wystąpienia i próg hello wartość too100, skalowanie występuje hello całkowita liczba wiadomości w kolejce hello 200. Który może być 100 komunikaty dla każdego wystąpienia, 120 i 80 lub wszelkie inne kombinacje dodające too200 lub więcej.

Skonfiguruj to ustawienie w hello portalu Azure w hello **ustawienia** bloku. W przypadku zestawy skalowania maszyny Wirtualnej, można aktualizować ustawieniu skalowania automatycznego hello w toouse szablonu usługi Resource Manager hello *metricName* jako *ApproximateMessageCount* i podaj identyfikator hello kolejki magazynu hello jako  *metricResourceUri*.

Na przykład z hello klasycznego konta magazynu obejmują metricTrigger Ustawienia skalowania automatycznego:

```
"metricName": "ApproximateMessageCount",
 "metricNamespace": "",
 "metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ClassicStorage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
 ```

Konto magazynu (z systemem innym niż klasyczne) hello metricTrigger zadania obejmują:

```
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.Storage/storageAccounts/STORAGE_ACCOUNT_NAME/services/queue/queues/QUEUE_NAME"
```

## <a name="commonly-used-service-bus-metrics"></a>Często używane metryki usługi Service Bus
Możesz skalować według długość kolejki usługi Service Bus, która jest hello liczba wiadomości powitania kolejki usługi Service Bus. Długość kolejki usługi Service Bus jest specjalne metryki i próg hello jest hello liczbę komunikatów dla każdego wystąpienia. Na przykład jeśli istnieją dwa wystąpienia i próg hello wartość too100, skalowanie występuje hello całkowita liczba wiadomości w kolejce hello 200. Który może być 100 komunikaty dla każdego wystąpienia, 120 i 80 lub wszelkie inne kombinacje dodające too200 lub więcej.

W przypadku zestawy skalowania maszyny Wirtualnej, można aktualizować ustawieniu skalowania automatycznego hello w toouse szablonu usługi Resource Manager hello *metricName* jako *ApproximateMessageCount* i podaj identyfikator hello kolejki magazynu hello jako  *metricResourceUri*.

```
"metricName": "MessageCount",
 "metricNamespace": "",
"metricResourceUri": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/RES_GROUP_NAME/providers/Microsoft.ServiceBus/namespaces/SB_NAMESPACE/queues/QUEUE_NAME"
```

> [!NOTE]
> Dla usługi Service Bus koncepcji grupy zasobów hello nie istnieje, ale usługi Azure Resource Manager tworzy domyślną grupę zasobów dla regionu. Grupa zasobów Hello jest zwykle w formacie "Default - magistrali usług — [region]" hello. Na przykład "Domyślne-magistrali usług-EastUS", "Domyślne-magistrali usług-WestUS", "Domyślne-magistrali usług-AustraliaEast" itp.
>
>
