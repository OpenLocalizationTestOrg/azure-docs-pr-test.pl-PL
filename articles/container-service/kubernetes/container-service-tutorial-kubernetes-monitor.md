---
title: "Samouczek usługi kontenera aaaAzure — Monitor Kubernetes | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — Kubernetes monitora z Microsoft Operations Management Suite (OMS)"
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenerów, Micro-services, Kubernetes, platforma Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 54fa789453768529deaf25d7575e5b21d0e41882
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="9f9b2-104">Monitor klastrze Kubernetes z pakietem Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="9f9b2-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="9f9b2-105">Monitorowanie sieci klastra Kubernetes i kontenery jest krytyczny, szczególnie w przypadku zarządzania klastrem produkcji na dużą skalę w wielu aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="9f9b2-106">Można korzystać z kilku Kubernetes rozwiązań w zakresie monitorowania, z firmy Microsoft lub innych dostawców.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="9f9b2-107">W tym samouczku klastra Kubernetes można monitorować za pomocą rozwiązania kontenery hello w [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), rozwiązania do zarządzania oparta na chmurze IT firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-107">In this tutorial, you monitor your Kubernetes cluster by using hello Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="9f9b2-108">(hello kontenery OMS rozwiązanie jest w wersji zapoznawczej.)</span><span class="sxs-lookup"><span data-stu-id="9f9b2-108">(hello OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="9f9b2-109">Ten samouczek, część 7 siedmiu, obejmuje hello następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="9f9b2-109">This tutorial, part seven of seven, covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9f9b2-110">Pobierz ustawienia obszarem roboczym pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="9f9b2-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="9f9b2-111">Konfigurowanie agentów OMS na węzłach Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="9f9b2-111">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="9f9b2-112">Dostęp do monitorowania informacji w portalu OMS hello lub w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9f9b2-112">Access monitoring information in hello OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="9f9b2-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="9f9b2-113">Before you begin</span></span>

<span data-ttu-id="9f9b2-114">W poprzednich samouczki aplikacji zostało umieszczone w kontenerze obrazów, przekazać te obrazy tooAzure rejestru kontenera i utworzyć klaster Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-114">In previous tutorials, an application was packaged into container images, these images uploaded tooAzure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="9f9b2-115">Jeśli nie zostało wykonane następujące kroki, a chcesz toofollow wzdłuż, zwróć zbyt[samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="9f9b2-115">If you have not done these steps, and would like toofollow along, return too[Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="9f9b2-116">Co najmniej tego samouczka wymaga Kubernetes klastra z węzłami agenta systemu Linux i konta Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="9f9b2-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="9f9b2-117">Jeśli to konieczne, należy zarejestrować się w celu [bezpłatnej wersji próbnej pakietu OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="9f9b2-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="9f9b2-118">Pobierz ustawienia obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="9f9b2-118">Get Workspace settings</span></span>

<span data-ttu-id="9f9b2-119">Podczas uzyskiwania dostępu hello [portalu OMS](https://mms.microsoft.com), przejdź do zbyt**ustawienia** > **połączonych źródeł** > **serwerów z systemem Linux**.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-119">When you can access hello [OMS portal](https://mms.microsoft.com), go too**Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="9f9b2-120">Istnieje, można znaleźć hello *identyfikator obszaru roboczego* i podstawowym lub pomocniczym *klucz obszaru roboczego*.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-120">There, you can find hello *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="9f9b2-121">Zanotuj te wartości, które należy tooset się OMS agentów na powitania klastra.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-121">Take note of these values, which you need tooset up OMS agents on hello cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="9f9b2-122">Konfigurowanie agentów OMS</span><span class="sxs-lookup"><span data-stu-id="9f9b2-122">Set up OMS agents</span></span>

<span data-ttu-id="9f9b2-123">Oto tooset pliku yaml programu się OMS agentów w węzłach klastra hello systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-123">Here is a YAML file tooset up OMS agents on hello Linux cluster nodes.</span></span> <span data-ttu-id="9f9b2-124">Tworzy Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), które są uruchamiane jednym pod identyczne w każdym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="9f9b2-125">Witaj DaemonSet zasobów jest idealny dla wdrażania agenta monitorowania.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-125">hello DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="9f9b2-126">Zapisz hello poniższe tekst tooa plik o nazwie `oms-daemonset.yaml`i zastąp symbole zastępcze powitania dla *myWorkspaceID* i *myWorkspaceKey* z OMS identyfikator i klucz.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-126">Save hello following text tooa file named `oms-daemonset.yaml`, and replace hello placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="9f9b2-127">(W środowisku produkcyjnym, użytkownik może zakodować te wartości jako klucze tajne.)</span><span class="sxs-lookup"><span data-stu-id="9f9b2-127">(In production, you can encode these values as secrets.)</span></span>

```YAML
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
 name: omsagent
spec:
 template:
  metadata:
   labels:
    app: omsagent
    agentVersion: v1.3.4-127
    dockerProviderVersion: 10.0.0-25
  spec:
   containers:
     - name: omsagent 
       image: "microsoft/oms"
       imagePullPolicy: Always
       env:
       - name: WSID
         value: myWorkspaceID
       - name: KEY 
         value: myWorkspaceKey
       - name: DOMAIN
         value: opinsights.azure.com
       securityContext:
         privileged: true
       ports:
       - containerPort: 25225
         protocol: TCP 
       - containerPort: 25224
         protocol: UDP
       volumeMounts:
        - mountPath: /var/run/docker.sock
          name: docker-sock
        - mountPath: /var/log 
          name: host-log
       livenessProbe:
        exec:
         command:
         - /bin/bash
         - -c
         - ps -ef | grep omsagent | grep -v "grep"
        initialDelaySeconds: 60
        periodSeconds: 60
   volumes:
    - name: docker-sock 
      hostPath:
       path: /var/run/docker.sock
    - name: host-log
      hostPath:
       path: /var/log
```

<span data-ttu-id="9f9b2-128">Utwórz hello DaemonSet z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="9f9b2-128">Create hello DaemonSet with hello following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="9f9b2-129">Uruchom ten hello DaemonSet jest tworzona, toosee:</span><span class="sxs-lookup"><span data-stu-id="9f9b2-129">toosee that hello DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="9f9b2-130">Dane wyjściowe są podobne toohello następujące czynności:</span><span class="sxs-lookup"><span data-stu-id="9f9b2-130">Output is similar toohello following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="9f9b2-131">Po agentów hello jest uruchomiony, ma OMS tooingest i przetwarzanie danych hello w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-131">After hello agents are running, it takes several minutes for OMS tooingest and process hello data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="9f9b2-132">Dostęp do danych monitorowania</span><span class="sxs-lookup"><span data-stu-id="9f9b2-132">Access monitoring data</span></span>

<span data-ttu-id="9f9b2-133">Wyświetlanie i analizowanie kontenera OMS hello monitorowania danych za pomocą hello [rozwiązania kontenera](../../log-analytics/log-analytics-containers.md) w portalu OMS hello lub hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-133">View and analyze hello OMS container monitoring data with hello [Container solution](../../log-analytics/log-analytics-containers.md) in either hello OMS portal or hello Azure portal.</span></span> 

<span data-ttu-id="9f9b2-134">rozwiązanie kontenera hello tooinstall przy użyciu hello [portalu OMS](https://mms.microsoft.com), przejdź do zbyt**galerii rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-134">tooinstall hello Container solution using hello [OMS portal](https://mms.microsoft.com), go too**Solutions Gallery**.</span></span> <span data-ttu-id="9f9b2-135">Następnie dodaj **rozwiązania kontenera**.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-135">Then add **Container Solution**.</span></span> <span data-ttu-id="9f9b2-136">Możesz też dodać hello kontenery rozwiązania z hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="9f9b2-136">Alternatively, add hello Containers solution from hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="9f9b2-137">W portalu OMS hello, poszukaj **kontenery** podsumowania kafelka na pulpicie nawigacyjnym OMS hello.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-137">In hello OMS portal, look for a **Containers** summary tile on hello OMS dashboard.</span></span> <span data-ttu-id="9f9b2-138">Kliknij Kafelek hello, aby uzyskać więcej informacji, łącznie z: kontenery zdarzeń, błędów, stan, obrazu spisu i użycia Procesora i pamięci.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-138">Click hello tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="9f9b2-139">Bardziej szczegółowe informacje, kliknij wiersz na każdy Kafelek, lub wykonaj [wyszukiwania dziennika](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="9f9b2-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Pulpit nawigacyjny kontenery w portalu OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="9f9b2-141">Podobnie, w hello portalu Azure, przejdź do pozycji zbyt**analizy dzienników** i wybierz nazwę obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-141">Similarly, in hello Azure portal, go too**Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="9f9b2-142">Witaj toosee **kontenery** Kafelek podsumowania, kliknij przycisk **rozwiązań** > **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-142">toosee hello **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="9f9b2-143">toosee uzyskać więcej informacji, kliknij Kafelek hello.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-143">toosee details, click hello tile.</span></span>

<span data-ttu-id="9f9b2-144">Zobacz hello [dokumentacji usługi Analiza dzienników Azure](../../log-analytics/index.md) szczegółowe wskazówki dotyczące zapytań i analizowanie danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-144">See hello [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9f9b2-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9f9b2-145">Next steps</span></span>

<span data-ttu-id="9f9b2-146">W tym samouczku monitorowane są klastra Kubernetes z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="9f9b2-147">Uwzględnione objętych zadań:</span><span class="sxs-lookup"><span data-stu-id="9f9b2-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9f9b2-148">Pobierz ustawienia obszarem roboczym pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="9f9b2-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="9f9b2-149">Konfigurowanie agentów OMS na węzłach Kubernetes hello</span><span class="sxs-lookup"><span data-stu-id="9f9b2-149">Set up OMS agents on hello Kubernetes nodes</span></span>
> * <span data-ttu-id="9f9b2-150">Dostęp do monitorowania informacji w portalu OMS hello lub w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="9f9b2-150">Access monitoring information in hello OMS portal or Azure portal</span></span>


<span data-ttu-id="9f9b2-151">Postępuj zgodnie z tym toosee łącze wstępnie skompilowany przykłady skryptów dla usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="9f9b2-151">Follow this link toosee pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9f9b2-152">Przykłady skryptów usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="9f9b2-152">Azure Container Service script samples</span></span>](cli-samples.md)
