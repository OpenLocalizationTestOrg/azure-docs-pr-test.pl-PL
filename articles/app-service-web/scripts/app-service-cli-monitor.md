---
title: "Azure CLI przykładowym skrypcie — monitorowanie aplikacji sieci web z dziennikami serwera sieci web | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: df4ca5b1270ada849e231ad9608a5b1d2edda8be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-web-app-with-web-server-logs"></a><span data-ttu-id="602a2-103">Monitorowanie aplikacji sieci web z dziennikami serwera sieci web</span><span class="sxs-lookup"><span data-stu-id="602a2-103">Monitor a web app with web server logs</span></span>

<span data-ttu-id="602a2-104">W tym scenariuszu utworzysz grupy zasobów, plan usługi aplikacji, aplikacji sieci web i konfigurowanie aplikacji sieci web, aby włączyć dzienniki serwera sieci web.</span><span class="sxs-lookup"><span data-stu-id="602a2-104">In this scenario you will create a resource group, app service plan, web app and configure the web app to enable web server logs.</span></span> <span data-ttu-id="602a2-105">Następnie pobierze pliki dzienników w celu przeglądu.</span><span class="sxs-lookup"><span data-stu-id="602a2-105">You will then download the log files for review.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="602a2-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="602a2-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="602a2-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="602a2-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="602a2-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="602a2-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="602a2-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="602a2-109">Sample script</span></span>

<span data-ttu-id="602a2-110">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "dzienników monitorowania")]</span><span class="sxs-lookup"><span data-stu-id="602a2-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/monitor-with-logs/monitor-with-logs.sh "Monitor Logs")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="602a2-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="602a2-111">Script explanation</span></span>

<span data-ttu-id="602a2-112">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, aplikacji sieci web i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="602a2-112">This script uses the following commands to create a resource group, web app, and all related resources.</span></span> <span data-ttu-id="602a2-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="602a2-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="602a2-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="602a2-114">Command</span></span> | <span data-ttu-id="602a2-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="602a2-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="602a2-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="602a2-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="602a2-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="602a2-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="602a2-118">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="602a2-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="602a2-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="602a2-119">Creates an App Service plan.</span></span> <span data-ttu-id="602a2-120">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="602a2-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="602a2-121">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="602a2-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="602a2-122">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="602a2-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="602a2-123">AZ aplikacji sieci Web dziennika konfiguracji</span><span class="sxs-lookup"><span data-stu-id="602a2-123">az webapp log config</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#config) | <span data-ttu-id="602a2-124">Określa, które dzienników aplikacji sieci web platformy Azure zostanie utrzymana.</span><span class="sxs-lookup"><span data-stu-id="602a2-124">Configures which logs an Azure web app will persist.</span></span> |
| [<span data-ttu-id="602a2-125">Pobieranie dziennika az aplikacji sieci Web</span><span class="sxs-lookup"><span data-stu-id="602a2-125">az webapp log download</span></span>](https://docs.microsoft.com/cli/azure/webapp/log#download) | <span data-ttu-id="602a2-126">Pobieranie dzienników z aplikacji sieci web platformy Azure na komputerze lokalnym.</span><span class="sxs-lookup"><span data-stu-id="602a2-126">Downloads the logs of the an Azure web app to your local machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="602a2-127">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="602a2-127">Next steps</span></span>

<span data-ttu-id="602a2-128">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="602a2-128">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="602a2-129">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="602a2-129">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
