---
title: "klaster Azure Kubernetes aaaMonitor - operacje zarządzania | Dokumentacja firmy Microsoft"
description: "Monitorowanie Kubernetes klastra usługi kontenera platformy Azure przy użyciu programu Microsoft Operations Management Suite"
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
ms.openlocfilehash: 7474ee1571134ffe43ff8e4041cf5a64f5635bb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-microsoft-operations-management-suite-oms"></a><span data-ttu-id="b95d7-103">Monitor klastra usługi kontenera platformy Azure z Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="b95d7-103">Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b95d7-104">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b95d7-104">Prerequisites</span></span>
<span data-ttu-id="b95d7-105">W tym przewodniku założono, że [utworzony klaster Kubernetes za pomocą usługi kontenera platformy Azure](container-service-kubernetes-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="b95d7-105">This walkthrough assumes that you have [created a Kubernetes cluster using Azure Container Service](container-service-kubernetes-walkthrough.md).</span></span>

<span data-ttu-id="b95d7-106">Założono również, że masz hello `az` interfejsu wiersza polecenia platformy Azure i `kubectl` narzędzia są zainstalowane.</span><span class="sxs-lookup"><span data-stu-id="b95d7-106">It also assumes that you have hello `az` Azure cli and `kubectl` tools installed.</span></span>

<span data-ttu-id="b95d7-107">Możesz przetestować, jeśli masz hello `az` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="b95d7-107">You can test if you have hello `az` tool installed by running:</span></span>

```console
$ az --version
```

<span data-ttu-id="b95d7-108">Jeśli nie masz hello `az` narzędzie zainstalowane, nie ma instrukcji [tutaj](https://github.com/azure/azure-cli#installation).</span><span class="sxs-lookup"><span data-stu-id="b95d7-108">If you don't have hello `az` tool installed, there are instructions [here](https://github.com/azure/azure-cli#installation).</span></span>  
<span data-ttu-id="b95d7-109">Alternatywnie można użyć [powłoki chmury Azure](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), mającego hello `az` interfejsu wiersza polecenia platformy Azure i `kubectl` narzędzia już zainstalowane automatycznie.</span><span class="sxs-lookup"><span data-stu-id="b95d7-109">Alternatively, you can use [Azure Cloud Shell](https://docs.microsoft.com/en-us/azure/cloud-shell/overview), which has hello `az` Azure cli and `kubectl` tools already installed for you.</span></span>  

<span data-ttu-id="b95d7-110">Możesz przetestować, jeśli masz hello `kubectl` zainstalowany, uruchamiając narzędzie:</span><span class="sxs-lookup"><span data-stu-id="b95d7-110">You can test if you have hello `kubectl` tool installed by running:</span></span>

```console
$ kubectl version
```

<span data-ttu-id="b95d7-111">Jeśli nie masz `kubectl` zainstalowany, możesz uruchomić:</span><span class="sxs-lookup"><span data-stu-id="b95d7-111">If you don't have `kubectl` installed, you can run:</span></span>
```console
$ az acs kubernetes install-cli
```

<span data-ttu-id="b95d7-112">tootest, jeśli masz zainstalowany w narzędziu do kubectl klucze kubernetes można uruchomić:</span><span class="sxs-lookup"><span data-stu-id="b95d7-112">tootest if you have kubernetes keys installed in your kubectl tool you can run:</span></span>
```console
$ kubectl get nodes
```

<span data-ttu-id="b95d7-113">Jeśli hello powyżej polecenie błędy wychodzących, należy do własnych narzędzi kubectl tooinstall kubernetes klastra kluczy.</span><span class="sxs-lookup"><span data-stu-id="b95d7-113">If hello above command errors out, you need tooinstall kubernetes cluster keys into your kubectl tool.</span></span> <span data-ttu-id="b95d7-114">Możesz to zrobić z hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b95d7-114">You can do that with hello following command:</span></span>
```console
RESOURCE_GROUP=my-resource-group
CLUSTER_NAME=my-acs-name
az acs kubernetes get-credentials --resource-group=$RESOURCE_GROUP --name=$CLUSTER_NAME
```

## <a name="monitoring-containers-with-operations-management-suite-oms"></a><span data-ttu-id="b95d7-115">Monitorowanie kontenerów w usłudze Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="b95d7-115">Monitoring Containers with Operations Management Suite (OMS)</span></span>

<span data-ttu-id="b95d7-116">Microsoft Operations Management (OMS) jest firmy Microsoft w chmurze IT rozwiązania do zarządzania ułatwiające zarządzanie i ochrona lokalnej infrastruktury w chmurze.</span><span class="sxs-lookup"><span data-stu-id="b95d7-116">Microsoft Operations Management (OMS) is Microsoft's cloud-based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="b95d7-117">Kontener rozwiązanie to rozwiązanie w OMS Log Analytics, który pomaga w widoku hello kontenera magazynu, wydajności i dzienniki w jednej lokalizacji.</span><span class="sxs-lookup"><span data-stu-id="b95d7-117">Container Solution is a solution in OMS Log Analytics, which helps you view hello container inventory, performance, and logs in a single location.</span></span> <span data-ttu-id="b95d7-118">Można inspekcji, rozwiązywanie problemów z kontenerów, wyświetlając hello dzienniki w centralnej lokalizacji oraz znaleźć zakłócenia, wykorzystywanie nadmiarowe kontenera na hoście.</span><span class="sxs-lookup"><span data-stu-id="b95d7-118">You can audit, troubleshoot containers by viewing hello logs in centralized location, and find noisy consuming excess container on a host.</span></span>

![](media/container-service-monitoring-oms/image1.png)

<span data-ttu-id="b95d7-119">Aby uzyskać więcej informacji o rozwiązaniu kontenera, zobacz toothe [analizy dzienników rozwiązania kontenera](../../log-analytics/log-analytics-containers.md).</span><span class="sxs-lookup"><span data-stu-id="b95d7-119">For more information about Container Solution, please refer toothe [Container Solution Log Analytics](../../log-analytics/log-analytics-containers.md).</span></span>

## <a name="installing-oms-on-kubernetes"></a><span data-ttu-id="b95d7-120">Instalowanie pakietu OMS na Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b95d7-120">Installing OMS on Kubernetes</span></span>

### <a name="obtain-your-workspace-id-and-key"></a><span data-ttu-id="b95d7-121">Uzyskaj identyfikator i klucz</span><span class="sxs-lookup"><span data-stu-id="b95d7-121">Obtain your workspace ID and key</span></span>
<span data-ttu-id="b95d7-122">Hello usługi toohello tootalk agent pakietu OMS musi on toobe skonfigurowany identyfikator obszaru roboczego i klucz obszaru roboczego.</span><span class="sxs-lookup"><span data-stu-id="b95d7-122">For hello OMS agent tootalk toohello service it needs toobe configured with a workspace id and a workspace key.</span></span> <span data-ttu-id="b95d7-123">Klucz należy toocreate OMS i identyfikator obszaru roboczego hello tooget konta w <https://mms.microsoft.com>. Wykonaj hello kroki toocreate konta.</span><span class="sxs-lookup"><span data-stu-id="b95d7-123">tooget hello workspace id and key you need toocreate an OMS account at <https://mms.microsoft.com>. Please follow hello steps toocreate an account.</span></span> <span data-ttu-id="b95d7-124">Po zakończeniu tworzenia konta hello należy tooobtain Twój identyfikator i klucz, klikając **ustawienia**, następnie **połączonych źródeł**, a następnie **serwerów z systemem Linux**, jak pokazano poniżej.</span><span class="sxs-lookup"><span data-stu-id="b95d7-124">Once you are done creating hello account, you need tooobtain your id and key by clicking **Settings**, then **Connected Sources**, and then **Linux Servers**, as shown below.</span></span>

 ![](media/container-service-monitoring-oms/image5.png)

### <a name="install-hello-oms-agent-using-a-daemonset"></a><span data-ttu-id="b95d7-125">Instalowanie agenta pakietu OMS hello za pomocą DaemonSet</span><span class="sxs-lookup"><span data-stu-id="b95d7-125">Install hello OMS agent using a DaemonSet</span></span>
<span data-ttu-id="b95d7-126">DaemonSets są używane przez Kubernetes toorun pojedynczego wystąpienia na każdym hoście w klastrze hello kontenera.</span><span class="sxs-lookup"><span data-stu-id="b95d7-126">DaemonSets are used by Kubernetes toorun a single instance of a container on each host in hello cluster.</span></span>
<span data-ttu-id="b95d7-127">Są one idealne w przypadku uruchamiania agenci monitorowania.</span><span class="sxs-lookup"><span data-stu-id="b95d7-127">They're perfect for running monitoring agents.</span></span>

<span data-ttu-id="b95d7-128">Oto hello [pliku yaml programu DaemonSet](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span><span class="sxs-lookup"><span data-stu-id="b95d7-128">Here is hello [DaemonSet YAML file](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes).</span></span> <span data-ttu-id="b95d7-129">Zapisz plik o nazwie pliku tooa `oms-daemonset.yaml` i Zastąp symbol zastępczy wartości hello `WSID` i `KEY` z identyfikator i klucz w pliku hello.</span><span class="sxs-lookup"><span data-stu-id="b95d7-129">Save it tooa file named `oms-daemonset.yaml` and replace hello place-holder values for `WSID` and `KEY` with your workspace id and key in hello file.</span></span>

<span data-ttu-id="b95d7-130">Po dodaniu klucza toohello DaemonSet konfiguracji i identyfikator obszaru roboczego, na których można zainstalować agenta pakietu OMS hello w klastrze z hello `kubectl` narzędzia wiersza polecenia:</span><span class="sxs-lookup"><span data-stu-id="b95d7-130">Once you have added your workspace ID and key toohello DaemonSet configuration, you can install hello OMS agent on your cluster with hello `kubectl` command line tool:</span></span>

```console
$ kubectl create -f oms-daemonset.yaml
```

### <a name="installing-hello-oms-agent-using-a-kubernetes-secret"></a><span data-ttu-id="b95d7-131">Instalowanie agenta pakietu OMS hello przy użyciu klucza tajnego Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b95d7-131">Installing hello OMS agent using a Kubernetes Secret</span></span>
<span data-ttu-id="b95d7-132">tooprotect OMS identyfikator i klucz tajny Kubernetes można użyć jako część pliku DaemonSet yaml programu.</span><span class="sxs-lookup"><span data-stu-id="b95d7-132">tooprotect your OMS workspace ID and key you can use Kubernetes Secret as a part of DaemonSet YAML file.</span></span>

 - <span data-ttu-id="b95d7-133">Skopiuj skrypt hello, pliku szablonu tajne i hello pliku DaemonSet yaml programu (z [repozytorium](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) i upewnij się, że są one na powitania tego samego katalogu.</span><span class="sxs-lookup"><span data-stu-id="b95d7-133">Copy hello script, secret template file and hello DaemonSet YAML file (from [repository](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes)) and make sure they are on hello same directory.</span></span> 
      - <span data-ttu-id="b95d7-134">Generowanie skryptu - gen.sh klucz tajny klucz tajny</span><span class="sxs-lookup"><span data-stu-id="b95d7-134">secret generating script - secret-gen.sh</span></span>
      - <span data-ttu-id="b95d7-135">Szablon tajne — template.yaml klucz tajny</span><span class="sxs-lookup"><span data-stu-id="b95d7-135">secret template - secret-template.yaml</span></span>
   - <span data-ttu-id="b95d7-136">Plik yaml programu DaemonSet — omsagent — ds-secrets.yaml</span><span class="sxs-lookup"><span data-stu-id="b95d7-136">DaemonSet YAML file - omsagent-ds-secrets.yaml</span></span>
 - <span data-ttu-id="b95d7-137">Uruchom skrypt hello.</span><span class="sxs-lookup"><span data-stu-id="b95d7-137">Run hello script.</span></span> <span data-ttu-id="b95d7-138">skrypt Hello poprosi o hello OMS identyfikator i klucz podstawowy.</span><span class="sxs-lookup"><span data-stu-id="b95d7-138">hello script will ask for hello OMS Workspace ID and Primary Key.</span></span> <span data-ttu-id="b95d7-139">Włóż który i hello skryptu zostanie utworzony plik tajny yaml programu, dlatego może być uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="b95d7-139">Please insert that and hello script will create a secret yaml file so you can run it.</span></span>   
   ```
   #> sudo bash ./secret-gen.sh 
   ```

   - <span data-ttu-id="b95d7-140">Utwórz pod kluczy tajnych hello, uruchamiając następujące hello:``` kubectl create -f omsagentsecret.yaml ```</span><span class="sxs-lookup"><span data-stu-id="b95d7-140">Create hello secrets pod by running hello following: ``` kubectl create -f omsagentsecret.yaml ```</span></span>
 
   - <span data-ttu-id="b95d7-141">toocheck, uruchom następujące hello:</span><span class="sxs-lookup"><span data-stu-id="b95d7-141">toocheck, run hello following:</span></span> 

   ``` 
   root@ubuntu16-13db:~# kubectl get secrets
   NAME                  TYPE                                  DATA      AGE
   default-token-gvl91   kubernetes.io/service-account-token   3         50d
   omsagent-secret       Opaque                                2         1d
   root@ubuntu16-13db:~# kubectl describe secrets omsagent-secret
   Name:           omsagent-secret
   Namespace:      default
   Labels:         <none>
   Annotations:    <none>

   Type:   Opaque

   Data
   ====
   WSID:   36 bytes
   KEY:    88 bytes 
   ```
 
  - <span data-ttu-id="b95d7-142">Tworzenie sieci omsagent demon set, uruchamiając``` kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="b95d7-142">Create your omsagent daemon-set by running ``` kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

### <a name="conclusion"></a><span data-ttu-id="b95d7-143">Podsumowanie</span><span class="sxs-lookup"><span data-stu-id="b95d7-143">Conclusion</span></span>
<span data-ttu-id="b95d7-144">Gotowe.</span><span class="sxs-lookup"><span data-stu-id="b95d7-144">That's it!</span></span> <span data-ttu-id="b95d7-145">Po kilku minutach powinno być możliwe toosee dane przepływające tooyour OMS z pulpitu nawigacyjnego.</span><span class="sxs-lookup"><span data-stu-id="b95d7-145">After a few minutes, you should be able toosee data flowing tooyour OMS dashboard.</span></span>
