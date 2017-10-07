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
# <a name="create-container-images-toobe-used-with-azure-container-service"></a><span data-ttu-id="83b7f-104">Tworzenie kontenera toobe obrazy używane z usługą kontenera Azure</span><span class="sxs-lookup"><span data-stu-id="83b7f-104">Create container images toobe used with Azure Container Service</span></span>

<span data-ttu-id="83b7f-105">W tym samouczku, część 7, pierwsza aplikacji kontenera wielu jest gotowy do użycia w Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="83b7f-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="83b7f-106">Ukończono kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="83b7f-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="83b7f-107">Klonowanie źródła aplikacji z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="83b7f-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="83b7f-108">Tworzenie obrazu kontenera ze źródła aplikacji hello</span><span class="sxs-lookup"><span data-stu-id="83b7f-108">Creating a container image from hello application source</span></span>
> * <span data-ttu-id="83b7f-109">Testowanie aplikacji hello w lokalnym środowisku Docker</span><span class="sxs-lookup"><span data-stu-id="83b7f-109">Testing hello application in a local Docker environment</span></span>

<span data-ttu-id="83b7f-110">Po ukończeniu po aplikacji hello jest dostępny w środowisku projektowania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="83b7f-110">Once completed, hello following application is accessible in your local development environment.</span></span>

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="83b7f-112">W kolejnych samouczkach obraz kontenera hello jest przekazany tooan rejestru kontenera platformy Azure, a następnie uruchom na platformie Azure hostowanej Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="83b7f-112">In subsequent tutorials, hello container image is uploaded tooan Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="83b7f-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="83b7f-113">Before you begin</span></span>

