---
title: "Azure CLI skrypt przykładowy — tworzenie aplikacji sieci web platformy ASP.NET Core w kontenerze Docker | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 5d1e2c7d2815df5fb9c176ec290a18d330ea3f7c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-aspnet-core-web-app-in-a-docker-container"></a><span data-ttu-id="2ba23-103">Tworzenie aplikacji sieci web platformy ASP.NET Core w kontenerze Docker</span><span class="sxs-lookup"><span data-stu-id="2ba23-103">Create an ASP.NET Core web app in a Docker container</span></span>

<span data-ttu-id="2ba23-104">W tym scenariuszu dowiesz się, jak utworzyć grupę zasobów, planu usług aplikacji dla systemu Linux i aplikacji sieci web i wdrażanie aplikacji platformy ASP.NET Core za pomocą kontenera Docker.</span><span class="sxs-lookup"><span data-stu-id="2ba23-104">In this scenario you will learn how to create a resource group, Linux app service plan, and web app, and deploy an ASP.NET Core application using a Docker Container.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2ba23-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="2ba23-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2ba23-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="2ba23-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="2ba23-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2ba23-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="2ba23-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="2ba23-108">Sample script</span></span>

<span data-ttu-id="2ba23-109">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Docker systemu Linux")]</span><span class="sxs-lookup"><span data-stu-id="2ba23-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-linux-docker/deploy-linux-docker.sh?highlight=6 "Linux Docker")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="2ba23-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="2ba23-110">Script explanation</span></span>

<span data-ttu-id="2ba23-111">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="2ba23-111">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="2ba23-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="2ba23-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2ba23-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="2ba23-113">Command</span></span> | <span data-ttu-id="2ba23-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="2ba23-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2ba23-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="2ba23-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="2ba23-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="2ba23-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2ba23-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="2ba23-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="2ba23-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="2ba23-118">Creates an App Service plan.</span></span> <span data-ttu-id="2ba23-119">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba23-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="2ba23-120">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="2ba23-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="2ba23-121">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba23-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="2ba23-122">zestaw kontenera konfiguracji aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="2ba23-122">az webapp config container set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/container#set) | <span data-ttu-id="2ba23-123">Ustawia kontener Docker dla aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="2ba23-123">Sets the Docker container for the Azure web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2ba23-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="2ba23-124">Next steps</span></span>

<span data-ttu-id="2ba23-125">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2ba23-125">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2ba23-126">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2ba23-126">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
