---
title: "Tworzenie aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie interfejsu wiersza polecenia platformy Azure — tworzenie aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub"
services: functions
keywords: 
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.service: functions
ms.custom: mvc
ms.openlocfilehash: d67e85f91c80efe464fceb1105243bedfba83a0f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-and-deploy-function-code-from-github"></a><span data-ttu-id="bba1f-103">Tworzenie aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub</span><span class="sxs-lookup"><span data-stu-id="bba1f-103">Create a function app and deploy function code from GitHub</span></span>

<span data-ttu-id="bba1f-104">Ten przykładowy skrypt tworzy aplikacji funkcji przy użyciu [planu zużycie](../functions-scale.md#consumption-plan) z jego powiązanych zasobów i wdraża kodu funkcji z publicznego repozytorium GitHub (bez ciągłego wdrażania).</span><span class="sxs-lookup"><span data-stu-id="bba1f-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and deploys your function code from a public GitHub repository (without continuous deployment).</span></span> <span data-ttu-id="bba1f-105">Ciągłego dostarczania kodu funkcji z witryny GitHub można odczytać [tworzenia aplikacji funkcji i stale wdrażania z usługi GitHub](functions-cli-create-function-app-github-continuous.md)</span><span class="sxs-lookup"><span data-stu-id="bba1f-105">For continuous delivery of function code from GitHub, read [Create a function app and continuously deploy from GitHub](functions-cli-create-function-app-github-continuous.md)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bba1f-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bba1f-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bba1f-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="bba1f-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="bba1f-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bba1f-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bba1f-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="bba1f-109">Sample script</span></span>

<span data-ttu-id="bba1f-110">Ten przykład tworzy aplikację funkcji platformy Azure i wdraża kod funkcji z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="bba1f-110">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="bba1f-111">[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "tworzenia aplikacji funkcji z wdrożeniem z usługi GitHub")]</span><span class="sxs-lookup"><span data-stu-id="bba1f-111">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github/deploy-function-app-with-function-github.sh?highlight=3 "Create a function app with deployment from GitHub")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bba1f-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="bba1f-112">Script explanation</span></span>

<span data-ttu-id="bba1f-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="bba1f-113">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="bba1f-114">Ten skrypt używa następujących poleceń:</span><span class="sxs-lookup"><span data-stu-id="bba1f-114">This script uses the following commands:</span></span>

| <span data-ttu-id="bba1f-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="bba1f-115">Command</span></span> | <span data-ttu-id="bba1f-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bba1f-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bba1f-117">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="bba1f-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bba1f-118">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="bba1f-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bba1f-119">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="bba1f-119">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bba1f-120">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="bba1f-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="bba1f-121">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="bba1f-121">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) | <span data-ttu-id="bba1f-122">Tworzy aplikację funkcji platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bba1f-122">Creates an Azure Function app.</span></span> |
| [<span data-ttu-id="bba1f-123">Konfiguracja kontroli źródła programu az usługi aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="bba1f-123">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="bba1f-124">Kojarzy aplikacji funkcji za pomocą Git lub repozytorium Mercurial.</span><span class="sxs-lookup"><span data-stu-id="bba1f-124">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bba1f-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bba1f-125">Next steps</span></span>

<span data-ttu-id="bba1f-126">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bba1f-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bba1f-127">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bba1f-127">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
