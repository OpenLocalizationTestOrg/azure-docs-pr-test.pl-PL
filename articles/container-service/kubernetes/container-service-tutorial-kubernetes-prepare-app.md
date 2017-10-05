---
title: "Samouczek usługi kontenera platformy Azure — przygotowanie aplikacji | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f02ee61ef1cd3b3dfaa051cfabe52866e3e7e838
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-container-images-to-be-used-with-azure-container-service"></a><span data-ttu-id="1e475-104">Tworzenie kontenera obrazów do użycia z usługą kontenera Azure</span><span class="sxs-lookup"><span data-stu-id="1e475-104">Create container images to be used with Azure Container Service</span></span>

<span data-ttu-id="1e475-105">W tym samouczku, część 7, pierwsza aplikacji kontenera wielu jest gotowy do użycia w Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="1e475-105">In this tutorial, part one of seven, a multi-container application is prepared for use in Kubernetes.</span></span> <span data-ttu-id="1e475-106">Ukończono kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="1e475-106">Steps completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="1e475-107">Klonowanie źródła aplikacji z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="1e475-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="1e475-108">Tworzenie obrazu kontenera ze źródła aplikacji</span><span class="sxs-lookup"><span data-stu-id="1e475-108">Creating a container image from the application source</span></span>
> * <span data-ttu-id="1e475-109">Testowanie aplikacji w środowisku lokalnym Docker</span><span class="sxs-lookup"><span data-stu-id="1e475-109">Testing the application in a local Docker environment</span></span>

<span data-ttu-id="1e475-110">Po wykonaniu następującej aplikacji jest dostępny w środowisku projektowania lokalnego.</span><span class="sxs-lookup"><span data-stu-id="1e475-110">Once completed, the following application is accessible in your local development environment.</span></span>

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

<span data-ttu-id="1e475-112">W kolejnych samouczkach obrazu kontenera jest przekazywany do rejestru kontenera platformy Azure, a następnie uruchom na platformie Azure hostowanej Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="1e475-112">In subsequent tutorials, the container image is uploaded to an Azure Container Registry, and then run in an Azure hosted Kubernetes cluster.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1e475-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="1e475-113">Before you begin</span></span>

