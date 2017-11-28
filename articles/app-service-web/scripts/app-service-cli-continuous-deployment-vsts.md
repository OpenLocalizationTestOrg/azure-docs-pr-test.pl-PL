---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od Visual Studio Team Services | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od Visual Studio Team Services"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 389d3bd3-cd8e-4715-a3a1-031ec061d385
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: f8d0c2645ec5311296ca9b2df20f97e77bab2283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="cca08-103">Tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="cca08-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="cca08-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie konfiguruje ciągłego wdrażania od repozytorium programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="cca08-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="cca08-105">Dla tego przykładu potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="cca08-105">For this sample, you will need:</span></span>

* <span data-ttu-id="cca08-106">Repozytorium programu Visual Studio Team Services z kodu aplikacji, które ma uprawnienia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="cca08-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="cca08-107">A [osobistych dostępu tokenu (PAWEŁ)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) dla Twojego konta Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="cca08-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="cca08-108">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="cca08-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="cca08-109">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="cca08-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="cca08-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="cca08-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="cca08-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="cca08-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="cca08-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="cca08-112">Script explanation</span></span>

<span data-ttu-id="cca08-113">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="cca08-113">This script uses hello following commands.</span></span> <span data-ttu-id="cca08-114">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="cca08-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="cca08-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="cca08-115">Command</span></span> | <span data-ttu-id="cca08-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="cca08-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="cca08-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="cca08-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="cca08-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="cca08-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="cca08-119">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="cca08-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="cca08-120">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="cca08-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="cca08-121">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="cca08-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="cca08-122">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="cca08-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="cca08-123">AZ aplikacji sieci Web wdrożenia źródło konfiguracji</span><span class="sxs-lookup"><span data-stu-id="cca08-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="cca08-124">Kojarzy aplikacji sieci web platformy Azure z repozytorium Git lub Mercurial.</span><span class="sxs-lookup"><span data-stu-id="cca08-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="cca08-125">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="cca08-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="cca08-126">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="cca08-126">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cca08-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="cca08-127">Next steps</span></span>

<span data-ttu-id="cca08-128">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="cca08-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="cca08-129">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cca08-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
