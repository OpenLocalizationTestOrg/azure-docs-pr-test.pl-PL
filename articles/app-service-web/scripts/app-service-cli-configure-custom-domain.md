---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - mapy domeny niestandardowej aplikacji sieci web tooa | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - mapy aplikacji sieci web tooa domeny niestandardowej"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a><span data-ttu-id="faa5a-103">Mapa aplikacji sieci web tooa domeny niestandardowej</span><span class="sxs-lookup"><span data-stu-id="faa5a-103">Map a custom domain tooa web app</span></span>

<span data-ttu-id="faa5a-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie mapuje `www.<yourdomain>` tooit.</span><span class="sxs-lookup"><span data-stu-id="faa5a-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` tooit.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="faa5a-105">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="faa5a-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="faa5a-106">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="faa5a-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="faa5a-107">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="faa5a-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="faa5a-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="faa5a-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="faa5a-109">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="faa5a-109">Script explanation</span></span>

<span data-ttu-id="faa5a-110">Ten skrypt używa hello następujące polecenia.</span><span class="sxs-lookup"><span data-stu-id="faa5a-110">This script uses hello following commands.</span></span> <span data-ttu-id="faa5a-111">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="faa5a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="faa5a-112">Polecenie</span><span class="sxs-lookup"><span data-stu-id="faa5a-112">Command</span></span> | <span data-ttu-id="faa5a-113">Uwagi</span><span class="sxs-lookup"><span data-stu-id="faa5a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="faa5a-114">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="faa5a-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="faa5a-115">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="faa5a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="faa5a-116">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="faa5a-116">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="faa5a-117">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="faa5a-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="faa5a-118">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="faa5a-118">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="faa5a-119">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="faa5a-119">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="faa5a-120">Dodaj az nazwy hosta z konfiguracji aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="faa5a-120">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="faa5a-121">Mapuje aplikacji sieci web tooa domeny niestandardowej.</span><span class="sxs-lookup"><span data-stu-id="faa5a-121">Maps a custom domain tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="faa5a-122">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="faa5a-122">Next steps</span></span>

<span data-ttu-id="faa5a-123">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="faa5a-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="faa5a-124">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="faa5a-124">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
