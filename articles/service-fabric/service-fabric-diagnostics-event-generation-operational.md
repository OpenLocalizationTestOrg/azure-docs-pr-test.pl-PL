---
title: "aaaAzure usługi sieć szkieletowa Operational kanału | Dokumentacja firmy Microsoft"
description: "Kompletna lista dzienniki generowane w klastrach operacyjne kanału z sieci szkieletowej usług Azure hello."
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
ms.date: 07/19/2017
ms.author: dekapur
ms.openlocfilehash: 358782420ed62b202d6a89fe0f200b5ef0384c9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="operational-channel"></a>Kanał operacyjne 

kanał operacyjne Hello składa się z dzienników z wysokiego poziomu akcje wykonywane przez sieć szkieletowa usług węzły i klastra. Po włączeniu "diagnostyki" dla klastra, hello agenta diagnostyki Azure jest wdrażany w klastrze i jest domyślnie skonfigurowany tooread w dziennikach hello operacyjne kanału. Dowiedz się więcej o konfigurowaniu hello [agenta diagnostyki Azure](service-fabric-diagnostics-event-aggregation-wad.md) toomodify hello diagnostyki konfiguracji sieci klastra toopick więcej dzienników lub liczniki wydajności. 

## <a name="operational-channel-logs"></a>Kanał operacyjne dzienniki 

Poniżej przedstawiono pełną listę dzienników udostępniane przez usługi Service Fabric w kanale operacyjne hello. 

| Identyfikator zdarzenia | Nazwa | Źródło (zadania) | Poziom |
| --- | --- | --- | --- |
| 25620 | NodeOpening | FabricNode | Informacyjny |
| 25621 | NodeOpenedSuccess | FabricNode | Informacyjny |
| 25622 | NodeOpenedFailed | FabricNode | Informacyjny |
| 25623 | NodeClosing | FabricNode | Informacyjny |
| 25624 | NodeClosed | FabricNode | Informacyjny |
| 25625 | NodeAborting | FabricNode | Informacyjny |
| 25626 | NodeAborted | FabricNode | Informacyjny |
| 29627 | ClusterUpgradeStart | CM | Informacyjny |
| 29628 | ClusterUpgradeComplete | CM | Informacyjny |
| 29629 | ClusterUpgradeRollback | CM | Informacyjny |
| 29630 | ClusterUpgradeRollbackComplete | CM | Informacyjny |
| 29631 | ClusterUpgradeDomainComplete | CM | Informacyjny |
| 23074 | ContainerActivated | Hosting | Informacyjny |
| 23075 | ContainerDeactivated | Hosting | Informacyjny |
| 29620 | ApplicationCreated | CM | Informacyjny |
| 29621 | ApplicationUpgradeStart | CM | Informacyjny |
| 29622 | ApplicationUpgradeComplete | CM | Informacyjny |
| 29623 | ApplicationUpgradeRollback | CM | Informacyjny |
| 29624 | ApplicationUpgradeRollbackComplete | CM | Informacyjny |
| 29625 | ApplicationDeleted | CM | Informacyjny |
| 29626 | ApplicationUpgradeDomainComplete | CM | Informacyjny |
| 18566 | ServiceCreated | FM | Informacyjny |
| 18567 | ServiceDeleted | FM | Informacyjny |

## <a name="next-steps"></a>Następne kroki

* Dowiedz się więcej na temat ogólnych [generowania zdarzeń na poziomie platformy hello](service-fabric-diagnostics-event-generation-infra.md) w sieci szkieletowej usług
* Modyfikowanie użytkownika [diagnostyki Azure](service-fabric-diagnostics-event-aggregation-wad.md) toocollect konfiguracji więcej dzienników.
* [Konfigurowanie usługi Application Insights](service-fabric-diagnostics-event-analysis-appinsights.md) toosee kanału operacyjne dzienniki
