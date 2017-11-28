---
title: "aaaManage Azure Kubernetes klaster z interfejsu użytkownika sieci web | Dokumentacja firmy Microsoft"
description: "Przy użyciu hello Kubernetes interfejs użytkownika sieci web w usłudze kontenera platformy Azure"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/21/2017
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: e24ea0b82c94d2fd4610e4442699ef756590e6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-kubernetes-web-ui-with-azure-container-service"></a><span data-ttu-id="71dfb-103">Przy użyciu hello Kubernetes interfejs użytkownika sieci web z usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="71dfb-103">Using hello Kubernetes web UI with Azure Container Service</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71dfb-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="71dfb-104">Prerequisites</span></span>
<span data-ttu-id="71dfb-105">W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="71dfb-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>


<span data-ttu-id="71dfb-106">Założono również, że masz hello Azure CLI 2.0 i `kubectl` narzędzia są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="71dfb-106">It also assumes that you have hello Azure CLI 2.0 and `kubectl` tools installed.</span></span>

<span data-ttu-id="71dfb-107">Możesz przetestować, jeśli masz hello `az` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="71dfb-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="71dfb-108">Jeśli nie masz hello `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="71dfb-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="71dfb-109">Możesz przetestować, jeśli masz hello `kubectl` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="71dfb-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="71dfb-110">Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:</span><span class="sxs-lookup"><span data-stu-id="71dfb-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="overview"></a><span data-ttu-id="71dfb-111">Omówienie</span><span class="sxs-lookup"><span data-stu-id="71dfb-111">Overview</span></span>

### <a name="connect-toohello-web-ui"></a><span data-ttu-id="71dfb-112">Połącz toohello interfejsu użytkownika sieci web</span><span class="sxs-lookup"><span data-stu-id="71dfb-112">Connect toohello web UI</span></span>
<span data-ttu-id="71dfb-113">Hello interfejsu użytkownika sieci web Kubernetes można uruchomić, uruchamiając:</span><span class="sxs-lookup"><span data-stu-id="71dfb-113">You can launch hello Kubernetes web UI by running:</span></span>

```console
$ az acs kubernetes browse -g [Resource Group] -n [Container service instance name]
```

<span data-ttu-id="71dfb-114">To powinno spowodować otwarcie serwer proxy sieci web przeglądarce skonfigurowane tootalk tooa bezpieczne połączenie z komputera lokalnego toohello Kubernetes interfejsu użytkownika sieci web.</span><span class="sxs-lookup"><span data-stu-id="71dfb-114">This should open a web browser configured tootalk tooa secure proxy connecting your local machine toohello Kubernetes web UI.</span></span>

### <a name="create-and-expose-a-service"></a><span data-ttu-id="71dfb-115">Utworzyć i uwidocznić usługę</span><span class="sxs-lookup"><span data-stu-id="71dfb-115">Create and expose a service</span></span>
1. <span data-ttu-id="71dfb-116">W hello Kubernetes interfejsu użytkownika sieci web, kliknij przycisk **Utwórz** przycisk w oknie prawym górnym hello.</span><span class="sxs-lookup"><span data-stu-id="71dfb-116">In hello Kubernetes web UI, click **Create** button in hello upper right window.</span></span>

    ![Kubernetes Tworzenie interfejsu użytkownika](./media/container-service-kubernetes-ui/create.png)

    <span data-ttu-id="71dfb-118">Zostanie otwarte okno dialogowe której będzie można rozpocząć tworzenie aplikacji.</span><span class="sxs-lookup"><span data-stu-id="71dfb-118">A dialog box opens where you can start creating your application.</span></span>

