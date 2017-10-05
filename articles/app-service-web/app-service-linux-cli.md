---
title: "Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu wiersza polecenia platformy Azure."
keywords: "Usługa aplikacji Azure, aplikacji sieci web, interfejsu wiersza polecenia, linux, oss"
services: app-service
documentationCenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: 
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: aelnably
ms.openlocfilehash: 04aceecf0cb4cad5c838b7254bf7079a36bbd0d8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="6f082-104">Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6f082-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="6f082-105">Za pomocą poleceń w tym artykule jest możliwe tworzenie i zarządzanie nimi w aplikacji sieci Web w systemie Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f082-105">Using the commands in this article you are able to create and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="6f082-106">Można uruchomić przy użyciu nowej wersji interfejsu wiersza polecenia na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="6f082-106">You can start using the new version of the CLI in two ways:</span></span>

* <span data-ttu-id="6f082-107">[Instalowanie Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="6f082-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="6f082-108">Przy użyciu [powłoki chmury Azure (wersja zapoznawcza)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="6f082-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="6f082-109">Tworzenie planu usługi aplikacji w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6f082-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="6f082-110">Aby utworzyć Plan usługi aplikacji systemu Linux, służy następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f082-110">To create a Linux App Service Plan, you can use the following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="6f082-111">Tworzenie niestandardowych kontenera Docker aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="6f082-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="6f082-112">Aby utworzyć aplikację sieci web i konfigurowanie go uruchomić niestandardowego kontenera Docker, służy następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f082-112">To create a web app and configuring it to run a custom Docker container, you can use the following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-the-docker-container-logging"></a><span data-ttu-id="6f082-113">Aktywacja rejestrowania kontenera Docker</span><span class="sxs-lookup"><span data-stu-id="6f082-113">Activate the Docker container logging</span></span>

<span data-ttu-id="6f082-114">Aby aktywować rejestrowania kontenera Docker, służy następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f082-114">To activate the Docker container logging, you can use the following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-the-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="6f082-115">Zmiana niestandardowych kontenera Docker istniejącą aplikację sieci Web w aplikacji dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="6f082-115">Change the custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="6f082-116">Aby zmienić utworzonej wcześniej aplikacji, z bieżącego obrazu Docker do nowego obrazu, można użyć następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f082-116">To change a previously created app, from the current Docker image to a new image, you can use the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="6f082-117">Przy użyciu obrazy usługi Docker z rejestru prywatnych</span><span class="sxs-lookup"><span data-stu-id="6f082-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="6f082-118">Możesz skonfigurować aplikację, aby używać obrazów z rejestru prywatnych.</span><span class="sxs-lookup"><span data-stu-id="6f082-118">You can configure your app to use images from a private registry.</span></span> <span data-ttu-id="6f082-119">Musisz podać adres url do rejestru, nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="6f082-119">You need to provide the url for your registry, user name, and password.</span></span> <span data-ttu-id="6f082-120">Można to osiągnąć przy użyciu następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f082-120">This can be achieved using the following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="6f082-121">Włącz ciągłego wdrożenia niestandardowe obrazy usługi Docker</span><span class="sxs-lookup"><span data-stu-id="6f082-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="6f082-122">Za pomocą następującego polecenia można włączyć funkcję CD i uzyskać adres url elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="6f082-122">With the following command you can enable the CD functionality, and get the webhook url.</span></span> <span data-ttu-id="6f082-123">Ten adres url, można skonfigurować repozytoriów DockerHub lub rejestru kontenera platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f082-123">This url can be used to configure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="6f082-124">Tworzenie aplikacji sieci Web w aplikacji systemu Linux przy użyciu jednej z naszych struktur wbudowanych środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="6f082-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="6f082-125">Aby utworzyć aplikację sieci Web 5.6 PHP w systemie Linux aplikacji który, służy następujące polecenie.</span><span class="sxs-lookup"><span data-stu-id="6f082-125">To create a PHP 5.6 Web App on Linux App that, you can use the following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="6f082-126">Zmień wersję framework dla istniejącej aplikacji sieci Web w aplikacji dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="6f082-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="6f082-127">Aby zmienić utworzonej wcześniej aplikacji, z bieżącej wersji framework do Node.js 6.11, można użyć następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="6f082-127">To change a previously created app, from the current framework version to Node.js 6.11, you can use the following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="6f082-128">Konfigurowanie wdrożenia Git dla aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="6f082-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="6f082-129">Aby skonfigurować wdrożenia Git dla aplikacji, służy następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="6f082-129">To set up Git deployments for your app, you can use the following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="6f082-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f082-130">Next steps</span></span>
* [<span data-ttu-id="6f082-131">Co to jest aplikacja sieci Web Azure w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="6f082-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="6f082-132">Zainstaluj interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6f082-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="6f082-133">Powłoka chmury Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="6f082-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="6f082-134">Konfigurowanie środowisk w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="6f082-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="6f082-135">Ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6f082-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
