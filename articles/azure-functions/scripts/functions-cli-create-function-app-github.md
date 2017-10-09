---
title: "aaaCreate aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie interfejsu wiersza polecenia platformy Azure — tworzenie aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: 026886f11909149db695d9a52d0aa37f109f64e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="145fd-103">Tworzenie aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="145fd-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="145fd-104">Ten przykładowy skrypt tworzy aplikacji funkcji przy użyciu hello [planu zużycie](../functions-scale.md#consumption-plan) z jego powiązanych zasobów i wdraża kodu funkcji z publicznego repozytorium GitHub (bez ciągłego wdrażania).</span><span class="sxs-lookup"><span data-stu-id="145fd-104">This sample script creates a function app using hello [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="145fd-105">Ciągłego dostarczania kodu funkcji z witryny GitHub można odczytać [tworzenia aplikacji funkcji i stale wdrażania z usługi GitHub](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="145fd-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="145fd-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="145fd-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="145fd-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="145fd-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="145fd-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="145fd-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="145fd-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="145fd-109">Sample script</span></span>

<span data-ttu-id="145fd-110">Ten przykład tworzy aplikację funkcji platformy Azure i wdraża kod funkcji z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="145fd-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="145fd-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="145fd-111">Script explanation</span></span>

<span data-ttu-id="145fd-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="145fd-112">Each command in hello table links toocommand specific documentation.</span></span> <span data-ttu-id="145fd-113">Ten skrypt używa hello następującego polecenia:</span><span class="sxs-lookup"><span data-stu-id="145fd-113">This script uses hello following commands:</span></span>

| <span data-ttu-id="145fd-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="145fd-114">Command</span></span> | <span data-ttu-id="145fd-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="145fd-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="145fd-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="145fd-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="145fd-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="145fd-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="145fd-118">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="145fd-118">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="145fd-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="145fd-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="145fd-120">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="145fd-120">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="145fd-121">Tworzy aplikację funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="145fd-121">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="145fd-122">Konfiguracja kontroli źródła programu az usługi aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="145fd-122">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="145fd-123">Kojarzy aplikacji funkcji za pomocą Git lub repozytorium Mercurial.</span><span class="sxs-lookup"><span data-stu-id="145fd-123">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="145fd-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="145fd-124">Next steps</span></span>

<span data-ttu-id="145fd-125">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="145fd-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="145fd-126">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w hello [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="145fd-126">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
