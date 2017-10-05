---
title: "Przykładowy skrypt interfejsu wiersza polecenia Azure — tworzenie aplikacji sieci web i wdrażanie kodu tymczasowej środowiska | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt interfejsu wiersza polecenia Azure — tworzenie aplikacji sieci web i wdrażania kodu w środowisku przemieszczania"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 2b995dcd-e471-4355-9fda-00babcdb156e
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d586b50258c32e44f55859aad0a89475e9e4d2eb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-web-app-and-deploy-code-to-a-staging-environment"></a><span data-ttu-id="a838c-103">Tworzenie aplikacji sieci web i wdrażanie kodu w środowisku przemieszczania</span><span class="sxs-lookup"><span data-stu-id="a838c-103">Create a web app and deploy code to a staging environment</span></span>

<span data-ttu-id="a838c-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z gniazdem dodatkowe wdrożenia o nazwie "tymczasowe", a następnie wdraża przykładową aplikację do miejsca "tymczasowe".</span><span class="sxs-lookup"><span data-stu-id="a838c-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app to the "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a838c-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="a838c-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="a838c-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="a838c-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="a838c-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a838c-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="a838c-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="a838c-108">Sample script</span></span>

<span data-ttu-id="a838c-109">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "tworzenie aplikacji sieci web i wdrażanie kodu w środowisku przemieszczania")]</span><span class="sxs-lookup"><span data-stu-id="a838c-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code to a staging environment")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="a838c-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="a838c-110">Script explanation</span></span>

<span data-ttu-id="a838c-111">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="a838c-111">This script uses the following commands.</span></span> <span data-ttu-id="a838c-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="a838c-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a838c-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="a838c-113">Command</span></span> | <span data-ttu-id="a838c-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="a838c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a838c-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="a838c-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a838c-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="a838c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a838c-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="a838c-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="a838c-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="a838c-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="a838c-119">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="a838c-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="a838c-120">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="a838c-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="a838c-121">Tworzenie miejsca wdrożenia aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="a838c-121">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="a838c-122">Tworzenie miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="a838c-122">Create a deployment slot.</span></span> |
| [<span data-ttu-id="a838c-123">AZ aplikacji sieci Web wdrożenia źródło konfiguracji</span><span class="sxs-lookup"><span data-stu-id="a838c-123">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="a838c-124">Kojarzy aplikacji sieci web platformy Azure z repozytorium Git lub Mercurial.</span><span class="sxs-lookup"><span data-stu-id="a838c-124">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="a838c-125">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="a838c-125">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="a838c-126">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="a838c-126">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="a838c-127">wymiany gniazd wdrożenia aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="a838c-127">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="a838c-128">Zamień miejsce wdrożenia do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="a838c-128">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a838c-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="a838c-129">Next steps</span></span>

<span data-ttu-id="a838c-130">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a838c-130">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a838c-131">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a838c-131">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
