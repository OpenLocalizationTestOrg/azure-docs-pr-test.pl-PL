---
title: "aaaCreate aplikacji funkcji i wdrażanie kodu funkcji z programu Visual Studio Team Services | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji funkcji i wdrażanie kodu funkcji z programu Visual Studio Team Services"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/28/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 774bee73025cc9ac46f8b2a6c10edbfa3c2d353b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="44082-103">Utwórz usługę aplikacji</span><span class="sxs-lookup"><span data-stu-id="44082-103">Create an App Service</span></span>

<span data-ttu-id="44082-104">W tym scenariuszu dowiesz się, jak hello toocreate aplikacji funkcji przy użyciu [planu zużycie](../functions-scale.md#consumption-plan) z jego powiązanych zasobów i stale wdraża kodu funkcji z repozytorium programu Visual Studio Team Services (VSTS).</span><span class="sxs-lookup"><span data-stu-id="44082-104">In this scenario you will learn how toocreate a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a Visual Studio Team Services (VSTS) repository.</span></span> <span data-ttu-id="44082-105">W tym przykładzie potrzebne są:</span><span class="sxs-lookup"><span data-stu-id="44082-105">In this sample, you will need:</span></span>

* <span data-ttu-id="44082-106">Repozytorium programu VSTS z kodem funkcje, które ma uprawnienia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="44082-106">A VSTS repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="44082-107">A [osobistych dostępu tokenu (PAWEŁ)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) na koncie usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="44082-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="44082-108">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="44082-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="44082-109">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="44082-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="44082-110">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="44082-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="44082-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="44082-111">Sample script</span></span>

<span data-ttu-id="44082-112">Ten przykład tworzy aplikację funkcji platformy Azure i wdraża kod funkcji z programu Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="44082-112">This sample creates an Azure Function app and deploys function code from Visual Studio Team Services.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-vsts/deploy-function-app-with-function-vsts.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="44082-113">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="44082-113">Script explanation</span></span>

<span data-ttu-id="44082-114">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web, usługi documentdb i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="44082-114">This script uses hello following commands toocreate a resource group, web app, documentdb and all related resources.</span></span> <span data-ttu-id="44082-115">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="44082-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="44082-116">Polecenie</span><span class="sxs-lookup"><span data-stu-id="44082-116">Command</span></span> | <span data-ttu-id="44082-117">Uwagi</span><span class="sxs-lookup"><span data-stu-id="44082-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="44082-118">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="44082-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="44082-119">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="44082-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="44082-120">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="44082-120">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="44082-121">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="44082-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="44082-122">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="44082-122">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="44082-123">Konfiguracja kontroli źródła programu az usługi aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="44082-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="44082-124">Kojarzy aplikacji funkcji za pomocą Git lub repozytorium Mercurial.</span><span class="sxs-lookup"><span data-stu-id="44082-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="44082-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="44082-125">Next steps</span></span>

<span data-ttu-id="44082-126">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="44082-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="44082-127">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w hello [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="44082-127">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
