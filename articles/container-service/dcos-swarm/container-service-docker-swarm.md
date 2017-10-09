---
title: aaaManage Azure Swarm klaster z interfejsu API Docker | Dokumentacja firmy Microsoft
description: "Wdrażanie kontenerów tooa Docker Swarm klastra usługi kontenera platformy Azure"
services: container-service
documentationcenter: 
author: rgardler
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: bb9b07c82a7b48caeb2e351455797cbf2a6e7480
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="container-management-with-docker-swarm"></a><span data-ttu-id="88c64-104">Zarządzanie kontenerami przy użyciu rozwiązania Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="88c64-104">Container management with Docker Swarm</span></span>
<span data-ttu-id="88c64-105">Rozwiązanie Docker Swarm oferuje środowisko wdrażania konteneryzowanych obciążeń w puli zestawów hostów Docker.</span><span class="sxs-lookup"><span data-stu-id="88c64-105">Docker Swarm provides an environment for deploying containerized workloads across a pooled set of Docker hosts.</span></span> <span data-ttu-id="88c64-106">Rozwiązanie docker Swarm używa hello natywnego interfejsu API Docker.</span><span class="sxs-lookup"><span data-stu-id="88c64-106">Docker Swarm uses hello native Docker API.</span></span> <span data-ttu-id="88c64-107">Witaj przepływ pracy zarządzania kontenerami w rozwiązaniu Docker Swarm jest niemal identyczny toowhat, który będzie hostem jeden kontener.</span><span class="sxs-lookup"><span data-stu-id="88c64-107">hello workflow for managing containers on a Docker Swarm is almost identical toowhat it would be on a single container host.</span></span> <span data-ttu-id="88c64-108">Ten dokument zawiera proste przykłady wdrażania konteneryzowanych obciążeń w wystąpieniu usługi kontenera platformy Azure w rozwiązaniu Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="88c64-108">This document provides simple examples of deploying containerized workloads in an Azure Container Service instance of Docker Swarm.</span></span> <span data-ttu-id="88c64-109">Szczegółową dokumentację dotyczącą rozwiązania Docker Swarm można znaleźć na stronie [Docker Swarm w witrynie Docker.com](https://docs.docker.com/swarm/).</span><span class="sxs-lookup"><span data-stu-id="88c64-109">For more in-depth documentation on Docker Swarm, see [Docker Swarm on Docker.com](https://docs.docker.com/swarm/).</span></span>

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="88c64-110">Wymagania wstępne dotyczące ćwiczeń toohello w tym dokumencie:</span><span class="sxs-lookup"><span data-stu-id="88c64-110">Prerequisites toohello exercises in this document:</span></span>

[<span data-ttu-id="88c64-111">Utworzenie klastra Swarm usługi Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="88c64-111">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)

[<span data-ttu-id="88c64-112">Połącz z klastrem Swarm hello usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="88c64-112">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)

## <a name="deploy-a-new-container"></a><span data-ttu-id="88c64-113">Wdrażanie nowego kontenera</span><span class="sxs-lookup"><span data-stu-id="88c64-113">Deploy a new container</span></span>
<span data-ttu-id="88c64-114">toocreate nowy kontener w hello Docker Swarm, użyj hello `docker run` polecenia (sprawdzeniu otwartych wzorców toohello tunelu SSH, zgodnie z harmonogramem powyższe wymagania wstępne hello).</span><span class="sxs-lookup"><span data-stu-id="88c64-114">toocreate a new container in hello Docker Swarm, use hello `docker run` command (ensuring that you have opened an SSH tunnel toohello masters as per hello prerequisites above).</span></span> <span data-ttu-id="88c64-115">W tym przykładzie kontener jest tworzony z hello `yeasy/simple-web` obrazu:</span><span class="sxs-lookup"><span data-stu-id="88c64-115">This example creates a container from hello `yeasy/simple-web` image:</span></span>

```bash
user@ubuntu:~$ docker run -d -p 80:80 yeasy/simple-web

4298d397b9ab6f37e2d1978ef3c8c1537c938e98a8bf096ff00def2eab04bf72
```

<span data-ttu-id="88c64-116">Po utworzeniu kontenera hello, za pomocą `docker ps` tooreturn informacji na temat hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="88c64-116">After hello container has been created, use `docker ps` tooreturn information about hello container.</span></span> <span data-ttu-id="88c64-117">Zauważ, znajduje się agent Swarm hello obsługujący hello kontenera:</span><span class="sxs-lookup"><span data-stu-id="88c64-117">Notice here that hello Swarm agent that is hosting hello container is listed:</span></span>

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   31 seconds ago      Up 9 seconds        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

<span data-ttu-id="88c64-118">Można teraz uzyskać dostępu do aplikacji hello, która działa w tym kontenerze, za pośrednictwem hello publicznej nazwy DNS modułu równoważenia obciążenia agenta Swarm hello.</span><span class="sxs-lookup"><span data-stu-id="88c64-118">You can now access hello application that is running in this container through hello public DNS name of hello Swarm agent load balancer.</span></span> <span data-ttu-id="88c64-119">Te informacje można znaleźć w portalu Azure hello:</span><span class="sxs-lookup"><span data-stu-id="88c64-119">You can find this information in hello Azure portal:</span></span>  

![Rzeczywiste wyniki dotyczące odwiedzin](./media/container-service-docker-swarm/real-visit.jpg)  

<span data-ttu-id="88c64-121">Domyślnie hello modułu równoważenia obciążenia ma porty 80, 8080 i 443 open.</span><span class="sxs-lookup"><span data-stu-id="88c64-121">By default hello Load Balancer has ports 80, 8080 and 443 open.</span></span> <span data-ttu-id="88c64-122">Jeśli chcesz, aby tooconnect na innym porcie należy tooopen ten port na powitania modułu równoważenia obciążenia Azure dla hello puli agenta.</span><span class="sxs-lookup"><span data-stu-id="88c64-122">If you want tooconnect on another port you will need tooopen that port on hello Azure Load Balancer for hello Agent Pool.</span></span>

## <a name="deploy-multiple-containers"></a><span data-ttu-id="88c64-123">Wdrażanie wielu kontenerów</span><span class="sxs-lookup"><span data-stu-id="88c64-123">Deploy multiple containers</span></span>
<span data-ttu-id="88c64-124">Uruchomiono wiele kontenerów, wykonując "Uruchom docker" wielokrotnie, program hello `docker ps` toosee polecenia, obsługującego kontenery hello są uruchomione na.</span><span class="sxs-lookup"><span data-stu-id="88c64-124">As multiple containers are started, by executing 'docker run' multiple times, you can use hello `docker ps` command toosee which hosts hello containers are running on.</span></span> <span data-ttu-id="88c64-125">W poniższym przykładzie hello trzy kontenery zostały rozmieszczone równomiernie w obrębie trzech agentów Swarm hello:</span><span class="sxs-lookup"><span data-stu-id="88c64-125">In hello example below, three containers are spread evenly across hello three Swarm agents:</span></span>  

```bash
user@ubuntu:~$ docker ps

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                 NAMES
11be062ff602        yeasy/simple-web    "/bin/sh -c 'python i"   11 seconds ago      Up 10 seconds       10.0.0.6:83->80/tcp   swarm-agent-34A73819-2/clever_banach
1ff421554c50        yeasy/simple-web    "/bin/sh -c 'python i"   49 seconds ago      Up 48 seconds       10.0.0.4:82->80/tcp   swarm-agent-34A73819-0/stupefied_ride
4298d397b9ab        yeasy/simple-web    "/bin/sh -c 'python i"   2 minutes ago       Up 2 minutes        10.0.0.5:80->80/tcp   swarm-agent-34A73819-1/happy_allen
```  

## <a name="deploy-containers-by-using-docker-compose"></a><span data-ttu-id="88c64-126">Wdrażanie kontenerów przy użyciu rozwiązania Docker Compose</span><span class="sxs-lookup"><span data-stu-id="88c64-126">Deploy containers by using Docker Compose</span></span>
<span data-ttu-id="88c64-127">Można użyć rozwiązania Docker Compose tooautomate hello wdrażania i konfigurowania wielu kontenerów.</span><span class="sxs-lookup"><span data-stu-id="88c64-127">You can use Docker Compose tooautomate hello deployment and configuration of multiple containers.</span></span> <span data-ttu-id="88c64-128">toodo tak, upewnij się, że utworzono tunel Secure Shell (SSH) i ustawiono zmienną DOCKER_HOST tego hello (patrz wymagania wstępne hello powyżej).</span><span class="sxs-lookup"><span data-stu-id="88c64-128">toodo so, ensure that a Secure Shell (SSH) tunnel has been created and that hello DOCKER_HOST variable has been set (see hello pre-requisites above).</span></span>

<span data-ttu-id="88c64-129">Utwórz plik docker-compose.yml w systemie lokalnym.</span><span class="sxs-lookup"><span data-stu-id="88c64-129">Create a docker-compose.yml file on your local system.</span></span> <span data-ttu-id="88c64-130">toodo, użyj tego [próbki](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span><span class="sxs-lookup"><span data-stu-id="88c64-130">toodo this, use this [sample](https://raw.githubusercontent.com/rgardler/AzureDevTestDeploy/master/docker-compose.yml).</span></span>

```bash
web:
  image: adtd/web:0.1
  ports:
    - "80:80"
  links:
    - rest:rest-demo-azure.marathon.mesos
rest:
  image: adtd/rest:0.1
  ports:
    - "8080:8080"

```

<span data-ttu-id="88c64-131">Uruchom `docker-compose up -d` toostart hello kontenera wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="88c64-131">Run `docker-compose up -d` toostart hello container deployments:</span></span>

```bash
user@ubuntu:~/compose$ docker-compose up -d
Pulling rest (adtd/rest:0.1)...
swarm-agent-3B7093B8-0: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/rest:0.1... : downloaded
swarm-agent-3B7093B8-3: Pulling adtd/rest:0.1... : downloaded
Creating compose_rest_1
Pulling web (adtd/web:0.1)...
swarm-agent-3B7093B8-3: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-0: Pulling adtd/web:0.1... : downloaded
swarm-agent-3B7093B8-2: Pulling adtd/web:0.1... : downloaded
Creating compose_web_1
```

<span data-ttu-id="88c64-132">Na koniec zostanie zwrócona lista uruchomionych kontenerów hello.</span><span class="sxs-lookup"><span data-stu-id="88c64-132">Finally, hello list of running containers will be returned.</span></span> <span data-ttu-id="88c64-133">Ta lista odzwierciedla hello kontenerów, które zostały wdrożone przy użyciu rozwiązania Docker Compose:</span><span class="sxs-lookup"><span data-stu-id="88c64-133">This list reflects hello containers that were deployed by using Docker Compose:</span></span>

```bash
user@ubuntu:~/compose$ docker ps
CONTAINER ID        IMAGE               COMMAND                CREATED             STATUS              PORTS                     NAMES
caf185d221b7        adtd/web:0.1        "apache2-foreground"   2 minutes ago       Up About a minute   10.0.0.4:80->80/tcp       swarm-agent-3B7093B8-0/compose_web_1
040efc0ea937        adtd/rest:0.1       "catalina.sh run"      3 minutes ago       Up 2 minutes        10.0.0.4:8080->8080/tcp   swarm-agent-3B7093B8-0/compose_rest_1
```

<span data-ttu-id="88c64-134">Oczywiście można użyć `docker-compose ps` tooexamine tylko hello kontenerów zdefiniowanych w Twojej `compose.yml` pliku.</span><span class="sxs-lookup"><span data-stu-id="88c64-134">Naturally, you can use `docker-compose ps` tooexamine only hello containers defined in your `compose.yml` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88c64-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="88c64-135">Next steps</span></span>
[<span data-ttu-id="88c64-136">Dowiedz się więcej na temat rozwiązania Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="88c64-136">Learn more about Docker Swarm</span></span>](https://docs.docker.com/swarm/)

