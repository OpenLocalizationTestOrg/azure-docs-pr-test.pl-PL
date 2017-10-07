---
title: "aaaContinuous wdrożenie z aplikacji sieci Web platformy Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Jak toosetup ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux."
keywords: "Usługa aplikacji Azure, linux, oss, acr"
services: app-service
documentationcenter: 
author: ahmedelnably
manager: erikre
editor: 
ms.assetid: a47fb43a-bbbd-4751-bdc1-cd382eae49f8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: aelnably;wesmc
ms.openlocfilehash: f94d837e27605da58428f507ab2b0eb3af3297e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="c7b76-104">Ciągłe wdrażanie z aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="c7b76-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="c7b76-105">W tym samouczku, skonfiguruj ciągłe wdrażanie dla kontenera niestandardowego obrazu z zarządzanego [rejestru kontenera Azure](https://azure.microsoft.com/en-us/services/container-registry/) repozytoria lub [Centrum Docker](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="c7b76-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-tooazure"></a><span data-ttu-id="c7b76-106">Krok 1 — Logowanie tooAzure</span><span class="sxs-lookup"><span data-stu-id="c7b76-106">Step 1 - Sign in tooAzure</span></span>

<span data-ttu-id="c7b76-107">Zaloguj się toohello portalu Azure w http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="c7b76-107">Sign in toohello Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="c7b76-108">Krok 2 — Włączanie kontenera ciągłe wdrażanie funkcji</span><span class="sxs-lookup"><span data-stu-id="c7b76-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="c7b76-109">Można włączyć za pomocą funkcji ciągłego wdrażania hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) i wykonywania hello następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="c7b76-109">You can enable hello continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="c7b76-110">W hello ** [portalu Azure](https://portal.azure.com/)**, kliknij przycisk hello **usługi aplikacji** opcję na powitania po lewej stronie hello.</span><span class="sxs-lookup"><span data-stu-id="c7b76-110">In hello **[Azure portal](https://portal.azure.com/)**, click hello **App Service** option on hello left of hello page.</span></span>

<span data-ttu-id="c7b76-111">Kliknij nazwę hello interesujące tooconfigure Centrum Docker ciągłe wdrażanie dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="c7b76-111">Click on hello name of your app that you want tooconfigure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="c7b76-112">W hello **ustawień aplikacji**, dodaj aplikację nosi nazwę `DOCKER_ENABLE_CI` z wartością hello `true`.</span><span class="sxs-lookup"><span data-stu-id="c7b76-112">In hello **App settings**, add an app setting called `DOCKER_ENABLE_CI` with hello value `true`.</span></span>

![Wstaw obraz ustawienia aplikacji](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="c7b76-114">Krok 3 — Przygotowanie adresu URL elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="c7b76-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="c7b76-115">Można uzyskać przy użyciu adresu URL elementu Webhook hello [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) i wykonywania hello następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="c7b76-115">You can obtain hello Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing hello following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="c7b76-116">Dla adresu URL elementu Webhook hello, potrzebujesz hello toohave następującego punktu końcowego: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="c7b76-116">For hello Webhook URL, you need toohave hello following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="c7b76-117">Można uzyskać z `publishingusername` i `publishingpwd` pobierając hello aplikacji sieci web Publikowanie profilu przy użyciu hello portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="c7b76-117">You can obtain your `publishingusername` and `publishingpwd` by downloading hello web app publish profile using hello Azure portal.</span></span>

![Wstaw obraz dodawania elementu webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="c7b76-119">Krok 4 — Dodaj haku sieci web</span><span class="sxs-lookup"><span data-stu-id="c7b76-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="c7b76-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c7b76-120">Azure Container Registry</span></span>

<span data-ttu-id="c7b76-121">W bloku portalu rejestru, kliknij **elementów Webhook**, Utwórz nowy element webhook, klikając **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="c7b76-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="c7b76-122">W hello **tworzenia elementu webhook** bloku, nazwę użytkownika elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="c7b76-122">In hello **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="c7b76-123">Dla hello identyfikator URI elementu Webhook, potrzebujesz adresu URL hello tooprovide uzyskane z **krok 3**</span><span class="sxs-lookup"><span data-stu-id="c7b76-123">For hello Webhook URI, you need tooprovide hello URL obtained from **Step 3**</span></span>

<span data-ttu-id="c7b76-124">Upewnij się, zdefiniuj zakres hello, jak hello repozytorium, który zawiera obraz kontenera.</span><span class="sxs-lookup"><span data-stu-id="c7b76-124">Make sure that you define hello scope as hello repo that contains your container image.</span></span>

![Wstaw obraz elementu webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="c7b76-126">Obraz powitania jest aktualizowana, hello aplikacji sieci web zostać zaktualizowane automatycznie z hello nowy obraz.</span><span class="sxs-lookup"><span data-stu-id="c7b76-126">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="c7b76-127">Centrum docker</span><span class="sxs-lookup"><span data-stu-id="c7b76-127">Docker Hub</span></span>

<span data-ttu-id="c7b76-128">Na stronie Centrum Docker kliknij **elementów Webhook**, następnie **tworzenia elementu WEBHOOK A**.</span><span class="sxs-lookup"><span data-stu-id="c7b76-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![Wstaw obraz dodawania elementu webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="c7b76-130">Dla hello adresu URL elementu Webhook, potrzebujesz adresu URL hello tooprovide uzyskane z **krok 3**</span><span class="sxs-lookup"><span data-stu-id="c7b76-130">For hello Webhook URL, you need tooprovide hello URL obtained from **Step 3**</span></span>

![Wstaw obraz dodawania elementu webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="c7b76-132">Obraz powitania jest aktualizowana, hello aplikacji sieci web zostać zaktualizowane automatycznie z hello nowy obraz.</span><span class="sxs-lookup"><span data-stu-id="c7b76-132">When hello image gets updated, hello web app get updated automatically with hello new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7b76-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="c7b76-133">Next steps</span></span>
* [<span data-ttu-id="c7b76-134">Co to jest aplikacja sieci Web Azure w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="c7b76-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="c7b76-135">Rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="c7b76-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="c7b76-136">Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="c7b76-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="c7b76-137">W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="c7b76-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="c7b76-138">W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu Ruby</span><span class="sxs-lookup"><span data-stu-id="c7b76-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="c7b76-139">Jak toouse Docker niestandardowego obrazu dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="c7b76-139">How toouse a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="c7b76-140">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="c7b76-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="c7b76-141">Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu usługi Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c7b76-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



