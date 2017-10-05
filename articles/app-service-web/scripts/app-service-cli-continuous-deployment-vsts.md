---
title: "Azure CLI skrypt przykładowy — tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od Visual Studio Team Services | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 2b983616757ca3c4226c12876f5fd4c285067318
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-visual-studio-team-services"></a><span data-ttu-id="6b716-103">Tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="6b716-103">Create a web app with continuous deployment from Visual Studio Team Services</span></span>

<span data-ttu-id="6b716-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie konfiguruje ciągłego wdrażania od repozytorium programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6b716-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a Visual Studio Team Services repository.</span></span> <span data-ttu-id="6b716-105">Dla tego przykładu potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="6b716-105">For this sample, you will need:</span></span>

* <span data-ttu-id="6b716-106">Repozytorium programu Visual Studio Team Services z kodu aplikacji, które ma uprawnienia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="6b716-106">A Visual Studio Team Services repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="6b716-107">A [osobistych dostępu tokenu (PAWEŁ)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) dla Twojego konta Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="6b716-107">A [Personal Access Token (PAT)](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) for your Visual Studio Team Services account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6b716-108">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6b716-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6b716-109">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="6b716-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="6b716-110">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6b716-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6b716-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="6b716-111">Sample script</span></span>

<span data-ttu-id="6b716-112">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "utworzenia aplikacji sieci web z ciągłego wdrażania od Visual Studio Team Services")]</span><span class="sxs-lookup"><span data-stu-id="6b716-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-vsts-continuous/deploy-vsts-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from Visual Studio Team Services")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6b716-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="6b716-113">Script explanation</span></span>

<span data-ttu-id="6b716-114">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="6b716-114">This script uses the following commands.</span></span> <span data-ttu-id="6b716-115">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="6b716-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6b716-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="6b716-116">Command</span></span> | <span data-ttu-id="6b716-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6b716-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6b716-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="6b716-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6b716-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="6b716-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6b716-120">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="6b716-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6b716-121">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="6b716-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6b716-122">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="6b716-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6b716-123">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6b716-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6b716-124">AZ aplikacji sieci Web wdrożenia źródło konfiguracji</span><span class="sxs-lookup"><span data-stu-id="6b716-124">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="6b716-125">Kojarzy aplikacji sieci web platformy Azure z repozytorium Git lub Mercurial.</span><span class="sxs-lookup"><span data-stu-id="6b716-125">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="6b716-126">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="6b716-126">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="6b716-127">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="6b716-127">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6b716-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6b716-128">Next steps</span></span>

<span data-ttu-id="6b716-129">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6b716-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6b716-130">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6b716-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
