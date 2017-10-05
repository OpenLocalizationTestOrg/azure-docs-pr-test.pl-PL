---
title: "Tworzenie aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 67eb41d89328ab57741c419d8b718e19b947dab1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-app-service"></a><span data-ttu-id="9f48c-103">Utwórz usługę aplikacji</span><span class="sxs-lookup"><span data-stu-id="9f48c-103">Create an App Service</span></span>

<span data-ttu-id="9f48c-104">Ten przykładowy skrypt tworzy aplikacji funkcji przy użyciu [planu zużycie](../functions-scale.md#consumption-plan) z jego powiązanych zasobów i stale wdraża kodu funkcji z repozytorium GitHub.</span><span class="sxs-lookup"><span data-stu-id="9f48c-104">This sample script creates a function app using the [consumption plan](../functions-scale.md#consumption-plan) with its related resources, and continuously deploys your function code from a GitHub repository.</span></span> <span data-ttu-id="9f48c-105">W tym przykładzie należy:</span><span class="sxs-lookup"><span data-stu-id="9f48c-105">In this sample, you need:</span></span>

* <span data-ttu-id="9f48c-106">Repozytorium GitHub z kodem funkcje, które ma uprawnienia administracyjne.</span><span class="sxs-lookup"><span data-stu-id="9f48c-106">A GitHub repository with functions code, that you have administrative permissions for.</span></span>
* <span data-ttu-id="9f48c-107">A [osobistych dostępu tokenu (PAWEŁ)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) na koncie usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="9f48c-107">A [Personal Access Token (PAT)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) for your GitHub account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9f48c-108">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="9f48c-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9f48c-109">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="9f48c-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="9f48c-110">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9f48c-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="9f48c-111">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9f48c-111">Sample script</span></span>

<span data-ttu-id="9f48c-112">Ten przykład tworzy aplikację funkcji platformy Azure i wdraża kod funkcji z usługi GitHub.</span><span class="sxs-lookup"><span data-stu-id="9f48c-112">This sample creates an Azure Function app and deploys function code from GitHub.</span></span>

<span data-ttu-id="9f48c-113">[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "usługi Azure")]</span><span class="sxs-lookup"><span data-stu-id="9f48c-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9f48c-114">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9f48c-114">Script explanation</span></span>

<span data-ttu-id="9f48c-115">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="9f48c-115">Each command in the table links to command specific documentation.</span></span> <span data-ttu-id="9f48c-116">Ten skrypt korzysta z następujących czynności:</span><span class="sxs-lookup"><span data-stu-id="9f48c-116">This script uses the following:</span></span>

| <span data-ttu-id="9f48c-117">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9f48c-117">Command</span></span> | <span data-ttu-id="9f48c-118">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9f48c-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9f48c-119">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="9f48c-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9f48c-120">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9f48c-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9f48c-121">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="9f48c-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9f48c-122">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="9f48c-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="9f48c-123">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="9f48c-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [<span data-ttu-id="9f48c-124">Konfiguracja kontroli źródła programu az usługi aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="9f48c-124">az appservice web source-control config</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | <span data-ttu-id="9f48c-125">Kojarzy aplikacji funkcji za pomocą Git lub repozytorium Mercurial.</span><span class="sxs-lookup"><span data-stu-id="9f48c-125">Associates a function app with a Git or Mercurial repository.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9f48c-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9f48c-126">Next steps</span></span>

<span data-ttu-id="9f48c-127">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9f48c-127">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9f48c-128">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9f48c-128">Additional Azure Functions CLI script samples can be found in the [Azure Functions documentation](../functions-cli-samples.md).</span></span>
