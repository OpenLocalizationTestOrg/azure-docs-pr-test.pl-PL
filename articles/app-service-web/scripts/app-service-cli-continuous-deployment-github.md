---
title: "Azure CLI skrypt przykładowy — tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od GitHub | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: a12085a7a8146c22d6b079381542d4fe3a8e6e87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-with-continuous-deployment-from-github"></a><span data-ttu-id="9a4ab-103">Tworzenie aplikacji sieci web w usłudze ciągłego wdrażania od GitHub</span><span class="sxs-lookup"><span data-stu-id="9a4ab-103">Create a web app with continuous deployment from GitHub</span></span>

<span data-ttu-id="9a4ab-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie konfiguruje ciągłego wdrażania od repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-104">This sample script creates a web app in App Service with its related resources, and then sets up continuous deployment from a GitHub repository.</span></span> <span data-ttu-id="9a4ab-105">GitHub wdrożenia bez ciągłego wdrażania, zobacz [tworzenie aplikacji sieci web i wdrażanie kodu z usługi GitHub](app-service-cli-deploy-github.md).</span><span class="sxs-lookup"><span data-stu-id="9a4ab-105">For GitHub deployment without continuous deployment, see [Create a web app and deploy code from GitHub](app-service-cli-deploy-github.md).</span></span> <span data-ttu-id="9a4ab-106">W tym przykładzie potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="9a4ab-106">In this sample, you will need:</span></span>

* <span data-ttu-id="9a4ab-107">Repozytorium GitHub z kodu aplikacji, które ma uprawnienia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-107">A GitHub repository with application code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="9a4ab-108">A [osobistych dostępu tokenu (PAWEŁ)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) na koncie usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-108">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9a4ab-109">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9a4ab-110">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="9a4ab-111">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9a4ab-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9a4ab-112">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9a4ab-112">Sample script</span></span>

<span data-ttu-id="9a4ab-113">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "utworzenia aplikacji sieci web z ciągłego wdrażania od GitHub")]</span><span class="sxs-lookup"><span data-stu-id="9a4ab-113">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-github-continuous/deploy-github-continuous.sh?highlight=3-4 "Create a web app with continuous deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9a4ab-114">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9a4ab-114">Script explanation</span></span>

<span data-ttu-id="9a4ab-115">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-115">This script uses the following commands.</span></span> <span data-ttu-id="9a4ab-116">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9a4ab-117">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9a4ab-117">Command</span></span> | <span data-ttu-id="9a4ab-118">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9a4ab-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9a4ab-119">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="9a4ab-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9a4ab-120">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9a4ab-121">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="9a4ab-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9a4ab-122">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9a4ab-123">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="9a4ab-123">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="9a4ab-124">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-124">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="9a4ab-125">AZ aplikacji sieci Web wdrożenia źródło konfiguracji</span><span class="sxs-lookup"><span data-stu-id="9a4ab-125">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="9a4ab-126">Kojarzy aplikacji sieci web platformy Azure z repozytorium Git lub Mercurial.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-126">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="9a4ab-127">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="9a4ab-127">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="9a4ab-128">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="9a4ab-128">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9a4ab-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9a4ab-129">Next steps</span></span>

<span data-ttu-id="9a4ab-130">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9a4ab-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9a4ab-131">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9a4ab-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
