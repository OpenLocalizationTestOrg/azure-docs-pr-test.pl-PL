---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt interfejsu wiersza polecenia Azure — tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a><span data-ttu-id="48951-103">Tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git</span><span class="sxs-lookup"><span data-stu-id="48951-103">Create a web app and deploy code from a local Git repository</span></span>

<span data-ttu-id="48951-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web w lokalnym repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="48951-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code in a local Git repository.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="48951-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="48951-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="48951-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="48951-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="48951-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="48951-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="48951-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="48951-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="48951-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="48951-109">Script explanation</span></span>

<span data-ttu-id="48951-110">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="48951-110">This script uses hello following commands.</span></span> <span data-ttu-id="48951-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="48951-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="48951-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="48951-112">Command</span></span> | <span data-ttu-id="48951-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="48951-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="48951-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="48951-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="48951-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="48951-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="48951-116">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="48951-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="48951-117">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="48951-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="48951-118">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="48951-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="48951-119">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="48951-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="48951-120">ustawiono użytkownika wdrożenia aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="48951-120">az webapp deployment user set</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | <span data-ttu-id="48951-121">Ustawia poświadczenia wdrożenia na poziomie konta hello usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="48951-121">Sets hello account-level deployment credentials for App Service.</span></span> |
| [<span data-ttu-id="48951-122">Źródło wdrożenia az aplikacji sieci Web — config lokalnej — git</span><span class="sxs-lookup"><span data-stu-id="48951-122">az webapp deployment source config-local-git</span></span>](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | <span data-ttu-id="48951-123">Tworzy konfiguracji kontroli źródła dla lokalnego repozytorium Git.</span><span class="sxs-lookup"><span data-stu-id="48951-123">Creates a source control configuration for a local Git repository.</span></span> |
| [<span data-ttu-id="48951-124">AZ przeglądania aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="48951-124">az webapp browse</span></span>](https://docs.microsoft.com/cli/azure/webapp#browse) | <span data-ttu-id="48951-125">Otwórz aplikację sieci web platformy Azure w przeglądarce.</span><span class="sxs-lookup"><span data-stu-id="48951-125">Open an Azure web app in a browser.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="48951-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="48951-126">Next steps</span></span>

<span data-ttu-id="48951-127">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="48951-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="48951-128">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="48951-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
