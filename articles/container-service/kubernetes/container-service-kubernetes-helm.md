---
title: "Wdrażanie kontenerów z Helm w Azure Kubernetes | Dokumentacja firmy Microsoft"
description: "Wdrażanie kontenerów w klastrze Kubernetes usługi kontenera platformy Azure za pomocą narzędzia pakowania Helm"
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
ms.openlocfilehash: 3cfcc5abbee03ca8fbbec4e4eae711e7c2d9deae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="use-helm-to-deploy-containers-on-a-kubernetes-cluster"></a><span data-ttu-id="4fc97-103">Umożliwia wdrażanie kontenerów w klastrze Kubernetes Helm</span><span class="sxs-lookup"><span data-stu-id="4fc97-103">Use Helm to deploy containers on a Kubernetes cluster</span></span> 

<span data-ttu-id="4fc97-104">[Helm](https://github.com/kubernetes/helm/) jest narzędziem open source tworzenia pakietów, które pomaga zainstalować i zarządzanie cyklem życia aplikacji Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4fc97-104">[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications.</span></span> <span data-ttu-id="4fc97-105">Podobnie jak menedżerów pakietu systemu Linux, takich jak Apt get i Yum, Helm służy do zarządzania Kubernetes wykresy, które są pakiety zasobów Kubernetes wstępnie skonfigurowane.</span><span class="sxs-lookup"><span data-stu-id="4fc97-105">Similar to Linux package managers such as Apt-get and Yum, Helm is used to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.</span></span> <span data-ttu-id="4fc97-106">W tym artykule przedstawiono sposób pracy z Helm w klastrze Kubernetes wdrożony w usłudze kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4fc97-106">This article shows you how to work with Helm on a Kubernetes cluster deployed in Azure Container Service.</span></span>

<span data-ttu-id="4fc97-107">Helm ma dwa składniki:</span><span class="sxs-lookup"><span data-stu-id="4fc97-107">Helm has two components:</span></span> 
* <span data-ttu-id="4fc97-108">**Helm CLI** jest klienta, który jest uruchamiany na komputerze lokalnie lub w chmurze</span><span class="sxs-lookup"><span data-stu-id="4fc97-108">The **Helm CLI** is a client that runs on your machine locally or in the cloud</span></span>  

* <span data-ttu-id="4fc97-109">**Sterownicy** serwera, która działa w klastrze Kubernetes i umożliwia zarządzanie cyklem życia aplikacji Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4fc97-109">**Tiller** is a server that runs on the Kubernetes cluster and manages the lifecycle of your Kubernetes applications</span></span> 
 
## <a name="prerequisites"></a><span data-ttu-id="4fc97-110">Wymagania wstępne</span><span class="sxs-lookup"><span data-stu-id="4fc97-110">Prerequisites</span></span>

* <span data-ttu-id="4fc97-111">[Tworzenie klastra Kubernetes](container-service-kubernetes-walkthrough.md) usługi kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="4fc97-111">[Create a Kubernetes cluster](container-service-kubernetes-walkthrough.md) in Azure Container Service</span></span>

* <span data-ttu-id="4fc97-112">[Instalowanie i konfigurowanie `kubectl` ](../container-service-connect.md) na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="4fc97-112">[Install and configure `kubectl`](../container-service-connect.md) on a local computer</span></span>

* <span data-ttu-id="4fc97-113">[Zainstaluj Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) na komputerze lokalnym</span><span class="sxs-lookup"><span data-stu-id="4fc97-113">[Install Helm](https://github.com/kubernetes/helm/blob/master/docs/install.md) on a local computer</span></span>

## <a name="helm-basics"></a><span data-ttu-id="4fc97-114">Podstawy Helm</span><span class="sxs-lookup"><span data-stu-id="4fc97-114">Helm basics</span></span> 

<span data-ttu-id="4fc97-115">Aby wyświetlić informacje o klastrze Kubernetes są sterownicy Instalowanie i wdrażanie aplikacji, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4fc97-115">To view information about the Kubernetes cluster that you are installing Tiller and deploying your applications to, type the following command:</span></span>

```bash
kubectl cluster-info 
```
![kubectl klastra — informacje](./media/container-service-kubernetes-helm/clusterinfo.png)
 
<span data-ttu-id="4fc97-117">Po zainstalowaniu Helm zainstalować sterownicy w klastrze Kubernetes, wpisując następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4fc97-117">After you have installed Helm, install Tiller on your Kubernetes cluster by typing the following command:</span></span>

```bash
helm init --upgrade
```
<span data-ttu-id="4fc97-118">Po pomyślnym ukończeniu, pojawić się dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="4fc97-118">When it completes successfully, you see output like the following:</span></span>

![Sterownicy instalacji](./media/container-service-kubernetes-helm/tiller-install.png)
 
 
 
 
<span data-ttu-id="4fc97-120">Aby wyświetlić wszystkie dostępne wykresy Helm w repozytorium, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4fc97-120">To view all the Helm charts available in the repository, type the following command:</span></span>

```bash 
helm search 
```

<span data-ttu-id="4fc97-121">Zostaną wyświetlone dane wyjściowe podobne do następujących:</span><span class="sxs-lookup"><span data-stu-id="4fc97-121">You see output like the following:</span></span>

![Helm wyszukiwania](./media/container-service-kubernetes-helm/helm-search.png)
 
<span data-ttu-id="4fc97-123">Aby zaktualizować wykresy, aby pobrać najnowsze wersje, wpisz:</span><span class="sxs-lookup"><span data-stu-id="4fc97-123">To update the charts to get the latest versions, type:</span></span>

```bash 
helm repo update 
```
## <a name="deploy-an-nginx-ingress-controller-chart"></a><span data-ttu-id="4fc97-124">Wdrażanie Nginx wejściowych kontrolera wykresu</span><span class="sxs-lookup"><span data-stu-id="4fc97-124">Deploy an Nginx ingress controller chart</span></span> 
 
<span data-ttu-id="4fc97-125">Aby wdrożyć wykresu kontrolera wejściowych Nginx, wpisz jedno polecenie:</span><span class="sxs-lookup"><span data-stu-id="4fc97-125">To deploy an Nginx ingress controller chart, type a single command:</span></span>

```bash
helm install stable/nginx-ingress 
```
![Wdrażanie kontrolera wejściowych](./media/container-service-kubernetes-helm/nginx-ingress.png)

<span data-ttu-id="4fc97-127">W przypadku wpisania `kubectl get svc` do wyświetlania wszystkich usług, które są uruchomione w klastrze, zobaczysz, że adres IP jest przypisane do kontrolera wejściowych.</span><span class="sxs-lookup"><span data-stu-id="4fc97-127">If you type `kubectl get svc` to view all services that are running on the cluster, you see that an IP address is assigned to the ingress controller.</span></span> <span data-ttu-id="4fc97-128">(Przypisania w trakcie, zobacz `<pending>`.</span><span class="sxs-lookup"><span data-stu-id="4fc97-128">(While the assignment is in progress, you see `<pending>`.</span></span> <span data-ttu-id="4fc97-129">Może potrwać kilka minut.)</span><span class="sxs-lookup"><span data-stu-id="4fc97-129">It takes a couple of minutes to complete.)</span></span> 

<span data-ttu-id="4fc97-130">Po adres IP przypisany adres, przejdź do wartości jako zewnętrzny adres IP, aby wyświetlić Nginx wewnętrznej bazy danych, systemem.</span><span class="sxs-lookup"><span data-stu-id="4fc97-130">After the IP address is assigned, navigate to the value of the external IP address to see the Nginx backend running.</span></span> 
 
![Transfer danych przychodzących adresów IP](./media/container-service-kubernetes-helm/ingress-ip-address.png)


<span data-ttu-id="4fc97-132">Aby wyświetlić listę wykresy zainstalowany w klastrze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="4fc97-132">To see a list of charts installed on your cluster, type:</span></span>

```bash
helm list 
```

<span data-ttu-id="4fc97-133">Polecenie można skrócić `helm ls`.</span><span class="sxs-lookup"><span data-stu-id="4fc97-133">You can abbreviate the command to `helm ls`.</span></span>
 
 
 
 
## <a name="deploy-a-mariadb-chart-and-client"></a><span data-ttu-id="4fc97-134">Wdrażanie wykresu MariaDB i klienta</span><span class="sxs-lookup"><span data-stu-id="4fc97-134">Deploy a MariaDB chart and client</span></span>

<span data-ttu-id="4fc97-135">Teraz można wdrożyć na wykresie MariaDB i MariaDB klienta do połączenia z bazą danych.</span><span class="sxs-lookup"><span data-stu-id="4fc97-135">Now deploy a MariaDB chart and a MariaDB client to connect to the database.</span></span>

<span data-ttu-id="4fc97-136">Aby wdrożyć wykresu MariaDB, wpisz następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="4fc97-136">To deploy the MariaDB chart, type the following command:</span></span>

```bash
helm install --name v1 stable/mariadb
```

<span data-ttu-id="4fc97-137">gdzie `--name` jest znacznika używany w wersjach.</span><span class="sxs-lookup"><span data-stu-id="4fc97-137">where `--name` is a tag used for releases.</span></span>

> [!TIP]
> <span data-ttu-id="4fc97-138">Jeśli wdrożenie nie powiedzie się, uruchom `helm repo update` i spróbuj ponownie.</span><span class="sxs-lookup"><span data-stu-id="4fc97-138">If the deployment fails, run `helm repo update` and try again.</span></span>
>
 
 
<span data-ttu-id="4fc97-139">Aby wyświetlić wszystkich schematów, które są wdrożone w klastrze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="4fc97-139">To view all the charts deployed on your cluster, type:</span></span>

```bash 
helm list
```
 
<span data-ttu-id="4fc97-140">Aby wyświetlić wszystkie wdrożenia uruchomiona w klastrze, wpisz:</span><span class="sxs-lookup"><span data-stu-id="4fc97-140">To view all deployments running on your cluster, type:</span></span>

```bash
kubectl get deployments 
``` 
 
 
<span data-ttu-id="4fc97-141">Na koniec aby uruchomić pod dostęp klienta do, wpisz:</span><span class="sxs-lookup"><span data-stu-id="4fc97-141">Finally, to run a pod to access the client, type:</span></span>

```bash
kubectl run v1-mariadb-client --rm --tty -i --image bitnami/mariadb --command -- bash  
``` 
 
 
<span data-ttu-id="4fc97-142">Aby nawiązać połączenie klient, wpisz następujące polecenie, zastępując `v1-mariadb` o nazwie wdrożenia:</span><span class="sxs-lookup"><span data-stu-id="4fc97-142">To connect to the client, type the following command, replacing `v1-mariadb` with the name of your deployment:</span></span>

```bash
sudo mysql –h v1-mariadb
```
 
 
<span data-ttu-id="4fc97-143">Można teraz używać standardowych poleceń SQL do tworzenia baz danych, tabelach itp. Na przykład `Create DATABASE testdb1;` tworzy pustą bazę danych.</span><span class="sxs-lookup"><span data-stu-id="4fc97-143">You can now use standard SQL commands to create databases, tables, etc. For example, `Create DATABASE testdb1;` creates an empty database.</span></span> 
 
 
 
## <a name="next-steps"></a><span data-ttu-id="4fc97-144">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4fc97-144">Next steps</span></span>

* <span data-ttu-id="4fc97-145">Aby uzyskać więcej informacji o zarządzaniu Kubernetes wykresy, zobacz [Helm dokumentacji](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span><span class="sxs-lookup"><span data-stu-id="4fc97-145">For more information about managing Kubernetes charts, see the [Helm documentation](https://github.com/kubernetes/helm/blob/master/docs/index.md).</span></span> 

