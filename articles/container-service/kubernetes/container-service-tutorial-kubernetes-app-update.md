---
title: "Samouczek usługi kontenera aaaAzure — aktualizacja aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — aktualizacja aplikacji"
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
ms.date: 07/26/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: c467498bab7952926a18e45ffbb21051a98739d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="update-an-application-in-kubernetes"></a>Aktualizuj aplikację w Kubernetes

Po wdrożeniu aplikacji w Kubernetes może zostać zaktualizowana, podając nowy obraz kontenera lub wersję obrazu. Podczas aktualizacji aplikacji hello aktualizacji wdrożenia są przygotowywane powoduje, że tylko część wdrożenia hello jest jednocześnie zaktualizowany. Ta aktualizacja przemieszczanego umożliwia uruchamianie procesu aktualizacji hello tookeep aplikacji hello i udostępnia mechanizm wycofywania w przypadku niepowodzenia wdrożenia. 

W tym samouczku sześciu część siedmiu hello przykładową aplikację Azure głos jest aktualizowana. Zadania, które należy wykonać obejmują:

> [!div class="checklist"]
> * Aktualizowanie hello kod aplikacji frontonu
> * Tworzenie obrazu zaktualizowane kontenera
> * Wypychanie hello kontener obrazu tooAzure rejestru kontenera
> * Wdrażanie hello zaktualizowano kontener obrazu

W kolejnych samouczkach Operations Management Suite jest skonfigurowany toomonitor hello Kubernetes klastra.

## <a name="before-you-begin"></a>Przed rozpoczęciem

W poprzednich samouczków aplikacji zostało umieszczone w obrazie kontenera, przekazać obraz powitania tooAzure rejestru kontenera i utworzyć klaster Kubernetes. Aplikacja Hello następnie zostało uruchomione na powitania Kubernetes klastra. 

Jeśli nie zostały wykonane następujące kroki i chcesz toofollow wzdłuż, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md). 

## <a name="update-application"></a>Aktualizowanie aplikacji

toocomplete hello kroki opisane w tym samouczku, użytkownik musi zostały sklonowane kopię hello Azure głos aplikacji. W razie potrzeby Utwórz tę kopię sklonowany z hello następujące polecenie:

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Otwórz hello `config_file.cfg` pliku w dowolnym edytorze kodu i tekstu. Można znaleźć tego pliku w obszarze hello następującego katalogu hello sklonować repozytorium.

```bash
 /azure-voting-app-redis/azure-vote/azure-vote/config_file.cfg
```

Zmienianie wartości hello `VOTE1VALUE` i `VOTE2VALUE`, a następnie zapisz plik hello.

```bash
# UI Configurations
TITLE = 'Azure Voting App'
VOTE1VALUE = 'Blue'
VOTE2VALUE = 'Purple'
SHOWHOST = 'false'
```

Użyj [rozwiązania docker compose](https://docs.docker.com/compose/) toore — tworzenie hello frontonu obrazu i aplikacji hello wykonywania aktualizacji.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up --build -d
```

## <a name="test-application-locally"></a>Testowanie aplikacji lokalnie

Przeglądaj zbyt`http://localhost:8080` toosee hello aktualizacji aplikacji.

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/vote-app-updated.png)

## <a name="tag-and-push-images"></a>Obrazy tagu i wypychania

Tag hello *azure głos początku* obrazu o loginServer hello hello kontenera rejestru.

Jeśli używasz rejestru kontenera Azure Pobierz hello nazwa serwera logowania z hello [listy acr az](/cli/azure/acr#list) polecenia.

```azurecli
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

Użyj [docker tag](https://docs.docker.com/engine/reference/commandline/tag/) tootag hello obrazu. Zastąp `<acrLoginServer>` z nazwą serwera logowania rejestru kontenera platformy Azure lub rejestru publicznej nazwy hosta.

```bash
docker tag azure-vote-front <acrLoginServer>/azure-vote-front:redis-v2
```

Użyj [wypychania docker](https://docs.docker.com/engine/reference/commandline/push/) tooupload hello obrazu tooyour rejestru. Zastąp `<acrLoginServer>` z nazwą serwera logowania rejestru kontenera platformy Azure lub rejestru publicznej nazwy hosta.

```bash
docker push <acrLoginServer>/azure-vote-front:redis-v2
```

## <a name="deploy-update-application"></a>Wdrażanie aktualizacji aplikacji

Maksymalny czas działania tooensure wiele wystąpień pod aplikacji hello musi być uruchomiona. Sprawdź konfigurację tego z hello [kubectl Pobierz pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) polecenia.

```bash
kubectl get pod
```

Dane wyjściowe:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-217588096-5w632    1/1       Running   0          10m
azure-vote-front-233282510-b5pkz   1/1       Running   0          10m
azure-vote-front-233282510-dhrtr   1/1       Running   0          10m
azure-vote-front-233282510-pqbfk   1/1       Running   0          10m
```

Jeśli masz wiele stanowiskami systemem hello azure głos początku obrazu skalować hello *azure głos początku* wdrożenia.


```azurecli-interactive
kubectl scale --replicas=3 deployment/azure-vote-front
```

tooupdate hello aplikacji, użyj hello [zestaw kubectl](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#set) polecenia. Aktualizacja `<acrLoginServer>` z hello logowania serwera lub nazwę hosta rejestru kontenera.

```azurecli-interactive
kubectl set image deployment azure-vote-front azure-vote-front=<acrLoginServer>/azure-vote-front:redis-v2
```

toomonitor hello wdrożenia, użyj hello [kubectl Pobierz pod](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#get) polecenia. Hello zaktualizowane aplikacja jest wdrażana, Twoje stanowiskami są zakończone i utworzony ponownie z hello nowego kontenera obrazu.

```azurecli-interactive
kubectl get pod
```

Dane wyjściowe:

```bash
NAME                               READY     STATUS    RESTARTS   AGE
azure-vote-back-2978095810-gq9g0   1/1       Running   0          5m
azure-vote-front-1297194256-tpjlg   1/1       Running   0         1m
azure-vote-front-1297194256-tptnx   1/1       Running   0         5m
azure-vote-front-1297194256-zktw9   1/1       Terminating   0         1m
```

## <a name="test-updated-application"></a>Zaktualizowano test aplikacji

Pobierz hello zewnętrzny adres IP hello *azure głos początku* usługi.

```azurecli-interactive
kubectl get service azure-vote-front
```

Przeglądaj toohello IP address toosee hello aktualizacji aplikacji.

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/vote-app-updated-external.png)

## <a name="next-steps"></a>Następne kroki

W tym samouczku aktualizacji aplikacji i wprowadzanie klastra Kubernetes tooa tej aktualizacji. Zakończono Hello następujące zadania:

> [!div class="checklist"]
> * Kod aplikacji frontonu hello zaktualizowane
> * Utworzony obraz zaktualizowane kontenera
> * Wypychana hello kontener obrazu tooAzure rejestru kontenera
> * Aplikacja hello wdrożonych aktualizacji

Następny samouczek toolearn toohello o tym, jak poprawić toomonitor Kubernetes w usłudze Operations Management Suite.

> [!div class="nextstepaction"]
> [Monitorowanie rozwiązania Kubernetes za pomocą pakietu OMS](./container-service-tutorial-kubernetes-monitor.md)