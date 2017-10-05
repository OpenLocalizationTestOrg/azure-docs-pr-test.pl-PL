---
title: "Azure CLI przykładowym skrypcie - skalowanie aplikacji sieci Web, ręcznie przy użyciu 2.0 interfejsu wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: fe05661eb4e2d5c37aebdbfde002b34588db69e7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="scale-a-web-app-manually"></a><span data-ttu-id="6f9a5-103">Ręcznie skalować aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="6f9a5-103">Scale a web app manually</span></span>

<span data-ttu-id="6f9a5-104">W tym scenariuszu przedstawiono tworzenie grupy zasobów, aplikacji sieci web i plan usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-104">In this scenario you will learn to create a resource group, app service plan and web app.</span></span> <span data-ttu-id="6f9a5-105">Zostanie następnie skalowanie planu usługi App Service z pojedynczym wystąpieniem do wielu wystąpień.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-105">You will then scale the App Service Plan from a single instance to multiple instances.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6f9a5-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6f9a5-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="6f9a5-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6f9a5-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="6f9a5-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="6f9a5-109">Sample script</span></span>

<span data-ttu-id="6f9a5-110">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]</span><span class="sxs-lookup"><span data-stu-id="6f9a5-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/scale-manual/scale-manual.sh "Manual Scale")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6f9a5-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="6f9a5-111">Script explanation</span></span>

<span data-ttu-id="6f9a5-112">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="6f9a5-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6f9a5-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="6f9a5-114">Command</span></span> | <span data-ttu-id="6f9a5-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="6f9a5-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6f9a5-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="6f9a5-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6f9a5-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6f9a5-118">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="6f9a5-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6f9a5-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-119">Creates an App Service plan.</span></span> <span data-ttu-id="6f9a5-120">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="6f9a5-121">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="6f9a5-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6f9a5-122">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6f9a5-123">Aktualizacja planu usługi aplikacji az</span><span class="sxs-lookup"><span data-stu-id="6f9a5-123">az appservice plan update</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#update) | <span data-ttu-id="6f9a5-124">Aktualizuje właściwości planu usługi aplikacji.</span><span class="sxs-lookup"><span data-stu-id="6f9a5-124">Updates properties of the App Service plan.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6f9a5-125">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="6f9a5-125">Next steps</span></span>

<span data-ttu-id="6f9a5-126">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6f9a5-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6f9a5-127">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6f9a5-127">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
