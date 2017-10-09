---
title: klaster Azure DC/OS aaaMonitor - Dynatrace | Dokumentacja firmy Microsoft
description: "Monitorowanie klastra usługi kontenera platformy Azure DC/OS z Dynatrace. Wdrażanie hello Dynatrace OneAgent przy użyciu pulpitu nawigacyjnego DC/OS hello."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Kontenery, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a>Monitor klastra usługi kontenera platformy Azure DC/OS z Dynatrace SaaS/zarządzane
W tym artykule zostanie przedstawiony zostanie sposób toodeploy hello [Dynatrace](https://www.dynatrace.com/) toomonitor OneAgent wszystkie hello agenta węzłów w klastrze usługi kontenera platformy Azure. Musisz mieć konto z Dynatrace SaaS/zarządzanego dla tej konfiguracji. 

## <a name="dynatrace-saasmanaged"></a>Dynatrace SaaS/zarządzaną
Dynatrace to rozwiązanie monitorowania chmury natywne dla środowiska klastra i dynamicznej kontenera. Umożliwia on toobetter zoptymalizować swoją wdrożenia kontenerów i alokacji pamięci za pomocą danych użycia w czasie rzeczywistym. Jest w stanie automatycznie trafić zapewniając automatycznego określania poziomu odniesienia, problem korelacji i wykrywania głównej przyczyny problemów dotyczących aplikacji i infrastruktury.

Hello następujący rysunek przedstawia hello Dynatrace interfejsu użytkownika:

![Dynatrace interfejsu użytkownika](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a>Wymagania wstępne 
[Wdrażanie](container-service-deployment.md) i [połączyć](./../container-service-connect.md) klastra tooa konfigurowane za pomocą usługi kontenera platformy Azure. Eksploruj hello [interfejs użytkownika platformy Marathon](container-service-mesos-marathon-ui.md). Przejdź za[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset konto Dynatrace SaaS.  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a>Konfigurowanie wdrożenia Dynatrace przy użyciu platformy Marathon
Te kroki przedstawiają sposób tooconfigure i wdrożenie klastra tooyour aplikacji Dynatrace przy użyciu platformy Marathon.

1. Dostęp za pośrednictwem interfejsu użytkownika platformy DC/OS [http://localhost:80 /](http://localhost:80/). Raz w hello interfejsu użytkownika DC/OS, przejdź toohello **Universe** karcie, a następnie wyszukaj **Dynatrace**.

    ![Dynatrace w Uniwersum DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. toocomplete hello konfiguracji, potrzebujesz konta Dynatrace SaaS lub bezpłatne konto próbne. Po zalogowaniu się do pulpitu nawigacyjnego Dynatrace hello, wybierz **wdrażanie Dynatrace**.

    ![Konfigurowanie Dynatrace PaaS integracji](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. Na stronie powitania wybierz **konfigurowania integracji PaaS**. 

    ![Token Dynatrace interfejsu API](./media/container-service-monitoring-dynatrace/api-token.png) 

4. Wprowadź token interfejsu API na powitania Dynatrace OneAgent konfiguracji w ramach hello Universe DC/OS. 

    ![Konfiguracja Dynatrace OneAgent w hello Universe DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. Ustawianie wystąpienia hello toohello liczby węzłów mają toorun. Ustawienie wyższej także działania, ale DC/OS będzie nadal próbować toofind nowych wystąpień do momentu rzeczywistości osiągnięciu tej liczby. Jeśli wolisz, możesz również tę wartość można ustawić tooa jak 1000000. W takim przypadku przy każdym dodaniu nowego węzła klastra toohello Dynatrace automatycznie wdraża agenta toothat nowy węzeł, na powitania ceny stale trakcie wystąpień dalsze toodeploy DC/OS.

    ![Konfiguracja Dynatrace w hello DC/OS Universe-wystąpienia](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a>Następne kroki

Po zainstalowaniu pakietu hello, przejdź wstecz toohello Dynatrace z pulpitu nawigacyjnego. Metryki użycia różnych hello kontenerów hello można sprawdzić w ramach klastra. 
