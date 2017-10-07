---
title: "aaaManage aplikacji sieci Web w systemie Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5e8e0da8a362450c56d2e87e087f77598ec874ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-web-app-on-linux-using-azure-cli"></a><span data-ttu-id="33541-104">Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu wiersza polecenia platformy Azure</span><span class="sxs-lookup"><span data-stu-id="33541-104">Manage Web App on Linux using Azure CLI</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="33541-105">Za pomocą poleceń hello w tym artykule są toocreate stanie i zarządzać aplikacji sieci Web w systemie Linux przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="33541-105">Using hello commands in this article you are able toocreate and manage a Web App on Linux using Azure CLI 2.0.</span></span>
<span data-ttu-id="33541-106">Możesz rozpocząć korzystanie z nowej wersji hello hello CLI na dwa sposoby:</span><span class="sxs-lookup"><span data-stu-id="33541-106">You can start using hello new version of hello CLI in two ways:</span></span>

* <span data-ttu-id="33541-107">[Instalowanie Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) na tym komputerze.</span><span class="sxs-lookup"><span data-stu-id="33541-107">[Installing Azure CLI 2.0](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span>
* <span data-ttu-id="33541-108">Przy użyciu [powłoki chmury Azure (wersja zapoznawcza)](../cloud-shell/overview.md)</span><span class="sxs-lookup"><span data-stu-id="33541-108">Using [Azure Cloud Shell (Preview)](../cloud-shell/overview.md)</span></span>


## <a name="create-a-linux-app-service-plan"></a><span data-ttu-id="33541-109">Tworzenie planu usługi aplikacji w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="33541-109">Create a Linux App Service Plan</span></span>

<span data-ttu-id="33541-110">toocreate Plan usługi aplikacji systemu Linux, możesz użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="33541-110">toocreate a Linux App Service Plan, you can use hello following command:</span></span>

```azurecli-interactive
az appservice plan create -n appname -g rgname --islinux -l "South Central US" --sku S1 --number-of-workers 1
``` 

## <a name="create-a-custom-docker-container-web-app"></a><span data-ttu-id="33541-111">Tworzenie niestandardowych kontenera Docker aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="33541-111">Create a custom Docker container Web App</span></span>

<span data-ttu-id="33541-112">toocreate aplikacji sieci web i skonfigurowania go toorun kontener Docker niestandardowych, można użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="33541-112">toocreate a web app and configuring it toorun a custom Docker container, you can use hello following command:</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -i elnably/dockerimagetest
```
 
## <a name="activate-hello-docker-container-logging"></a><span data-ttu-id="33541-113">Aktywacja rejestrowania kontenera Docker hello</span><span class="sxs-lookup"><span data-stu-id="33541-113">Activate hello Docker container logging</span></span>

<span data-ttu-id="33541-114">tooactivate hello rejestrowania kontenera Docker, możesz użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="33541-114">tooactivate hello Docker container logging, you can use hello following command:</span></span>

```azurecli-interactive
az webapp log config -n sname -g rgname --web-server-logging filesystem
```
 
## <a name="change-hello-custom-docker-container-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="33541-115">Zmień hello niestandardowych kontenera Docker dla istniejącej aplikacji sieci Web w aplikacji dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33541-115">Change hello custom Docker container for an existing Web App on Linux App</span></span>

<span data-ttu-id="33541-116">toochange utworzonej wcześniej aplikacji, z hello bieżącego Docker obrazu tooa nowy obraz, możesz użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="33541-116">toochange a previously created app, from hello current Docker image tooa new image, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname -g rgname -c apurvajo/mariohtml5
``` 

## <a name="using-docker-images-from-a-private-registry"></a><span data-ttu-id="33541-117">Przy użyciu obrazy usługi Docker z rejestru prywatnych</span><span class="sxs-lookup"><span data-stu-id="33541-117">Using Docker images from a private registry</span></span>

<span data-ttu-id="33541-118">Można skonfigurować obrazów toouse aplikacji z rejestru prywatnych.</span><span class="sxs-lookup"><span data-stu-id="33541-118">You can configure your app toouse images from a private registry.</span></span> <span data-ttu-id="33541-119">Adres url hello tooprovide potrzebę rejestru, nazwę użytkownika i hasło.</span><span class="sxs-lookup"><span data-stu-id="33541-119">You need tooprovide hello url for your registry, user name, and password.</span></span> <span data-ttu-id="33541-120">Można to osiągnąć przy użyciu hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="33541-120">This can be achieved using hello following command:</span></span>

```azurecli-interactive
az webapp config container set -n sname1 -g rgname -c <container name> -r <server url> -u <username> -p <password>
``` 

## <a name="enable-continuous-deployments-for-custom-docker-images"></a><span data-ttu-id="33541-121">Włącz ciągłego wdrożenia niestandardowe obrazy usługi Docker</span><span class="sxs-lookup"><span data-stu-id="33541-121">Enable continuous deployments for custom Docker images</span></span>

<span data-ttu-id="33541-122">Z hello następujące polecenia można włączyć funkcję CD hello i uzyskać adres url elementu webhook hello.</span><span class="sxs-lookup"><span data-stu-id="33541-122">With hello following command you can enable hello CD functionality, and get hello webhook url.</span></span> <span data-ttu-id="33541-123">Ten adres url może być używane tooconfigure możesz DockerHub lub rejestru kontenera Azure repozytoriów.</span><span class="sxs-lookup"><span data-stu-id="33541-123">This url can be used tooconfigure you DockerHub or Azure Container Registry repos.</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

## <a name="create-a-web-app-on-linux-app-using-one-of-our-built-in-runtime-frameworks"></a><span data-ttu-id="33541-124">Tworzenie aplikacji sieci Web w aplikacji systemu Linux przy użyciu jednej z naszych struktur wbudowanych środowiska wykonawczego</span><span class="sxs-lookup"><span data-stu-id="33541-124">Create a Web App on Linux App using one of our built-in runtime frameworks</span></span>

<span data-ttu-id="33541-125">toocreate 5.6 aplikacji sieci Web PHP na Linux aplikacji, których można używać hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="33541-125">toocreate a PHP 5.6 Web App on Linux App that, you can use hello following command.</span></span>

```azurecli-interactive
az webapp create -n sname -g rgname -p pname -r "php|5.6"
``` 

## <a name="change-framework-version-for-an-existing-web-app-on-linux-app"></a><span data-ttu-id="33541-126">Zmień wersję framework dla istniejącej aplikacji sieci Web w aplikacji dla systemu Linux</span><span class="sxs-lookup"><span data-stu-id="33541-126">Change framework version for an existing Web App on Linux App</span></span>

<span data-ttu-id="33541-127">toochange utworzonej wcześniej aplikacji, z tooNode.js hello do wersji bieżącej framework 6.11, możesz użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="33541-127">toochange a previously created app, from hello current framework version tooNode.js 6.11, you can use hello following command:</span></span>

```azurecli-interactive
az webapp config set -n sname -g rgname --linux-fx-version "node|6.11"
``` 

## <a name="set-up-git-deployments-for-your-web-app"></a><span data-ttu-id="33541-128">Konfigurowanie wdrożenia Git dla aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="33541-128">Set up Git deployments for your Web App</span></span>

<span data-ttu-id="33541-129">tooset się wdrożenia Git dla aplikacji, można użyć hello następujące polecenie:</span><span class="sxs-lookup"><span data-stu-id="33541-129">tooset up Git deployments for your app, you can use hello following command:</span></span>

```azurecli-interactive
az webapp deployment source config -n sname -g rgname --repo-url <gitrepo url> --branch <branch>
``` 


## <a name="next-steps"></a><span data-ttu-id="33541-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="33541-130">Next steps</span></span>
* [<span data-ttu-id="33541-131">Co to jest aplikacja sieci Web Azure w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="33541-131">What is Azure Web App on Linux?</span></span>](app-service-linux-intro.md)
* [<span data-ttu-id="33541-132">Zainstaluj interfejs wiersza polecenia platformy Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="33541-132">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
* [<span data-ttu-id="33541-133">Powłoka chmury Azure (wersja zapoznawcza)</span><span class="sxs-lookup"><span data-stu-id="33541-133">Azure Cloud Shell (Preview)</span></span>](../cloud-shell/overview.md)
* [<span data-ttu-id="33541-134">Konfigurowanie środowisk w usłudze Azure App Service przejściowych</span><span class="sxs-lookup"><span data-stu-id="33541-134">Set up staging environments in Azure App Service</span></span>](./web-sites-staged-publishing.md)
* [<span data-ttu-id="33541-135">Ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="33541-135">Continuous Deployment with Azure Web App on Linux</span></span>](./app-service-linux-ci-cd.md)
