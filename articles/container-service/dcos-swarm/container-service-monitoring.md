---
title: klaster Azure DC/OS aaaMonitor - Datadog | Dokumentacja firmy Microsoft
description: "Monitorowanie klastra usługi kontenera platformy Azure z Datadog. Używać hello DC/OS web UI toodeploy hello Datadog agentów tooyour klastra."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kontenery, Azure DC/OS, rozwiązanie Docker Swarm"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a>Monitor klastra usługi kontenera platformy Azure DC/OS z Datadog
W tym artykule wdrożymy Datadog agentów tooall hello agenta węzłów w klastrze usługi kontenera platformy Azure. Musisz mieć konto z Datadog dla tej konfiguracji. 

## <a name="prerequisites"></a>Wymagania wstępne
[Wdróż](container-service-deployment.md) i [połącz](../container-service-connect.md) klaster skonfigurowany przez usługę Azure Container Service. Eksploruj hello [interfejs użytkownika platformy Marathon](container-service-mesos-marathon-ui.md). Przejdź za[http://datadoghq.com](http://datadoghq.com) tooset konto Datadog. 

## <a name="datadog"></a>Datadog
Datadog jest usługą monitorowania, która gromadzi dane monitorowania z kontenerów w ramach klastra usługi kontenera platformy Azure. Datadog ma pulpitu nawigacyjnego Docker integracji umożliwia wyświetlenie określonych metryk w kontenerów. Metryki zebrane z kontenerów są zorganizowane według Procesora, pamięci, sieci i we/wy. Datadog dzieli metryki na kontenery i obrazów. Przykład Witaj, jakie interfejsu użytkownika wygląda dla Procesora użycia jest poniżej.

![Datadog interfejsu użytkownika](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a>Konfigurowanie wdrożenia Datadog przy użyciu platformy Marathon
Te kroki opisano, jak tooconfigure i wdrożenie klastra tooyour aplikacji Datadog przy użyciu platformy Marathon. 

Dostęp za pośrednictwem interfejsu użytkownika platformy DC/OS [http://localhost:80 /](http://localhost:80/). Raz w hello Przejdź interfejsu użytkownika DC/OS toohello "Universe", który znajduje się na powitania dołu w lewo i następnie wyszukaj "Datadog" i kliknij przycisk Zainstaluj.

![Datadog pakietu w hello Universe DC/OS](./media/container-service-monitoring/datadog1.png)

Teraz toocomplete hello konfiguracji konieczne będzie konto Datadog lub bezpłatne konto próbne. Po zalogowaniu w witrynie sieci Web toohello Datadog Szukaj toohello po lewej i przejść, następnie -> tooIntegrations [interfejsów API](https://app.datadoghq.com/account/settings#api). 

![Klucz interfejsu API Datadog](./media/container-service-monitoring/datadog2.png)

Obok wprowadź klucz interfejsu API w konfiguracji Datadog hello w hello Universe DC/OS. 

![Konfiguracja Datadog w hello Universe DC/OS](./media/container-service-monitoring/datadog3.png) 

W hello powyżej konfiguracji wystąpienia są ustawiane too10000000, przy każdym dodaniu nowego węzła klastra toohello Datadog zostaną automatycznie wdrożone węzła toothat agenta. To rozwiązanie tymczasowe. Po zainstalowaniu pakietu hello Przejdź wstecz toohello Datadog witryny sieci Web i Znajdź "[pulpity nawigacyjne](https://app.datadoghq.com/dash/list)." Z tego miejsca pojawi się niestandardowy i integracja z pulpitów nawigacyjnych. Witaj [pulpitu nawigacyjnego Docker](https://app.datadoghq.com/screen/integration/docker) będzie miał wszystkie metryki kontenera hello potrzebne do monitorowania sieci klastra. 

