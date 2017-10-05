---
title: Monitor Azure Kubernetes klaster z Datadog | Dokumentacja firmy Microsoft
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
ms.openlocfilehash: 40b34457447a8f80d8cdf77579750e0c42df22d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-datadog"></a><span data-ttu-id="2bb35-103">Monitor klastra usługi kontenera platformy Azure z DataDog</span><span class="sxs-lookup"><span data-stu-id="2bb35-103">Monitor an Azure Container Service cluster with DataDog</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2bb35-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="2bb35-104">Prerequisites</span></span>
<span data-ttu-id="2bb35-105">W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="2bb35-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="2bb35-106">Założono również, że masz `az` interfejsu wiersza polecenia platformy Azure i `kubectl` narzędzia są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="2bb35-106">It also assumes that you have the `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="2bb35-107">Możesz przetestować, jeśli masz `az` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="2bb35-107">You can test if you have the `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="2bb35-108">Jeśli nie masz `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="2bb35-108">If you don't have the `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="2bb35-109">Możesz przetestować, jeśli masz `kubectl` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="2bb35-109">You can test if you have the `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="2bb35-110">Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:</span><span class="sxs-lookup"><span data-stu-id="2bb35-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="datadog"></a><span data-ttu-id="2bb35-111">DataDog</span><span class="sxs-lookup"><span data-stu-id="2bb35-111">DataDog</span></span>
<span data-ttu-id="2bb35-112">Datadog jest usługą monitorowania, która gromadzi dane monitorowania z kontenerów w ramach klastra usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2bb35-112">Datadog is a monitoring service that gathers monitoring data from your containers within your Azure Container Service cluster.</span></span> <span data-ttu-id="2bb35-113">Datadog ma pulpitu nawigacyjnego Docker integracji umożliwia wyświetlenie określonych metryk w kontenerów.</span><span class="sxs-lookup"><span data-stu-id="2bb35-113">Datadog has a Docker Integration Dashboard where you can see specific metrics within your containers.</span></span> <span data-ttu-id="2bb35-114">Metryki zebrane z kontenerów są zorganizowane według Procesora, pamięci, sieci i we/wy.</span><span class="sxs-lookup"><span data-stu-id="2bb35-114">Metrics gathered from your containers are organized by CPU, Memory, Network and I/O.</span></span> <span data-ttu-id="2bb35-115">Datadog dzieli metryki na kontenery i obrazów.</span><span class="sxs-lookup"><span data-stu-id="2bb35-115">Datadog splits metrics into containers and images.</span></span>

<span data-ttu-id="2bb35-116">Należy najpierw [Tworzenie konta usługi](https://www.datadoghq.com/lpg/)</span><span class="sxs-lookup"><span data-stu-id="2bb35-116">You first need to [create an account](https://www.datadoghq.com/lpg/)</span></span>

## <a name="installing-the-datadog-agent-with-a-daemonset"></a><span data-ttu-id="2bb35-117">Instalowanie agenta Datadog z DaemonSet</span><span class="sxs-lookup"><span data-stu-id="2bb35-117">Installing the Datadog Agent with a DaemonSet</span></span>
<span data-ttu-id="2bb35-118">DaemonSets są używane przez Kubernetes do uruchomienia pojedynczego wystąpienia kontenera na każdym hoście w klastrze.</span><span class="sxs-lookup"><span data-stu-id="2bb35-118">DaemonSets are used by Kubernetes to run a single instance of a container on each host in the cluster.</span></span>
<span data-ttu-id="2bb35-119">Są one idealne w przypadku uruchamiania agenci monitorowania.</span><span class="sxs-lookup"><span data-stu-id="2bb35-119">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="2bb35-120">Po zalogowania do Datadog, można użyć [instrukcje Datadog](https://app.datadoghq.com/account/settings#agent/kubernetes) do instalacji agentów Datadog w klastrze za pomocą DaemonSet.</span><span class="sxs-lookup"><span data-stu-id="2bb35-120">Once you have logged into Datadog, you can follow the [Datadog instructions](https://app.datadoghq.com/account/settings#agent/kubernetes) to install Datadog agents on your cluster using a DaemonSet.</span></span>

## <a name="conclusion"></a><span data-ttu-id="2bb35-121">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="2bb35-121">Conclusion</span></span>
<span data-ttu-id="2bb35-122">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="2bb35-122">That's it!</span></span> <span data-ttu-id="2bb35-123">Po skonfigurowaniu i uruchomieniu agentów danych w konsoli powinna zostać wyświetlona za kilka minut.</span><span class="sxs-lookup"><span data-stu-id="2bb35-123">Once the agents are up and running you should see data in the console in a few minutes.</span></span> <span data-ttu-id="2bb35-124">Użytkownik może odwiedzić zintegrowanego [pulpitu nawigacyjnego kubernetes](https://app.datadoghq.com/screen/integration/kubernetes) wyświetlić podsumowanie klastra.</span><span class="sxs-lookup"><span data-stu-id="2bb35-124">You can visit the integrated [kubernetes dashboard](https://app.datadoghq.com/screen/integration/kubernetes) to see a summary of your cluster.</span></span>
