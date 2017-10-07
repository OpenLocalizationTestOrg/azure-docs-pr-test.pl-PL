---
title: "Samouczek usługi kontenera aaaAzure — przygotowanie aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — przygotowanie aplikacji"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: azurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b537ecc9ff50358fb65b128bfe6eb894dd088cc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-images-toobe-used-with-azure-container-service"></a>Tworzenie kontenera toobe obrazy używane z usługą kontenera Azure

W tym samouczku, część 7, pierwsza aplikacji kontenera wielu jest gotowy do użycia w Kubernetes. Ukończono kroki obejmują:  

> [!div class="checklist"]
> * Klonowanie źródła aplikacji z usługi GitHub  
> * Tworzenie obrazu kontenera ze źródła aplikacji hello
> * Testowanie aplikacji hello w lokalnym środowisku Docker

Po ukończeniu po aplikacji hello jest dostępny w środowisku projektowania lokalnego.

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

W kolejnych samouczkach obraz kontenera hello jest przekazany tooan rejestru kontenera platformy Azure, a następnie uruchom na platformie Azure hostowanej Kubernetes klastra.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Ten samouczek zakłada, że masz podstawową wiedzę na temat bazowych koncepcji usługi Docker, takich jak kontenery, obrazy kontenerów i podstawowe polecenia usługi Docker. W razie potrzeby zapoznaj się z tematem [Get starter with Docker (Rozpoczynanie pracy z platformą Docker)]( https://docs.docker.com/get-started/), aby uzyskać podstawowe informacje na temat kontenerów. 

toocomplete tego samouczka potrzebne jest środowisko rozwoju Docker. Środowisko Docker zawiera pakiety, które umożliwiają łatwe konfigurowanie platformy Docker w systemie [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) lub [Linux](https://docs.docker.com/engine/installation/#supported-platforms).

## <a name="get-application-code"></a>Pobieranie kodu aplikacji

Witaj przykładowej aplikacji używanych w tym samouczku jest podstawowa aplikacja głosu. Aplikacja Hello składa się z składników frontonu sieci web oraz wystąpienia pamięci podręcznej Redis zaplecza. składnik web Hello jest umieszczone w obrazu niestandardowego kontenera. wystąpienie pamięci podręcznej Redis Hello używa niezmodyfikowanego obrazu z Centrum Docker.  

Użyj narzędzia git toodownload kopię środowisko projektowe tooyour aplikacji hello.

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

Katalog sklonowany hello wewnątrz kodu źródłowego aplikacji hello, wstępnie utworzone rozwiązania Docker compose plików i Kubernetes pliku manifestu. Te pliki są zasoby toocreate używanych w całym hello samouczek zestawu. 

## <a name="create-container-images"></a>Tworzenie kontenera obrazów

[Rozwiązania docker Compose](https://docs.docker.com/compose/) może być używany kompilacji hello tooautomate poza kontener obrazów i hello wdrożenia usługi kontenera aplikacji.

Uruchom hello docker-compose.yml pliku toocreate hello kontener obrazu, pobierania hello Redis obrazu i uruchomić aplikacji hello.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

Po zakończeniu Użyj hello [obrazy usługi docker](https://docs.docker.com/engine/reference/commandline/images/) polecenia toosee hello utworzyć obrazy.

```bash
docker images
```

Zwróć uwagę, że zostały pobrane lub utworzone trzy obrazy. Witaj *azure głos początku* obraz zawiera hello aplikacji. Został utworzony z hello *nginx flask* obrazu. Obraz Redis Hello pobranego z Centrum Docker.

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

Uruchom hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) hello toosee polecenia uruchomionych kontenerów.

```bash
docker ps
```

Dane wyjściowe:

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a>Testowanie aplikacji lokalnie

Przeglądaj hello toosee toohttp://localhost:8080 uruchomiona aplikacja.

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a>Oczyszczanie zasobów

Teraz, gdy została zweryfikowana funkcjonalność aplikacji hello uruchomionych kontenerów można zatrzymana i usunięta. Nie należy usuwać hello kontener obrazów. Witaj *azure głos początku* obrazu jest wystąpieniem rejestru kontenera Azure tooan przekazanego w następnym samouczku hello.

Uruchom powitania po hello toostop uruchomionych kontenerów.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

Usuń kontenery hello zatrzymana z hello następujące polecenia.

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

Po ukończeniu masz obraz kontenera, który zawiera hello Azure głos aplikacji.

## <a name="next-steps"></a>Następne kroki

W tym samouczku przetestowano aplikacji i kontener obrazów utworzonych dla aplikacji hello. Zakończono Hello następujące kroki:

> [!div class="checklist"]
> * Klonowanie źródła aplikacji hello z usługi GitHub  
> * Utworzony obraz kontenera ze źródła aplikacji
> * Hello przetestowanej aplikacji w środowisku lokalnym Docker

Przejdź dalej toolearn samouczka toohello o przechowywania obrazów kontenera w rejestrze kontenera platformy Azure.

> [!div class="nextstepaction"]
> [Wypychanie tooAzure obrazów rejestru kontenera](./container-service-tutorial-kubernetes-prepare-acr.md)
