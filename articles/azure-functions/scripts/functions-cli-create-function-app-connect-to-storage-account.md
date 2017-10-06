---
title: "aaaCreate funkcji Azure, która łączy tooan usługi Azure Storage | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie funkcji platformy Azure, łączącego tooan usługi Azure Storage"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: a51a2c17149478eb2d3d0d4034400ed00cd8416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-function-app-into-azure-storage-account"></a><span data-ttu-id="6a20c-103">Integrowanie aplikacji funkcji kontem magazynu platformy Azure</span><span class="sxs-lookup"><span data-stu-id="6a20c-103">Integrate Function App into Azure Storage Account</span></span>

<span data-ttu-id="6a20c-104">Ten przykładowy skrypt tworzy aplikację funkcji oraz konto magazynu.</span><span class="sxs-lookup"><span data-stu-id="6a20c-104">This sample script creates a Function App and Storage Account.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6a20c-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6a20c-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6a20c-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="6a20c-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6a20c-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6a20c-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6a20c-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="6a20c-108">Sample script</span></span>

<span data-ttu-id="6a20c-109">Ten przykład tworzy aplikację funkcji platformy Azure i dodaje ustawienie aplikacji tooan parametrów połączenia magazynu hello.</span><span class="sxs-lookup"><span data-stu-id="6a20c-109">This sample creates an Azure Function app and adds hello storage connection string tooan app setting.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-storage/create-function-app-connect-to-storage-account.sh "Integrate Function App into Azure Storage Account")]


## <a name="clean-up-deployment"></a><span data-ttu-id="6a20c-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="6a20c-110">Clean up deployment</span></span>

<span data-ttu-id="6a20c-111">Po uruchomieniu przykładowym skrypcie hello hello następujące polecenia można grupy zasobów hello tooremove używanych aplikacji usługi app Service i wszystkie powiązane zasoby:</span><span class="sxs-lookup"><span data-stu-id="6a20c-111">After hello script sample has been run, hello following command can be used tooremove hello resource group, App Service app, and all related resources:</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6a20c-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="6a20c-112">Script explanation</span></span>

<span data-ttu-id="6a20c-113">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="6a20c-113">This script uses hello following commands.</span></span> <span data-ttu-id="6a20c-114">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="6a20c-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6a20c-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="6a20c-115">Command</span></span> | <span data-ttu-id="6a20c-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6a20c-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6a20c-117">AZ logowania</span><span class="sxs-lookup"><span data-stu-id="6a20c-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="6a20c-118">TooAzure logowania.</span><span class="sxs-lookup"><span data-stu-id="6a20c-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="6a20c-119">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="6a20c-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6a20c-120">Utwórz grupę zasobów z lokalizacji</span><span class="sxs-lookup"><span data-stu-id="6a20c-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="6a20c-121">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="6a20c-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="6a20c-122">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="6a20c-122">Create a storage account</span></span> |
| [<span data-ttu-id="6a20c-123">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="6a20c-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="6a20c-124">Utwórz nową aplikację funkcji</span><span class="sxs-lookup"><span data-stu-id="6a20c-124">Create a new function app</span></span> |
| [<span data-ttu-id="6a20c-125">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="6a20c-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="6a20c-126">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="6a20c-126">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6a20c-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6a20c-127">Next steps</span></span>

<span data-ttu-id="6a20c-128">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6a20c-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6a20c-129">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w hello [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6a20c-129">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>
