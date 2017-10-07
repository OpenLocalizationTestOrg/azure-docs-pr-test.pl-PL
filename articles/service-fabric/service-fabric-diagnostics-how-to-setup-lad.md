---
title: "Dzienniki aaaCollect za pomocą diagnostyki Azure systemu Linux | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano sposób rejestrowania tooset się toocollect diagnostyki Azure z klastra usługi sieć szkieletowa Linux działających na platformie Azure."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a160d469-8b7d-4560-82dd-8500db34a44a
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/28/2017
ms.author: subramar
ms.openlocfilehash: f61172876e744ea3e361f9ae513254239d6ba27f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Zbieranie dzienników za pomocą Diagnostyki Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Jeśli korzystasz z klastra usługi sieć szkieletowa usług Azure, jest dobrze toocollect hello dzienniki ze wszystkich węzłów hello w centralnej lokalizacji. O dzienniki hello w centralnej lokalizacji umożliwia łatwe tooanalyze i rozwiązywania problemów, czy są one usług, aplikacji lub hello samego klastra. Jednym ze sposobów tooupload i zbieranie dzienników jest toouse hello Azure Diagnostics rozszerzenia, które przekazywania dzienników tooAzure magazynu, usługi Application Insights dla platformy Azure lub usługi Azure Event Hubs. Można odczytywać zdarzeń hello magazynu lub centra zdarzeń i umieszczenie ich w produkcie takich jak [analizy dzienników](../log-analytics/log-analytics-service-fabric.md) lub innego rozwiązania do analizowania dziennika. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) zawiera kompleksowe dziennik wyszukiwania i analiza usługi wbudowanych.

## <a name="log-sources-that-you-might-want-toocollect"></a>Dziennik źródeł rozważ toocollect
* **Dzienniki usługi sieć szkieletowa**: wysyłanego z platformy hello za pośrednictwem [LTTng](http://lttng.org) i przekazać tooyour konta magazynu. Dzienniki mogą być zdarzenia operacyjne lub emituje zdarzenia środowiska uruchomieniowego, które hello platformy. Te dzienniki są przechowywane w lokalizacji hello Określa, że hello manifestu klastra. (tooget hello szczegóły konta magazynu, wyszukaj hello tag **AzureTableWinFabETWQueryable** i poszukaj **StoreConnectionString**.)
* **Zdarzenia aplikacji**: wysyłanego z kodu usługi. Można użyć dowolnego rozwiązania rejestrowania, który zapisuje pliki dzienników tekstowych — na przykład LTTng. Uzyskać więcej informacji zobacz dokumentację LTTng hello śledzenia aplikacji.  

## <a name="deploy-hello-diagnostics-extension"></a>Wdrażanie rozszerzenia diagnostyki hello
pierwszym krokiem Hello zbierania dzienników jest rozszerzeniem diagnostyki hello toodeploy na poszczególnych maszyn wirtualnych hello w klastrze usługi sieć szkieletowa hello. Hello rozszerzenia diagnostyki zbiera dzienniki na każdej maszynie Wirtualnej i przekazuje je toohello konta magazynu, który określisz. kroki Hello różnić w zależności od użycia hello portalu Azure lub usługi Azure Resource Manager.

Ustaw toodeploy hello diagnostyki rozszerzenia toohello maszyn wirtualnych w klastrze hello w ramach tworzenia klastra **diagnostyki** za**na**. Po utworzeniu klastra hello, nie możesz zmienić to ustawienie za pomocą portalu hello.

Następnie skonfiguruj pliki hello toocollect Linux Azure Diagnostics (LAD) i umieszczenie ich w koncie magazynu. Ten proces jest wyjaśniono, jak w scenariuszu 3 ("przekazać pliki dzienników") w artykule hello [toomonitor przy użyciu LAD i diagnozowanie maszyn wirtualnych systemu Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Po tym pobiera procesu dostępu toohello śledzi. Możesz przekazać hello śladów tooa wizualizatora wybranych przez użytkownika.

Można także wdrożyć hello diagnostyki rozszerzenia przy użyciu usługi Azure Resource Manager. Witaj proces jest podobny do systemu Windows i Linux i jest udokumentowany klastrów systemu Windows w [sposób rejestrowania toocollect Diagnostyka Azure](service-fabric-diagnostics-how-to-setup-wad.md).

Można również użyć usługi Operations Management Suite, zgodnie z opisem w [Operations Management Suite Log Analytics z systemem Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Po zakończeniu tej konfiguracji monitorów agenta LAD hello hello określone pliki dziennika. Zawsze, gdy nowy wiersz jest plik dołączany toohello, tworzy wpisu dziennika systemu, który określonej w magazynie toohello wysłane.

## <a name="next-steps"></a>Następne kroki
jakie zdarzenia należy sprawdzić podczas rozwiązywania problemów, toounderstand bardziej szczegółowo w temacie [dokumentacji LTTng](http://lttng.org/docs) i [przy użyciu LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

