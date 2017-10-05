---
title: Monitor klastra Azure DC/OS - Dynatrace | Dokumentacja firmy Microsoft
description: "Monitorowanie klastra usługi kontenera platformy Azure DC/OS z Dynatrace. Wdrażanie Dynatrace OneAgent przy użyciu pulpitu nawigacyjnego DC/OS."
services: container-service
documentationcenter: 
author: MartinGoodwell
manager: 
editor: 
tags: acs, azure-container-service
keywords: Kontenery, DC/OS, Azure
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/13/2016
ms.author: rogardle
ms.custom: mvc
ms.openlocfilehash: 6fa23728680779e33eda7bb9aa8a01b9cad9a82b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="f47a3-105">Monitor klastra usługi kontenera platformy Azure DC/OS z Dynatrace SaaS/zarządzane</span><span class="sxs-lookup"><span data-stu-id="f47a3-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="f47a3-106">W tym artykule zostanie przedstawiony zostanie sposób wdrażania [Dynatrace](https://www.dynatrace.com/) OneAgent do wszystkich węzłów w klastrze usługi kontenera platformy Azure agenta monitorowania.</span><span class="sxs-lookup"><span data-stu-id="f47a3-106">In this article, we show you how to deploy the [Dynatrace](https://www.dynatrace.com/) OneAgent to monitor all the agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="f47a3-107">Musisz mieć konto z Dynatrace SaaS/zarządzanego dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="f47a3-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="f47a3-108">Dynatrace SaaS/zarządzaną</span><span class="sxs-lookup"><span data-stu-id="f47a3-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="f47a3-109">Dynatrace to rozwiązanie monitorowania chmury natywne dla środowiska klastra i dynamicznej kontenera.</span><span class="sxs-lookup"><span data-stu-id="f47a3-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="f47a3-110">Pozwala na lepsze zoptymalizować wdrożenia kontenerów, a przydziału pamięci za pomocą danych użycia w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="f47a3-110">It allows you to better optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="f47a3-111">Jest w stanie automatycznie trafić zapewniając automatycznego określania poziomu odniesienia, problem korelacji i wykrywania głównej przyczyny problemów dotyczących aplikacji i infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="f47a3-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="f47a3-112">Na poniższej ilustracji przedstawiono Dynatrace interfejsu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="f47a3-112">The following figure shows the Dynatrace UI:</span></span>

![Dynatrace interfejsu użytkownika](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="f47a3-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="f47a3-114">Prerequisites</span></span> 
<span data-ttu-id="f47a3-115">[Wdrażanie](container-service-deployment.md) i [połączyć](./../container-service-connect.md) klastrowi konfigurowane za pomocą usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f47a3-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) to a cluster configured by Azure Container Service.</span></span> <span data-ttu-id="f47a3-116">Przegląd [interfejsu użytkownika platformy Marathon](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="f47a3-116">Explore the [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="f47a3-117">Przejdź do [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) skonfigurować konto Dynatrace SaaS.</span><span class="sxs-lookup"><span data-stu-id="f47a3-117">Go to [https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) to set up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="f47a3-118">Konfigurowanie wdrożenia Dynatrace przy użyciu platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="f47a3-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="f47a3-119">Te kroki pokazują, jak skonfigurować i wdrożyć aplikacje Dynatrace do klastra przy użyciu platformy Marathon.</span><span class="sxs-lookup"><span data-stu-id="f47a3-119">These steps show you how to configure and deploy Dynatrace applications to your cluster with Marathon.</span></span>

1. <span data-ttu-id="f47a3-120">Dostęp za pośrednictwem interfejsu użytkownika platformy DC/OS [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="f47a3-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="f47a3-121">Raz w Interfejsie użytkownika DC/OS, przejdź do **Universe** karcie, a następnie wyszukaj **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="f47a3-121">Once in the DC/OS UI, navigate to the **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace w Uniwersum DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="f47a3-123">Aby zakończyć konfigurację, należy na koncie Dynatrace SaaS lub bezpłatne konto próbne.</span><span class="sxs-lookup"><span data-stu-id="f47a3-123">To complete the configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="f47a3-124">Po zalogowaniu się do pulpitu nawigacyjnego Dynatrace, wybierz **wdrażanie Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="f47a3-124">Once you log into the Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Konfigurowanie Dynatrace PaaS integracji](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="f47a3-126">Na stronie wybierz **konfigurowania integracji PaaS**.</span><span class="sxs-lookup"><span data-stu-id="f47a3-126">On the page, select **Set up PaaS integration**.</span></span> 

    ![Token Dynatrace interfejsu API](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="f47a3-128">Wprowadź token interfejsu API w konfiguracji Dynatrace OneAgent w Uniwersum DC/OS.</span><span class="sxs-lookup"><span data-stu-id="f47a3-128">Enter your API token into the Dynatrace OneAgent configuration within the DC/OS Universe.</span></span> 

    ![Konfiguracja Dynatrace OneAgent na całym świecie DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="f47a3-130">Zestaw wystąpień do liczby węzłów, które zamierzasz uruchomić.</span><span class="sxs-lookup"><span data-stu-id="f47a3-130">Set the instances to the number of nodes you intend to run.</span></span> <span data-ttu-id="f47a3-131">Ustawienie wyższej także działania, ale DC/OS będzie próbować znaleźć nowych wystąpień do momentu rzeczywistości osiągnięciu tej liczby.</span><span class="sxs-lookup"><span data-stu-id="f47a3-131">Setting a higher number also works, but DC/OS will keep trying to find new instances until that number is actually reached.</span></span> <span data-ttu-id="f47a3-132">Jeśli wolisz, możesz także ustawić dla tej wartości, takich jak 1000000.</span><span class="sxs-lookup"><span data-stu-id="f47a3-132">If you prefer, you can also set this to a value like 1000000.</span></span> <span data-ttu-id="f47a3-133">W takim przypadku zawsze, gdy nowy węzeł zostanie dodany do klastra, Dynatrace automatycznie wdraża agenta tego nowego węzła w cenie DC/OS stale w trakcie wdrażania dalsze wystąpień.</span><span class="sxs-lookup"><span data-stu-id="f47a3-133">In this case, whenever a new node is added to the cluster, Dynatrace automatically deploys an agent to that new node, at the price of DC/OS constantly trying to deploy further instances.</span></span>

    ![Konfiguracja Dynatrace w DC/OS Universe-wystąpienia](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="f47a3-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f47a3-135">Next steps</span></span>

<span data-ttu-id="f47a3-136">Po zainstalowaniu pakietu przejdź z powrotem do pulpitu nawigacyjnego Dynatrace.</span><span class="sxs-lookup"><span data-stu-id="f47a3-136">Once you've installed the package, navigate back to the Dynatrace dashboard.</span></span> <span data-ttu-id="f47a3-137">Metryki użycia różnych kontenerów można sprawdzić w ramach klastra.</span><span class="sxs-lookup"><span data-stu-id="f47a3-137">You can explore the different usage metrics for the containers within your cluster.</span></span> 