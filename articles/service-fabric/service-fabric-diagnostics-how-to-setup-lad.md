---
title: "Zbieranie dzienników przy użyciu diagnostyki Azure systemu Linux | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak skonfigurować diagnostyki Azure do zbierania dzienników z klastra usługi sieć szkieletowa Linux działających na platformie Azure."
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
ms.openlocfilehash: 3e41caaeb38c55d1c6c3bfdce2f81c86b4aff4d0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-logs-by-using-azure-diagnostics"></a>Zbieranie dzienników za pomocą Diagnostyki Azure
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-how-to-setup-wad.md)
> * [Linux](service-fabric-diagnostics-how-to-setup-lad.md)
> 
> 

Jeśli korzystasz z klastra usługi sieć szkieletowa usług Azure, jest dobrym pomysłem jest zebrać dzienniki ze wszystkich węzłów w centralnej lokalizacji. Posiadanie dzienniki w centralnej lokalizacji ułatwia do analizowania i rozwiązywania problemów, czy są one usług, aplikacji lub samego klastra. Jednym ze sposobów przekazywania i zbierania dzienników jest używane rozszerzenie diagnostyki Azure, która przekazuje dzienniki do magazynu Azure, Azure Application Insights lub usługi Azure Event Hubs. Możesz również odczytywane zdarzenia z magazynu lub centra zdarzeń i umieszczenie ich w produkcie takich jak [analizy dzienników](../log-analytics/log-analytics-service-fabric.md) lub innego rozwiązania do analizowania dziennika. [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) zawiera kompleksowe dziennik wyszukiwania i analiza usługi wbudowanych.

## <a name="log-sources-that-you-might-want-to-collect"></a>Dziennik źródła, które mają być zbierane
* **Dzienniki usługi sieć szkieletowa**: wysyłanego z platformy za pośrednictwem [LTTng](http://lttng.org) i przekazania jej do konta magazynu. Dzienniki można operacyjne lub zdarzenia środowiska uruchomieniowego emitowanych przez platformę. Te dzienniki są przechowywane w lokalizacji, która określa manifestu klastra. (Aby uzyskać szczegóły konta magazynu, wyszukaj tagu **AzureTableWinFabETWQueryable** i poszukaj **StoreConnectionString**.)
* **Zdarzenia aplikacji**: wysyłanego z kodu usługi. Można użyć dowolnego rozwiązania rejestrowania, który zapisuje pliki dzienników tekstowych — na przykład LTTng. Aby uzyskać więcej informacji zobacz dokumentację LTTng na śledzenia aplikacji.  

## <a name="deploy-the-diagnostics-extension"></a>Wdrażanie rozszerzenia diagnostyki
Pierwszym etapem zbierania dzienników jest wdrażanie rozszerzenia diagnostyki na wszystkich maszynach wirtualnych w klastrze usługi sieć szkieletowa usług. Rozszerzenie diagnostycznych zbiera dzienniki na każdej maszynie Wirtualnej i przekazuje je do konta magazynu, który określisz. Kroki różnić w zależności od tego, czy używasz portalu Azure lub usługi Azure Resource Manager.

Aby wdrożyć rozszerzenie diagnostyki maszyny wirtualne w klastrze, w ramach tworzenia klastra, należy ustawić **diagnostyki** do **na**. Po utworzeniu klastra nie można zmienić to ustawienie, korzystając z portalu.

Następnie należy skonfigurować Linux Azure Diagnostics (LAD) do zbierania plików i umieszczenie ich w koncie magazynu. Ten proces jest wyjaśniono, jak w scenariuszu 3 ("przekazać pliki dzienników") w artykule [przy użyciu LAD monitorowanie i diagnozowanie maszyn wirtualnych systemu Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Ten proces po pobiera dostępu do śledzenia. Możesz przekazać dane śledzenia do wizualizatora wybranych przez użytkownika.

Można także wdrożyć rozszerzenie diagnostyki za pomocą usługi Azure Resource Manager. Proces jest podobny do systemu Windows i Linux i jest udokumentowany klastrów systemu Windows w [jak zbierać dzienniki Diagnostyka Azure](service-fabric-diagnostics-how-to-setup-wad.md).

Można również użyć usługi Operations Management Suite, zgodnie z opisem w [Operations Management Suite Log Analytics z systemem Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Po zakończeniu tej konfiguracji agenta LAD monitoruje pliki określony dziennik. Zawsze, gdy nowy wiersz jest dołączany do pliku, tworzy wpis dziennika systemowego, wysyłany do magazynu, który można określić.

## <a name="next-steps"></a>Następne kroki
Aby bardziej szczegółowo zrozumieć, jakie zdarzenia należy sprawdzić podczas rozwiązywania problemów, zobacz [dokumentacji LTTng](http://lttng.org/docs) i [przy użyciu LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

