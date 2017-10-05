---
title: "Samouczek usługi kontenera platformy Azure — Monitor Kubernetes | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — Kubernetes monitora z Microsoft Operations Management Suite (OMS)"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenerów, Micro-services, Kubernetes, platforma Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: f4d09973ada8e3cd0ff2b00d20aca979e834cd7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Monitor klastrze Kubernetes z pakietem Operations Management Suite

Monitorowanie sieci klastra Kubernetes i kontenery jest krytyczny, szczególnie w przypadku zarządzania klastrem produkcji na dużą skalę w wielu aplikacjach. 

Można korzystać z kilku Kubernetes rozwiązań w zakresie monitorowania, z firmy Microsoft lub innych dostawców. W tym samouczku klastra Kubernetes można monitorować za pomocą rozwiązania kontenery w [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), rozwiązania do zarządzania oparta na chmurze IT firmy Microsoft. (OMS kontenery rozwiązanie jest w wersji zapoznawczej.)

Ten samouczek, część 7 7, obejmuje następujące zadania:

> [!div class="checklist"]
> * Pobierz ustawienia obszarem roboczym pakietu OMS
> * Konfigurowanie agentów OMS na węzłach Kubernetes
> * Dostęp do monitorowania informacji w portalu OMS lub w portalu Azure

## <a name="before-you-begin"></a>Przed rozpoczęciem

W poprzednim samouczki aplikacji zostało umieszczone w kontener obrazów, te obrazy przekazane do rejestru kontenera Azure i klastra Kubernetes utworzone. Jeśli nie zostało wykonane następujące kroki, a następnie zostać z niego skorzystać, wróć do [samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md). 

Co najmniej tego samouczka wymaga Kubernetes klastra z węzłami agenta systemu Linux i konta Operations Management Suite (OMS). Jeśli to konieczne, należy zarejestrować się w celu [bezpłatnej wersji próbnej pakietu OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).

## <a name="get-workspace-settings"></a>Pobierz ustawienia obszaru roboczego

Podczas uzyskiwania dostępu [portalu OMS](https://mms.microsoft.com), przejdź do **ustawienia** > **połączonych źródeł** > **serwerów z systemem Linux**. Istnieje, można znaleźć *identyfikator obszaru roboczego* i podstawowym lub pomocniczym *klucz obszaru roboczego*. Zanotuj te wartości, które należy skonfigurować OMS agentów w klastrze.

## <a name="set-up-oms-agents"></a>Konfigurowanie agentów OMS

W tym miejscu jest plikiem yaml programu do skonfigurowania OMS agentów w węzłach klastra systemu Linux. Tworzy Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), które są uruchamiane jednym pod identyczne w każdym węźle klastra. Zasób DaemonSet jest idealne rozwiązanie w przypadku wdrażania agenta monitorowania. 

Zapisz poniższy tekst do pliku o nazwie `oms-daemonset.yaml`i zastąp symbole zastępcze dla *myWorkspaceID* i *myWorkspaceKey* z OMS identyfikator i klucz. (W środowisku produkcyjnym, użytkownik może zakodować te wartości jako klucze tajne.)

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

Utwórz DaemonSet przy użyciu następującego polecenia:

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

Aby sprawdzić, czy DaemonSet został utworzony, uruchom polecenie:

```azurecli-interactive
kubectl get daemonset
```

Dane wyjściowe będą podobne do następujących:

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

Po agenci są uruchomione, przyjmuje OMS do pozyskiwania i przetwarzania danych w ciągu kilku minut.

## <a name="access-monitoring-data"></a>Dostęp do danych monitorowania

Wyświetlanie i analizowanie kontenera OMS monitorowania danych za pomocą [rozwiązania kontenera](../../log-analytics/log-analytics-containers.md) w portalu OMS lub w portalu Azure. 

Przeprowadzanie instalacji przy użyciu rozwiązania kontenera [portalu OMS](https://mms.microsoft.com), przejdź do **galerii rozwiązań**. Następnie dodaj **rozwiązania kontenera**. Możesz też dodać kontenery rozwiązania z [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).

W portalu OMS poszukaj **kontenery** podsumowania kafelka na pulpicie nawigacyjnym OMS. Kliknij Kafelek, aby uzyskać więcej informacji, łącznie z: kontenery zdarzeń, błędów, stan, obrazu spisu i użycia Procesora i pamięci. Bardziej szczegółowe informacje, kliknij wiersz na każdy Kafelek, lub wykonaj [wyszukiwania dziennika](../../log-analytics/log-analytics-log-searches.md).

![Pulpit nawigacyjny kontenery w portalu OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

Podobnie, w portalu Azure, przejdź do **analizy dzienników** i wybierz nazwę obszaru roboczego. Aby wyświetlić **kontenery** Kafelek podsumowania, kliknij przycisk **rozwiązań** > **kontenery**. Aby wyświetlić szczegóły, kliknij Kafelek.

Zobacz [dokumentacji usługi Analiza dzienników Azure](../../log-analytics/index.md) szczegółowe wskazówki dotyczące zapytań i analizowanie danych monitorowania.

## <a name="next-steps"></a>Następne kroki

W tym samouczku monitorowane są klastra Kubernetes z usługą OMS. Uwzględnione objętych zadań:

> [!div class="checklist"]
> * Pobierz ustawienia obszarem roboczym pakietu OMS
> * Konfigurowanie agentów OMS na węzłach Kubernetes
> * Dostęp do monitorowania informacji w portalu OMS lub w portalu Azure


Wykonaj to łącze, aby wyświetlić przykłady wbudowanych skryptów dla usługi kontenera.

> [!div class="nextstepaction"]
> [Przykłady skryptów usługi kontenera platformy Azure](cli-samples.md)
