---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Połącz pamięci podręcznej redis tooa aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Połącz pamięci podręcznej redis tooa aplikacji sieci web"
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
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a><span data-ttu-id="b4e39-103">Połączenie pamięci podręcznej redis tooa aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b4e39-103">Connect a web app tooa redis cache</span></span>

<span data-ttu-id="b4e39-104">W tym scenariuszu dowiesz się, jak toocreate Azure redis pamięci podręcznej i aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e39-104">In this scenario you will learn how toocreate an Azure redis cache and an Azure web app.</span></span> <span data-ttu-id="b4e39-105">Następnie zostanie Połącz hello redis pamięci podręcznej toohello web app przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4e39-105">Then you will link hello redis cache toohello web app using app settings.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b4e39-106">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b4e39-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b4e39-107">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b4e39-107">Script explanation</span></span>

<span data-ttu-id="b4e39-108">Ten skrypt używa hello następujące polecenia redis toocreate grupę zasobów aplikacji sieci web i wszystkie powiązane zasoby pamięci podręcznej.</span><span class="sxs-lookup"><span data-stu-id="b4e39-108">This script uses hello following commands toocreate a resource group, web app, redis cache and all related resources.</span></span> <span data-ttu-id="b4e39-109">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="b4e39-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b4e39-110">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b4e39-110">Command</span></span> | <span data-ttu-id="b4e39-111">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b4e39-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b4e39-112">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="b4e39-112">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b4e39-113">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b4e39-113">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b4e39-114">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="b4e39-114">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b4e39-115">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="b4e39-115">Creates an App Service plan.</span></span> <span data-ttu-id="b4e39-116">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e39-116">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="b4e39-117">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="b4e39-117">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="b4e39-118">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e39-118">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="b4e39-119">Tworzenie pamięci podręcznej redis az</span><span class="sxs-lookup"><span data-stu-id="b4e39-119">az redis create</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#create) | <span data-ttu-id="b4e39-120">Utwórz nowe wystąpienie pamięci podręcznej Redis.</span><span class="sxs-lookup"><span data-stu-id="b4e39-120">Create new Redis Cache instance.</span></span> <span data-ttu-id="b4e39-121">Jest to, gdzie będą przechowywane dane hello.</span><span class="sxs-lookup"><span data-stu-id="b4e39-121">This is where hello data will be stored.</span></span> |
| [<span data-ttu-id="b4e39-122">klucze listy az redis</span><span class="sxs-lookup"><span data-stu-id="b4e39-122">az redis list-keys</span></span>](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | <span data-ttu-id="b4e39-123">Wyświetla listę hello klucze dostępu dla wystąpienia pamięci podręcznej redis hello.</span><span class="sxs-lookup"><span data-stu-id="b4e39-123">Lists hello access keys for hello redis cache instance.</span></span> |
| [<span data-ttu-id="b4e39-124">AZ aplikacji sieci Web config appsettings zestawu</span><span class="sxs-lookup"><span data-stu-id="b4e39-124">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="b4e39-125">Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b4e39-125">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="b4e39-126">Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b4e39-126">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b4e39-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b4e39-127">Next steps</span></span>

<span data-ttu-id="b4e39-128">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b4e39-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b4e39-129">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b4e39-129">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
