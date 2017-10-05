---
title: "Azure CLI przykładowym skrypcie - mapy domeny niestandardowej aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - mapy domeny niestandardowej aplikacji sieci web"
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
ms.openlocfilehash: 6712be8a551731fbafd92ef19564e89399e23e76
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-web-app"></a><span data-ttu-id="dad8f-103">Zamapować niestandardową domenę do aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="dad8f-103">Map a custom domain to a web app</span></span>

<span data-ttu-id="dad8f-104">Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie mapuje `www.<yourdomain>` do niego.</span><span class="sxs-lookup"><span data-stu-id="dad8f-104">This sample script creates a web app in App Service with its related resources, and then maps `www.<yourdomain>` to it.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dad8f-105">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="dad8f-105">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dad8f-106">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="dad8f-106">Run `az --version` to find the version.</span></span> <span data-ttu-id="dad8f-107">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dad8f-107">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="dad8f-108">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="dad8f-108">Sample script</span></span>

<span data-ttu-id="dad8f-109">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "zamapować niestandardową domenę do aplikacji sieci web")]</span><span class="sxs-lookup"><span data-stu-id="dad8f-109">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="dad8f-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="dad8f-110">Script explanation</span></span>

<span data-ttu-id="dad8f-111">Ten skrypt używa następujących poleceń.</span><span class="sxs-lookup"><span data-stu-id="dad8f-111">This script uses the following commands.</span></span> <span data-ttu-id="dad8f-112">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="dad8f-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="dad8f-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="dad8f-113">Command</span></span> | <span data-ttu-id="dad8f-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="dad8f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dad8f-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="dad8f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dad8f-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="dad8f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dad8f-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="dad8f-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="dad8f-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="dad8f-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="dad8f-119">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="dad8f-119">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="dad8f-120">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="dad8f-120">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="dad8f-121">Dodaj az nazwy hosta z konfiguracji aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="dad8f-121">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="dad8f-122">Mapuje domeny niestandardowej aplikacji sieci web.</span><span class="sxs-lookup"><span data-stu-id="dad8f-122">Maps a custom domain to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dad8f-123">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="dad8f-123">Next steps</span></span>

<span data-ttu-id="dad8f-124">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dad8f-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dad8f-125">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dad8f-125">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
