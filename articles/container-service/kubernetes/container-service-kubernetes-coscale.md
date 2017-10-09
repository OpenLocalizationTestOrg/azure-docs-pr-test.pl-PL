---
title: aaaMonitor Kubernetes Azure klaster z CoScale | Dokumentacja firmy Microsoft
description: "Monitor Kubernetes klastra usługi kontenera platformy Azure przy użyciu CoScale"
services: container-service
documentationcenter: 
author: fryckbos
manager: 
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.assetid: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: f835e82d2be3afe1d85070bd0bf69649cc6dd2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-with-coscale"></a><span data-ttu-id="c5bec-103">Monitor klaster Kubernetes usługi kontenera platformy Azure z CoScale</span><span class="sxs-lookup"><span data-stu-id="c5bec-103">Monitor an Azure Container Service Kubernetes cluster with CoScale</span></span>

<span data-ttu-id="c5bec-104">W tym artykule zostanie przedstawiony zostanie sposób toodeploy hello [CoScale](https://www.coscale.com/) toomonitor agenta, wszystkie węzły i kontenerów w Twojej Kubernetes klastra usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="c5bec-104">In this article, we show you how toodeploy hello [CoScale](https://www.coscale.com/) agent toomonitor all nodes and containers in your Kubernetes cluster in Azure Container Service.</span></span> <span data-ttu-id="c5bec-105">Musisz mieć konto z CoScale dla tej konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="c5bec-105">You need an account with CoScale for this configuration.</span></span> 


## <a name="about-coscale"></a><span data-ttu-id="c5bec-106">O CoScale</span><span class="sxs-lookup"><span data-stu-id="c5bec-106">About CoScale</span></span> 

<span data-ttu-id="c5bec-107">CoScale to platforma monitorowania, która zbiera metryki i zdarzenia z wszystkich kontenerów w różnych platform aranżacji.</span><span class="sxs-lookup"><span data-stu-id="c5bec-107">CoScale is a monitoring platform that gathers metrics and events from all containers in several orchestration platforms.</span></span> <span data-ttu-id="c5bec-108">CoScale oferuje pełnego stosu monitorowania dla środowisk Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="c5bec-108">CoScale offers full-stack monitoring for Kubernetes environments.</span></span> <span data-ttu-id="c5bec-109">Zapewnia wszystkie warstwy stosu hello wizualizacje i analiza: hello systemu operacyjnego, Kubernetes Docker i aplikacji uruchamianych wewnątrz kontenerów.</span><span class="sxs-lookup"><span data-stu-id="c5bec-109">It provides visualizations and analytics for all layers in hello stack: hello OS, Kubernetes, Docker, and applications running inside your containers.</span></span> <span data-ttu-id="c5bec-110">CoScale oferuje kilka wbudowanych nawigacyjnych monitorowania i ma operatory tooallow wykrywania anomalii wbudowanych i szybkie toofind deweloperzy problemów infrastruktury i aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c5bec-110">CoScale offers several built-in monitoring dashboards, and it has built-in anomaly detection tooallow operators and developers toofind infrastructure and application issues fast.</span></span>

![CoScale interfejsu użytkownika](./media/container-service-kubernetes-coscale/coscale.png)

<span data-ttu-id="c5bec-112">Jak pokazano w tym artykule, można zainstalować agentów na toorun klastra Kubernetes CoScale jako rozwiązaniem SaaS.</span><span class="sxs-lookup"><span data-stu-id="c5bec-112">As shown in this article, you can install agents on a Kubernetes cluster toorun CoScale as a SaaS solution.</span></span> <span data-ttu-id="c5bec-113">Jeśli chcesz tookeep danych na miejscu, CoScale jest również dostępny do instalacji lokalnej.</span><span class="sxs-lookup"><span data-stu-id="c5bec-113">If you want tookeep your data on-site, CoScale is also available for on-premises installation.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c5bec-114">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="c5bec-114">Prerequisites</span></span>

<span data-ttu-id="c5bec-115">Musisz najpierw za[Utwórz konto CoScale](https://www.coscale.com/free-trial).</span><span class="sxs-lookup"><span data-stu-id="c5bec-115">You first need too[create a CoScale account](https://www.coscale.com/free-trial).</span></span>

<span data-ttu-id="c5bec-116">W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="c5bec-116">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="c5bec-117">Założono również, że masz hello `az` wiersza polecenia platformy Azure i `kubectl` narzędzia są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="c5bec-117">It also assumes that you have hello `az` Azure CLI and `kubectl` tools installed.</span></span>

<span data-ttu-id="c5bec-118">Możesz przetestować, jeśli masz hello `az` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="c5bec-118">You can test if you have hello `az` tool installed by running:</span></span>

```azurecli
az --version
```

<span data-ttu-id="c5bec-119">Jeśli nie masz hello `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c5bec-119">If you don't have hello `az` tool installed, there are instructions [here](/cli/azure/install-azure-cli).</span></span>

<span data-ttu-id="c5bec-120">Możesz przetestować, jeśli masz hello `kubectl` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="c5bec-120">You can test if you have hello `kubectl` tool installed by running:</span></span>

```bash
kubectl version
```

<span data-ttu-id="c5bec-121">Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:</span><span class="sxs-lookup"><span data-stu-id="c5bec-121">If you don't have `kubectl` installed, you can run:</span></span>

```azurecli
az acs kubernetes install-cli
```

## <a name="installing-hello-coscale-agent-with-a-daemonset"></a><span data-ttu-id="c5bec-122">Instalowanie agenta CoScale hello z DaemonSet</span><span class="sxs-lookup"><span data-stu-id="c5bec-122">Installing hello CoScale agent with a DaemonSet</span></span>
<span data-ttu-id="c5bec-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) są używane przez Kubernetes toorun pojedynczego wystąpienia kontenera na każdym hoście w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c5bec-123">[DaemonSets](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/) are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="c5bec-124">Są one idealne w przypadku uruchamiania agenci monitorowania, takich jak hello CoScale agenta.</span><span class="sxs-lookup"><span data-stu-id="c5bec-124">They're perfect for running monitoring agents such as hello CoScale agent.</span></span>

<span data-ttu-id="c5bec-125">Po zalogowaniu tooCoScale Przejdź toohello [agent strona](https://app.coscale.com/) tooinstall CoScale agentów w klastrze za pomocą DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="c5bec-125">After you log in tooCoScale, go toohello [agent page](https://app.coscale.com/) tooinstall CoScale agents on your cluster using a DaemonSet.</span></span> <span data-ttu-id="c5bec-126">Hello CoScale interfejsu użytkownika zawiera toocreate kroki z przewodnikiem konfiguracji agenta i rozpocząć monitorowanie pełną Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="c5bec-126">hello CoScale UI provides guided configuration steps toocreate an agent and start monitoring your complete Kubernetes cluster.</span></span>

![CoScale konfiguracji agenta](./media/container-service-kubernetes-coscale/installation.png)

<span data-ttu-id="c5bec-128">agent hello toostart w klastrze hello, uruchom polecenie hello dostarczone:</span><span class="sxs-lookup"><span data-stu-id="c5bec-128">toostart hello agent on hello cluster, run hello supplied command:</span></span>

![Uruchom agenta CoScale hello](./media/container-service-kubernetes-coscale/agent_script.png)

<span data-ttu-id="c5bec-130">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="c5bec-130">That's it!</span></span> <span data-ttu-id="c5bec-131">Po skonfigurowaniu i uruchomieniu agentów hello danych w konsoli hello powinna zostać wyświetlona za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="c5bec-131">Once hello agents are up and running, you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="c5bec-132">Odwiedź hello [agent strona](https://app.coscale.com/) toosee podsumowanie klastra, wykonanie dodatkowych kroków konfiguracji, a następnie zobacz pulpitów nawigacyjnych, takich jak hello **Kubernetes klastra omówienie**.</span><span class="sxs-lookup"><span data-stu-id="c5bec-132">Visit hello [agent page](https://app.coscale.com/) toosee a summary of your cluster, perform additional configuration steps, and see dashboards such as hello **Kubernetes cluster overview**.</span></span>

![Omówienie klastrów Kubernetes](./media/container-service-kubernetes-coscale/dashboard_clusteroverview.png)

<span data-ttu-id="c5bec-134">Hello CoScale agent jest automatycznie wdrażane na nowych maszyn w klastrze hello.</span><span class="sxs-lookup"><span data-stu-id="c5bec-134">hello CoScale agent is automatically deployed on new machines in hello cluster.</span></span> <span data-ttu-id="c5bec-135">aktualizacje agenta Hello automatycznie po wydaniu nowej wersji.</span><span class="sxs-lookup"><span data-stu-id="c5bec-135">hello agent updates automatically when a new version is released.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c5bec-136">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c5bec-136">Next steps</span></span>

<span data-ttu-id="c5bec-137">Zobacz hello [CoScale dokumentacji](http://docs.coscale.com/) i [blogu](https://www.coscale.com/blog) uzyskać więcej informacji o CoScale monitorowanie rozwiązań.</span><span class="sxs-lookup"><span data-stu-id="c5bec-137">See hello [CoScale documentation](http://docs.coscale.com/) and [blog](https://www.coscale.com/blog) for more more information about CoScale monitoring solutions.</span></span> 

