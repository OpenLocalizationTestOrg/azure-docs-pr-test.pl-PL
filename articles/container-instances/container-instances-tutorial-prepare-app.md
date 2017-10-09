---
title: "aaaAzure samouczek wystąpień kontenera — przygotowanie aplikacji | Dokumentacja platformy Azure"
description: "Przygotowywanie aplikacji do wdrożenia tooAzure wystąpień kontenera"
services: container-instances
documentationcenter: 
author: seanmck
manager: timlt
editor: 
tags: 
keywords: 
ms.assetid: 
ms.service: container-instances
ms.devlang: na
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 406ba796e5fefb1527f2e894cc3f7bbd8f7a5fd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-container-for-deployment-tooazure-container-instances"></a><span data-ttu-id="342d2-103">Utwórz kontener dla wdrożenia tooAzure wystąpień kontenera</span><span class="sxs-lookup"><span data-stu-id="342d2-103">Create container for deployment tooAzure Container Instances</span></span>

<span data-ttu-id="342d2-104">Usługa Azure Container Instances umożliwia wdrażanie kontenerów Docker w infrastrukturze platformy Azure bez aprowizowania maszyn wirtualnych ani adaptowania usług wyższego poziomu.</span><span class="sxs-lookup"><span data-stu-id="342d2-104">Azure Container Instances enables deployment of Docker containers onto Azure infrastructure without provisioning any virtual machines or adopting any higher-level service.</span></span> <span data-ttu-id="342d2-105">Podczas pracy z tym samouczkiem utworzysz prostą aplikację internetową w środowisku Node.js i spakujesz ją w kontenerze, który można uruchomić za pomocą usługi Azure Container Instances.</span><span class="sxs-lookup"><span data-stu-id="342d2-105">In this tutorial, you will build a simple web application in Node.js and package it in a container that can be run using Azure Container Instances.</span></span> <span data-ttu-id="342d2-106">Przedstawimy następujące zagadnienia:</span><span class="sxs-lookup"><span data-stu-id="342d2-106">We will cover:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="342d2-107">Klonowanie źródła aplikacji z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="342d2-107">Cloning application source from GitHub</span></span>  
> * <span data-ttu-id="342d2-108">Tworzenie obrazów kontenera z poziomu źródła aplikacji</span><span class="sxs-lookup"><span data-stu-id="342d2-108">Creating container images from application source</span></span>
> * <span data-ttu-id="342d2-109">Testowanie obrazów hello w lokalnym środowisku Docker</span><span class="sxs-lookup"><span data-stu-id="342d2-109">Testing hello images in a local Docker environment</span></span>

<span data-ttu-id="342d2-110">W kolejnych samouczkach będzie przekazać tooan Twojego obrazu rejestru kontenera platformy Azure, a następnie wdrożyć je tooAzure wystąpień kontenera.</span><span class="sxs-lookup"><span data-stu-id="342d2-110">In subsequent tutorials, you will upload your image tooan Azure Container Registry, and then deploy them tooAzure Container Instances.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="342d2-111">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="342d2-111">Before you begin</span></span>

