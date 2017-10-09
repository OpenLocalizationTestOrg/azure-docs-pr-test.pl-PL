---
title: "aaaAzure usługi sieć szkieletowa zdarzeń agregacji Diagnostyka Azure systemu Linux | Dokumentacja firmy Microsoft"
description: "Więcej informacji na temat agregowania i zbierania zdarzeń przy użyciu LAD monitorowania i diagnostyki klastrów sieci szkieletowej usług Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/17/2017
ms.author: dekapur
ms.openlocfilehash: aefa869219a0dd219e01e6574816fe3ce47fe472
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="event-aggregation-and-collection-using-linux-azure-diagnostics"></a>Agregacja zdarzeń i kolekcji za pomocą diagnostyki Azure systemu Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-diagnostics-event-aggregation-wad.md)
> * [Linux](service-fabric-diagnostics-event-aggregation-lad.md)
>
>

Jeśli korzystasz z klastra usługi sieć szkieletowa usług Azure, jest dobrze toocollect hello dzienniki ze wszystkich węzłów hello w centralnej lokalizacji. O dzienniki hello w centralnej lokalizacji ułatwiają analizowanie i rozwiązywanie problemów w klastrze, lub problemy w hello aplikacje i usługi działające w klastrze.

Zbieranie dzienników i tooupload jedną z metod jest toouse hello Linux Azure Diagnostics (LAD) rozszerzenie, które przekazuje dzienniki tooAzure magazynu, a także ma hello opcja toosend dzienniki tooAzure usługi Application Insights lub Event Hubs. Można również użyć procesu zewnętrznego tooread hello zdarzenia z magazynu i umieścić w produkcie platformy analizy, takich jak [analizy dzienników OMS](../log-analytics/log-analytics-service-fabric.md) lub innego rozwiązania do analizowania dziennika.

## <a name="log-and-event-sources"></a>Źródła dziennika i zdarzenie

### <a name="service-fabric-platform-events"></a>Zdarzenia platformy Service Fabric
Sieć szkieletowa usług emituje kilka poza pole dzienniki za pośrednictwem [LTTng](http://lttng.org), w tym zdarzenia operacyjne lub zdarzeniach środowiska uruchomieniowego. Te dzienniki są przechowywane w lokalizacji hello hello Określa szablon Menedżera zasobów klastra. tooget lub szczegóły konta magazynu hello, odszukaj tagu hello **AzureTableWinFabETWQueryable** i poszukaj **StoreConnectionString**.

### <a name="application-events"></a>Zdarzenia aplikacji
 Zdarzenia wysyłanego z Twojej aplikacji i usług kodu określonych przez użytkownika podczas Instrumentacji oprogramowania. Można użyć dowolnego rozwiązania rejestrowania, który zapisuje pliki dzienników tekstowych — na przykład LTTng. Uzyskać więcej informacji zobacz dokumentację LTTng hello śledzenia aplikacji.

[Monitorowanie i diagnozowanie usług w Instalatorze programowanie komputera lokalnego](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

## <a name="deploy-hello-diagnostics-extension"></a>Wdrażanie rozszerzenia diagnostyki hello
pierwszym krokiem Hello zbierania dzienników jest rozszerzeniem diagnostyki hello toodeploy na poszczególnych maszyn wirtualnych hello w klastrze usługi sieć szkieletowa hello. Hello rozszerzenia diagnostyki zbiera dzienniki na każdej maszynie Wirtualnej i przekazuje je toohello konta magazynu, który określisz. kroki Hello różnić w zależności od użycia hello portalu Azure lub usługi Azure Resource Manager.

Ustaw toodeploy hello diagnostyki rozszerzenia toohello maszyn wirtualnych w klastrze hello w ramach tworzenia klastra **diagnostyki** za**na**. Po utworzeniu klastra hello, nie możesz zmienić to ustawienie za pomocą portalu hello.

Następnie skonfiguruj pliki hello toocollect Linux Azure Diagnostics (LAD) i umieszczenie ich w koncie magazynu. Ten proces jest wyjaśniono, jak w scenariuszu 3 ("przekazać pliki dzienników") w artykule hello [toomonitor przy użyciu LAD i diagnozowanie maszyn wirtualnych systemu Linux](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json). Po tym pobiera procesu dostępu toohello śledzi. Możesz przekazać hello śladów tooa wizualizatora wybranych przez użytkownika.

Można także wdrożyć hello diagnostyki rozszerzenia przy użyciu usługi Azure Resource Manager. Witaj proces jest podobny do systemu Windows i Linux i jest udokumentowany klastrów systemu Windows w [sposób rejestrowania toocollect Diagnostyka Azure](service-fabric-diagnostics-how-to-setup-wad.md).

Można również użyć usługi Operations Management Suite, zgodnie z opisem w [Operations Management Suite Log Analytics z systemem Linux](https://blogs.technet.microsoft.com/hybridcloud/2016/01/28/operations-management-suite-log-analytics-with-linux/).

Po zakończeniu tej konfiguracji monitorów agenta LAD hello hello określone pliki dziennika. Zawsze, gdy nowy wiersz jest plik dołączany toohello, tworzy wpisu dziennika systemu, który określonej w magazynie toohello wysłane.

## <a name="next-steps"></a>Następne kroki

jakie zdarzenia należy sprawdzić podczas rozwiązywania problemów, toounderstand bardziej szczegółowo w temacie [dokumentacji LTTng](http://lttng.org/docs) i [przy użyciu LAD](../virtual-machines/linux/classic/diagnostic-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).