<span data-ttu-id="83b7f-114">Ten samouczek zakłada, że masz podstawową wiedzę na temat bazowych koncepcji usługi Docker, takich jak kontenery, obrazy kontenerów i podstawowe polecenia usługi Docker.</span><span class="sxs-lookup"><span data-stu-id="83b7f-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="83b7f-115">W razie potrzeby zapoznaj się z tematem [Get starter with Docker (Rozpoczynanie pracy z platformą Docker)]( https://docs.docker.com/get-started/), aby uzyskać podstawowe informacje na temat kontenerów.</span><span class="sxs-lookup"><span data-stu-id="83b7f-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="83b7f-116">toocomplete tego samouczka potrzebne jest środowisko rozwoju Docker.</span><span class="sxs-lookup"><span data-stu-id="83b7f-116">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="83b7f-117">Środowisko Docker zawiera pakiety, które umożliwiają łatwe konfigurowanie platformy Docker w systemie [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) lub [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="83b7f-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="83b7f-118">Pobieranie kodu aplikacji</span><span class="sxs-lookup"><span data-stu-id="83b7f-118">Get application code</span></span>

<span data-ttu-id="83b7f-119">Witaj przykładowej aplikacji używanych w tym samouczku jest podstawowa aplikacja głosu.</span><span class="sxs-lookup"><span data-stu-id="83b7f-119">hello sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="83b7f-120">Aplikacja Hello składa się z składników frontonu sieci web oraz wystąpienia pamięci podręcznej Redis zaplecza.</span><span class="sxs-lookup"><span data-stu-id="83b7f-120">hello application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="83b7f-121">składnik web Hello jest umieszczone w obrazu niestandardowego kontenera.</span><span class="sxs-lookup"><span data-stu-id="83b7f-121">hello web component is packaged into a custom container image.</span></span> <span data-ttu-id="83b7f-122">wystąpienie pamięci podręcznej Redis Hello używa niezmodyfikowanego obrazu z Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="83b7f-122">hello Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="83b7f-123">Użyj narzędzia git toodownload kopię środowisko projektowe tooyour aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="83b7f-123">Use git toodownload a copy of hello application tooyour development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="83b7f-124">Katalog sklonowany hello wewnątrz kodu źródłowego aplikacji hello, wstępnie utworzone rozwiązania Docker compose plików i Kubernetes pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="83b7f-124">Inside hello cloned directory is hello application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="83b7f-125">Te pliki są zasoby toocreate używanych w całym hello samouczek zestawu.</span><span class="sxs-lookup"><span data-stu-id="83b7f-125">These files are used toocreate assets throughout hello tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="83b7f-126">Tworzenie kontenera obrazów</span><span class="sxs-lookup"><span data-stu-id="83b7f-126">Create container images</span></span>

<span data-ttu-id="83b7f-127">[Rozwiązania docker Compose](https://docs.docker.com/compose/) może być używany kompilacji hello tooautomate poza kontener obrazów i hello wdrożenia usługi kontenera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83b7f-127">[Docker Compose](https://docs.docker.com/compose/) can be used tooautomate hello build out of container images and hello deployment of multi-container applications.</span></span>

<span data-ttu-id="83b7f-128">Uruchom hello docker-compose.yml pliku toocreate hello kontener obrazu, pobierania hello Redis obrazu i uruchomić aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="83b7f-128">Run hello docker-compose.yml file toocreate hello container image, download hello Redis image, and start hello application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="83b7f-129">Po zakończeniu Użyj hello [obrazy usługi docker](https://docs.docker.com/engine/reference/commandline/images/) polecenia toosee hello utworzyć obrazy.</span><span class="sxs-lookup"><span data-stu-id="83b7f-129">When completed, use hello [docker images](https://docs.docker.com/engine/reference/commandline/images/) command toosee hello created images.</span></span>

```bash
docker images
```

<span data-ttu-id="83b7f-130">Zwróć uwagę, że zostały pobrane lub utworzone trzy obrazy.</span><span class="sxs-lookup"><span data-stu-id="83b7f-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="83b7f-131">Witaj *azure głos początku* obraz zawiera hello aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83b7f-131">hello *azure-vote-front* image contains hello application.</span></span> <span data-ttu-id="83b7f-132">Został utworzony z hello *nginx flask* obrazu.</span><span class="sxs-lookup"><span data-stu-id="83b7f-132">It was derived from hello *nginx-flask* image.</span></span> <span data-ttu-id="83b7f-133">Obraz Redis Hello pobranego z Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="83b7f-133">hello Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="83b7f-134">Uruchom hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) hello toosee polecenia uruchomionych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="83b7f-134">Run hello [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command toosee hello running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="83b7f-135">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="83b7f-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="83b7f-136">Testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="83b7f-136">Test application locally</span></span>

<span data-ttu-id="83b7f-137">Przeglądaj hello toosee toohttp://localhost:8080 uruchomiona aplikacja.</span><span class="sxs-lookup"><span data-stu-id="83b7f-137">Browse toohttp://localhost:8080 toosee hello running application.</span></span>

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="83b7f-139">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="83b7f-139">Clean up resources</span></span>

<span data-ttu-id="83b7f-140">Teraz, gdy została zweryfikowana funkcjonalność aplikacji hello uruchomionych kontenerów można zatrzymana i usunięta.</span><span class="sxs-lookup"><span data-stu-id="83b7f-140">Now that application functionality has been validated, hello running containers can be stopped and removed.</span></span> <span data-ttu-id="83b7f-141">Nie należy usuwać hello kontener obrazów.</span><span class="sxs-lookup"><span data-stu-id="83b7f-141">Do not delete hello container images.</span></span> <span data-ttu-id="83b7f-142">Witaj *azure głos początku* obrazu jest wystąpieniem rejestru kontenera Azure tooan przekazanego w następnym samouczku hello.</span><span class="sxs-lookup"><span data-stu-id="83b7f-142">hello *azure-vote-front* image is uploaded tooan Azure Container Registry instance in hello next tutorial.</span></span>

<span data-ttu-id="83b7f-143">Uruchom powitania po hello toostop uruchomionych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="83b7f-143">Run hello following toostop hello running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="83b7f-144">Usuń kontenery hello zatrzymana z hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="83b7f-144">Delete hello stopped containers with hello following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="83b7f-145">Po ukończeniu masz obraz kontenera, który zawiera hello Azure głos aplikacji.</span><span class="sxs-lookup"><span data-stu-id="83b7f-145">At completion, you have a container image that contains hello Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83b7f-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="83b7f-146">Next steps</span></span>

<span data-ttu-id="83b7f-147">W tym samouczku przetestowano aplikacji i kontener obrazów utworzonych dla aplikacji hello.</span><span class="sxs-lookup"><span data-stu-id="83b7f-147">In this tutorial, an application was tested and container images created for hello application.</span></span> <span data-ttu-id="83b7f-148">Zakończono Hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="83b7f-148">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="83b7f-149">Klonowanie źródła aplikacji hello z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="83b7f-149">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="83b7f-150">Utworzony obraz kontenera ze źródła aplikacji</span><span class="sxs-lookup"><span data-stu-id="83b7f-150">Created a container image from application source</span></span>
> * <span data-ttu-id="83b7f-151">Hello przetestowanej aplikacji w środowisku lokalnym Docker</span><span class="sxs-lookup"><span data-stu-id="83b7f-151">Tested hello application in a local Docker environment</span></span>

<span data-ttu-id="83b7f-152">Przejdź dalej toolearn samouczka toohello o przechowywania obrazów kontenera w rejestrze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="83b7f-152">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="83b7f-153">Wypychanie tooAzure obrazów rejestru kontenera</span><span class="sxs-lookup"><span data-stu-id="83b7f-153">Push images tooAzure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)
