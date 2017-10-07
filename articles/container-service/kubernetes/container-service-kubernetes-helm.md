---
title: kontenery aaaDeploy z Helm w Azure Kubernetes | Dokumentacja firmy Microsoft
description: "Użyj hello Helm pakowania narzędzia toodeploy kontenery w klastrze Kubernetes usługi kontenera platformy Azure"
services: container-service
documentationcenter: 
author: sauryadas
manager: madhana
editor: 
tags: acs, azure-container-service
keywords: 
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/10/2017
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: c7bd780afe00084ebe4e3a14873e1e340a29d144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="use-helm-toodeploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="b4c6d-103">Używanie kontenerów toodeploy Helm w klastrze Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b4c6d-103">Use Helm toodeploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="b4c6d-104">[Helm](https://github.com/kubernetes/helm/) jest narzędziem open source tworzenia pakietów, które pomaga zainstalować i zarządzanie cyklem życia hello Kubernetes aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage hello lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="b4c6d-105">Podobne tooLinux pakietu menedżerów takich jak Apt get i Yum Helm jest używane toomanage Kubernetes wykresy, które są pakiety zasobów Kubernetes wstępnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-105">Similar tooLinux package managers such as Apt-get and Yum, Helm is used toomanage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="b4c6d-106">W tym artykule opisano sposób toowork z Helm w klastrze Kubernetes wdrożenia usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-106">This article shows you how toowork with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="b4c6d-107">Helm ma dwa składniki:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-107">Helm has two components:</span></span> 
* <span data-ttu-id="b4c6d-108">Witaj **Helm CLI** uruchomioną na komputerze lokalnie lub w chmurze powitania klienta</span><span class="sxs-lookup"><span data-stu-id="b4c6d-108">hello **Helm CLI** is a client that runs on your machine locally or in hello cloud</span></span>  

* <span data-ttu-id="b4c6d-109">**Sterownicy** jest serwer, który działa w klastrze Kubernetes hello i zarządza hello cyklem życia aplikacji Kubernetes</span><span class="sxs-lookup"><span data-stu-id="b4c6d-109">**Tiller** is a server that runs on hello Kubernetes cluster and manages hello lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="b4c6d-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="b4c6d-110">Prerequisites</span></span>

* <span data-ttu-id="b4c6d-111">[Tworzenie klastra Kubernetes](container-service-kubernetes-walkthrough.md) usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="b4c6d-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="b4c6d-112">[Instalowanie i konfigurowanie `kubectl` ](../container-service-connect.md) na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="b4c6d-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="b4c6d-113">[Zainstaluj Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="b4c6d-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="b4c6d-114">Podstawy Helm</span><span class="sxs-lookup"><span data-stu-id="b4c6d-114">Helm basics</span></span> 

<span data-ttu-id="b4c6d-115">tooview informacji na temat hello Kubernetes klastra są sterownicy Instalowanie i wdrażanie aplikacji, wpisz następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-115">tooview information about hello Kubernetes cluster that you are installing Tiller and deploying your applications to, type hello following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl klastra — informacje](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="b4c6d-117">Po zainstalowaniu Helm zainstalować sterownicy w klastrze Kubernetes, wpisując następujące polecenie hello:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing hello following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="b4c6d-118">Po pomyślnym ukończeniu, pojawić się dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-118">When it completes successfully, you see output like hello following:</span></span>

![Sterownicy instalacji](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="b4c6d-120">tooview wszystkich hello Helm wykresów dostępne w repozytorium hello hello wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-120">tooview all hello Helm charts available in hello repository, type hello following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="b4c6d-121">Zostaną wyświetlone dane wyjściowe podobne do następujących hello:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-121">You see output like hello following:</span></span>

![Helm wyszukiwania](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="b4c6d-123">tooupdate hello wykresy tooget hello najnowsze wersje, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-123">tooupdate hello charts tooget hello latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="b4c6d-124">Wdrażanie Nginx wejściowych kontrolera wykresu</span><span class="sxs-lookup"><span data-stu-id="b4c6d-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="b4c6d-125">toodeploy Nginx wejściowych kontrolera wykresu wpisz jedno polecenie:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-125">toodeploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Wdrażanie kontrolera wejściowych](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="b4c6d-127">W przypadku wpisania `kubectl get svc` tooview wszystkich usług, które są uruchomione w klastrze hello, zostanie wyświetlony adres IP jest przypisania toohello wejściowych kontrolera.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-127">If you type `kubectl get svc` tooview all services that are running on hello cluster, you see that an IP address is assigned toohello ingress controller.</span></span> <span data-ttu-id="b4c6d-128">(Podczas przypisywania hello jest w toku, zobacz `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-128">(While hello assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="b4c6d-129">Może potrwać kilka minut toocomplete.)</span><span class="sxs-lookup"><span data-stu-id="b4c6d-129">It takes a couple of minutes toocomplete.)</span></span> 

<span data-ttu-id="b4c6d-130">Po przypisaniu adres IP hello Przejdź wartość toohello hello zewnętrznego adresu IP adres toosee hello Nginx zaplecza uruchomiony.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-130">After hello IP address is assigned, navigate toohello value of hello external IP address toosee hello Nginx backend running.</span></span> 
 
![Transfer danych przychodzących adresów IP](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="b4c6d-132">toosee listę wykresy zainstalowanych w klastrze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-132">toosee a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="b4c6d-133">Polecenie hello można skrócić zbyt`helm ls`.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-133">You can abbreviate hello command too`helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="b4c6d-134">Wdrażanie wykresu MariaDB i klienta</span><span class="sxs-lookup"><span data-stu-id="b4c6d-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="b4c6d-135">Teraz można wdrożyć wykresu MariaDB i bazy danych MariaDB klienta tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-135">Now deploy a MariaDB chart and a MariaDB client tooconnect toohello database.</span></span>

<span data-ttu-id="b4c6d-136">Wykres toodeploy hello MariaDB, hello wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-136">toodeploy hello MariaDB chart, type hello following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="b4c6d-137">gdzie `--name` jest znacznika używany w wersjach.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="b4c6d-138">W przypadku niepowodzenia wdrożenia hello Uruchom `helm repo update` i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-138">If hello deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="b4c6d-139">tooview wszystkich schematów hello wdrożone w klastrze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-139">tooview all hello charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="b4c6d-140">tooview wszystkich wdrożeń uruchomiona w klastrze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-140">tooview all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="b4c6d-141">Na koniec toorun pod tooaccess powitania klienta, wpisz:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-141">Finally, toorun a pod tooaccess hello client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="b4c6d-142">tooconnect toohello klienta, hello wpisz następujące polecenie, zastępując `v1-mariadb` o nazwie hello wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="b4c6d-142">tooconnect toohello client, type hello following command, replacing `v1-mariadb` with hello name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="b4c6d-143">Można teraz używać standardowych poleceń toocreate baz danych, tabelach itp. Na przykład `Create DATABASE testdb1;` tworzy pustą bazę danych.</span><span class="sxs-lookup"><span data-stu-id="b4c6d-143">You can now use standard SQL commands toocreate databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="b4c6d-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4c6d-144">Next steps</span></span>

* <span data-ttu-id="b4c6d-145">Aby uzyskać więcej informacji o zarządzaniu Kubernetes wykresy, zobacz hello [Helm dokumentacji](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="b4c6d-145">For more information about managing Kubernetes charts, see hello [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

