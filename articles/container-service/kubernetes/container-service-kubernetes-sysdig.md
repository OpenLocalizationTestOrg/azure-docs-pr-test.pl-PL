---
title: klaster Azure Kubernetes aaaMonitor - Sysdig | Dokumentacja firmy Microsoft
description: "Monitorowanie Kubernetes klastra usługi kontenera platformy Azure przy użyciu Sysdig"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a>Monitorowanie klastra Kubernetes usługi kontenera platformy Azure przy użyciu Sysdig

## <a name="prerequisites"></a>Wymagania wstępne
W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).

Przyjęto założenie, że masz hello azure cli i kubectl narzędzia są zainstalowane.

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

## <a name="sysdig"></a>Sysdig
Sysdig jest zewnętrznych monitorowanie jako firmy usługi, które można monitorować kontenery w klastrze Kubernetes działające na platformie Azure. Przy użyciu Sysdig wymaga aktywnego konta Sysdig.
Można założyć konto ich [lokacji](https://app.sysdigcloud.com).

Po zalogowaniu się w witrynie sieci Web toohello Sysdig chmury, kliknij swoją nazwę użytkownika, a na stronie powitania powinna zostać wyświetlona "Klucz dostępu do." 

![Klucz interfejsu API usługi Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a>Instalowanie hello Sysdig agentów tooKubernetes
toomonitor kontenerów, Sysdig uruchamia proces na każdym komputerze, za pomocą Kubernetes `DaemonSet`.
DaemonSets są obiektami Kubernetes interfejsu API, które uruchomienia pojedynczego wystąpienia kontenera dla poszczególnych komputerów.
Są one idealne w przypadku instalowania narzędzi, takich jak hello agenta monitorowania firmy Sysdig.

tooinstall hello Sysdig daemonset, należy najpierw pobrać [szablonu hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) z sysdig. Zapisz ten plik jako `sysdig-daemonset.yaml`.

W systemie Linux i OS X, można uruchomić:

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

W programie PowerShell:

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

Klucz dostępu, uzyskany z Twojego konta Sysdig obok edytować tooinsert tego pliku.

Na koniec Utwórz hello DaemonSet:

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a>Wyświetlanie, monitorowanie
Gdy zainstalowana i uruchomiona, hello agentów powinien pompa tooSysdig wstecz danych.  Przejdź wstecz toothe [pulpitu nawigacyjnego sysdig](https://app.sysdigcloud.com) i powinny być widoczne informacje o kontenerów.

Można także zainstalować pulpity nawigacyjne Kubernetes określonego za pomocą [Kreator nowego pulpitu nawigacyjnego](https://app.sysdigcloud.com/#/dashboards/new).
