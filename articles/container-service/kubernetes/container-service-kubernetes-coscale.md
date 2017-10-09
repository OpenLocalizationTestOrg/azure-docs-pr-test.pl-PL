---
title: aaaMonitor Kubernetes Azure klaster z CoScale | Dokumentacja firmy Microsoft
description: "Monitor Kubernetes klastra usługi kontenera platformy Azure przy użyciu CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a>Monitor klaster Kubernetes usługi kontenera platformy Azure z CoScale

W tym artykule zostanie przedstawiony zostanie sposób toodeploy hello [CoScale](https://www.coscale.com/) toomonitor agenta, wszystkie węzły i kontenerów w Twojej Kubernetes klastra usługi kontenera platformy Azure. Musisz mieć konto z CoScale dla tej konfiguracji. 


## <a name="about-coscale"></a>O CoScale 

CoScale to platforma monitorowania, która zbiera metryki i zdarzenia z wszystkich kontenerów w różnych platform aranżacji. CoScale oferuje pełnego stosu monitorowania dla środowisk Kubernetes. Zapewnia wszystkie warstwy stosu hello wizualizacje i analiza: hello systemu operacyjnego, Kubernetes Docker i aplikacji uruchamianych wewnątrz kontenerów. CoScale oferuje kilka wbudowanych nawigacyjnych monitorowania i ma operatory tooallow wykrywania anomalii wbudowanych i szybkie toofind deweloperzy problemów infrastruktury i aplikacji.

![CoScale interfejsu użytkownika](./media/container-service-kubernetes-coscale/coscale.png)

Jak pokazano w tym artykule, można zainstalować agentów na toorun klastra Kubernetes CoScale jako rozwiązaniem SaaS. Jeśli chcesz tookeep danych na miejscu, CoScale jest również dostępny do instalacji lokalnej.


## <a name="prerequisites"></a>Wymagania wstępne

Musisz najpierw za[Utwórz konto CoScale](https://www.coscale.com/free-trial).

W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).

Założono również, że masz hello `az` wiersza polecenia platformy Azure i `kubectl` narzędzia są zainstalowane.

Możesz przetestować, jeśli masz hello `az` zainstalowany, uruchamiając narzędzie:

```azurecli
az --version
```

Jeśli nie masz hello `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](/cli/azure/install-azure-cli).

Możesz przetestować, jeśli masz hello `kubectl` zainstalowany, uruchamiając narzędzie:

```bash
kubectl version
```

Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a>Instalowanie agenta CoScale hello z DaemonSet
[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) są używane przez Kubernetes toorun pojedynczego wystąpienia kontenera na każdym hoście w klastrze hello.
Są one idealne w przypadku uruchamiania agenci monitorowania, takich jak hello CoScale agenta.

Po zalogowaniu tooCoScale Przejdź toohello [agent strona](https://app.coscale.com/) tooinstall CoScale agentów w klastrze za pomocą DaemonSet. Hello CoScale interfejsu użytkownika zawiera toocreate kroki z przewodnikiem konfiguracji agenta i rozpocząć monitorowanie pełną Kubernetes klastra.

![CoScale konfiguracji agenta](./media/container-service-kubernetes-coscale/installation.png)

agent hello toostart w klastrze hello, uruchom polecenie hello dostarczone:

![Uruchom agenta CoScale hello](./media/container-service-kubernetes-coscale/agent_script.png)

Gotowe. Po skonfigurowaniu i uruchomieniu agentów hello danych w konsoli hello powinna zostać wyświetlona za kilka minut. Odwiedź hello [agent strona](https://app.coscale.com/) toosee podsumowanie klastra, wykonanie dodatkowych kroków konfiguracji, a następnie zobacz pulpitów nawigacyjnych, takich jak hello **Kubernetes klastra omówienie**.

![Omówienie klastrów Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

Hello CoScale agent jest automatycznie wdrażane na nowych maszyn w klastrze hello. aktualizacje agenta Hello automatycznie po wydaniu nowej wersji.


## <a name="next-steps"></a>Następne kroki

Zobacz hello [CoScale dokumentacji](http://docs.coscale.com/) i [blogu](https://www.coscale.com/blog) uzyskać więcej informacji o CoScale monitorowanie rozwiązań. 

