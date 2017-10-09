---
title: "Samouczek usługi kontenera aaaAzure — wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — wdrażanie aplikacji"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7e2fa06d359caf83e684df3966624a6e9a8e7efa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="run-applications-in-kubernetes"></a>Uruchamianie aplikacji w Kubernetes

W tym samouczku część cztery siedmiu, przykładowa aplikacja jest wdrażana w klastrze Kubernetes. Ukończono kroki obejmują:

> [!div class="checklist"]
> * Pobierz pliki manifestu Kubernetes
> * Uruchom aplikację w Kubernetes
> * Testowanie aplikacji hello

W kolejnych samouczkach tej aplikacji jest skalowanie, aktualizacji i Operations Management Suite skonfigurowany toomonitor hello Kubernetes klastra.

Ten samouczek zakłada podstawową wiedzę na temat pojęć Kubernetes, aby uzyskać szczegółowe informacje na temat Kubernetes Zobacz hello [dokumentacji Kubernetes](https://kubernetes.io/docs/home/).

## <a name="before-you-begin"></a>Przed rozpoczęciem

W poprzednich samouczki aplikacji zostało umieszczone w obrazie kontenera, ten obraz został przekazany tooAzure rejestru kontenera i klaster Kubernetes został utworzony. Jeśli nie zostało wykonane następujące kroki, a chcesz toofollow wzdłuż, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md). 

Co najmniej tego samouczka wymaga Kubernetes klastra.

## <a name="get-manifest-file"></a>Pobierz plik manifestu

W tym samouczku [obiektów Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) są wdrażane za pomocą Kubernetes manifestu. Kubernetes manifest jest yaml programu lub JSON sformatowanym plikiem instrukcjami Kubernetes obiektu wdrażania i konfiguracji.

Plik manifestu aplikacji Hello w tym samouczku jest dostępna w hello Azure głos aplikacji repozytorium, który został sklonowany w poprzednim samouczka. Jeśli nie zostało to jeszcze zrobione, klonowanie repozytorium hello z hello następujące polecenie: 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Plik manifestu Hello znajduje się w hello następującego katalogu hello sklonować repozytorium.

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>Aktualizacja pliku manifestu

Jeśli za pomocą rejestru kontenera Azure toostore hello kontener obrazów, toobe manifestu potrzeb hello zaktualizowane hello nazwa ACR loginServer.

Pobierz nazwę serwera hello ACR logowania z hello [listy acr az](/cli/azure/acr#list) polecenia.

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Witaj próbki manifest został wstępnie utworzone przy użyciu nazwy repozytorium *microsoft*. Otwórz plik hello w dowolnym edytorze tekstu i Zastąp hello *microsoft* wartości z nazwą serwera logowania hello wystąpienia ACR.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>Wdrażanie aplikacji

Użyj hello [kubectl utworzyć](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) polecenia aplikacji hello toorun. Tego polecenia po analizie hello pliku manifestu i tworzenie obiektów Kubernetes hello zdefiniowane.

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

Dane wyjściowe:

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a>Testowanie aplikacji

A [usługi Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) jest tworzony, który udostępnia toohello aplikacji hello internet. Może to potrwać kilka minut. 

postęp toomonitor, użyj hello [kubectl pobrać usługi](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) z hello `--watch` argumentu.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Początkowo hello **IP zewnętrznego** dla hello *azure głos początku* usługi pojawia się jako *oczekujące*. Gdy adres IP zewnętrznego hello zmienił się z *oczekujące* tooan *adres IP*, użyj `CTRL-C` toostop hello kubectl czujki procesu.

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

Aplikacja hello toosee, przeglądania toohello zewnętrzny adres IP.

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>Następne kroki

W tym samouczku hello Azure głos aplikacji został wdrożony tooan klastra Kubernetes usługi kontenera platformy Azure. Zadania ukończone obejmują:  

> [!div class="checklist"]
> * Pobierz pliki manifestu Kubernetes
> * Uruchamianie aplikacji hello w Kubernetes
> * Aplikacja hello przetestowany

Przejdź dalej toolearn toohello temat skalowania aplikacji Kubernetes jak hello podstawowej infrastruktury Kubernetes samouczka. 

> [!div class="nextstepaction"]
> [Skala Kubernetes aplikacji i infrastruktury](./container-service-tutorial-kubernetes-scale.md)