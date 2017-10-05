---
title: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web do bazy danych rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web do bazy danych rozwiązania Cosmos"
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
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a><span data-ttu-id="5e43b-103">Łączenie aplikacji sieci web do bazy danych rozwiązania Cosmos</span><span class="sxs-lookup"><span data-stu-id="5e43b-103">Connect a web app to Cosmos DB</span></span>

<span data-ttu-id="5e43b-104">W tym scenariuszu dowiesz się, jak utworzyć konto bazy danych rozwiązania Cosmos Azure i aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5e43b-104">In this scenario you will learn how to create an Azure Cosmos DB account and an Azure web app.</span></span> <span data-ttu-id="5e43b-105">Następnie połączy DB rozwiązania Cosmos w aplikacji sieci web przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e43b-105">Then you will link the Cosmos DB to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5e43b-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="5e43b-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5e43b-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="5e43b-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="5e43b-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5e43b-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5e43b-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5e43b-109">Sample script</span></span>

<span data-ttu-id="5e43b-110">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "bazy danych Azure rozwiązania Cosmos")]</span><span class="sxs-lookup"><span data-stu-id="5e43b-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "Azure Cosmos DB")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5e43b-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5e43b-111">Script explanation</span></span>

<span data-ttu-id="5e43b-112">Ten skrypt używa następujących poleceń w celu utworzenia grupy zasobów, aplikacji sieci web, bazy danych rozwiązania Cosmos i wszystkich powiązanych zasobów.</span><span class="sxs-lookup"><span data-stu-id="5e43b-112">This script uses the following commands to create a resource group, web app, Cosmos DB and all related resources.</span></span> <span data-ttu-id="5e43b-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="5e43b-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5e43b-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5e43b-114">Command</span></span> | <span data-ttu-id="5e43b-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5e43b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5e43b-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="5e43b-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5e43b-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5e43b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5e43b-118">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="5e43b-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5e43b-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="5e43b-119">Creates an App Service plan.</span></span> <span data-ttu-id="5e43b-120">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5e43b-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5e43b-121">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="5e43b-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5e43b-122">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5e43b-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5e43b-123">Utwórz az cosmosdb</span><span class="sxs-lookup"><span data-stu-id="5e43b-123">az cosmosdb create</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | <span data-ttu-id="5e43b-124">Tworzy konto DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5e43b-124">Creates a Cosmos DB account.</span></span> <span data-ttu-id="5e43b-125">Jest to, gdzie będą przechowywane dane.</span><span class="sxs-lookup"><span data-stu-id="5e43b-125">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="5e43b-126">AZ cosmosdb listy kluczy</span><span class="sxs-lookup"><span data-stu-id="5e43b-126">az cosmosdb list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | <span data-ttu-id="5e43b-127">Wyświetla klucze dostępu dla określonego konta DB rozwiązania Cosmos.</span><span class="sxs-lookup"><span data-stu-id="5e43b-127">Lists the access keys for the specified Cosmos DB account.</span></span> |
| [<span data-ttu-id="5e43b-128">AZ aplikacji sieci Web config appsettings zestawu</span><span class="sxs-lookup"><span data-stu-id="5e43b-128">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="5e43b-129">Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5e43b-129">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="5e43b-130">Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5e43b-130">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5e43b-131">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5e43b-131">Next steps</span></span>

<span data-ttu-id="5e43b-132">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5e43b-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5e43b-133">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5e43b-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
