---
title: klaster Azure Kubernetes aaaMonitor - Sysdig | Dokumentacja firmy Microsoft
description: "Monitorowanie Kubernetes klastra usługi kontenera platformy Azure przy użyciu Sysdig"
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
ms.date: 12/09/2016
ms.author: bburns
ms.custom: mvc
ms.openlocfilehash: a27813d01ee4624b9e993f6185169ad73aeec3a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-kubernetes-cluster-using-sysdig"></a><span data-ttu-id="02456-103">Monitorowanie klastra Kubernetes usługi kontenera platformy Azure przy użyciu Sysdig</span><span class="sxs-lookup"><span data-stu-id="02456-103">Monitor an Azure Container Service Kubernetes cluster using Sysdig</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02456-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="02456-104">Prerequisites</span></span>
<span data-ttu-id="02456-105">W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="02456-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="02456-106">Przyjęto założenie, że masz hello azure cli i kubectl narzędzia są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="02456-106">It also assumes that you have hello azure cli and kubectl tools installed.</span></span>

<span data-ttu-id="02456-107">Możesz przetestować, jeśli masz hello `az` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="02456-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="02456-108">Jeśli nie masz hello `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="02456-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>

<span data-ttu-id="02456-109">Możesz przetestować, jeśli masz hello `kubectl` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="02456-109">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="02456-110">Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:</span><span class="sxs-lookup"><span data-stu-id="02456-110">If you don't have `kubectl` installed, you can run:</span></span>

```console
$ az acs kubernetes install-cli
```

## <a name="sysdig"></a><span data-ttu-id="02456-111">Sysdig</span><span class="sxs-lookup"><span data-stu-id="02456-111">Sysdig</span></span>
<span data-ttu-id="02456-112">Sysdig jest zewnętrznych monitorowanie jako firmy usługi, które można monitorować kontenery w klastrze Kubernetes działające na platformie Azure.</span><span class="sxs-lookup"><span data-stu-id="02456-112">Sysdig is an external monitoring as a service company which can monitor containers in your Kubernetes cluster running in Azure.</span></span> <span data-ttu-id="02456-113">Przy użyciu Sysdig wymaga aktywnego konta Sysdig.</span><span class="sxs-lookup"><span data-stu-id="02456-113">Using Sysdig requires an active Sysdig account.</span></span>
<span data-ttu-id="02456-114">Można założyć konto ich [lokacji](https://app.sysdigcloud.com).</span><span class="sxs-lookup"><span data-stu-id="02456-114">You can sign up for an account on their [site](https://app.sysdigcloud.com).</span></span>

<span data-ttu-id="02456-115">Po zalogowaniu się w witrynie sieci Web toohello Sysdig chmury, kliknij swoją nazwę użytkownika, a na stronie powitania powinna zostać wyświetlona "Klucz dostępu do."</span><span class="sxs-lookup"><span data-stu-id="02456-115">Once you're logged in toohello Sysdig cloud website, click on your user name, and on hello page you should see your "Access Key."</span></span> 

![Klucz interfejsu API usługi Sysdig](./media/container-service-kubernetes-sysdig/sysdig2.png)

## <a name="installing-hello-sysdig-agents-tookubernetes"></a><span data-ttu-id="02456-117">Instalowanie hello Sysdig agentów tooKubernetes</span><span class="sxs-lookup"><span data-stu-id="02456-117">Installing hello Sysdig agents tooKubernetes</span></span>
<span data-ttu-id="02456-118">toomonitor kontenerów, Sysdig uruchamia proces na każdym komputerze, za pomocą Kubernetes `DaemonSet`.</span><span class="sxs-lookup"><span data-stu-id="02456-118">toomonitor your containers, Sysdig runs a process on each machine using a Kubernetes `DaemonSet`.</span></span>
<span data-ttu-id="02456-119">DaemonSets są obiektami Kubernetes interfejsu API, które uruchomienia pojedynczego wystąpienia kontenera dla poszczególnych komputerów.</span><span class="sxs-lookup"><span data-stu-id="02456-119">DaemonSets are Kubernetes API objects that run a single instance of a container per machine.</span></span>
<span data-ttu-id="02456-120">Są one idealne w przypadku instalowania narzędzi, takich jak hello agenta monitorowania firmy Sysdig.</span><span class="sxs-lookup"><span data-stu-id="02456-120">They're perfect for installing tools like hello Sysdig's monitoring agent.</span></span>

<span data-ttu-id="02456-121">tooinstall hello Sysdig daemonset, należy najpierw pobrać [szablonu hello](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) z sysdig.</span><span class="sxs-lookup"><span data-stu-id="02456-121">tooinstall hello Sysdig daemonset, you should first download [hello template](https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml) from sysdig.</span></span> <span data-ttu-id="02456-122">Zapisz ten plik jako `sysdig-daemonset.yaml`.</span><span class="sxs-lookup"><span data-stu-id="02456-122">Save that file as `sysdig-daemonset.yaml`.</span></span>

<span data-ttu-id="02456-123">W systemie Linux i OS X, można uruchomić:</span><span class="sxs-lookup"><span data-stu-id="02456-123">On Linux and OS X you can run:</span></span>

```console
$ curl -O https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml
```

<span data-ttu-id="02456-124">W programie PowerShell:</span><span class="sxs-lookup"><span data-stu-id="02456-124">In PowerShell:</span></span>

```console
$ Invoke-WebRequest -Uri https://raw.githubusercontent.com/draios/sysdig-cloud-scripts/master/agent_deploy/kubernetes/sysdig-daemonset.yaml | Select-Object -ExpandProperty Content > sysdig-daemonset.yaml
```

<span data-ttu-id="02456-125">Klucz dostępu, uzyskany z Twojego konta Sysdig obok edytować tooinsert tego pliku.</span><span class="sxs-lookup"><span data-stu-id="02456-125">Next edit that file tooinsert your Access Key, that you obtained from your Sysdig account.</span></span>

<span data-ttu-id="02456-126">Na koniec Utwórz hello DaemonSet:</span><span class="sxs-lookup"><span data-stu-id="02456-126">Finally, create hello DaemonSet:</span></span>

```console
$ kubectl create -f sysdig-daemonset.yaml
```

## <a name="view-your-monitoring"></a><span data-ttu-id="02456-127">Wyświetlanie, monitorowanie</span><span class="sxs-lookup"><span data-stu-id="02456-127">View your monitoring</span></span>
<span data-ttu-id="02456-128">Gdy zainstalowana i uruchomiona, hello agentów powinien pompa tooSysdig wstecz danych.</span><span class="sxs-lookup"><span data-stu-id="02456-128">Once installed and running, hello agents should pump data back tooSysdig.</span></span>  <span data-ttu-id="02456-129">Przejdź wstecz toothe [pulpitu nawigacyjnego sysdig](https://app.sysdigcloud.com) i powinny być widoczne informacje o kontenerów.</span><span class="sxs-lookup"><span data-stu-id="02456-129">Go back toothe [sysdig dashboard](https://app.sysdigcloud.com) and you should see information about your containers.</span></span>

<span data-ttu-id="02456-130">Można także zainstalować pulpity nawigacyjne Kubernetes określonego za pomocą [Kreator nowego pulpitu nawigacyjnego](https://app.sysdigcloud.com/#/dashboards/new).</span><span class="sxs-lookup"><span data-stu-id="02456-130">You can also install Kubernetes-specific dashboards via the [new dashboard wizard](https://app.sysdigcloud.com/#/dashboards/new).</span></span>
