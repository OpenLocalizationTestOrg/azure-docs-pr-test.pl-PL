---
title: "Samouczek usługi kontenera aaaAzure — skalowania aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — skalowania aplikacji"
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
ms.openlocfilehash: 29571eef0fd91bd6b40f00d8c018539f320179bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-kubernetes-pods-and-kubernetes-infrastructure"></a>Infrastruktura Kubernetes i stanowiskami Kubernetes skali

Jeśli została już następujące samouczki hello, masz działające Kubernetes klastra usługi kontenera platformy Azure i hello Azure głosowania aplikacja została wdrożona. 

W tym samouczku, część 5, 7 skalowanie w poziomie stanowiskami hello w aplikacji hello i spróbuj pod Skalowanie automatyczne. Możesz też dowiedzieć się, jak tooscale hello liczba toochange węzłów agenta maszyny Wirtualnej Azure hello wydajności obsługi obciążeń klastra. Zadania ukończone obejmują:

> [!div class="checklist"]
> * Ręcznie skalowanie stanowiskami Kubernetes
> * Konfigurowanie stanowiskami skalowania automatycznego uruchamiania fronton aplikacji hello
> * Skalowanie hello Kubernetes agenta programu Azure węzłów

W kolejnych samouczkach hello aplikacji Azure głos jest aktualizowana, a usługi Operations Management Suite skonfigurowane toomonitor hello Kubernetes klastra.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W poprzednich samouczków aplikacji zostało umieszczone w obrazie kontenera, ten obraz przekazany tooAzure rejestru kontenera i utworzyć klaster Kubernetes. Aplikacja Hello następnie zostało uruchomione na powitania Kubernetes klastra. Jeśli nie zostało wykonane następujące kroki, a chcesz toofollow wzdłuż, zwróć toohello [samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md). 

Co najmniej tego samouczka wymaga klastra Kubernetes z działającej aplikacji.

## <a name="manually-scale-pods"></a>Ręcznie skalować stanowiskami

W związku z tym do tej pory, zostały wdrożone hello Azure głos frontonu i wystąpienia pamięci podręcznej Redis, każda z pojedynczą replikę. tooverify Uruchom hello [kubectl uzyskać](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) polecenia.

```azurecli-interactive
kubectl get pods
```

Dane wyjściowe:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2549686872-4d2r5   1/1       Running   0          31m
azure-vote-front-848767080-tf34m   1/1       Running   0          31m
```

Ręcznie zmień liczbę hello stanowiskami w hello `azure-vote-front` wdrożenia przy użyciu hello [kubectl skali](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#scale) polecenia. W tym przykładzie zwiększa numer too5 hello.

```azurecli-interactive
kubectl scale --replicas=5 deployment/azure-vote-front
```

Uruchom [kubectl uzyskać stanowiskami](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) tooverify czy Kubernetes tworzy stanowiskami hello. Po minucie lub tak system hello stanowiskami dodatkowe:

```azurecli-interactive
kubectl get pods
```

Dane wyjściowe:

```bash
NAME                                READY     STATUS    RESTARTS   AGE
azure-vote-back-2606967446-nmpcf    1/1       Running   0          15m
azure-vote-front-3309479140-2hfh0   1/1       Running   0          3m
azure-vote-front-3309479140-bzt05   1/1       Running   0          3m
azure-vote-front-3309479140-fvcvm   1/1       Running   0          3m
azure-vote-front-3309479140-hrbf2   1/1       Running   0          15m
azure-vote-front-3309479140-qphz8   1/1       Running   0          3m
```

## <a name="autoscale-pods"></a>Stanowiskami skalowania automatycznego

Obsługuje Kubernetes [Skalowanie automatyczne poziome pod](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) tooadjust hello liczba stanowiskami we wdrożeniu w zależności od użycia procesora CPU lub inne wybrać metryki. 

toouse hello autoscaler, Twoje stanowiskami musi mieć żądań procesora CPU i zdefiniowano limitów. W hello `azure-vote-front` wdrożenia, hello Procesora żądań 0,25 kontenera frontonu, limit 0,5 procesora CPU. Ustawienia Hello następującą postać:

```YAML
resources:
  requests:
     cpu: 250m
  limits:
     cpu: 500m
```

Witaj poniższym przykładzie użyto hello [skalowania automatycznego kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#autoscale) polecenia tooautoscale hello liczba stanowiskami w hello `azure-vote-front` wdrożenia. W tym miejscu Jeśli wykorzystanie procesora CPU przekracza 50%, hello autoscaler zwiększa hello stanowiskami tooa maksymalnie 10.


```azurecli-interactive
kubectl autoscale deployment azure-vote-front --cpu-percent=50 --min=3 --max=10
```

Stan hello toosee autoscaler hello, uruchom następujące polecenie hello:

```azurecli-interactive
kubectl get hpa
```

Dane wyjściowe:

```bash
NAME               REFERENCE                     TARGETS    MINPODS   MAXPODS   REPLICAS   AGE
azure-vote-front   Deployment/azure-vote-front   0% / 50%   3         10        3          2m
```

Po upływie kilku minut przy minimalnym obciążeniu hello Azure głos aplikacji hello liczby replik pod zmniejsza automatycznie too3.

## <a name="scale-hello-agents"></a>Agenci hello skali

Jeśli utworzony klaster Kubernetes przy użyciu polecenia domyślne w samouczku poprzedniej hello ma trzy węzły agenta. Hello liczby agentów można dostosować ręcznie, jeśli planujesz więcej lub mniej obciążeń kontenera w klastrze. Użyj hello [skalować acs az](/cli/azure/acs#scale) polecenia i określić hello liczby agentów z hello `--new-agent-count` parametru.

Hello poniższy przykład zwiększa liczbę hello agenta too4 węzłów w klastrze Kubernetes hello o nazwie *myK8sCluster*. polecenie Hello zajmuje kilka minut toocomplete.

```azurecli-interactive
az acs scale --resource-group=myResourceGroup --name=myK8SCluster --new-agent-count 4
```

Hello dane wyjściowe polecenia zawiera hello numer agenta węzłów w wartości hello `agentPoolProfiles:count`:

```azurecli
{
  "agentPoolProfiles": [
    {
      "count": 4,
      "dnsPrefix": "myK8SCluster-myK8SCluster-e44f25-k8s-agents",
      "fqdn": "",
      "name": "agentpools",
      "vmSize": "Standard_D2_v2"
    }
  ],
...

```

## <a name="next-steps"></a>Następne kroki

W tym samouczku użyto różnych funkcji skalowania w klastrze Kubernetes. Uwzględnione objętych zadań:

> [!div class="checklist"]
> * Ręcznie skalowanie stanowiskami Kubernetes
> * Konfigurowanie stanowiskami skalowania automatycznego uruchamiania fronton aplikacji hello
> * Skalowanie hello Kubernetes agenta programu Azure węzłów

Przejdź dalej toolearn toohello dotyczące aktualizowania aplikacji w Kubernetes samouczka.

> [!div class="nextstepaction"]
> [Aktualizuj aplikację w Kubernetes](./container-service-tutorial-kubernetes-app-update.md)

