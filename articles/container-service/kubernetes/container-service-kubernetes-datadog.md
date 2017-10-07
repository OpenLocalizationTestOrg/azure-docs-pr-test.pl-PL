---
title: aaaMonitor Azure Kubernetes klaster z Datadog | Dokumentacja firmy Microsoft
description: "Monitorowanie Kubernetes klastra usługi kontenera platformy Azure przy użyciu Datadog"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a>Monitor klastra usługi kontenera platformy Azure z DataDog

## <a name="prerequisites"></a>Wymagania wstępne
W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).

Założono również, że masz hello `az` interfejsu wiersza polecenia platformy Azure i `kubectl` narzędzia są zainstalowane.

Możesz przetestować, jeśli masz hello `az` zainstalowany, uruchamiając narzędzie:

```console
$ az --version
```

Jeśli nie masz hello `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](https://github.com/azure/azure-cli#installation).

Możesz przetestować, jeśli masz hello `kubectl` zainstalowany, uruchamiając narzędzie:

```console
$ kubectl version
```

Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a>DataDog
Datadog jest usługą monitorowania, która gromadzi dane monitorowania z kontenerów w ramach klastra usługi kontenera platformy Azure. Datadog ma pulpitu nawigacyjnego Docker integracji umożliwia wyświetlenie określonych metryk w kontenerów. Metryki zebrane z kontenerów są zorganizowane według Procesora, pamięci, sieci i we/wy. Datadog dzieli metryki na kontenery i obrazów.

Należy najpierw zbyt[Tworzenie konta usługi](https://www.datadoghq.com/lpg/)

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a>Instalowanie agenta Datadog hello z DaemonSet
DaemonSets są używane przez Kubernetes toorun pojedynczego wystąpienia na każdym hoście w klastrze hello kontenera.
Są one idealne w przypadku uruchamiania agenci monitorowania.

Gdy użytkownik zalogował się do Datadog, możesz wykonać hello [instrukcje Datadog](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agentów w klastrze za pomocą DaemonSet.

## <a name="conclusion"></a>Podsumowanie
Gotowe. Po hello agenci są uruchomione i systemem można powinny być widoczne dane w konsoli hello za kilka minut. Użytkownik może odwiedzić hello zintegrowane [pulpitu nawigacyjnego kubernetes](https://app.datadoghq.com/screen/integration/kubernetes) toosee podsumowanie klastra.