<span data-ttu-id="342d2-112">Ten samouczek zakłada, że masz podstawową wiedzę na temat bazowych koncepcji usługi Docker, takich jak kontenery, obrazy kontenerów i podstawowe polecenia usługi Docker.</span><span class="sxs-lookup"><span data-stu-id="342d2-112">This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and basic docker commands.</span></span> <span data-ttu-id="342d2-113">W razie potrzeby zapoznaj się z tematem [Get starter with Docker (Rozpoczynanie pracy z platformą Docker)]( https://docs.docker.com/get-started/), aby uzyskać podstawowe informacje na temat kontenerów.</span><span class="sxs-lookup"><span data-stu-id="342d2-113">If needed, see [Get started with Docker]( https://docs.docker.com/get-started/) for a primer on container basics.</span></span> 

<span data-ttu-id="342d2-114">toocomplete tego samouczka potrzebne jest środowisko rozwoju Docker.</span><span class="sxs-lookup"><span data-stu-id="342d2-114">toocomplete this tutorial, you need a Docker development environment.</span></span> <span data-ttu-id="342d2-115">Środowisko Docker zawiera pakiety, które umożliwiają łatwe konfigurowanie platformy Docker w systemie [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/) lub [Linux](https://docs.docker.com/engine/installation/#supported-platforms).</span><span class="sxs-lookup"><span data-stu-id="342d2-115">Docker provides packages that easily configure Docker on any [Mac](https://docs.docker.com/docker-for-mac/), [Windows](https://docs.docker.com/docker-for-windows/), or [Linux](https://docs.docker.com/engine/installation/#supported-platforms) system.</span></span>

## <a name="get-application-code"></a><span data-ttu-id="342d2-116">Pobieranie kodu aplikacji</span><span class="sxs-lookup"><span data-stu-id="342d2-116">Get application code</span></span>

<span data-ttu-id="342d2-117">Przykładowe Hello w tym samouczku obejmuje prostą aplikację sieci web wbudowane [Node.js](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="342d2-117">hello sample in this tutorial includes a simple web application built in [Node.js](http://nodejs.org).</span></span> <span data-ttu-id="342d2-118">Aplikacja Hello służy statyczne strony HTML i wygląda następująco:</span><span class="sxs-lookup"><span data-stu-id="342d2-118">hello app serves a static HTML page and looks like this:</span></span>

![Samouczek aplikacji wyświetlony w przeglądarce][aci-tutorial-app]

<span data-ttu-id="342d2-120">Użyj przykładowych hello toodownload git:</span><span class="sxs-lookup"><span data-stu-id="342d2-120">Use git toodownload hello sample:</span></span>

```bash
git clone https://github.com/Azure-Samples/aci-helloworld.git
```

## <a name="build-hello-container-image"></a><span data-ttu-id="342d2-121">Utwórz obraz kontenera hello</span><span class="sxs-lookup"><span data-stu-id="342d2-121">Build hello container image</span></span>

<span data-ttu-id="342d2-122">Hello plik Dockerfile w repozytorium przykładowej hello pokazuje, jak kontenera hello jest wbudowana.</span><span class="sxs-lookup"><span data-stu-id="342d2-122">hello Dockerfile provided in hello sample repo shows how hello container is built.</span></span> <span data-ttu-id="342d2-123">Rozpoczyna od [oficjalnego obrazu Node.js] [ dockerhub-nodeimage] na podstawie [Alpine Linux](https://alpinelinux.org/), małych dystrybucji, który jest dobrze nadają się toouse z kontenerami.</span><span class="sxs-lookup"><span data-stu-id="342d2-123">It starts from an [official Node.js image][dockerhub-nodeimage] based on [Alpine Linux](https://alpinelinux.org/), a small distribution that is well suited toouse with containers.</span></span> <span data-ttu-id="342d2-124">Następnie kopiuje pliki aplikacji hello do kontenera hello, instalacji zależności za pomocą hello Node Package Manager, a na koniec uruchamia aplikację hello.</span><span class="sxs-lookup"><span data-stu-id="342d2-124">It then copies hello application files into hello container, installs dependencies using hello Node Package Manager, and finally starts hello application.</span></span>

```
FROM node:8.2.0-alpine
RUN mkdir -p /usr/src/app
COPY ./app/* /usr/src/app/
WORKDIR /usr/src/app
RUN npm install
CMD node /usr/src/app/index.js
```

<span data-ttu-id="342d2-125">Użyj hello `docker build` polecenia toocreate hello kontener obrazu, oznaczanie go jako *aci samouczek aplikacji*:</span><span class="sxs-lookup"><span data-stu-id="342d2-125">Use hello `docker build` command toocreate hello container image, tagging it as *aci-tutorial-app*:</span></span>

```bash
docker build ./aci-helloworld -t aci-tutorial-app
```

<span data-ttu-id="342d2-126">Użyj hello `docker images` toosee hello wbudowane obrazu:</span><span class="sxs-lookup"><span data-stu-id="342d2-126">Use hello `docker images` toosee hello built image:</span></span>

```bash
docker images
```

<span data-ttu-id="342d2-127">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="342d2-127">Output:</span></span>

```bash
REPOSITORY                   TAG                 IMAGE ID            CREATED              SIZE
aci-tutorial-app             latest              5c745774dfa9        39 seconds ago       68.1 MB
```

## <a name="run-hello-container-locally"></a><span data-ttu-id="342d2-128">Uruchom lokalnie hello kontenera</span><span class="sxs-lookup"><span data-stu-id="342d2-128">Run hello container locally</span></span>

<span data-ttu-id="342d2-129">Przed przystąpieniem do wdrażania tooAzure kontenera hello wystąpień kontenera, uruchomić je lokalnie tooconfirm jego działanie.</span><span class="sxs-lookup"><span data-stu-id="342d2-129">Before you try deploying hello container tooAzure Container Instances, run it locally tooconfirm that it works.</span></span> <span data-ttu-id="342d2-130">Witaj `-d` przełącznik umożliwia kontenera hello wykonywane w tle hello podczas `-p` pozwala toomap dowolnego portu tooport Twojego obliczeń 80 w kontenerze hello.</span><span class="sxs-lookup"><span data-stu-id="342d2-130">hello `-d` switch lets hello container run in hello background, while `-p` allows you toomap an arbitrary port on your compute tooport 80 in hello container.</span></span>

```bash
docker run -d -p 8080:80 aci-tutorial-app
```

<span data-ttu-id="342d2-131">Otwórz hello tooconfirm toohttp://localhost:8080 przeglądarki, która hello kontenera jest uruchomiona.</span><span class="sxs-lookup"><span data-stu-id="342d2-131">Open hello browser toohttp://localhost:8080 tooconfirm that hello container is running.</span></span>

![Uruchomionej aplikacji hello lokalnie w przeglądarce hello][aci-tutorial-app-local]

## <a name="next-steps"></a><span data-ttu-id="342d2-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="342d2-133">Next steps</span></span>

<span data-ttu-id="342d2-134">W tym samouczku utworzony obraz kontenera, który może być wdrożony tooAzure wystąpień kontenera.</span><span class="sxs-lookup"><span data-stu-id="342d2-134">In this tutorial, you created a container image that can be deployed tooAzure Container Instances.</span></span> <span data-ttu-id="342d2-135">Zakończono Hello następujące kroki:</span><span class="sxs-lookup"><span data-stu-id="342d2-135">hello following steps were completed:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="342d2-136">Klonowanie źródła aplikacji hello z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="342d2-136">Cloning hello application source from GitHub</span></span>  
> * <span data-ttu-id="342d2-137">Tworzenie obrazów kontenera z poziomu źródła aplikacji</span><span class="sxs-lookup"><span data-stu-id="342d2-137">Creating container images from application source</span></span>
> * <span data-ttu-id="342d2-138">Testowanie kontenera hello lokalnie</span><span class="sxs-lookup"><span data-stu-id="342d2-138">Testing hello container locally</span></span>

<span data-ttu-id="342d2-139">Przejdź dalej toolearn samouczka toohello o przechowywania obrazów kontenera w rejestrze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="342d2-139">Advance toohello next tutorial toolearn about storing container images in an Azure Container Registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="342d2-140">Wypychanie tooAzure obrazów rejestru kontenera</span><span class="sxs-lookup"><span data-stu-id="342d2-140">Push images tooAzure Container Registry</span></span>](./container-instances-tutorial-prepare-acr.md)

<!-- LINKS -->
[dockerhub-nodeimage]: https://hub.docker.com/r/library/node/tags/8.2.0-alpine/

<!--- IMAGES --->
[aci-tutorial-app]:./media/container-instances-quickstart/aci-app-browser.png
[aci-tutorial-app-local]: ./media/container-instances-tutorial-prepare-app/aci-app-browser-local.png