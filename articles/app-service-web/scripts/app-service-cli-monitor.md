---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — monitorowanie aplikacji sieci web z dziennikami serwera sieci web | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie — monitorowanie aplikacji sieci web z dziennikami serwera sieci web"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0887656f-611c-4627-8247-b5cded7cef60
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 012b800c03af77387bed3d098fae3c96d82aee29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="84951-103">Monitorowanie aplikacji sieci web z dziennikami serwera sieci web</span><span class="sxs-lookup"><span data-stu-id="84951-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="84951-104">W tym scenariuszu utworzysz grupy zasobów, plan usługi aplikacji, aplikacji sieci web i konfigurowanie aplikacji sieci web hello tooenable dzienniki serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="84951-104">In this scenario you will create a resource group, app service plan, web app and configure hello web app tooenable web server logs.</span></span> <span data-ttu-id="84951-105">Następnie pobierze pliki dziennika hello do przeglądu.</span><span class="sxs-lookup"><span data-stu-id="84951-105">You will then download hello log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="84951-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="84951-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="84951-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="84951-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="84951-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="84951-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="84951-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="84951-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="84951-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="84951-110">Script explanation</span></span>

<span data-ttu-id="84951-111">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="84951-111">This script uses hello following commands toocreate a resource group, web app, and all related resources.</span></span> <span data-ttu-id="84951-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="84951-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="84951-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="84951-113">Command</span></span> | <span data-ttu-id="84951-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="84951-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="84951-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="84951-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="84951-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="84951-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="84951-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="84951-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="84951-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="84951-118">Creates an App Service plan.</span></span> <span data-ttu-id="84951-119">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="84951-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="84951-120">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="84951-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="84951-121">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="84951-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="84951-122">AZ aplikacji sieci Web dziennika konfiguracji</span><span class="sxs-lookup"><span data-stu-id="84951-122">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="84951-123">Określa, które dzienników aplikacji sieci web platformy Azure zostanie utrzymana.</span><span class="sxs-lookup"><span data-stu-id="84951-123">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="84951-124">Pobieranie dziennika az aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="84951-124">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="84951-125">Pliki do pobrania hello rejestruje hello tooyour aplikacji sieci web platformy Azure dla komputera lokalnego.</span><span class="sxs-lookup"><span data-stu-id="84951-125">Downloads hello logs of hello an Azure web app tooyour local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="84951-126">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="84951-126">Next steps</span></span>

<span data-ttu-id="84951-127">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="84951-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="84951-128">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="84951-128">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
