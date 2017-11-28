---
title: klaster Azure DC/OS aaaMonitor - Datadog | Dokumentacja firmy Microsoft
description: "Monitorowanie klastra usługi kontenera platformy Azure z Datadog. Używać hello DC/OS web UI toodeploy hello Datadog agentów tooyour klastra."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Kontenery, Azure DC/OS, rozwiązanie Docker Swarm"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure
ms.date: 07/28/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 10268c04b5c2ef393429e706ed4a467fff80f718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="f8355-105">Monitor klastra usługi kontenera platformy Azure DC/OS z Datadog</span><span class="sxs-lookup"><span data-stu-id="f8355-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="f8355-106">W tym artykule wdrożymy Datadog agentów tooall hello agenta węzłów w klastrze usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f8355-106">In this article we will deploy Datadog agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="f8355-107">Musisz mieć konto z Datadog dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f8355-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f8355-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f8355-108">Prerequisites</span></span>
<span data-ttu-id="f8355-109">[Wdróż](container-service-deployment.md) i [połącz](../container-service-connect.md) klaster skonfigurowany przez usługę Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="f8355-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="f8355-110">Eksploruj hello [interfejs użytkownika platformy Marathon](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="f8355-110">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="f8355-111">Przejdź za[http://datadoghq.com](http://datadoghq.com) tooset konto Datadog.</span><span class="sxs-lookup"><span data-stu-id="f8355-111">Go too[http://datadoghq.com](http://datadoghq.com) tooset up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="f8355-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="f8355-112">Datadog</span></span>
<span data-ttu-id="f8355-113">Datadog jest usługą monitorowania, która gromadzi dane monitorowania z kontenerów w ramach klastra usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f8355-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="f8355-114">Datadog ma pulpitu nawigacyjnego Docker integracji umożliwia wyświetlenie określonych metryk w kontenerów.</span><span class="sxs-lookup"><span data-stu-id="f8355-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="f8355-115">Metryki zebrane z kontenerów są zorganizowane według Procesora, pamięci, sieci i we/wy.</span><span class="sxs-lookup"><span data-stu-id="f8355-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="f8355-116">Datadog dzieli metryki na kontenery i obrazów.</span><span class="sxs-lookup"><span data-stu-id="f8355-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="f8355-117">Przykład Witaj, jakie interfejsu użytkownika wygląda dla Procesora użycia jest poniżej.</span><span class="sxs-lookup"><span data-stu-id="f8355-117">An example of what hello UI looks like for CPU usage is below.</span></span>

![Datadog interfejsu użytkownika](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="f8355-119">Konfigurowanie wdrożenia Datadog przy użyciu platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="f8355-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="f8355-120">Te kroki opisano, jak tooconfigure i wdrożenie klastra tooyour aplikacji Datadog przy użyciu platformy Marathon.</span><span class="sxs-lookup"><span data-stu-id="f8355-120">These steps will show you how tooconfigure and deploy Datadog applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="f8355-121">Dostęp za pośrednictwem interfejsu użytkownika platformy DC/OS [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="f8355-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="f8355-122">Raz w hello Przejdź interfejsu użytkownika DC/OS toohello "Universe", który znajduje się na powitania dołu w lewo i następnie wyszukaj "Datadog" i kliknij przycisk Zainstaluj.</span><span class="sxs-lookup"><span data-stu-id="f8355-122">Once in hello DC/OS UI navigate toohello "Universe" which is on hello bottom left and then search for "Datadog" and click "Install."</span></span>

![Datadog pakietu w hello Universe DC/OS](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="f8355-124">Teraz toocomplete hello konfiguracji konieczne będzie konto Datadog lub bezpłatne konto próbne.</span><span class="sxs-lookup"><span data-stu-id="f8355-124">Now toocomplete hello configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="f8355-125">Po zalogowaniu w witrynie sieci Web toohello Datadog Szukaj toohello po lewej i przejść, następnie -> tooIntegrations [interfejsów API](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="f8355-125">Once you're logged in toohello Datadog website look toohello left and go tooIntegrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Klucz interfejsu API Datadog](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="f8355-127">Obok wprowadź klucz interfejsu API w konfiguracji Datadog hello w hello Universe DC/OS.</span><span class="sxs-lookup"><span data-stu-id="f8355-127">Next enter your API key into hello Datadog configuration within hello DC/OS Universe.</span></span> 

![Konfiguracja Datadog w hello Universe DC/OS](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="f8355-129">W hello powyżej konfiguracji wystąpienia są ustawiane too10000000, przy każdym dodaniu nowego węzła klastra toohello Datadog zostaną automatycznie wdrożone węzła toothat agenta.</span><span class="sxs-lookup"><span data-stu-id="f8355-129">In hello above configuration instances are set too10000000 so whenever a new node is added toohello cluster Datadog will automatically deploy an agent toothat node.</span></span> <span data-ttu-id="f8355-130">To rozwiązanie tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="f8355-130">This is an interim solution.</span></span> <span data-ttu-id="f8355-131">Po zainstalowaniu pakietu hello Przejdź wstecz toohello Datadog witryny sieci Web i Znajdź "[pulpity nawigacyjne](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="f8355-131">Once you've installed hello package you should navigate back toohello Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="f8355-132">Z tego miejsca pojawi się niestandardowy i integracja z pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="f8355-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="f8355-133">Witaj [pulpitu nawigacyjnego Docker](https://app.datadoghq.com/screen/integration/docker) będzie miał wszystkie metryki kontenera hello potrzebne do monitorowania sieci klastra.</span><span class="sxs-lookup"><span data-stu-id="f8355-133">hello [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all hello container metrics you need for monitoring your cluster.</span></span> 

