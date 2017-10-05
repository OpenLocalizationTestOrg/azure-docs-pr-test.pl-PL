---
title: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web z pamięci podręcznej redis | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web z pamięci podręcznej redis"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a><span data-ttu-id="9ff24-103">Łączenie aplikacji sieci web z pamięci podręcznej redis</span><span class="sxs-lookup"><span data-stu-id="9ff24-103">Connect a web app to a redis cache</span></span>

<span data-ttu-id="9ff24-104">W tym scenariuszu dowiesz się, jak tworzyć pamięć podręczna Azure redis i aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff24-104">In this scenario you will learn how to create an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="9ff24-105">Następnie połączy pamięć podręczna redis do aplikacji sieci web, przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ff24-105">Then you will link the redis cache to the web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9ff24-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="9ff24-106">Sample script</span></span>

<span data-ttu-id="9ff24-107">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "pamięć podręczna Redis Azure")]</span><span class="sxs-lookup"><span data-stu-id="9ff24-107">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="9ff24-108">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="9ff24-108">Script explanation</span></span>

<span data-ttu-id="9ff24-109">Ten skrypt używa następujących poleceń, aby utworzyć grupę zasobów, aplikacji sieci web, redis pamięci podręcznej i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="9ff24-109">This script uses the following commands to create a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="9ff24-110">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="9ff24-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9ff24-111">Polecenie</span><span class="sxs-lookup"><span data-stu-id="9ff24-111">Command</span></span> | <span data-ttu-id="9ff24-112">Uwagi</span><span class="sxs-lookup"><span data-stu-id="9ff24-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9ff24-113">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="9ff24-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9ff24-114">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="9ff24-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9ff24-115">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="9ff24-115">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="9ff24-116">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="9ff24-116">Creates an App Service plan.</span></span> <span data-ttu-id="9ff24-117">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff24-117">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="9ff24-118">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="9ff24-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="9ff24-119">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff24-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="9ff24-120">Tworzenie pamięci podręcznej redis az</span><span class="sxs-lookup"><span data-stu-id="9ff24-120">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="9ff24-121">Utwórz nowe wystąpienie pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="9ff24-121">Create new Redis Cache instance.</span></span> <span data-ttu-id="9ff24-122">Jest to, gdzie będą przechowywane dane.</span><span class="sxs-lookup"><span data-stu-id="9ff24-122">This is where the data will be stored.</span></span> |
| [<span data-ttu-id="9ff24-123">klucze listy az redis</span><span class="sxs-lookup"><span data-stu-id="9ff24-123">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="9ff24-124">Wyświetla klucze dostępu do wystąpienia pamięci podręcznej redis.</span><span class="sxs-lookup"><span data-stu-id="9ff24-124">Lists the access keys for the redis cache instance.</span></span> |
| [<span data-ttu-id="9ff24-125">AZ aplikacji sieci Web config appsettings zestawu</span><span class="sxs-lookup"><span data-stu-id="9ff24-125">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="9ff24-126">Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff24-126">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="9ff24-127">Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="9ff24-127">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9ff24-128">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="9ff24-128">Next steps</span></span>

<span data-ttu-id="9ff24-129">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9ff24-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9ff24-130">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="9ff24-130">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