2. <span data-ttu-id="71dfb-119">Nadaj nazwę hello `hello-nginx`.</span><span class="sxs-lookup"><span data-stu-id="71dfb-119">Give it hello name `hello-nginx`.</span></span> <span data-ttu-id="71dfb-120">Użyj hello [ `nginx` kontenera z Docker](https://hub.docker.com/_/nginx/) i wdrażanie trzech replik tej usługi sieci web.</span><span class="sxs-lookup"><span data-stu-id="71dfb-120">Use hello [`nginx` container from Docker](https://hub.docker.com/_/nginx/) and deploy three replicas of this web service.</span></span>

    ![Okno dialogowe Tworzenie Kubernetes Pod](./media/container-service-kubernetes-ui/nginx.png)

3. <span data-ttu-id="71dfb-122">W obszarze **usługi**, wybierz pozycję **zewnętrznych** i wprowadź port 80.</span><span class="sxs-lookup"><span data-stu-id="71dfb-122">Under **Service**, select **External** and enter port 80.</span></span>

    <span data-ttu-id="71dfb-123">To ustawienie zrównoważenie obciążenia ruchu toohello trzy repliki.</span><span class="sxs-lookup"><span data-stu-id="71dfb-123">This setting load-balances traffic toohello three replicas.</span></span>

    ![Okno dialogowe Tworzenie usługi Kubernetes](./media/container-service-kubernetes-ui/service.png)

4. <span data-ttu-id="71dfb-125">Kliknij przycisk **Wdróż** toodeploy tych kontenerów i usług.</span><span class="sxs-lookup"><span data-stu-id="71dfb-125">Click **Deploy** toodeploy these containers and services.</span></span>

    ![Wdrażanie Kubernetes](./media/container-service-kubernetes-ui/deploy.png)

### <a name="view-your-containers"></a><span data-ttu-id="71dfb-127">Wyświetl kontenerów</span><span class="sxs-lookup"><span data-stu-id="71dfb-127">View your containers</span></span>
<span data-ttu-id="71dfb-128">Po kliknięciu **Wdróż**, hello interfejsu użytkownika przedstawiono usługi wdrażania:</span><span class="sxs-lookup"><span data-stu-id="71dfb-128">After you click **Deploy**, hello UI shows a view of your service as it deploys:</span></span>

![Stan Kubernetes](./media/container-service-kubernetes-ui/status.png)

<span data-ttu-id="71dfb-130">Można wyświetlić hello stan każdego obiektu Kubernetes hello okrąg na powitania po lewej stronie interfejsu użytkownika, w obszarze **stanowiskami**.</span><span class="sxs-lookup"><span data-stu-id="71dfb-130">You can see hello status of each Kubernetes object in hello circle on hello left-hand side of the UI, under **Pods**.</span></span> <span data-ttu-id="71dfb-131">Jeśli jest częściowo koło obiektu hello nadal jest wdrażana.</span><span class="sxs-lookup"><span data-stu-id="71dfb-131">If it is a partially full circle, then hello object is still deploying.</span></span> <span data-ttu-id="71dfb-132">Gdy obiekt pełni zostanie wdrożona, Wyświetla zielony znacznik wyboru:</span><span class="sxs-lookup"><span data-stu-id="71dfb-132">When an object is fully deployed, it displays a green check mark:</span></span>

![Kubernetes wdrożony](./media/container-service-kubernetes-ui/deployed.png)

<span data-ttu-id="71dfb-134">Gdy wszystko jest uruchomiona, kliknij jeden z szczegóły toosee stanowiskami o hello uruchomiona usługa sieci web.</span><span class="sxs-lookup"><span data-stu-id="71dfb-134">Once everything is running, click one of your pods toosee details about hello running web service.</span></span>

![Stanowiskami Kubernetes](./media/container-service-kubernetes-ui/pods.png)

<span data-ttu-id="71dfb-136">W hello **stanowiskami** widoku wyświetlane są informacje o kontenery hello hello pod, jak również zasoby Procesora i pamięci hello używane przez tych kontenerach:</span><span class="sxs-lookup"><span data-stu-id="71dfb-136">In hello **Pods** view, you can see information about hello containers in hello pod as well as hello CPU and memory resources used by those containers:</span></span>

![Kubernetes zasobów](./media/container-service-kubernetes-ui/resources.png)

<span data-ttu-id="71dfb-138">Jeśli nie widzisz hello zasobów, może być konieczne toowait kilka minut dla hello toopropagate danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="71dfb-138">If you don't see hello resources, you may need toowait a few minutes for hello monitoring data toopropagate.</span></span>

<span data-ttu-id="71dfb-139">Dzienniki hello toosee Twojego kontenera, kliknij przycisk **Sprawdź dzienniki**.</span><span class="sxs-lookup"><span data-stu-id="71dfb-139">toosee hello logs for your container, click **View logs**.</span></span>

![Dzienniki Kubernetes](./media/container-service-kubernetes-ui/logs.png)

### <a name="viewing-your-service"></a><span data-ttu-id="71dfb-141">Wyświetlanie usługi</span><span class="sxs-lookup"><span data-stu-id="71dfb-141">Viewing your service</span></span>
<span data-ttu-id="71dfb-142">W dodatku toorunning kontenerów, hello Kubernetes interfejsu użytkownika została utworzona zewnętrzne `Service` który inicjuje opakowaniu toohello ruchu toobring usługi równoważenia obciążenia w klastrze.</span><span class="sxs-lookup"><span data-stu-id="71dfb-142">In addition toorunning your containers, hello Kubernetes UI has created an external `Service` which provisions a load balancer toobring traffic toohello containers in your cluster.</span></span>

<span data-ttu-id="71dfb-143">W okienku nawigacji po lewej stronie powitania kliknij **usług** tooview wszystkie usługi (powinien istnieć tylko jeden).</span><span class="sxs-lookup"><span data-stu-id="71dfb-143">In hello left navigation pane, click **Services** tooview all services (there should be only one).</span></span>

![Kubernetes usług](./media/container-service-kubernetes-ui/service-deployed.png)

<span data-ttu-id="71dfb-145">W tym widoku powinny pojawić się punkt końcowy zewnętrzne (adres IP), która została przydzielona tooyour usługi.</span><span class="sxs-lookup"><span data-stu-id="71dfb-145">In that view, you should see an external endpoint (IP address) that has been allocated tooyour service.</span></span>
<span data-ttu-id="71dfb-146">Kliknięcie tego adresu IP, powinna zostać wyświetlona z kontener Nginx uruchomiony za usługą równoważenia obciążenia.</span><span class="sxs-lookup"><span data-stu-id="71dfb-146">If you click that IP address, you should see your Nginx container running behind the load balancer.</span></span>

![Widok nginx](./media/container-service-kubernetes-ui/nginx-page.png)

### <a name="resizing-your-service"></a><span data-ttu-id="71dfb-148">Zmiana rozmiaru usługi</span><span class="sxs-lookup"><span data-stu-id="71dfb-148">Resizing your service</span></span>
<span data-ttu-id="71dfb-149">W tooviewing Dodawanie obiektów w hello interfejsu użytkownika, możesz edytować i aktualizowanie obiektów interfejsu API Kubernetes hello.</span><span class="sxs-lookup"><span data-stu-id="71dfb-149">In addition tooviewing your objects in hello UI, you can edit and update hello Kubernetes API objects.</span></span>

<span data-ttu-id="71dfb-150">Najpierw kliknij **wdrożeń** w hello pozostałych nawigacji w okienku toosee hello wdrożenia usługi.</span><span class="sxs-lookup"><span data-stu-id="71dfb-150">First, click **Deployments** in hello left navigation pane toosee hello deployment for your service.</span></span>

<span data-ttu-id="71dfb-151">Po przejściu do tego widoku, kliknij na powitania zestawu replik, a następnie kliknij **Edytuj** hello nawigacji w górnym pasku:</span><span class="sxs-lookup"><span data-stu-id="71dfb-151">Once you are in that view, click on hello replica set, and then click **Edit** in hello upper navigation bar:</span></span>

![Edytuj Kubernetes](./media/container-service-kubernetes-ui/edit.png)

<span data-ttu-id="71dfb-153">Edytuj hello `spec.replicas` toobe pola `2`i kliknij przycisk **aktualizacji**.</span><span class="sxs-lookup"><span data-stu-id="71dfb-153">Edit hello `spec.replicas` field toobe `2`, and click **Update**.</span></span>

<span data-ttu-id="71dfb-154">Powoduje to hello liczby replikami toodrop tootwo usuwając jeden z stanowiskami.</span><span class="sxs-lookup"><span data-stu-id="71dfb-154">This causes hello number of replicas toodrop tootwo by deleting one of your pods.</span></span>

 

