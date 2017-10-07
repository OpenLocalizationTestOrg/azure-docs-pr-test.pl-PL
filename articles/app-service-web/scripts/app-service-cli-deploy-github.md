---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie aplikacji sieci web z wdrożeniem z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie aplikacji sieci web z wdrożeniem z usługi GitHub"
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
ms.tgt_pltfrm: sample
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: eb7231aa5c6a7e23d76885107e733008382f7487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="9d49b-103">Tworzenie aplikacji sieci web z wdrożeniem z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="9d49b-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="9d49b-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web z publicznego repozytorium GitHub (bez ciągłego wdrażania).</span><span class="sxs-lookup"><span data-stu-id="9d49b-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="9d49b-105">Do wdrożenia usługi GitHub z ciągłego wdrażania, zobacz [utworzenia aplikacji sieci web z ciągłego wdrażania od GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="9d49b-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9d49b-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9d49b-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9d49b-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="9d49b-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="9d49b-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9d49b-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9d49b-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9d49b-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9d49b-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9d49b-110">Script explanation</span></span> 

<span data-ttu-id="9d49b-111">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="9d49b-111">This script uses hello following commands.</span></span> <span data-ttu-id="9d49b-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="9d49b-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9d49b-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9d49b-113">Command</span></span> | <span data-ttu-id="9d49b-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9d49b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9d49b-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="9d49b-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9d49b-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9d49b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9d49b-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="9d49b-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9d49b-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="9d49b-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9d49b-119">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="9d49b-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="9d49b-120">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9d49b-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="9d49b-121">AZ aplikacji sieci Web wdrożenia źródło konfiguracji</span><span class="sxs-lookup"><span data-stu-id="9d49b-121">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="9d49b-122">Kojarzy aplikacji sieci web platformy Azure z repozytorium Git lub Mercurial.</span><span class="sxs-lookup"><span data-stu-id="9d49b-122">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="9d49b-123">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="9d49b-123">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="9d49b-124">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="9d49b-124">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9d49b-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9d49b-125">Next steps</span></span>

<span data-ttu-id="9d49b-126">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9d49b-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9d49b-127">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9d49b-127">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
