---
title: Monitor klastra Azure DC/OS - Datadog | Dokumentacja firmy Microsoft
description: "Monitorowanie klastra usługi kontenera platformy Azure z Datadog. Użyj interfejsu użytkownika sieci web platformy DC/OS, aby wdrożyć agentów Datadog do klastra."
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
ms.openlocfilehash: 9dd451f994940d7cc3a59bd7fd08a8f067345e34
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-datadog"></a><span data-ttu-id="c8052-105">Monitor klastra usługi kontenera platformy Azure DC/OS z Datadog</span><span class="sxs-lookup"><span data-stu-id="c8052-105">Monitor an Azure Container Service DC/OS cluster with Datadog</span></span>
<span data-ttu-id="c8052-106">W tym artykule wdrożymy Datadog agentów dla wszystkich węzłów w klastrze usługi kontenera platformy Azure agenta.</span><span class="sxs-lookup"><span data-stu-id="c8052-106">In this article we will deploy Datadog agents to all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="c8052-107">Musisz mieć konto z Datadog dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c8052-107">You will need an account with Datadog for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c8052-108">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c8052-108">Prerequisites</span></span>
<span data-ttu-id="c8052-109">[Wdróż](container-service-deployment.md) i [połącz](../container-service-connect.md) klaster skonfigurowany przez usługę Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="c8052-109">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="c8052-110">Przegląd [interfejsu użytkownika platformy Marathon](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="c8052-110">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="c8052-111">Przejdź do [http://datadoghq.com](http://datadoghq.com) skonfigurować konto Datadog.</span><span class="sxs-lookup"><span data-stu-id="c8052-111">Go to [http://datadoghq.com](http://datadoghq.com) to set up a Datadog account.</span></span> 

## <a name="datadog"></a><span data-ttu-id="c8052-112">Datadog</span><span class="sxs-lookup"><span data-stu-id="c8052-112">Datadog</span></span>
<span data-ttu-id="c8052-113">Datadog jest usługą monitorowania, która gromadzi dane monitorowania z kontenerów w ramach klastra usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c8052-113">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="c8052-114">Datadog ma pulpitu nawigacyjnego Docker integracji umożliwia wyświetlenie określonych metryk w kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c8052-114">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="c8052-115">Metryki zebrane z kontenerów są zorganizowane według Procesora, pamięci, sieci i we/wy.</span><span class="sxs-lookup"><span data-stu-id="c8052-115">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="c8052-116">Datadog dzieli metryki na kontenery i obrazów.</span><span class="sxs-lookup"><span data-stu-id="c8052-116">Datadog splits metrics into containers and images.</span></span> <span data-ttu-id="c8052-117">Przykładem jak wygląda interfejs użytkownika użycia procesora CPU jest poniżej.</span><span class="sxs-lookup"><span data-stu-id="c8052-117">An example of what the UI looks like for CPU usage is below.</span></span>

![Datadog interfejsu użytkownika](./media/container-service-monitoring/datadog4.png)

## <a name="configure-a-datadog-deployment-with-marathon"></a><span data-ttu-id="c8052-119">Konfigurowanie wdrożenia Datadog przy użyciu platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="c8052-119">Configure a Datadog deployment with Marathon</span></span>
<span data-ttu-id="c8052-120">Te kroki opisano sposób konfigurowania i wdrażania aplikacji Datadog do klastra przy użyciu platformy Marathon.</span><span class="sxs-lookup"><span data-stu-id="c8052-120">These steps will show you how to configure and deploy Datadog applications to your cluster with Marathon.</span></span> 

<span data-ttu-id="c8052-121">Dostęp za pośrednictwem interfejsu użytkownika platformy DC/OS [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="c8052-121">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="c8052-122">Raz w Interfejsie użytkownika DC/OS przejdź do "Universe", który znajduje się w lewym dolnym rogu okna, następnie odszukaj "Datadog" i kliknij przycisk Zainstaluj.</span><span class="sxs-lookup"><span data-stu-id="c8052-122">Once in the DC/OS UI navigate to the "Universe" which is on the bottom left and then search for "Datadog" and click "Install."</span></span>

![Pakiet Datadog w Uniwersum DC/OS](./media/container-service-monitoring/datadog1.png)

<span data-ttu-id="c8052-124">Teraz w celu ukończenia konfiguracji konieczne będzie konto Datadog lub bezpłatne konto próbne.</span><span class="sxs-lookup"><span data-stu-id="c8052-124">Now to complete the configuration you will need a Datadog account or a free trial account.</span></span> <span data-ttu-id="c8052-125">Gdy jest zalogowany Datadog wyglądu witryny sieci Web w lewo i przejdź do integracji -> następnie [interfejsów API](https://app.datadoghq.com/account/settings#api).</span><span class="sxs-lookup"><span data-stu-id="c8052-125">Once you're logged in to the Datadog website look to the left and go to Integrations -> then [APIs](https://app.datadoghq.com/account/settings#api).</span></span> 

![Klucz interfejsu API Datadog](./media/container-service-monitoring/datadog2.png)

<span data-ttu-id="c8052-127">Następnie wprowadź klucz interfejsu API w konfiguracji Datadog w Uniwersum DC/OS.</span><span class="sxs-lookup"><span data-stu-id="c8052-127">Next enter your API key into the Datadog configuration within the DC/OS Universe.</span></span> 

![Konfiguracja Datadog na całym świecie DC/OS](./media/container-service-monitoring/datadog3.png) 

<span data-ttu-id="c8052-129">W powyższej konfiguracji wystąpienia są ustawione na 10000000 to zawsze, gdy nowy węzeł zostanie dodany do klastra Datadog automatycznie wdraża agenta do tego węzła.</span><span class="sxs-lookup"><span data-stu-id="c8052-129">In the above configuration instances are set to 10000000 so whenever a new node is added to the cluster Datadog will automatically deploy an agent to that node.</span></span> <span data-ttu-id="c8052-130">To rozwiązanie tymczasowe.</span><span class="sxs-lookup"><span data-stu-id="c8052-130">This is an interim solution.</span></span> <span data-ttu-id="c8052-131">Po zainstalowaniu pakietu, należy przejść z powrotem do witryny sieci Web Datadog i Znajdź "[pulpity nawigacyjne](https://app.datadoghq.com/dash/list)."</span><span class="sxs-lookup"><span data-stu-id="c8052-131">Once you've installed the package you should navigate back to the Datadog website and find "[Dashboards](https://app.datadoghq.com/dash/list)."</span></span> <span data-ttu-id="c8052-132">Z tego miejsca pojawi się niestandardowy i integracja z pulpitów nawigacyjnych.</span><span class="sxs-lookup"><span data-stu-id="c8052-132">From there you will see Custom and Integration Dashboards.</span></span> <span data-ttu-id="c8052-133">[Pulpitu nawigacyjnego Docker](https://app.datadoghq.com/screen/integration/docker) będą miały metryki kontenera potrzebne do monitorowania sieci klastra.</span><span class="sxs-lookup"><span data-stu-id="c8052-133">The [Docker dashboard](https://app.datadoghq.com/screen/integration/docker) will have all the container metrics you need for monitoring your cluster.</span></span> 

