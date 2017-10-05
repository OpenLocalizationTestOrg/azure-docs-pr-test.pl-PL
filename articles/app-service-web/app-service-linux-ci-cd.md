---
title: "Ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux | Dokumentacja firmy Microsoft"
description: "Jak skonfigurować ciągłe wdrażanie w aplikacji sieci Web platformy Azure w systemie Linux."
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
ms.openlocfilehash: f8f7d51003f8a55b7f51e8cc2cea838e8e5a6196
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="continuous-deployment-with-azure-web-app-on-linux"></a><span data-ttu-id="6c8dc-104">Ciągłe wdrażanie z aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6c8dc-104">Continuous deployment with Azure Web App on Linux</span></span>

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="6c8dc-105">W tym samouczku, skonfiguruj ciągłe wdrażanie dla kontenera niestandardowego obrazu z zarządzanego [rejestru kontenera Azure](https://azure.microsoft.com/en-us/services/container-registry/) repozytoria lub [Centrum Docker](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="6c8dc-105">In this tutorial, you configure continuous deployment for a custom container image from Managed [Azure Container Registry](https://azure.microsoft.com/en-us/services/container-registry/) repositories or [Docker Hub](https://hub.docker.com).</span></span>

## <a name="step-1---sign-in-to-azure"></a><span data-ttu-id="6c8dc-106">Krok 1 — znak w na platformie Azure</span><span class="sxs-lookup"><span data-stu-id="6c8dc-106">Step 1 - Sign in to Azure</span></span>

<span data-ttu-id="6c8dc-107">Zaloguj się do portalu Azure pod adresem http://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="6c8dc-107">Sign in to the Azure portal at http://portal.azure.com</span></span>

## <a name="step-2---enable-container-continuous-deployment-feature"></a><span data-ttu-id="6c8dc-108">Krok 2 — Włączanie kontenera ciągłe wdrażanie funkcji</span><span class="sxs-lookup"><span data-stu-id="6c8dc-108">Step 2 - Enable container continuous deployment feature</span></span>

<span data-ttu-id="6c8dc-109">Można włączyć za pomocą funkcji ciągłego wdrażania [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) i wykonując następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="6c8dc-109">You can enable the continuous deployment feature using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container config -n sname -g rgname -e true
``` 

<span data-ttu-id="6c8dc-110">W  **[portalu Azure](https://portal.azure.com/)**, kliknij przycisk **usługi aplikacji** opcję z lewej strony.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-110">In the **[Azure portal](https://portal.azure.com/)**, click the **App Service** option on the left of the page.</span></span>

<span data-ttu-id="6c8dc-111">Kliknij nazwę aplikacji, który chcesz skonfigurować wdrożenie ciągłe Centrum Docker.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-111">Click on the name of your app that you want to configure Docker Hub continuous deployment for.</span></span>

<span data-ttu-id="6c8dc-112">W **ustawień aplikacji**, dodaj aplikację nosi nazwę `DOCKER_ENABLE_CI` z wartością `true`.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-112">In the **App settings**, add an app setting called `DOCKER_ENABLE_CI` with the value `true`.</span></span>

![Wstaw obraz ustawienia aplikacji](./media/app-service-webapp-service-linux-ci-cd/step2.png)

## <a name="step-3---prepare-webhook-url"></a><span data-ttu-id="6c8dc-114">Krok 3 — Przygotowanie adresu URL elementu Webhook</span><span class="sxs-lookup"><span data-stu-id="6c8dc-114">Step 3 - Prepare Webhook URL</span></span>

<span data-ttu-id="6c8dc-115">Można uzyskać przy użyciu adresu URL elementu Webhook [interfejsu wiersza polecenia Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) i wykonując następujące polecenie</span><span class="sxs-lookup"><span data-stu-id="6c8dc-115">You can obtain the Webhook URL using [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) and executing the following command</span></span>

```azurecli-interactive
az webapp deployment container -n sname1 -g rgname -e true --show-cd-url
``` 

<span data-ttu-id="6c8dc-116">Adres URL elementu Webhook, musisz mieć następujący punkt końcowy: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-116">For the Webhook URL, you need to have the following endpoint: `https://<publishingusername>:<publishingpwd>@<sitename>.scm.azurewebsites.net/docker/hook`.</span></span>

<span data-ttu-id="6c8dc-117">Można uzyskać z `publishingusername` i `publishingpwd` pobierając aplikacji sieci web Publikowanie profilu przy użyciu portalu Azure.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-117">You can obtain your `publishingusername` and `publishingpwd` by downloading the web app publish profile using the Azure portal.</span></span>

![Wstaw obraz dodawania elementu webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-3.png)

## <a name="step-4---add-a-web-hook"></a><span data-ttu-id="6c8dc-119">Krok 4 — Dodaj haku sieci web</span><span class="sxs-lookup"><span data-stu-id="6c8dc-119">Step 4 - Add a web hook</span></span>

### <a name="azure-container-registry"></a><span data-ttu-id="6c8dc-120">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="6c8dc-120">Azure Container Registry</span></span>

<span data-ttu-id="6c8dc-121">W bloku portalu rejestru, kliknij **elementów Webhook**, Utwórz nowy element webhook, klikając **Dodaj**.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-121">In your registry portal blade, click **Webhooks**, create a new webhook by clicking **Add**.</span></span> <span data-ttu-id="6c8dc-122">W **tworzenia elementu webhook** bloku, nazwę użytkownika elementu webhook.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-122">In the **Create webhook** blade, give your webhook a name.</span></span> <span data-ttu-id="6c8dc-123">Dla identyfikatora URI elementu Webhook, musisz podać adres URL uzyskane z **krok 3**</span><span class="sxs-lookup"><span data-stu-id="6c8dc-123">For the Webhook URI, you need to provide the URL obtained from **Step 3**</span></span>

<span data-ttu-id="6c8dc-124">Upewnij się, zdefiniuj zakres jako repozytorium, który zawiera obraz kontenera.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-124">Make sure that you define the scope as the repo that contains your container image.</span></span>

![Wstaw obraz elementu webhook](./media/app-service-webapp-service-linux-ci-cd/step3ACRWebhook-1.png)

<span data-ttu-id="6c8dc-126">Gdy obraz zostanie zaktualizowany, aplikacji sieci web aktualizowany automatycznie z nowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-126">When the image gets updated, the web app get updated automatically with the new image.</span></span>

### <a name="docker-hub"></a><span data-ttu-id="6c8dc-127">Centrum docker</span><span class="sxs-lookup"><span data-stu-id="6c8dc-127">Docker Hub</span></span>

<span data-ttu-id="6c8dc-128">Na stronie Centrum Docker kliknij **elementów Webhook**, następnie **tworzenia elementu WEBHOOK A**.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-128">In your Docker Hub page, click **Webhooks**, then **CREATE A WEBHOOK**.</span></span>

![Wstaw obraz dodawania elementu webhook 1](./media/app-service-webapp-service-linux-ci-cd/step3-1.png)

<span data-ttu-id="6c8dc-130">Dla adresu URL elementu Webhook, musisz podać adres URL uzyskane z **krok 3**</span><span class="sxs-lookup"><span data-stu-id="6c8dc-130">For the Webhook URL, you need to provide the URL obtained from **Step 3**</span></span>

![Wstaw obraz dodawania elementu webhook 2](./media/app-service-webapp-service-linux-ci-cd/step3-2.png)

<span data-ttu-id="6c8dc-132">Gdy obraz zostanie zaktualizowany, aplikacji sieci web aktualizowany automatycznie z nowego obrazu.</span><span class="sxs-lookup"><span data-stu-id="6c8dc-132">When the image gets updated, the web app get updated automatically with the new image.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6c8dc-133">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6c8dc-133">Next steps</span></span>
* [<span data-ttu-id="6c8dc-134">Co to jest aplikacja sieci Web Azure w systemie Linux?</span><span class="sxs-lookup"><span data-stu-id="6c8dc-134">What is Azure Web App on Linux?</span></span>](./app-service-linux-intro.md)
* [<span data-ttu-id="6c8dc-135">Rejestru kontenera platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6c8dc-135">Azure Container Registry</span></span>](https://azure.microsoft.com/en-us/services/container-registry/)
* [<span data-ttu-id="6c8dc-136">Za pomocą konfiguracji PM2 dla środowiska Node.js w aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6c8dc-136">Using PM2 Configuration for Node.js in Azure Web App on Linux</span></span>](app-service-linux-using-nodejs-pm2.md)
* [<span data-ttu-id="6c8dc-137">W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu platformy .NET Core</span><span class="sxs-lookup"><span data-stu-id="6c8dc-137">Using .NET Core in Azure Web App on Linux</span></span>](app-service-linux-using-dotnetcore.md)
* [<span data-ttu-id="6c8dc-138">W aplikacji sieci Web platformy Azure w systemie Linux przy użyciu Ruby</span><span class="sxs-lookup"><span data-stu-id="6c8dc-138">Using Ruby in Azure Web App on Linux</span></span>](app-service-linux-ruby-get-started.md)
* [<span data-ttu-id="6c8dc-139">Sposób użycia niestandardowego obrazu Docker dla aplikacji sieci Web platformy Azure w systemie Linux</span><span class="sxs-lookup"><span data-stu-id="6c8dc-139">How to use a custom Docker image for Azure Web App on Linux</span></span>](./app-service-linux-using-custom-docker-image.md)
* [<span data-ttu-id="6c8dc-140">Usługa aplikacji Azure aplikacji sieci Web w systemie Linux — często zadawane pytania</span><span class="sxs-lookup"><span data-stu-id="6c8dc-140">Azure App Service Web App on Linux FAQ</span></span>](./app-service-linux-faq.md) 
* [<span data-ttu-id="6c8dc-141">Zarządzanie aplikacją sieci Web w systemie Linux przy użyciu usługi Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6c8dc-141">Manage Web App on Linux using Azure CLI 2.0</span></span>](./app-service-linux-cli.md)



