---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie aplikacji sieci web platformy ASP.NET Core w kontenerze Docker | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie aplikacji sieci web platformy ASP.NET Core w kontenerze Docker"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 3a2d1983-ff7b-476a-ac44-49ec2aabb31a
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 23106345bfbbf1f68757d99010db98e7c9a7da49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="85d83-103">Tworzenie aplikacji sieci web platformy ASP.NET Core w kontenerze Docker</span><span class="sxs-lookup"><span data-stu-id="85d83-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="85d83-104">W tym scenariuszu dowiesz się, jak toocreate grupę zasobów aplikacji w systemie Linux usługi planowania i aplikacji sieci web i wdrażanie aplikacji platformy ASP.NET Core za pomocą kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="85d83-104">In this scenario you will learn how toocreate a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="85d83-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="85d83-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="85d83-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="85d83-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="85d83-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="85d83-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="85d83-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="85d83-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="85d83-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="85d83-109">Script explanation</span></span>

<span data-ttu-id="85d83-110">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="85d83-110">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="85d83-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="85d83-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="85d83-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="85d83-112">Command</span></span> | <span data-ttu-id="85d83-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="85d83-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="85d83-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="85d83-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="85d83-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="85d83-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="85d83-116">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="85d83-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="85d83-117">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="85d83-117">Creates an App Service plan.</span></span> <span data-ttu-id="85d83-118">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="85d83-118">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="85d83-119">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="85d83-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="85d83-120">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="85d83-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="85d83-121">zestaw kontenera konfiguracji aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="85d83-121">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="85d83-122">Ustawia kontener Docker hello hello aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="85d83-122">Sets hello Docker container for hello Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="85d83-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="85d83-123">Next steps</span></span>

<span data-ttu-id="85d83-124">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="85d83-124">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="85d83-125">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="85d83-125">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
