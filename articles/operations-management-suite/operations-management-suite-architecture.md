---
title: aaaOperations architektura Management Suite (OMS) | Dokumentacja firmy Microsoft
description: "Pakiet Microsoft Operations Management Suite (OMS) to oparte na chmurze rozwiązanie firmy Microsoft do zarządzania systemami IT, które ułatwia zarządzanie infrastrukturą lokalną i chmurową oraz jej ochronę.  W tym artykule identyfikuje hello różnych usług objęte OMS i linki tootheir szczegółowe zawartości."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 40e41686-7e35-4d85-bbe8-edbcb295a534
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: bwren
ms.openlocfilehash: fa3227aa9c19219009ebe363b7fd2d6565cec59c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="oms-architecture"></a>Architektura pakietu OMS
[Pakiet Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/services/operations-management-suite/) to zbiór opartych na chmurze usług zarządzania środowiskami lokalnymi i chmurowymi.  W tym artykule opisano hello różnych lokalnych i chmurze składniki pakietu OMS i ich obliczeniowych Architektura wysokiego poziomu chmury.  Dla każdej usługi, aby uzyskać dodatkowe szczegóły można znaleźć toohello dokumentacji.

## <a name="log-analytics"></a>Log Analytics
Wszystkie dane zebrane przez [analizy dzienników](https://azure.microsoft.com/documentation/services/log-analytics/) znajduje się w repozytorium OMS hello, która jest hostowana na platformie Azure.  Połączonych źródeł generować dane zbierane w repozytorium OMS hello.  Obecnie istnieją trzy typy obsługiwanych połączonych źródeł.

* Agent zainstalowany na [Windows](../log-analytics/log-analytics-windows-agents.md) lub [Linux](../log-analytics/log-analytics-linux-agents.md) komputer bezpośrednio połączony tooOMS.
* Grupa zarządzania programu System Center Operations Manager (SCOM) [połączone tooLog Analytics](../log-analytics/log-analytics-om-agents.md) .  Agenci SCOM nadal toocommunicate z serwerami zarządzania, które przekazywania zdarzeń i wydajności danych tooLog Analytics.
* [Konto usługi Azure Storage](../log-analytics/log-analytics-azure-storage.md), które zbiera dane usługi [Diagnostyka Azure](../cloud-services/cloud-services-dotnet-diagnostics.md) z roli Proces roboczy, roli Sieć Web lub z maszyny wirtualnej na platformie Azure.

Źródła danych zdefiniować dane hello, która gromadzi analizy dzienników z połączonych źródeł, takich jak dzienniki zdarzeń i liczniki wydajności.  Rozwiązania dodać tooOMS funkcjonalność i można łatwo dodać tooyour obszaru roboczego z hello [galerii rozwiązań OMS](../log-analytics/log-analytics-add-solutions.md).  Niektóre rozwiązania może wymagać tooLog bezpośrednie połączenie Analytics z agentów programu SCOM, podczas gdy inne osoby mogą wymagać toobe dodatkowe agent zainstalowany.

Analiza dzienników ma portalu sieci web można korzystać z zasobów OMS toomanage, Dodaj i skonfigurowanie rozwiązania OMS i wyświetlanie i analizowanie danych w repozytorium OMS hello.

![Architektura wysokiego poziomu usługi Log Analytics](media/operations-management-suite-architecture/log-analytics.png)

## <a name="azure-automation"></a>Azure Automation
[Elementy runbook automatyzacji Azure](http://azure.microsoft.com/documentation/services/automation) są wykonywane w hello chmury Azure i mają dostęp do zasobów, które znajdują się w innych usług w chmurze platformy Azure lub niedostępny z hello publicznej sieci Internet.  Można również przydzielić komputery lokalne w lokalnym centrum danych za pomocą [hybrydowego procesu roboczego elementu Runbook](../automation/automation-hybrid-runbook-worker.md) w taki sposób, aby elementy Runbook mogły uzyskać dostęp do zasobów lokalnych.

[Konfiguracji DSC](../automation/automation-dsc-overview.md) przechowywane w automatyzacji Azure mogą być bezpośrednio zastosowane tooAzure maszyn wirtualnych.  Konfiguracje mogą żądać innych fizycznych i maszyn wirtualnych z serwera ściągania usługi Konfiguracja DSC automatyzacji Azure hello.

Automatyzacja Azure ma rozwiązania OMS, która wyświetla statystyki i łączy hello toolaunch portalu Azure dla wszystkich operacji.

![Architektura wysokiego poziomu usługi Azure Automation](media/operations-management-suite-architecture/automation.png)

## <a name="azure-backup"></a>Azure Backup
Chronione dane w usłudze [Azure Backup](http://azure.microsoft.com/documentation/services/backup) są przechowywane w magazynie kopii zapasowych, znajdującym się w określonym regionie geograficznym.  Witaj, dane są replikowane w hello na tym samym regionie i, w zależności od typu hello magazynu, może być również region replikowanych tooanother dalsze nadmiarowości.

Usługa Azure Backup ma trzy podstawowe scenariusze.

* Komputer z systemem Windows z agentem usługi Azure Backup.  Dzięki temu można toobackup plików i folderów z systemu Windows server lub klienta bezpośrednio tooyour magazynu kopii zapasowych systemu Azure.  
* System Center Data Protection Manager (DPM) lub serwer usługi Microsoft Azure Backup. Dzięki temu można tooleverage programu DPM lub serwera kopii zapasowej Microsoft Azure toobackup plików i folderów oprócz tooapplication obciążeń, takich jak SQL i SharePoint magazynu toolocal i następnie replikowania tooyour magazynu kopii zapasowych systemu Azure.
* Rozszerzenia maszyny wirtualnej platformy Azure.  Dzięki temu toobackup maszyn wirtualnych platformy Azure tooyour magazynu kopii zapasowych systemu Azure.

Kopia zapasowa Azure ma rozwiązania OMS, która wyświetla statystyki i łączy hello toolaunch portalu Azure dla wszystkich operacji.

![Architektura wysokiego poziomu usługi Azure Backup](media/operations-management-suite-architecture/backup.png)

## <a name="azure-site-recovery"></a>Azure Site Recovery
Usługa [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) organizuje replikację, pracę w trybie failover i powrót po awarii maszyn wirtualnych i serwerów fizycznych. Dane replikacji są wymieniane między hostami funkcji Hyper-V, funkcjami hypervisor VMware i serwerów fizycznych w centrach danych podstawowych i pomocniczych lub między hello centrum danych i magazynu systemu Azure.  Usługa Site Recovery przechowuje metadane w magazynach znajdujących się w określonym regionie geograficznym świadczenia usługi Azure. Nie replikowane dane są przechowywane przez hello usługi Site Recovery.

Usługa Azure Site Recovery ma trzy podstawowe scenariusze replikacji.

**Replikacja maszyn wirtualnych funkcji Hyper-V**

* Jeśli maszyny wirtualne funkcji Hyper-V są zarządzane w chmurach programu VMM, można replikować tooa zapasowy Centrum lub tooAzure magazyn danych.  TooAzure replikacji jest za pośrednictwem bezpiecznego połączenia internetowego.  Replikacja tooa dodatkowego centrum danych znajduje się nad hello sieci LAN.
* Jeśli maszyny wirtualne funkcji Hyper-V nie są zarządzane przez program VMM, można replikować tylko tooAzure magazynu.  TooAzure replikacji jest za pośrednictwem bezpiecznego połączenia internetowego.

**Replikacja maszyn wirtualnych VMWare**

* Można replikować VMware maszyn wirtualnych tooa dodatkowego centrum danych z magazynu VMware lub tooAzure.  TooAzure replikacji może wystąpić w sieci VPN lokacja lokacja lub usługa Azure ExpressRoute lub za pośrednictwem bezpiecznego połączenia internetowego. Replikacja tooa dodatkowego centrum danych odbywa się za pośrednictwem hello InMage Scout kanału danych.

**Replikacja serwerów fizycznych z systemami Windows i Linux** 

* Można replikować serwerów fizycznych tooa pomocniczego centrum danych lub tooAzure magazynu. TooAzure replikacji może wystąpić w sieci VPN lokacja lokacja lub usługa Azure ExpressRoute lub za pośrednictwem bezpiecznego połączenia internetowego. Replikacja tooa dodatkowego centrum danych odbywa się za pośrednictwem hello InMage Scout kanału danych.  Usługa Azure Site Recovery zawiera rozwiązanie OMS, która wyświetla statystykami, ale muszą używać hello portalu Azure, dla wszystkich operacji.

![Architektura wysokiego poziomu usługi Azure Site Recovery](media/operations-management-suite-architecture/site-recovery.png)

## <a name="next-steps"></a>Następne kroki
* Dowiedz się więcej o usłudze [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics).
* Dowiedz się więcej o usłudze [Azure Automation](https://azure.microsoft.com/documentation/services/automation).
* Dowiedz się więcej o usłudze [Azure Backup](http://azure.microsoft.com/documentation/services/backup).
* Dowiedz się więcej o usłudze [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery).

