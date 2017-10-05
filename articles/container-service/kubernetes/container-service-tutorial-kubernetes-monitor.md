---
title: "Samouczek usługi kontenera platformy Azure — Monitor Kubernetes | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: f4d09973ada8e3cd0ff2b00d20aca979e834cd7f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-a-kubernetes-cluster-with-operations-management-suite"></a><span data-ttu-id="98497-104">Monitor klastrze Kubernetes z pakietem Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="98497-104">Monitor a Kubernetes cluster with Operations Management Suite</span></span>

<span data-ttu-id="98497-105">Monitorowanie sieci klastra Kubernetes i kontenery jest krytyczny, szczególnie w przypadku zarządzania klastrem produkcji na dużą skalę w wielu aplikacjach.</span><span class="sxs-lookup"><span data-stu-id="98497-105">Monitoring your Kubernetes cluster and containers is critical, especially when you manage a production cluster at scale with multiple apps.</span></span> 

<span data-ttu-id="98497-106">Można korzystać z kilku Kubernetes rozwiązań w zakresie monitorowania, z firmy Microsoft lub innych dostawców.</span><span class="sxs-lookup"><span data-stu-id="98497-106">You can take advantage of several Kubernetes monitoring solutions, either from Microsoft or other providers.</span></span> <span data-ttu-id="98497-107">W tym samouczku klastra Kubernetes można monitorować za pomocą rozwiązania kontenery w [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), rozwiązania do zarządzania oparta na chmurze IT firmy Microsoft.</span><span class="sxs-lookup"><span data-stu-id="98497-107">In this tutorial, you monitor your Kubernetes cluster by using the Containers solution in [Operations Management Suite](../../operations-management-suite/operations-management-suite-overview.md), Microsoft's cloud-based IT management solution.</span></span> <span data-ttu-id="98497-108">(OMS kontenery rozwiązanie jest w wersji zapoznawczej.)</span><span class="sxs-lookup"><span data-stu-id="98497-108">(The OMS Containers solution is in preview.)</span></span>

<span data-ttu-id="98497-109">Ten samouczek, część 7 7, obejmuje następujące zadania:</span><span class="sxs-lookup"><span data-stu-id="98497-109">This tutorial, part seven of seven, covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98497-110">Pobierz ustawienia obszarem roboczym pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="98497-110">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="98497-111">Konfigurowanie agentów OMS na węzłach Kubernetes</span><span class="sxs-lookup"><span data-stu-id="98497-111">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="98497-112">Dostęp do monitorowania informacji w portalu OMS lub w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="98497-112">Access monitoring information in the OMS portal or Azure portal</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="98497-113">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="98497-113">Before you begin</span></span>

