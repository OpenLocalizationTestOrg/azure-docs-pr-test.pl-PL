---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie aplikacji sieci web z ciągłego wdrażania od GitHub | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od GitHub"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0205c991-0989-4ca3-bb41-237dcc964460
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6adb06a35ceea8ea64723c9887c25c50f046e280
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="4c7ff-103">Tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od GitHub</span><span class="sxs-lookup"><span data-stu-id="4c7ff-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="4c7ff-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie konfiguruje ciągłego wdrażania od repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="4c7ff-105">GitHub wdrożenia bez ciągłego wdrażania, zobacz [tworzenie aplikacji sieci web i wdrażanie kodu z usługi GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="4c7ff-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="4c7ff-106">W tym przykładzie potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="4c7ff-106">In this sample, you will need:</span></span>

* <span data-ttu-id="4c7ff-107">Repozytorium GitHub z kodu aplikacji, które ma uprawnienia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="4c7ff-108">A [osobistych dostępu tokenu (PAWEŁ)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) na koncie usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4c7ff-109">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4c7ff-110">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4c7ff-111">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4c7ff-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="4c7ff-112">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="4c7ff-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4c7ff-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="4c7ff-113">Script explanation</span></span>

<span data-ttu-id="4c7ff-114">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-114">This script uses hello following commands.</span></span> <span data-ttu-id="4c7ff-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4c7ff-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="4c7ff-116">Command</span></span> | <span data-ttu-id="4c7ff-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="4c7ff-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4c7ff-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="4c7ff-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4c7ff-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4c7ff-120">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="4c7ff-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="4c7ff-121">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4c7ff-122">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="4c7ff-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="4c7ff-123">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="4c7ff-124">AZ aplikacji sieci Web wdrożenia źródło konfiguracji</span><span class="sxs-lookup"><span data-stu-id="4c7ff-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="4c7ff-125">Kojarzy aplikacji sieci web platformy Azure z repozytorium Git lub Mercurial.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="4c7ff-126">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="4c7ff-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="4c7ff-127">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="4c7ff-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4c7ff-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="4c7ff-128">Next steps</span></span>

<span data-ttu-id="4c7ff-129">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4c7ff-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4c7ff-130">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4c7ff-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
