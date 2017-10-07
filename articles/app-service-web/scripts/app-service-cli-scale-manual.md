---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - skalowanie aplikacji sieci Web, ręcznie przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - skalowanie aplikacji sieci Web, ręcznie przy użyciu usługi Azure CLI 2.0"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 251d9074-8fff-4121-ad16-9eca9556ac96
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 64464c8a44522fdc2c8f3d0192388302a1d12667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="b83cd-103">Ręcznie skalować aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="b83cd-103">Scale a web app manually</span></span>

<span data-ttu-id="b83cd-104">W tym scenariuszu dowiesz się toocreate grupę zasobów aplikacji sieci web i plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b83cd-104">In this scenario you will learn toocreate a resource group, app service plan and web app.</span></span> <span data-ttu-id="b83cd-105">Następnie będzie skalować hello planu usługi App Service z wystąpień toomultiple pojedynczego wystąpienia.</span><span class="sxs-lookup"><span data-stu-id="b83cd-105">You will then scale hello App Service Plan from a single instance toomultiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b83cd-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="b83cd-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b83cd-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="b83cd-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="b83cd-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b83cd-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b83cd-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="b83cd-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="b83cd-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="b83cd-110">Script explanation</span></span>

<span data-ttu-id="b83cd-111">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="b83cd-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="b83cd-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="b83cd-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b83cd-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="b83cd-113">Command</span></span> | <span data-ttu-id="b83cd-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="b83cd-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b83cd-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="b83cd-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b83cd-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="b83cd-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b83cd-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="b83cd-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="b83cd-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="b83cd-118">Creates an App Service plan.</span></span> <span data-ttu-id="b83cd-119">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b83cd-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="b83cd-120">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="b83cd-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="b83cd-121">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="b83cd-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="b83cd-122">Aktualizacja planu usługi aplikacji az</span><span class="sxs-lookup"><span data-stu-id="b83cd-122">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="b83cd-123">Aktualizuje właściwości hello planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="b83cd-123">Updates properties of hello App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b83cd-124">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="b83cd-124">Next steps</span></span>

<span data-ttu-id="b83cd-125">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b83cd-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b83cd-126">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="b83cd-126">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
