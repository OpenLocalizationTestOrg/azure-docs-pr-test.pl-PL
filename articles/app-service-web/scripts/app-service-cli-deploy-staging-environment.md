---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie aplikacji sieci web i wdrażanie tooa kodu tymczasowej środowiska | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt interfejsu wiersza polecenia Azure — tworzenie aplikacji sieci web i wdrażanie tooa kodu tymczasowej środowiska"
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
ms.openlocfilehash: cd07f5eda31041effd7b7334f5ecc04e6c1a0514
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-tooa-staging-environment"></a><span data-ttu-id="ab57b-103">Tworzenie aplikacji sieci web i wdrażanie tooa kodu tymczasowej środowiska</span><span class="sxs-lookup"><span data-stu-id="ab57b-103">Create a web app and deploy code tooa staging environment</span></span>

<span data-ttu-id="ab57b-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z gniazdem dodatkowe wdrożenia o nazwie "tymczasowe", a następnie wdraża toohello aplikacji przykładowej, "staging" miejsca.</span><span class="sxs-lookup"><span data-stu-id="ab57b-104">This sample script creates a web app in App Service with an additional deployment slot called "staging", and then deploys a sample app toohello "staging" slot.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ab57b-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="ab57b-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ab57b-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="ab57b-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="ab57b-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ab57b-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="ab57b-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="ab57b-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-deployment-slot/deploy-deployment-slot.sh "Create a web app and deploy code tooa staging environment")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="ab57b-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="ab57b-109">Script explanation</span></span>

<span data-ttu-id="ab57b-110">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="ab57b-110">This script uses hello following commands.</span></span> <span data-ttu-id="ab57b-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="ab57b-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ab57b-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="ab57b-112">Command</span></span> | <span data-ttu-id="ab57b-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="ab57b-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ab57b-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="ab57b-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ab57b-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="ab57b-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ab57b-116">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="ab57b-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="ab57b-117">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="ab57b-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="ab57b-118">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="ab57b-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="ab57b-119">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="ab57b-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="ab57b-120">Tworzenie miejsca wdrożenia aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="ab57b-120">az webapp deployment slot create</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#create) | <span data-ttu-id="ab57b-121">Tworzenie miejsca wdrożenia.</span><span class="sxs-lookup"><span data-stu-id="ab57b-121">Create a deployment slot.</span></span> |
| [<span data-ttu-id="ab57b-122">AZ aplikacji sieci Web wdrożenia źródło konfiguracji</span><span class="sxs-lookup"><span data-stu-id="ab57b-122">az webapp deployment source config</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/source#config) | <span data-ttu-id="ab57b-123">Kojarzy aplikacji sieci web platformy Azure z repozytorium Git lub Mercurial.</span><span class="sxs-lookup"><span data-stu-id="ab57b-123">Associates an Azure web app with a Git or Mercurial repository.</span></span> |
| [<span data-ttu-id="ab57b-124">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="ab57b-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="ab57b-125">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="ab57b-125">Open an Azure web app in a browser.</span></span> |
| [<span data-ttu-id="ab57b-126">wymiany gniazd wdrożenia aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="ab57b-126">az webapp deployment slot swap</span></span>](https://docs.microsoft.com/cli/azure/webapp/deployment/slot#swap) | <span data-ttu-id="ab57b-127">Zamień miejsce wdrożenia do środowiska produkcyjnego.</span><span class="sxs-lookup"><span data-stu-id="ab57b-127">Swap a specified deployment slot into production.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ab57b-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="ab57b-128">Next steps</span></span>

<span data-ttu-id="ab57b-129">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ab57b-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ab57b-130">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="ab57b-130">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
