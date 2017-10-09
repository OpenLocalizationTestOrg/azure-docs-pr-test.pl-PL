---
title: "klaster usługi kontenera platformy Azure aaaMonitor z Sysdig | Dokumentacja firmy Microsoft"
description: "Monitorowanie klastra usługi Azure Container Service przy użyciu rozwiązania Sysdig."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kontenery, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Monitorowanie klastra usługi Azure Container Service przy użyciu rozwiązania Sysdig
W tym artykule wdrożymy Sysdig agentów tooall hello agenta węzłów w klastrze usługi kontenera platformy Azure. Ta konfiguracja wymaga konta z rozwiązaniem Sysdig. 

## <a name="prerequisites"></a>Wymagania wstępne
[Wdróż](container-service-deployment.md) i [połącz](../container-service-connect.md) klaster skonfigurowany przez usługę Azure Container Service. Eksploruj hello [interfejs użytkownika platformy Marathon](container-service-mesos-marathon-ui.md). Przejdź za[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset konto Sysdig chmury. 

## <a name="sysdig"></a>Sysdig
Usługa monitorowania, która pozwala toomonitor jest Sysdig kontenerów w ramach klastra. Sysdig jest znany toohelp w rozwiązywaniu problemów, ale ma także Twoje podstawowe metryki monitorowania dla procesora CPU, pamięci, sieci i we/wy. Sysdig umożliwia łatwe toosee kontenery, które działają hello hardest lub zasadniczo przy użyciu hello większość pamięci i procesora CPU. Ten widok jest hello sekcji "Przegląd", który jest obecnie w wersji beta. 

![Interfejs użytkownika usługi Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Konfigurowanie wdrożenia usługi Sysdig przy użyciu usługi Marathon
Te kroki opisano, jak tooconfigure i wdrożenie klastra tooyour aplikacji Sysdig przy użyciu platformy Marathon. 

Dostęp za pośrednictwem interfejsu użytkownika DC/OS [http://localhost:80 /](http://localhost:80/) raz w hello interfejsu użytkownika DC/OS Przejdź toohello "Universe", który znajduje się na powitania dołu w lewo, a następnie wyszukaj polecenie "Sysdig."

![Usługa Sysdig we wszechświecie rozwiązania DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

Teraz hello toocomplete konfiguracji należy Sysdig chmury konta lub bezpłatne konto próbne. Po zalogowaniu się w witrynie sieci Web toohello Sysdig chmury, kliknij swoją nazwę użytkownika, a na stronie powitania powinna zostać wyświetlona "Klucz dostępu do." 

![Klucz interfejsu API usługi Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

Obok wprowadź klucz dostępu do konfiguracji Sysdig hello w hello Universe DC/OS. 

![Konfiguracja Sysdig w hello Universe DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

Teraz ustawić too10000000 wystąpień hello, przy każdym dodaniu nowego węzła klastra toohello Sysdig automatycznie wdraża agenta toothat nowego węzła. To jest tymczasowo toomake się, że Sysdig wdroży tooall nowych agentów w ramach klastra hello. 

![Konfiguracja Sysdig w hello DC/OS Universe-wystąpienia](./media/container-service-monitoring-sysdig/sysdig4.png)

Po zainstalowaniu pakietu hello Przejdź wstecz toohello Sysdig interfejsu użytkownika i będzie metryki użycia różnych hello stanie tooexplore hello kontenerów w ramach klastra. 

Możesz także zainstalować pulpity nawigacyjne określone dla rozwiązań Mesos i Marathon, korzystając z [Kreatora nowego pulpitu nawigacyjnego](https://app.sysdigcloud.com/#/dashboards/new).
