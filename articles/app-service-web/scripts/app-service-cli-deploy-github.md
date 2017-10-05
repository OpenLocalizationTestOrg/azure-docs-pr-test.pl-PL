---
title: "Azure CLI skrypt przykładowy — tworzenie aplikacji sieci web z wdrożeniem z serwisu GitHub | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 61e9d65319cecf3ea4e9152ebdf1035566aad74c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-web-app-with-deployment-from-github"></a><span data-ttu-id="23fe3-103">Tworzenie aplikacji sieci web z wdrożeniem z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="23fe3-103">Create a web app with deployment from GitHub</span></span>

<span data-ttu-id="23fe3-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web z publicznego repozytorium GitHub (bez ciągłego wdrażania).</span><span class="sxs-lookup"><span data-stu-id="23fe3-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="23fe3-105">Do wdrożenia usługi GitHub z ciągłego wdrażania, zobacz [utworzenia aplikacji sieci web z ciągłego wdrażania od GitHub](app-service-cli-continuous-deployment-github.md).</span><span class="sxs-lookup"><span data-stu-id="23fe3-105">For GitHub deployment with continuous deployment, see [Create a web app with continuous deployment from GitHub](app-service-cli-continuous-deployment-github.md).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="23fe3-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="23fe3-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="23fe3-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="23fe3-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="23fe3-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="23fe3-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="23fe3-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="23fe3-109">Sample script</span></span>

<span data-ttu-id="23fe3-110">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "utworzenia aplikacji sieci web z wdrożeniem z usługi GitHub")]</span><span class="sxs-lookup"><span data-stu-id="23fe3-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github/deploy-github.sh?highlight=3 "Create a web app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="23fe3-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="23fe3-111">Script explanation</span></span> 

<span data-ttu-id="23fe3-112">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="23fe3-112">This script uses the following commands.</span></span> <span data-ttu-id="23fe3-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="23fe3-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="23fe3-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="23fe3-114">Command</span></span> | <span data-ttu-id="23fe3-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="23fe3-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="23fe3-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="23fe3-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="23fe3-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="23fe3-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="23fe3-118">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="23fe3-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="23fe3-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="23fe3-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="23fe3-120">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="23fe3-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="23fe3-121">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="23fe3-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="23fe3-122">AZ aplikacji sieci Web wdrożenia źródło konfiguracji</span><span class="sxs-lookup"><span data-stu-id="23fe3-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="23fe3-123">Kojarzy aplikacji sieci web platformy Azure z repozytorium Git lub Mercurial.</span><span class="sxs-lookup"><span data-stu-id="23fe3-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="23fe3-124">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="23fe3-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="23fe3-125">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="23fe3-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="23fe3-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="23fe3-126">Next steps</span></span>

<span data-ttu-id="23fe3-127">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="23fe3-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="23fe3-128">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="23fe3-128">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
