---
title: "klaster usługi kontenera platformy Azure aaaMonitor z Sysdig | Dokumentacja firmy Microsoft"
description: "Monitorowanie klastra usługi Azure Container Service przy użyciu rozwiązania Sysdig."
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Kontenery, DC/OS, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a><span data-ttu-id="367e5-104">Monitorowanie klastra usługi Azure Container Service przy użyciu rozwiązania Sysdig</span><span class="sxs-lookup"><span data-stu-id="367e5-104">Monitor an Azure Container Service cluster with Sysdig</span></span>
<span data-ttu-id="367e5-105">W tym artykule wdrożymy Sysdig agentów tooall hello agenta węzłów w klastrze usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="367e5-105">In this article, we will deploy Sysdig agents tooall hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="367e5-106">Ta konfiguracja wymaga konta z rozwiązaniem Sysdig.</span><span class="sxs-lookup"><span data-stu-id="367e5-106">You need an account with Sysdig for this configuration.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="367e5-107">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="367e5-107">Prerequisites</span></span>
<span data-ttu-id="367e5-108">[Wdróż](container-service-deployment.md) i [połącz](../container-service-connect.md) klaster skonfigurowany przez usługę Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="367e5-108">[Deploy](container-service-deployment.md) and [connect](../container-service-connect.md) a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="367e5-109">Eksploruj hello [interfejs użytkownika platformy Marathon](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="367e5-109">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="367e5-110">Przejdź za[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset konto Sysdig chmury.</span><span class="sxs-lookup"><span data-stu-id="367e5-110">Go too[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset up a Sysdig cloud account.</span></span> 

## <a name="sysdig"></a><span data-ttu-id="367e5-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="367e5-111">Sysdig</span></span>
<span data-ttu-id="367e5-112">Usługa monitorowania, która pozwala toomonitor jest Sysdig kontenerów w ramach klastra.</span><span class="sxs-lookup"><span data-stu-id="367e5-112">Sysdig is a monitoring service that allows you toomonitor your containers within your cluster.</span></span> <span data-ttu-id="367e5-113">Sysdig jest znany toohelp w rozwiązywaniu problemów, ale ma także Twoje podstawowe metryki monitorowania dla procesora CPU, pamięci, sieci i we/wy.</span><span class="sxs-lookup"><span data-stu-id="367e5-113">Sysdig is known toohelp with troubleshooting but it also has your basic monitoring metrics for CPU, Networking, Memory, and I/O.</span></span> <span data-ttu-id="367e5-114">Sysdig umożliwia łatwe toosee kontenery, które działają hello hardest lub zasadniczo przy użyciu hello większość pamięci i procesora CPU.</span><span class="sxs-lookup"><span data-stu-id="367e5-114">Sysdig makes it easy toosee which containers are working hello hardest or essentially using hello most memory and CPU.</span></span> <span data-ttu-id="367e5-115">Ten widok jest hello sekcji "Przegląd", który jest obecnie w wersji beta.</span><span class="sxs-lookup"><span data-stu-id="367e5-115">This view is in hello “Overview” section, which is currently in beta.</span></span> 

![Interfejs użytkownika usługi Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a><span data-ttu-id="367e5-117">Konfigurowanie wdrożenia usługi Sysdig przy użyciu usługi Marathon</span><span class="sxs-lookup"><span data-stu-id="367e5-117">Configure a Sysdig deployment with Marathon</span></span>
<span data-ttu-id="367e5-118">Te kroki opisano, jak tooconfigure i wdrożenie klastra tooyour aplikacji Sysdig przy użyciu platformy Marathon.</span><span class="sxs-lookup"><span data-stu-id="367e5-118">These steps will show you how tooconfigure and deploy Sysdig applications tooyour cluster with Marathon.</span></span> 

<span data-ttu-id="367e5-119">Dostęp za pośrednictwem interfejsu użytkownika DC/OS [http://localhost:80 /](http://localhost:80/) raz w hello interfejsu użytkownika DC/OS Przejdź toohello "Universe", który znajduje się na powitania dołu w lewo, a następnie wyszukaj polecenie "Sysdig."</span><span class="sxs-lookup"><span data-stu-id="367e5-119">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/) Once in hello DC/OS UI navigate toohello "Universe", which is on hello bottom left and then search for "Sysdig."</span></span>

![Usługa Sysdig we wszechświecie rozwiązania DC/OS](./media/container-service-monitoring-sysdig/sysdig1.png)

<span data-ttu-id="367e5-121">Teraz hello toocomplete konfiguracji należy Sysdig chmury konta lub bezpłatne konto próbne.</span><span class="sxs-lookup"><span data-stu-id="367e5-121">Now toocomplete hello configuration you need a Sysdig cloud account or a free trial account.</span></span> <span data-ttu-id="367e5-122">Po zalogowaniu się w witrynie sieci Web toohello Sysdig chmury, kliknij swoją nazwę użytkownika, a na stronie powitania powinna zostać wyświetlona "Klucz dostępu do."</span><span class="sxs-lookup"><span data-stu-id="367e5-122">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Klucz interfejsu API usługi Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

<span data-ttu-id="367e5-124">Obok wprowadź klucz dostępu do konfiguracji Sysdig hello w hello Universe DC/OS.</span><span class="sxs-lookup"><span data-stu-id="367e5-124">Next enter your Access Key into hello Sysdig configuration within hello DC/OS Universe.</span></span> 

![Konfiguracja Sysdig w hello Universe DC/OS](./media/container-service-monitoring-sysdig/sysdig3.png)

<span data-ttu-id="367e5-126">Teraz ustawić too10000000 wystąpień hello, przy każdym dodaniu nowego węzła klastra toohello Sysdig automatycznie wdraża agenta toothat nowego węzła.</span><span class="sxs-lookup"><span data-stu-id="367e5-126">Now set hello instances too10000000 so whenever a new node is added toohello cluster Sysdig will automatically deploy an agent toothat new node.</span></span> <span data-ttu-id="367e5-127">To jest tymczasowo toomake się, że Sysdig wdroży tooall nowych agentów w ramach klastra hello.</span><span class="sxs-lookup"><span data-stu-id="367e5-127">This is an interim solution toomake sure Sysdig will deploy tooall new agents within hello cluster.</span></span> 

![Konfiguracja Sysdig w hello DC/OS Universe-wystąpienia](./media/container-service-monitoring-sysdig/sysdig4.png)

<span data-ttu-id="367e5-129">Po zainstalowaniu pakietu hello Przejdź wstecz toohello Sysdig interfejsu użytkownika i będzie metryki użycia różnych hello stanie tooexplore hello kontenerów w ramach klastra.</span><span class="sxs-lookup"><span data-stu-id="367e5-129">Once you've installed hello package navigate back toohello Sysdig UI and you'll be able tooexplore hello different usage metrics for hello containers within your cluster.</span></span> 

<span data-ttu-id="367e5-130">Możesz także zainstalować pulpity nawigacyjne określone dla rozwiązań Mesos i Marathon, korzystając z [Kreatora nowego pulpitu nawigacyjnego](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="367e5-130">You can also install Mesos and Marathon specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
