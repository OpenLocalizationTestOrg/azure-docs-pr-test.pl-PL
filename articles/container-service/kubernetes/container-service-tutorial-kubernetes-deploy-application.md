---
title: "Samouczek usługi kontenera platformy Azure — wdrażanie aplikacji | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: ea67f0beb6a5926393b26e7590302ad0f46a63f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="run-applications-in-kubernetes"></a>Uruchamianie aplikacji w Kubernetes

W tym samouczku część cztery siedmiu, przykładowa aplikacja jest wdrażana w klastrze Kubernetes. Ukończono kroki obejmują:

> [!div class="checklist"]
> * Pobierz pliki manifestu Kubernetes
> * Uruchom aplikację w Kubernetes
> * Testowanie aplikacji

W kolejnych samouczkach tej aplikacji jest skalowana, aktualizacji, oraz Operations Management Suite jest skonfigurowana do monitorowania Kubernetes klastra.

Ten samouczek zakłada podstawową wiedzę na temat pojęć Kubernetes, aby uzyskać szczegółowe informacje o Zobacz Kubernetes [dokumentacji Kubernetes](https://kubernetes.io/docs/home/).

## <a name="before-you-begin"></a>Przed rozpoczęciem

W poprzednim samouczki aplikacji zostało umieszczone w obrazie kontenera, ten obraz został załadowany w rejestrze kontenera Azure i klaster Kubernetes został utworzony. Jeśli nie zostało wykonane następujące kroki, a następnie zostać z niego skorzystać, wróć do [samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md). 

Co najmniej tego samouczka wymaga Kubernetes klastra.

## <a name="get-manifest-file"></a>Pobierz plik manifestu

W tym samouczku [obiektów Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) są wdrażane za pomocą Kubernetes manifestu. Kubernetes manifest jest yaml programu lub JSON sformatowanym plikiem instrukcjami Kubernetes obiektu wdrażania i konfiguracji.

Plik manifestu aplikacji do celów tego samouczka jest dostępna w repozytorium aplikacji głos Azure, który został sklonowany w poprzednim samouczka. Jeśli jeszcze nie sklonuj repozytorium przy użyciu następującego polecenia: 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Plik manifestu znajduje się w następującym katalogu sklonowanego repozytorium.

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a>Aktualizacja pliku manifestu

Jeśli za pomocą rejestru kontenera Azure do przechowywania obrazów kontenera, manifest musi zostać zaktualizowany o nazwie loginServer ACR.

Pobierz nazwę serwera ACR logowania z [listy acr az](/cli/azure/acr#list) polecenia.

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Manifest próbki został wstępnie utworzone przy użyciu nazwy repozytorium *microsoft*. Otwórz plik w dowolnym edytorze tekstu i Zastąp *microsoft* wartości z nazwą serwera logowania wystąpienia ACR.

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a>Wdrażanie aplikacji

Użyj polecenia [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create), aby uruchomić aplikację. To polecenie analizuje pliku manifestu i tworzenia zdefiniowanych obiektów Kubernetes.

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

A [usługi Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) jest tworzony, który udostępnia aplikacji w Internecie. Może to potrwać kilka minut. 

Aby monitorować postęp, użyj polecenia [kubectl get-service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) z argumentem `--watch`.

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

Początkowo **IP zewnętrznego** dla *azure głos początku* usługi pojawia się jako *oczekujące*. Po zmianie adresu EXTERNAL-IP z *oczekującego* na *adres IP*, użyj polecenia `CTRL-C`, aby zatrzymać proces śledzenia narzędzia kubectl.

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

Aby wyświetlić aplikację, przejdź do zewnętrznego adresu IP.

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a>Następne kroki

W tym samouczku aplikacji Azure głos został wdrożony do klastra Kubernetes usługi kontenera platformy Azure. Zadania ukończone obejmują:  

> [!div class="checklist"]
> * Pobierz pliki manifestu Kubernetes
> * Uruchom aplikację w Kubernetes
> * Przetestowane aplikacji

Przejdź do następnego samouczka, aby dowiedzieć się więcej na temat skalowania aplikacji Kubernetes jak podstawowej infrastruktury Kubernetes. 

> [!div class="nextstepaction"]
> [Skala Kubernetes aplikacji i infrastruktury](./container-service-tutorial-kubernetes-scale.md)