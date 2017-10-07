---
title: "Samouczek usługi kontenera aaaAzure — Monitor Kubernetes | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a>Monitor klastrze Kubernetes z pakietem Operations Management Suite

Monitorowanie sieci klastra Kubernetes i kontenery jest krytyczny, szczególnie w przypadku zarządzania klastrem produkcji na dużą skalę w wielu aplikacjach. 

Można korzystać z kilku Kubernetes rozwiązań w zakresie monitorowania, z firmy Microsoft lub innych dostawców. W tym samouczku klastra Kubernetes można monitorować za pomocą rozwiązania kontenery hello w [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), rozwiązania do zarządzania oparta na chmurze IT firmy Microsoft. (hello kontenery OMS rozwiązanie jest w wersji zapoznawczej.)

Ten samouczek, część 7 siedmiu, obejmuje hello następujące zadania:

> [!div class="checklist"]
> * Pobierz ustawienia obszarem roboczym pakietu OMS
> * Konfigurowanie agentów OMS na węzłach Kubernetes hello
> * Dostęp do monitorowania informacji w portalu OMS hello lub w portalu Azure

## <a name="before-you-begin"></a>Przed rozpoczęciem

W poprzednich samouczki aplikacji zostało umieszczone w kontenerze obrazów, przekazać te obrazy tooAzure rejestru kontenera i utworzyć klaster Kubernetes. Jeśli nie zostało wykonane następujące kroki, a chcesz toofollow wzdłuż, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md). 

Co najmniej tego samouczka wymaga Kubernetes klastra z węzłami agenta systemu Linux i konta Operations Management Suite (OMS). Jeśli to konieczne, należy zarejestrować się w celu [bezpłatnej wersji próbnej pakietu OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).

## <a name="get-workspace-settings"></a>Pobierz ustawienia obszaru roboczego

Podczas uzyskiwania dostępu hello [portalu OMS](https://mms.microsoft.com), przejdź do zbyt**ustawienia** > **połączonych źródeł** > **serwerów z systemem Linux**. Istnieje, można znaleźć hello *identyfikator obszaru roboczego* i podstawowym lub pomocniczym *klucz obszaru roboczego*. Zanotuj te wartości, które należy tooset się OMS agentów na powitania klastra.

## <a name="set-up-oms-agents"></a>Konfigurowanie agentów OMS

Oto tooset pliku yaml programu się OMS agentów w węzłach klastra hello systemu Linux. Tworzy Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), które są uruchamiane jednym pod identyczne w każdym węźle klastra. Witaj DaemonSet zasobów jest idealny dla wdrażania agenta monitorowania. 

Zapisz hello poniższe tekst tooa plik o nazwie `oms-daemonset.yaml`i zastąp symbole zastępcze powitania dla *myWorkspaceID* i *myWorkspaceKey* z OMS identyfikator i klucz. (W środowisku produkcyjnym, użytkownik może zakodować te wartości jako klucze tajne.)

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

Utwórz hello DaemonSet z hello następujące polecenie:

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

Uruchom ten hello DaemonSet jest tworzona, toosee:

```azurecli-interactive
kubectl get daemonset
```

Dane wyjściowe są podobne toohello następujące czynności:

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

Po agentów hello jest uruchomiony, ma OMS tooingest i przetwarzanie danych hello w ciągu kilku minut.

## <a name="access-monitoring-data"></a>Dostęp do danych monitorowania

Wyświetlanie i analizowanie kontenera OMS hello monitorowania danych za pomocą hello [rozwiązania kontenera](../../log-analytics/log-analytics-containers.md) w portalu OMS hello lub hello portalu Azure. 

rozwiązanie kontenera hello tooinstall przy użyciu hello [portalu OMS](https://mms.microsoft.com), przejdź do zbyt**galerii rozwiązań**. Następnie dodaj **rozwiązania kontenera**. Możesz też dodać hello kontenery rozwiązania z hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).

W portalu OMS hello, poszukaj **kontenery** podsumowania kafelka na pulpicie nawigacyjnym OMS hello. Kliknij Kafelek hello, aby uzyskać więcej informacji, łącznie z: kontenery zdarzeń, błędów, stan, obrazu spisu i użycia Procesora i pamięci. Bardziej szczegółowe informacje, kliknij wiersz na każdy Kafelek, lub wykonaj [wyszukiwania dziennika](../../log-analytics/log-analytics-log-searches.md).

![Pulpit nawigacyjny kontenery w portalu OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

Podobnie, w hello portalu Azure, przejdź do pozycji zbyt**analizy dzienników** i wybierz nazwę obszaru roboczego. Witaj toosee **kontenery** Kafelek podsumowania, kliknij przycisk **rozwiązań** > **kontenery**. toosee uzyskać więcej informacji, kliknij Kafelek hello.

Zobacz hello [dokumentacji usługi Analiza dzienników Azure](../../log-analytics/index.md) szczegółowe wskazówki dotyczące zapytań i analizowanie danych monitorowania.

## <a name="next-steps"></a>Następne kroki

W tym samouczku monitorowane są klastra Kubernetes z usługą OMS. Uwzględnione objętych zadań:

> [!div class="checklist"]
> * Pobierz ustawienia obszarem roboczym pakietu OMS
> * Konfigurowanie agentów OMS na węzłach Kubernetes hello
> * Dostęp do monitorowania informacji w portalu OMS hello lub w portalu Azure


Postępuj zgodnie z tym toosee łącze wstępnie skompilowany przykłady skryptów dla usługi kontenera.

> [!div class="nextstepaction"]
> [Przykłady skryptów usługi kontenera platformy Azure](cli-samples.md)
