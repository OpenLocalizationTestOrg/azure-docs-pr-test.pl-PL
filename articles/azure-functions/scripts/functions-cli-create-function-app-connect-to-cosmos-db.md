---
title: "aaaCreate funkcji Azure, która łączy tooan bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie funkcji platformy Azure, łączącego tooan bazy danych Azure rozwiązania Cosmos"
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
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a><span data-ttu-id="04472-103">Tworzenie funkcji platformy Azure, łączącego tooan bazy danych Azure rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="04472-103">Create an Azure Function that connects tooan Azure Cosmos DB</span></span>

<span data-ttu-id="04472-104">Ten przykładowy skrypt tworzy aplikacji funkcji platformy Azure i łączy tooan bazy danych Azure rozwiązania Cosmos w bazie danych.</span><span class="sxs-lookup"><span data-stu-id="04472-104">This sample script creates an Azure Function App and connects tooan Azure Cosmos DB database.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="04472-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="04472-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="04472-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="04472-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="04472-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="04472-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="04472-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="04472-108">Sample script</span></span>

<span data-ttu-id="04472-109">Ten przykład tworzy aplikację funkcji platformy Azure i dodaje DB rozwiązania Cosmos punktu końcowego i dostępu do klucza tooapp ustawień.</span><span class="sxs-lookup"><span data-stu-id="04472-109">This sample creates an Azure Function app and adds a Cosmos DB endpoint and access key tooapp settings.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="04472-110">Czyszczenie wdrożenia</span><span class="sxs-lookup"><span data-stu-id="04472-110">Clean up deployment</span></span>

<span data-ttu-id="04472-111">Po uruchomieniu przykładowym skrypcie hello hello wykonaj polecenie może być grupa zasobów hello tooremove używanych, i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="04472-111">After hello script sample has been run, hello follow command can be used tooremove hello resource group and all related resources.</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="04472-112">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="04472-112">Script explanation</span></span>

<span data-ttu-id="04472-113">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="04472-113">This script uses hello following commands.</span></span> <span data-ttu-id="04472-114">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="04472-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="04472-115">Polecenie</span><span class="sxs-lookup"><span data-stu-id="04472-115">Command</span></span> | <span data-ttu-id="04472-116">Uwagi</span><span class="sxs-lookup"><span data-stu-id="04472-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="04472-117">AZ logowania</span><span class="sxs-lookup"><span data-stu-id="04472-117">az login</span></span>](https://docs.microsoft.com/cli/azure/#login) | <span data-ttu-id="04472-118">TooAzure logowania.</span><span class="sxs-lookup"><span data-stu-id="04472-118">Login tooAzure.</span></span> |
| [<span data-ttu-id="04472-119">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="04472-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="04472-120">Utwórz grupę zasobów z lokalizacji</span><span class="sxs-lookup"><span data-stu-id="04472-120">Create a resource group with location</span></span> |
| [<span data-ttu-id="04472-121">Tworzenie konta magazynu az</span><span class="sxs-lookup"><span data-stu-id="04472-121">az storage account create</span></span>](https://docs.microsoft.com/cli/azure/storage/account) | <span data-ttu-id="04472-122">Tworzenie konta magazynu</span><span class="sxs-lookup"><span data-stu-id="04472-122">Create a storage account</span></span> |
| [<span data-ttu-id="04472-123">Utwórz az functionapp</span><span class="sxs-lookup"><span data-stu-id="04472-123">az functionapp create</span></span>](https://docs.microsoft.com/cli/azure/functionapp#create) | <span data-ttu-id="04472-124">Utwórz nową aplikację funkcji</span><span class="sxs-lookup"><span data-stu-id="04472-124">Create a new function app</span></span> |
| [<span data-ttu-id="04472-125">Utwórz az usługi documentdb</span><span class="sxs-lookup"><span data-stu-id="04472-125">az documentdb create</span></span>](https://docs.microsoft.com/cli/azure/documentdb#create) | <span data-ttu-id="04472-126">Utwórz bazę danych usługi documentdb</span><span class="sxs-lookup"><span data-stu-id="04472-126">Create documentdb database</span></span> |
| [<span data-ttu-id="04472-127">Usuwanie grupy az</span><span class="sxs-lookup"><span data-stu-id="04472-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="04472-128">Czyszczenie</span><span class="sxs-lookup"><span data-stu-id="04472-128">Clean up</span></span> |

## <a name="next-steps"></a><span data-ttu-id="04472-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="04472-129">Next steps</span></span>

<span data-ttu-id="04472-130">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="04472-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="04472-131">Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w hello [dokumentacji usługi Azure Functions](../functions-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="04472-131">Additional Azure Functions CLI script samples can be found in hello [Azure Functions documentation](../functions-cli-samples.md).</span></span>




