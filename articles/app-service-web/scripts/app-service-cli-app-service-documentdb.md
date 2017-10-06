---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Połącz tooCosmos aplikacji sieci web DB | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Połącz tooCosmos aplikacji sieci web bazy danych"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 1f2123378b9d5812fa793730f7fa5a5bc9ab63c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-toocosmos-db"></a><span data-ttu-id="f0fbc-103">Połącz tooCosmos aplikacji sieci web bazy danych</span><span class="sxs-lookup"><span data-stu-id="f0fbc-103">Connect a web app tooCosmos DB</span></span>

<span data-ttu-id="f0fbc-104">W tym scenariuszu dowiesz się, jak toocreate konta bazy danych rozwiązania Cosmos Azure i usługi Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-104">In this scenario you will learn how toocreate an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="f0fbc-105">Następnie zostanie Połącz hello DB rozwiązania Cosmos toohello aplikacji sieci web przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-105">Then you will link hello Cosmos DB toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f0fbc-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f0fbc-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f0fbc-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f0fbc-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="f0fbc-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="f0fbc-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="f0fbc-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="f0fbc-110">Script explanation</span></span>

<span data-ttu-id="f0fbc-111">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web, bazy danych rozwiązania Cosmos i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-111">This script uses hello following commands toocreate a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="f0fbc-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f0fbc-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="f0fbc-113">Command</span></span> | <span data-ttu-id="f0fbc-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="f0fbc-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f0fbc-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="f0fbc-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f0fbc-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f0fbc-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="f0fbc-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="f0fbc-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-118">Creates an App Service plan.</span></span> <span data-ttu-id="f0fbc-119">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="f0fbc-120">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="f0fbc-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="f0fbc-121">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="f0fbc-122">Utwórz az cosmosdb</span><span class="sxs-lookup"><span data-stu-id="f0fbc-122">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="f0fbc-123">Tworzy konto DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-123">Creates a Cosmos DB account.</span></span> <span data-ttu-id="f0fbc-124">Jest to, gdzie będą przechowywane dane hello.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-124">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="f0fbc-125">AZ cosmosdb listy kluczy</span><span class="sxs-lookup"><span data-stu-id="f0fbc-125">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="f0fbc-126">Wyświetla klucze dostępu hello hello określone konto DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-126">Lists hello access keys for hello specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="f0fbc-127">AZ aplikacji sieci Web config appsettings zestawu</span><span class="sxs-lookup"><span data-stu-id="f0fbc-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="f0fbc-128">Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="f0fbc-129">Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="f0fbc-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0fbc-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="f0fbc-130">Next steps</span></span>

<span data-ttu-id="f0fbc-131">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0fbc-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f0fbc-132">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f0fbc-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
