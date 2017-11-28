---
title: "Samouczek usługi kontenera platformy Azure — wdrażanie aplikacji | Dokumentacja firmy Microsoft"
description: "Samouczek usługi kontenera platformy Azure — wdrażanie aplikacji"
services: container-service
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, kontenery, mikrousługi, Kubernetes, DC/OS, Azure"
ms.assetid: 
ms.service: container-service
ms.devlang: aurecli
ms.topic: tutorial
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ea67f0beb6a5926393b26e7590302ad0f46a63f9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="run-applications-in-kubernetes"></a><span data-ttu-id="7ed40-104">Uruchamianie aplikacji w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7ed40-104">Run applications in Kubernetes</span></span>

<span data-ttu-id="7ed40-105">W tym samouczku część cztery siedmiu, przykładowa aplikacja jest wdrażana w klastrze Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="7ed40-105">In this tutorial, part four of seven, a sample application is deployed into a Kubernetes cluster.</span></span> <span data-ttu-id="7ed40-106">Ukończono kroki obejmują:</span><span class="sxs-lookup"><span data-stu-id="7ed40-106">Steps completed include:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ed40-107">Pobierz pliki manifestu Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7ed40-107">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="7ed40-108">Uruchom aplikację w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7ed40-108">Run application in Kubernetes</span></span>
> * <span data-ttu-id="7ed40-109">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="7ed40-109">Test the application</span></span>

<span data-ttu-id="7ed40-110">W kolejnych samouczkach tej aplikacji jest skalowana, aktualizacji, oraz Operations Management Suite jest skonfigurowana do monitorowania Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="7ed40-110">In subsequent tutorials, this application is scaled out, updated, and Operations Management Suite configured to monitor the Kubernetes cluster.</span></span>