<span data-ttu-id="98497-114">W poprzednim samouczki aplikacji zostało umieszczone w kontener obrazów, te obrazy przekazane do rejestru kontenera Azure i klastra Kubernetes utworzone.</span><span class="sxs-lookup"><span data-stu-id="98497-114">In previous tutorials, an application was packaged into container images, these images uploaded to Azure Container Registry, and a Kubernetes cluster created.</span></span> <span data-ttu-id="98497-115">Jeśli nie zostało wykonane następujące kroki, a następnie zostać z niego skorzystać, wróć do [samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="98497-115">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="98497-116">Co najmniej tego samouczka wymaga Kubernetes klastra z węzłami agenta systemu Linux i konta Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="98497-116">At minimum, this tutorial requires a Kubernetes cluster with Linux agent nodes, and an Operations Management Suite (OMS) account.</span></span> <span data-ttu-id="98497-117">Jeśli to konieczne, należy zarejestrować się w celu [bezpłatnej wersji próbnej pakietu OMS](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span><span class="sxs-lookup"><span data-stu-id="98497-117">If needed, sign up for a [free OMS trial](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial).</span></span>

## <a name="get-workspace-settings"></a><span data-ttu-id="98497-118">Pobierz ustawienia obszaru roboczego</span><span class="sxs-lookup"><span data-stu-id="98497-118">Get Workspace settings</span></span>

<span data-ttu-id="98497-119">Podczas uzyskiwania dostępu [portalu OMS](https://mms.microsoft.com), przejdź do **ustawienia** > **połączonych źródeł** > **serwerów z systemem Linux**.</span><span class="sxs-lookup"><span data-stu-id="98497-119">When you can access the [OMS portal](https://mms.microsoft.com), go to **Settings** > **Connected Sources** > **Linux Servers**.</span></span> <span data-ttu-id="98497-120">Istnieje, można znaleźć *identyfikator obszaru roboczego* i podstawowym lub pomocniczym *klucz obszaru roboczego*.</span><span class="sxs-lookup"><span data-stu-id="98497-120">There, you can find the *Workspace ID* and a primary or secondary *Workspace Key*.</span></span> <span data-ttu-id="98497-121">Zanotuj te wartości, które należy skonfigurować OMS agentów w klastrze.</span><span class="sxs-lookup"><span data-stu-id="98497-121">Take note of these values, which you need to set up OMS agents on the cluster.</span></span>

## <a name="set-up-oms-agents"></a><span data-ttu-id="98497-122">Konfigurowanie agentów OMS</span><span class="sxs-lookup"><span data-stu-id="98497-122">Set up OMS agents</span></span>

<span data-ttu-id="98497-123">W tym miejscu jest plikiem yaml programu do skonfigurowania OMS agentów w węzłach klastra systemu Linux.</span><span class="sxs-lookup"><span data-stu-id="98497-123">Here is a YAML file to set up OMS agents on the Linux cluster nodes.</span></span> <span data-ttu-id="98497-124">Tworzy Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), które są uruchamiane jednym pod identyczne w każdym węźle klastra.</span><span class="sxs-lookup"><span data-stu-id="98497-124">It creates a Kubernetes [DaemonSet](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/), which runs a single identical pod on each cluster node.</span></span> <span data-ttu-id="98497-125">Zasób DaemonSet jest idealne rozwiązanie w przypadku wdrażania agenta monitorowania.</span><span class="sxs-lookup"><span data-stu-id="98497-125">The DaemonSet resource is ideal for deploying a monitoring agent.</span></span> 

<span data-ttu-id="98497-126">Zapisz poniższy tekst do pliku o nazwie `oms-daemonset.yaml`i zastąp symbole zastępcze dla *myWorkspaceID* i *myWorkspaceKey* z OMS identyfikator i klucz.</span><span class="sxs-lookup"><span data-stu-id="98497-126">Save the following text to a file named `oms-daemonset.yaml`, and replace the placeholder values for *myWorkspaceID* and *myWorkspaceKey* with your OMS Workspace ID and Key.</span></span> <span data-ttu-id="98497-127">(W środowisku produkcyjnym, użytkownik może zakodować te wartości jako klucze tajne.)</span><span class="sxs-lookup"><span data-stu-id="98497-127">(In production, you can encode these values as secrets.)</span></span>

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

<span data-ttu-id="98497-128">Utwórz DaemonSet przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="98497-128">Create the DaemonSet with the following command:</span></span>

```azurecli-interactive
kubectl create -f oms-daemonset.yaml
```

<span data-ttu-id="98497-129">Aby sprawdzić, czy DaemonSet został utworzony, uruchom polecenie:</span><span class="sxs-lookup"><span data-stu-id="98497-129">To see that the DaemonSet is created, run:</span></span>

```azurecli-interactive
kubectl get daemonset
```

<span data-ttu-id="98497-130">Dane wyjściowe będą podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="98497-130">Output is similar to the following:</span></span>

```azurecli-interactive
NAME       DESIRED   CURRENT   READY     UP-TO-DATE   AVAILABLE   NODE-SELECTOR   AGE
omsagent   3         3         3         0            3           <none>          5m
```

<span data-ttu-id="98497-131">Po agenci są uruchomione, przyjmuje OMS do pozyskiwania i przetwarzania danych w ciągu kilku minut.</span><span class="sxs-lookup"><span data-stu-id="98497-131">After the agents are running, it takes several minutes for OMS to ingest and process the data.</span></span>

## <a name="access-monitoring-data"></a><span data-ttu-id="98497-132">Dostęp do danych monitorowania</span><span class="sxs-lookup"><span data-stu-id="98497-132">Access monitoring data</span></span>

<span data-ttu-id="98497-133">Wyświetlanie i analizowanie kontenera OMS monitorowania danych za pomocą [rozwiązania kontenera](../../log-analytics/log-analytics-containers.md) w portalu OMS lub w portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="98497-133">View and analyze the OMS container monitoring data with the [Container solution](../../log-analytics/log-analytics-containers.md) in either the OMS portal or the Azure portal.</span></span> 

<span data-ttu-id="98497-134">Przeprowadzanie instalacji przy użyciu rozwiązania kontenera [portalu OMS](https://mms.microsoft.com), przejdź do **galerii rozwiązań**.</span><span class="sxs-lookup"><span data-stu-id="98497-134">To install the Container solution using the [OMS portal](https://mms.microsoft.com), go to **Solutions Gallery**.</span></span> <span data-ttu-id="98497-135">Następnie dodaj **rozwiązania kontenera**.</span><span class="sxs-lookup"><span data-stu-id="98497-135">Then add **Container Solution**.</span></span> <span data-ttu-id="98497-136">Możesz też dodać kontenery rozwiązania z [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span><span class="sxs-lookup"><span data-stu-id="98497-136">Alternatively, add the Containers solution from the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft.containersoms?tab=Overview).</span></span>

<span data-ttu-id="98497-137">W portalu OMS poszukaj **kontenery** podsumowania kafelka na pulpicie nawigacyjnym OMS.</span><span class="sxs-lookup"><span data-stu-id="98497-137">In the OMS portal, look for a **Containers** summary tile on the OMS dashboard.</span></span> <span data-ttu-id="98497-138">Kliknij Kafelek, aby uzyskać więcej informacji, łącznie z: kontenery zdarzeń, błędów, stan, obrazu spisu i użycia Procesora i pamięci.</span><span class="sxs-lookup"><span data-stu-id="98497-138">Click the tile for details including: container events, errors, status, image inventory, and CPU and memory usage.</span></span> <span data-ttu-id="98497-139">Bardziej szczegółowe informacje, kliknij wiersz na każdy Kafelek, lub wykonaj [wyszukiwania dziennika](../../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="98497-139">For more granular information, click a row on any tile, or perform a [log search](../../log-analytics/log-analytics-log-searches.md).</span></span>

![Pulpit nawigacyjny kontenery w portalu OMS](./media/container-service-tutorial-kubernetes-monitor/oms-containers-dashboard.png)

<span data-ttu-id="98497-141">Podobnie, w portalu Azure, przejdź do **analizy dzienników** i wybierz nazwę obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="98497-141">Similarly, in the Azure portal, go to **Log Analytics** and select your workspace name.</span></span> <span data-ttu-id="98497-142">Aby wyświetlić **kontenery** Kafelek podsumowania, kliknij przycisk **rozwiązań** > **kontenery**.</span><span class="sxs-lookup"><span data-stu-id="98497-142">To see the **Containers** summary tile, click **Solutions** > **Containers**.</span></span> <span data-ttu-id="98497-143">Aby wyświetlić szczegóły, kliknij Kafelek.</span><span class="sxs-lookup"><span data-stu-id="98497-143">To see details, click the tile.</span></span>

<span data-ttu-id="98497-144">Zobacz [dokumentacji usługi Analiza dzienników Azure](../../log-analytics/index.md) szczegółowe wskazówki dotyczące zapytań i analizowanie danych monitorowania.</span><span class="sxs-lookup"><span data-stu-id="98497-144">See the [Azure Log Analytics documentation](../../log-analytics/index.md) for detailed guidance on querying and analyzing monitoring data.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98497-145">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="98497-145">Next steps</span></span>

<span data-ttu-id="98497-146">W tym samouczku monitorowane są klastra Kubernetes z usługą OMS.</span><span class="sxs-lookup"><span data-stu-id="98497-146">In this tutorial, you monitored your Kubernetes cluster with OMS.</span></span> <span data-ttu-id="98497-147">Uwzględnione objętych zadań:</span><span class="sxs-lookup"><span data-stu-id="98497-147">Tasks covered included:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98497-148">Pobierz ustawienia obszarem roboczym pakietu OMS</span><span class="sxs-lookup"><span data-stu-id="98497-148">Get OMS Workspace settings</span></span>
> * <span data-ttu-id="98497-149">Konfigurowanie agentów OMS na węzłach Kubernetes</span><span class="sxs-lookup"><span data-stu-id="98497-149">Set up OMS agents on the Kubernetes nodes</span></span>
> * <span data-ttu-id="98497-150">Dostęp do monitorowania informacji w portalu OMS lub w portalu Azure</span><span class="sxs-lookup"><span data-stu-id="98497-150">Access monitoring information in the OMS portal or Azure portal</span></span>


<span data-ttu-id="98497-151">Wykonaj to łącze, aby wyświetlić przykłady wbudowanych skryptów dla usługi kontenera.</span><span class="sxs-lookup"><span data-stu-id="98497-151">Follow this link to see pre-built script samples for Container Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="98497-152">Przykłady skryptów usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="98497-152">Azure Container Service script samples</span></span>](cli-samples.md)