<span data-ttu-id="1e475-114">Ten samouczek zakłada, że masz podstawową wiedzę na temat bazowych koncepcji usługi Docker, takich jak kontenery, obrazy kontenerów i podstawowe polecenia usługi Docker.</span><span class="sxs-lookup"><span data-stu-id="1e475-114">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="1e475-115">W razie potrzeby zapoznaj się z tematem [Get starter with Docker (Rozpoczynanie pracy z platformą Docker)]( https://docs.docker.com/get-started/), aby uzyskać podstawowe informacje na temat kontenerów.</span><span class="sxs-lookup"><span data-stu-id="1e475-115">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="1e475-116">Do ukończenia tego samouczka konieczne będzie środowisko programowania Docker.</span><span class="sxs-lookup"><span data-stu-id="1e475-116">To complete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="1e475-117">Środowisko Docker zawiera pakiety, które umożliwiają łatwe konfigurowanie platformy Docker w systemie [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) lub [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="1e475-117">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="1e475-118">Pobieranie kodu aplikacji</span><span class="sxs-lookup"><span data-stu-id="1e475-118">Get application code</span></span>

<span data-ttu-id="1e475-119">Przykładowa aplikacja używana w tym samouczku jest podstawowa aplikacja głosu.</span><span class="sxs-lookup"><span data-stu-id="1e475-119">The sample application used in this tutorial is a basic voting app.</span></span> <span data-ttu-id="1e475-120">Aplikacja składa się z składników frontonu sieci web oraz wystąpienia pamięci podręcznej Redis zaplecza.</span><span class="sxs-lookup"><span data-stu-id="1e475-120">The application consists of a front-end web component and a back-end Redis instance.</span></span> <span data-ttu-id="1e475-121">Części sieci web jest dostarczana w obraz niestandardowy kontenera.</span><span class="sxs-lookup"><span data-stu-id="1e475-121">The web component is packaged into a custom container image.</span></span> <span data-ttu-id="1e475-122">Wystąpienie pamięci podręcznej Redis używa niezmodyfikowanego obrazu z Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="1e475-122">The Redis instance uses an unmodified image from Docker Hub.</span></span>  

<span data-ttu-id="1e475-123">Użyj git, aby pobrać kopię aplikacji w środowisku deweloperskim.</span><span class="sxs-lookup"><span data-stu-id="1e475-123">Use git to download a copy of the application to your development environment.</span></span>

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="1e475-124">W katalogu sklonowany jest kodu źródłowego aplikacji, wstępnie utworzone rozwiązania Docker compose plików i Kubernetes pliku manifestu.</span><span class="sxs-lookup"><span data-stu-id="1e475-124">Inside the cloned directory is the application source code, a pre-created Docker compose file, and a Kubernetes manifest file.</span></span> <span data-ttu-id="1e475-125">Te pliki służą do tworzenia zasobów w całym zestawie samouczka.</span><span class="sxs-lookup"><span data-stu-id="1e475-125">These files are used to create assets throughout the tutorial set.</span></span> 

## <a name="create-container-images"></a><span data-ttu-id="1e475-126">Tworzenie kontenera obrazów</span><span class="sxs-lookup"><span data-stu-id="1e475-126">Create container images</span></span>

<span data-ttu-id="1e475-127">[Rozwiązania docker Compose](https://docs.docker.com/compose/) może służyć do automatyzowania kompilacji poza kontener obrazów i wdrożenia usługi kontenera aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e475-127">[Docker Compose](https://docs.docker.com/compose/) can be used to automate the build out of container images and the deployment of multi-container applications.</span></span>

<span data-ttu-id="1e475-128">Uruchom plik docker-compose.yml, aby utworzyć obraz kontenera, pobranie obrazu do pamięci podręcznej Redis i uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="1e475-128">Run the docker-compose.yml file to create the container image, download the Redis image, and start the application.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml up -d
```

<span data-ttu-id="1e475-129">Po zakończeniu użyj [obrazy usługi docker](https://docs.docker.com/engine/reference/commandline/images/) polecenie, aby wyświetlić utworzony obrazów.</span><span class="sxs-lookup"><span data-stu-id="1e475-129">When completed, use the [docker images](https://docs.docker.com/engine/reference/commandline/images/) command to see the created images.</span></span>

```bash
docker images
```

<span data-ttu-id="1e475-130">Zwróć uwagę, że zostały pobrane lub utworzone trzy obrazy.</span><span class="sxs-lookup"><span data-stu-id="1e475-130">Notice that three images have been downloaded or created.</span></span> <span data-ttu-id="1e475-131">*Azure głos początku* obraz zawiera aplikację.</span><span class="sxs-lookup"><span data-stu-id="1e475-131">The *azure-vote-front* image contains the application.</span></span> <span data-ttu-id="1e475-132">Został uzyskany z *nginx flask* obrazu.</span><span class="sxs-lookup"><span data-stu-id="1e475-132">It was derived from the *nginx-flask* image.</span></span> <span data-ttu-id="1e475-133">Obraz Redis pobranego z Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="1e475-133">The Redis image was downloaded from Docker Hub.</span></span>

```bash
REPOSITORY                   TAG        IMAGE ID            CREATED             SIZE
azure-vote-front             latest     9cc914e25834        40 seconds ago      694MB
redis                        latest     a1b99da73d05        7 days ago          106MB
tiangolo/uwsgi-nginx-flask   flask      788ca94b2313        9 months ago        694MB
```

<span data-ttu-id="1e475-134">Uruchom [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) polecenie, aby wyświetlić uruchomionych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="1e475-134">Run the [docker ps](https://docs.docker.com/engine/reference/commandline/ps/) command to see the running containers.</span></span>

```bash
docker ps
```

<span data-ttu-id="1e475-135">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="1e475-135">Output:</span></span>

```bash
CONTAINER ID        IMAGE             COMMAND                  CREATED             STATUS              PORTS                           NAMES
82411933e8f9        azure-vote-front  "/usr/bin/supervisord"   57 seconds ago      Up 30 seconds       443/tcp, 0.0.0.0:8080->80/tcp   azure-vote-front
b68fed4b66b6        redis             "docker-entrypoint..."   57 seconds ago      Up 30 seconds       0.0.0.0:6379->6379/tcp          azure-vote-back
```

## <a name="test-application-locally"></a><span data-ttu-id="1e475-136">Testowanie aplikacji lokalnie</span><span class="sxs-lookup"><span data-stu-id="1e475-136">Test application locally</span></span>

<span data-ttu-id="1e475-137">Przejdź do adresem http://localhost: 8080, aby zobaczyć działającej aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e475-137">Browse to http://localhost:8080 to see the running application.</span></span>

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="clean-up-resources"></a><span data-ttu-id="1e475-139">Oczyszczanie zasobów</span><span class="sxs-lookup"><span data-stu-id="1e475-139">Clean up resources</span></span>

<span data-ttu-id="1e475-140">Teraz, funkcjonalność aplikacji została zweryfikowana, uruchomionych kontenerów można zatrzymać i usunięte.</span><span class="sxs-lookup"><span data-stu-id="1e475-140">Now that application functionality has been validated, the running containers can be stopped and removed.</span></span> <span data-ttu-id="1e475-141">Nie należy usuwać obrazy kontenera.</span><span class="sxs-lookup"><span data-stu-id="1e475-141">Do not delete the container images.</span></span> <span data-ttu-id="1e475-142">*Azure głos początku* obraz jest przekazywany do wystąpienia rejestru kontenera platformy Azure w następnym samouczku.</span><span class="sxs-lookup"><span data-stu-id="1e475-142">The *azure-vote-front* image is uploaded to an Azure Container Registry instance in the next tutorial.</span></span>

<span data-ttu-id="1e475-143">Uruchom następujące polecenie, aby zatrzymać uruchomionych kontenerów.</span><span class="sxs-lookup"><span data-stu-id="1e475-143">Run the following to stop the running containers.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml stop
```

<span data-ttu-id="1e475-144">Usuń zatrzymane kontenerów przy użyciu następującego polecenia.</span><span class="sxs-lookup"><span data-stu-id="1e475-144">Delete the stopped containers with the following command.</span></span>

```bash
docker-compose -f ./azure-voting-app-redis/docker-compose.yml rm
```

<span data-ttu-id="1e475-145">Po ukończeniu masz obraz kontenera, który zawiera aplikację Azure głos.</span><span class="sxs-lookup"><span data-stu-id="1e475-145">At completion, you have a container image that contains the Azure Vote application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e475-146">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="1e475-146">Next steps</span></span>

<span data-ttu-id="1e475-147">W tym samouczku przetestowano aplikacji i kontener obrazów utworzonych dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="1e475-147">In this tutorial, an application was tested and container images created for the application.</span></span> <span data-ttu-id="1e475-148">Wykonano następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="1e475-148">The following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1e475-149">Klonowanie źródła aplikacji z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="1e475-149">Cloning the application source from GitHub</span></span>  
> * <span data-ttu-id="1e475-150">Utworzony obraz kontenera ze źródła aplikacji</span><span class="sxs-lookup"><span data-stu-id="1e475-150">Created a container image from application source</span></span>
> * <span data-ttu-id="1e475-151">Przetestowany aplikacji w lokalnym środowisku Docker</span><span class="sxs-lookup"><span data-stu-id="1e475-151">Tested the application in a local Docker environment</span></span>

<span data-ttu-id="1e475-152">Przejdź do kolejnego samouczka, aby dowiedzieć się więcej o przechowywaniu obrazów kontenera w usłudze Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="1e475-152">Advance to the next tutorial to learn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e475-153">Wypychanie obrazów do usługi Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="1e475-153">Push images to Azure Container Registry</span></span>](./container-service-tutorial-kubernetes-prepare-acr.md)