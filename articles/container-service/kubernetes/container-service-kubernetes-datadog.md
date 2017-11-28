---
title: aaaMonitor Azure Kubernetes klaster z Datadog | Dokumentacja firmy Microsoft
description: "Monitorowanie Kubernetes klastra usługi kontenera platformy Azure przy użyciu Datadog"
services: container-service
documentationcenter: 
author: bburns
manager: timlt
editor: 
tags: acs, azure-container-service, kubernetes
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: bccd8b59a048e0f791172fcfc4eeba6370dafcc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="2ea52-103">Monitor klastra usługi kontenera platformy Azure z DataDog</span><span class="sxs-lookup"><span data-stu-id="2ea52-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ea52-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2ea52-104">Prerequisites</span></span>
<span data-ttu-id="2ea52-105">W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="2ea52-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="2ea52-106">Założono również, że masz hello `az` interfejsu wiersza polecenia platformy Azure i `kubectl` narzędzia są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="2ea52-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="2ea52-107">Możesz przetestować, jeśli masz hello `az` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="2ea52-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="2ea52-108">Jeśli nie masz hello `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="2ea52-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="2ea52-109">Możesz przetestować, jeśli masz hello `kubectl` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="2ea52-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="2ea52-110">Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:</span><span class="sxs-lookup"><span data-stu-id="2ea52-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="2ea52-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="2ea52-111">DataDog</span></span>
<span data-ttu-id="2ea52-112">Datadog jest usługą monitorowania, która gromadzi dane monitorowania z kontenerów w ramach klastra usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ea52-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="2ea52-113">Datadog ma pulpitu nawigacyjnego Docker integracji umożliwia wyświetlenie określonych metryk w kontenerów.</span><span class="sxs-lookup"><span data-stu-id="2ea52-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="2ea52-114">Metryki zebrane z kontenerów są zorganizowane według Procesora, pamięci, sieci i we/wy.</span><span class="sxs-lookup"><span data-stu-id="2ea52-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="2ea52-115">Datadog dzieli metryki na kontenery i obrazów.</span><span class="sxs-lookup"><span data-stu-id="2ea52-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="2ea52-116">Należy najpierw zbyt[Tworzenie konta usługi](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="2ea52-116">You first need too[create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-hello-datadog-agent-with-a-daemonset"></a><span data-ttu-id="2ea52-117">Instalowanie agenta Datadog hello z DaemonSet</span><span class="sxs-lookup"><span data-stu-id="2ea52-117">Installing hello Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="2ea52-118">DaemonSets są używane przez Kubernetes toorun pojedynczego wystąpienia na każdym hoście w klastrze hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="2ea52-118">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="2ea52-119">Są one idealne w przypadku uruchamiania agenci monitorowania.</span><span class="sxs-lookup"><span data-stu-id="2ea52-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="2ea52-120">Gdy użytkownik zalogował się do Datadog, możesz wykonać hello [instrukcje Datadog](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agentów w klastrze za pomocą DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="2ea52-120">Once you have logged into Datadog, you can follow hello [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) tooinstall Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="2ea52-121">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="2ea52-121">Conclusion</span></span>
<span data-ttu-id="2ea52-122">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="2ea52-122">That's it!</span></span> <span data-ttu-id="2ea52-123">Po hello agenci są uruchomione i systemem można powinny być widoczne dane w konsoli hello za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="2ea52-123">Once hello agents are up and running you should see data in hello console in a few minutes.</span></span> <span data-ttu-id="2ea52-124">Użytkownik może odwiedzić hello zintegrowane [pulpitu nawigacyjnego kubernetes](https://app.datadoghq.com/screen/integration/kubernetes) toosee podsumowanie klastra.</span><span class="sxs-lookup"><span data-stu-id="2ea52-124">You can visit hello integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) toosee a summary of your cluster.</span></span>
