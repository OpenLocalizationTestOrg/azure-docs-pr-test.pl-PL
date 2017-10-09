---
title: klaster Azure DC/OS aaaMonitor - Dynatrace | Dokumentacja firmy Microsoft
description: "Monitorowanie klastra usługi kontenera platformy Azure DC/OS z Dynatrace. Wdrażanie hello Dynatrace OneAgent przy użyciu pulpitu nawigacyjnego DC/OS hello."
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
ms.openlocfilehash: 9e2e2d1c8b454422d1db30dac7c385d31d336853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-dcos-cluster-with-dynatrace-saasmanaged"></a><span data-ttu-id="2c7e6-105">Monitor klastra usługi kontenera platformy Azure DC/OS z Dynatrace SaaS/zarządzane</span><span class="sxs-lookup"><span data-stu-id="2c7e6-105">Monitor an Azure Container Service DC/OS cluster with Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="2c7e6-106">W tym artykule zostanie przedstawiony zostanie sposób toodeploy hello [Dynatrace](https://www.dynatrace.com/) toomonitor OneAgent wszystkie hello agenta węzłów w klastrze usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-106">In this article, we show you how toodeploy hello [Dynatrace](https://www.dynatrace.com/) OneAgent toomonitor all hello agent nodes in your Azure Container Service cluster.</span></span> <span data-ttu-id="2c7e6-107">Musisz mieć konto z Dynatrace SaaS/zarządzanego dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-107">You need an account with Dynatrace SaaS/Managed for this configuration.</span></span> 

## <a name="dynatrace-saasmanaged"></a><span data-ttu-id="2c7e6-108">Dynatrace SaaS/zarządzaną</span><span class="sxs-lookup"><span data-stu-id="2c7e6-108">Dynatrace SaaS/Managed</span></span>
<span data-ttu-id="2c7e6-109">Dynatrace to rozwiązanie monitorowania chmury natywne dla środowiska klastra i dynamicznej kontenera.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-109">Dynatrace is a cloud-native monitoring solution for highly dynamic container and cluster environments.</span></span> <span data-ttu-id="2c7e6-110">Umożliwia on toobetter zoptymalizować swoją wdrożenia kontenerów i alokacji pamięci za pomocą danych użycia w czasie rzeczywistym.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-110">It allows you toobetter optimize your container deployments and memory allocations by using real-time usage data.</span></span> <span data-ttu-id="2c7e6-111">Jest w stanie automatycznie trafić zapewniając automatycznego określania poziomu odniesienia, problem korelacji i wykrywania głównej przyczyny problemów dotyczących aplikacji i infrastruktury.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-111">It is capable of automatically pinpointing application and infrastructure issues by providing automated baselining, problem correlation, and root-cause detection.</span></span>

<span data-ttu-id="2c7e6-112">Hello następujący rysunek przedstawia hello Dynatrace interfejsu użytkownika:</span><span class="sxs-lookup"><span data-stu-id="2c7e6-112">hello following figure shows hello Dynatrace UI:</span></span>

![Dynatrace interfejsu użytkownika](./media/container-service-monitoring-dynatrace/dynatrace.png)

## <a name="prerequisites"></a><span data-ttu-id="2c7e6-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2c7e6-114">Prerequisites</span></span> 
<span data-ttu-id="2c7e6-115">[Wdrażanie](container-service-deployment.md) i [połączyć](./../container-service-connect.md) klastra tooa konfigurowane za pomocą usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-115">[Deploy](container-service-deployment.md) and [connect](./../container-service-connect.md) tooa cluster configured by Azure Container Service.</span></span> <span data-ttu-id="2c7e6-116">Eksploruj hello [interfejs użytkownika platformy Marathon](container-service-mesos-marathon-ui.md).</span><span class="sxs-lookup"><span data-stu-id="2c7e6-116">Explore hello [Marathon UI](container-service-mesos-marathon-ui.md).</span></span> <span data-ttu-id="2c7e6-117">Przejdź za[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset konto Dynatrace SaaS.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-117">Go too[https://www.dynatrace.com/trial/](https://www.dynatrace.com/trial/) tooset up a Dynatrace SaaS account.</span></span>  

## <a name="configure-a-dynatrace-deployment-with-marathon"></a><span data-ttu-id="2c7e6-118">Konfigurowanie wdrożenia Dynatrace przy użyciu platformy Marathon</span><span class="sxs-lookup"><span data-stu-id="2c7e6-118">Configure a Dynatrace deployment with Marathon</span></span>
<span data-ttu-id="2c7e6-119">Te kroki przedstawiają sposób tooconfigure i wdrożenie klastra tooyour aplikacji Dynatrace przy użyciu platformy Marathon.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-119">These steps show you how tooconfigure and deploy Dynatrace applications tooyour cluster with Marathon.</span></span>

1. <span data-ttu-id="2c7e6-120">Dostęp za pośrednictwem interfejsu użytkownika platformy DC/OS [http://localhost:80 /](http://localhost:80/).</span><span class="sxs-lookup"><span data-stu-id="2c7e6-120">Access your DC/OS UI via [http://localhost:80/](http://localhost:80/).</span></span> <span data-ttu-id="2c7e6-121">Raz w hello interfejsu użytkownika DC/OS, przejdź toohello **Universe** karcie, a następnie wyszukaj **Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-121">Once in hello DC/OS UI, navigate toohello **Universe** tab and then search for **Dynatrace**.</span></span>

    ![Dynatrace w Uniwersum DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-universe.png)

2. <span data-ttu-id="2c7e6-123">toocomplete hello konfiguracji, potrzebujesz konta Dynatrace SaaS lub bezpłatne konto próbne.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-123">toocomplete hello configuration, you need a Dynatrace SaaS account or a free trial account.</span></span> <span data-ttu-id="2c7e6-124">Po zalogowaniu się do pulpitu nawigacyjnego Dynatrace hello, wybierz **wdrażanie Dynatrace**.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-124">Once you log into hello Dynatrace dashboard, select **Deploy Dynatrace**.</span></span>

    ![Konfigurowanie Dynatrace PaaS integracji](./media/container-service-monitoring-dynatrace/setup-paas.png)

3. <span data-ttu-id="2c7e6-126">Na stronie powitania wybierz **konfigurowania integracji PaaS**.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-126">On hello page, select **Set up PaaS integration**.</span></span> 

    ![Token Dynatrace interfejsu API](./media/container-service-monitoring-dynatrace/api-token.png) 

4. <span data-ttu-id="2c7e6-128">Wprowadź token interfejsu API na powitania Dynatrace OneAgent konfiguracji w ramach hello Universe DC/OS.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-128">Enter your API token into hello Dynatrace OneAgent configuration within hello DC/OS Universe.</span></span> 

    ![Konfiguracja Dynatrace OneAgent w hello Universe DC/OS](./media/container-service-monitoring-dynatrace/dynatrace-config.png)

5. <span data-ttu-id="2c7e6-130">Ustawianie wystąpienia hello toohello liczby węzłów mają toorun.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-130">Set hello instances toohello number of nodes you intend toorun.</span></span> <span data-ttu-id="2c7e6-131">Ustawienie wyższej także działania, ale DC/OS będzie nadal próbować toofind nowych wystąpień do momentu rzeczywistości osiągnięciu tej liczby.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-131">Setting a higher number also works, but DC/OS will keep trying toofind new instances until that number is actually reached.</span></span> <span data-ttu-id="2c7e6-132">Jeśli wolisz, możesz również tę wartość można ustawić tooa jak 1000000.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-132">If you prefer, you can also set this tooa value like 1000000.</span></span> <span data-ttu-id="2c7e6-133">W takim przypadku przy każdym dodaniu nowego węzła klastra toohello Dynatrace automatycznie wdraża agenta toothat nowy węzeł, na powitania ceny stale trakcie wystąpień dalsze toodeploy DC/OS.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-133">In this case, whenever a new node is added toohello cluster, Dynatrace automatically deploys an agent toothat new node, at hello price of DC/OS constantly trying toodeploy further instances.</span></span>

    ![Konfiguracja Dynatrace w hello DC/OS Universe-wystąpienia](./media/container-service-monitoring-dynatrace/dynatrace-config2.png)

## <a name="next-steps"></a><span data-ttu-id="2c7e6-135">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2c7e6-135">Next steps</span></span>

<span data-ttu-id="2c7e6-136">Po zainstalowaniu pakietu hello, przejdź wstecz toohello Dynatrace z pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-136">Once you've installed hello package, navigate back toohello Dynatrace dashboard.</span></span> <span data-ttu-id="2c7e6-137">Metryki użycia różnych hello kontenerów hello można sprawdzić w ramach klastra.</span><span class="sxs-lookup"><span data-stu-id="2c7e6-137">You can explore hello different usage metrics for hello containers within your cluster.</span></span> 