<span data-ttu-id="7ed40-111">Ten samouczek zakłada podstawową wiedzę na temat pojęć Kubernetes, aby uzyskać szczegółowe informacje o Zobacz Kubernetes [dokumentacji Kubernetes](https://kubernetes.io/docs/home/).</span><span class="sxs-lookup"><span data-stu-id="7ed40-111">This tutorial assumes a basic understanding of Kubernetes concepts, for detailed information on Kubernetes see the [Kubernetes documentation](https://kubernetes.io/docs/home/).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7ed40-112">Przed rozpoczęciem</span><span class="sxs-lookup"><span data-stu-id="7ed40-112">Before you begin</span></span>

<span data-ttu-id="7ed40-113">W poprzednim samouczki aplikacji zostało umieszczone w obrazie kontenera, ten obraz został załadowany w rejestrze kontenera Azure i klaster Kubernetes został utworzony.</span><span class="sxs-lookup"><span data-stu-id="7ed40-113">In previous tutorials, an application was packaged into a container image, this image was uploaded to Azure Container Registry, and a Kubernetes cluster was created.</span></span> <span data-ttu-id="7ed40-114">Jeśli nie zostało wykonane następujące kroki, a następnie zostać z niego skorzystać, wróć do [samouczek 1 — Tworzenie kontenera obrazów](./container-service-tutorial-kubernetes-prepare-app.md).</span><span class="sxs-lookup"><span data-stu-id="7ed40-114">If you have not done these steps, and would like to follow along, return to [Tutorial 1 – Create container images](./container-service-tutorial-kubernetes-prepare-app.md).</span></span> 

<span data-ttu-id="7ed40-115">Co najmniej tego samouczka wymaga Kubernetes klastra.</span><span class="sxs-lookup"><span data-stu-id="7ed40-115">At minimum, this tutorial requires a Kubernetes cluster.</span></span>

## <a name="get-manifest-file"></a><span data-ttu-id="7ed40-116">Pobierz plik manifestu</span><span class="sxs-lookup"><span data-stu-id="7ed40-116">Get manifest file</span></span>

<span data-ttu-id="7ed40-117">W tym samouczku [obiektów Kubernetes](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) są wdrażane za pomocą Kubernetes manifestu.</span><span class="sxs-lookup"><span data-stu-id="7ed40-117">For this tutorial, [Kubernetes objects](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/) are deployed using a Kubernetes manifest.</span></span> <span data-ttu-id="7ed40-118">Kubernetes manifest jest yaml programu lub JSON sformatowanym plikiem instrukcjami Kubernetes obiektu wdrażania i konfiguracji.</span><span class="sxs-lookup"><span data-stu-id="7ed40-118">A Kubernetes manifest is a YAML or JSON formatted file containing Kubernetes object deployment and configuration instructions.</span></span>

<span data-ttu-id="7ed40-119">Plik manifestu aplikacji do celów tego samouczka jest dostępna w repozytorium aplikacji głos Azure, który został sklonowany w poprzednim samouczka.</span><span class="sxs-lookup"><span data-stu-id="7ed40-119">The application manifest file for this tutorial is available in the Azure Vote application repo, which was cloned in a previous tutorial.</span></span> <span data-ttu-id="7ed40-120">Jeśli jeszcze nie sklonuj repozytorium przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="7ed40-120">If you have not already done so, clone the repo with the following command:</span></span> 

```bash
git clone https://github.com/Azure-Samples/azure-voting-app-redis.git
```

<span data-ttu-id="7ed40-121">Plik manifestu znajduje się w następującym katalogu sklonowanego repozytorium.</span><span class="sxs-lookup"><span data-stu-id="7ed40-121">The manifest file is found in the following directory of the cloned repo.</span></span>

```bash
/azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

## <a name="update-manifest-file"></a><span data-ttu-id="7ed40-122">Aktualizacja pliku manifestu</span><span class="sxs-lookup"><span data-stu-id="7ed40-122">Update manifest file</span></span>

<span data-ttu-id="7ed40-123">Jeśli za pomocą rejestru kontenera Azure do przechowywania obrazów kontenera, manifest musi zostać zaktualizowany o nazwie loginServer ACR.</span><span class="sxs-lookup"><span data-stu-id="7ed40-123">If using Azure Container Registry to store the container images, the manifest needs to be updated with the ACR loginServer name.</span></span>

<span data-ttu-id="7ed40-124">Pobierz nazwę serwera ACR logowania z [listy acr az](/cli/azure/acr#list) polecenia.</span><span class="sxs-lookup"><span data-stu-id="7ed40-124">Get the ACR login server name with the [az acr list](/cli/azure/acr#list) command.</span></span>

```azurecli-interactive
az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table
```

<span data-ttu-id="7ed40-125">Manifest próbki został wstępnie utworzone przy użyciu nazwy repozytorium *microsoft*.</span><span class="sxs-lookup"><span data-stu-id="7ed40-125">The sample manifest has been pre-created with a repository name of *microsoft*.</span></span> <span data-ttu-id="7ed40-126">Otwórz plik w dowolnym edytorze tekstu i Zastąp *microsoft* wartości z nazwą serwera logowania wystąpienia ACR.</span><span class="sxs-lookup"><span data-stu-id="7ed40-126">Open the file with any text editor, and replace the *microsoft* value with the login server name of your ACR instance.</span></span>

```yaml
containers:
- name: azure-vote-front
  image: microsoft/azure-vote-front:redis-v1
```

## <a name="deploy-application"></a><span data-ttu-id="7ed40-127">Wdrażanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="7ed40-127">Deploy application</span></span>

<span data-ttu-id="7ed40-128">Użyj polecenia [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create), aby uruchomić aplikację.</span><span class="sxs-lookup"><span data-stu-id="7ed40-128">Use the [kubectl create](https://kubernetes.io/docs/user-guide/kubectl/v1.6/#create) command to run the application.</span></span> <span data-ttu-id="7ed40-129">To polecenie analizuje pliku manifestu i tworzenia zdefiniowanych obiektów Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="7ed40-129">This command parses the manifest file and create the defined Kubernetes objects.</span></span>

```azurecli-interactive
kubectl create -f ./azure-voting-app-redis/kubernetes-manifests/azure-vote-all-in-one-redis.yml
```

<span data-ttu-id="7ed40-130">Dane wyjściowe:</span><span class="sxs-lookup"><span data-stu-id="7ed40-130">Output:</span></span>

```bash
deployment "azure-vote-back" created
service "azure-vote-back" created
deployment "azure-vote-front" created
service "azure-vote-front" created
```

## <a name="test-application"></a><span data-ttu-id="7ed40-131">Testowanie aplikacji</span><span class="sxs-lookup"><span data-stu-id="7ed40-131">Test application</span></span>

<span data-ttu-id="7ed40-132">A [usługi Kubernetes](https://kubernetes.io/docs/concepts/services-networking/service/) jest tworzony, który udostępnia aplikacji w Internecie.</span><span class="sxs-lookup"><span data-stu-id="7ed40-132">A [Kubernetes service](https://kubernetes.io/docs/concepts/services-networking/service/) is created which exposes the application to the internet.</span></span> <span data-ttu-id="7ed40-133">Może to potrwać kilka minut.</span><span class="sxs-lookup"><span data-stu-id="7ed40-133">This process can take a few minutes.</span></span> 

<span data-ttu-id="7ed40-134">Aby monitorować postęp, użyj polecenia [kubectl get-service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) z argumentem `--watch`.</span><span class="sxs-lookup"><span data-stu-id="7ed40-134">To monitor progress, use the [kubectl get service](https://review.docs.microsoft.com/en-us/azure/container-service/container-service-kubernetes-walkthrough?branch=pr-en-us-17681) command with the `--watch` argument.</span></span>

```azurecli-interactive
kubectl get service azure-vote-front --watch
```

<span data-ttu-id="7ed40-135">Początkowo **IP zewnętrznego** dla *azure głos początku* usługi pojawia się jako *oczekujące*.</span><span class="sxs-lookup"><span data-stu-id="7ed40-135">Initially, the **EXTERNAL-IP** for the *azure-vote-front* service appears as *pending*.</span></span> <span data-ttu-id="7ed40-136">Po zmianie adresu EXTERNAL-IP z *oczekującego* na *adres IP*, użyj polecenia `CTRL-C`, aby zatrzymać proces śledzenia narzędzia kubectl.</span><span class="sxs-lookup"><span data-stu-id="7ed40-136">Once the EXTERNAL-IP address has changed from *pending* to an *IP address*, use `CTRL-C` to stop the kubectl watch process.</span></span>

```bash
NAME               CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
azure-vote-front   10.0.42.158   <pending>     80:31873/TCP   1m
azure-vote-front   10.0.42.158   52.179.23.131 80:31873/TCP   2m
```

<span data-ttu-id="7ed40-137">Aby wyświetlić aplikację, przejdź do zewnętrznego adresu IP.</span><span class="sxs-lookup"><span data-stu-id="7ed40-137">To see the application, browse to the external IP address.</span></span>

![Obraz przedstawiający klaster Kubernetes na platformie Azure](media/container-service-kubernetes-tutorials/azure-vote.png)

## <a name="next-steps"></a><span data-ttu-id="7ed40-139">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="7ed40-139">Next steps</span></span>

<span data-ttu-id="7ed40-140">W tym samouczku aplikacji Azure głos został wdrożony do klastra Kubernetes usługi kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="7ed40-140">In this tutorial, the Azure vote application was deployed to an Azure Container Service Kubernetes cluster.</span></span> <span data-ttu-id="7ed40-141">Zadania ukończone obejmują:</span><span class="sxs-lookup"><span data-stu-id="7ed40-141">Tasks completed include:</span></span>  

> [!div class="checklist"]
> * <span data-ttu-id="7ed40-142">Pobierz pliki manifestu Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7ed40-142">Download Kubernetes manifest files</span></span>
> * <span data-ttu-id="7ed40-143">Uruchom aplikację w Kubernetes</span><span class="sxs-lookup"><span data-stu-id="7ed40-143">Run the application in Kubernetes</span></span>
> * <span data-ttu-id="7ed40-144">Przetestowane aplikacji</span><span class="sxs-lookup"><span data-stu-id="7ed40-144">Tested the application</span></span>

<span data-ttu-id="7ed40-145">Przejdź do następnego samouczka, aby dowiedzieć się więcej na temat skalowania aplikacji Kubernetes jak podstawowej infrastruktury Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="7ed40-145">Advance to the next tutorial to learn about scaling both a Kubernetes application and the underlying Kubernetes infrastructure.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ed40-146">Skala Kubernetes aplikacji i infrastruktury</span><span class="sxs-lookup"><span data-stu-id="7ed40-146">Scale Kubernetes application and infrastructure</span></span>](./container-service-tutorial-kubernetes-scale.md)