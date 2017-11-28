---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — połączyć z bazą danych SQL tooa aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Połącz z bazą danych SQL tooa aplikacji sieci web"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 7c2efdd0-f553-4038-a77a-e953021b3f77
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: adee42cd659d977b49e71d974d240324f68f67f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-sql-database"></a><span data-ttu-id="5eed5-103">Połącz z bazą danych SQL tooa aplikacji sieci web</span><span class="sxs-lookup"><span data-stu-id="5eed5-103">Connect a web app tooa SQL database</span></span>

<span data-ttu-id="5eed5-104">W tym scenariuszu dowiesz się, jak toocreate bazy danych Azure SQL i usługi Azure web app.</span><span class="sxs-lookup"><span data-stu-id="5eed5-104">In this scenario you will learn how toocreate an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="5eed5-105">Następnie zostanie Połącz hello SQL bazy danych toohello web app przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5eed5-105">Then you will link hello SQL database toohello web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5eed5-106">Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="5eed5-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5eed5-107">Uruchom `az --version` toofind hello wersji.</span><span class="sxs-lookup"><span data-stu-id="5eed5-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5eed5-108">Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5eed5-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5eed5-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="5eed5-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5eed5-110">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="5eed5-110">Script explanation</span></span>

<span data-ttu-id="5eed5-111">Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web, bazy danych SQL i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="5eed5-111">This script uses hello following commands toocreate a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="5eed5-112">Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.</span><span class="sxs-lookup"><span data-stu-id="5eed5-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5eed5-113">Polecenie</span><span class="sxs-lookup"><span data-stu-id="5eed5-113">Command</span></span> | <span data-ttu-id="5eed5-114">Uwagi</span><span class="sxs-lookup"><span data-stu-id="5eed5-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5eed5-115">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="5eed5-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5eed5-116">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="5eed5-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5eed5-117">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="5eed5-117">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5eed5-118">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="5eed5-118">Creates an App Service plan.</span></span> <span data-ttu-id="5eed5-119">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5eed5-119">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="5eed5-120">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="5eed5-120">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="5eed5-121">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5eed5-121">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="5eed5-122">Utwórz az programu sql server</span><span class="sxs-lookup"><span data-stu-id="5eed5-122">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="5eed5-123">Tworzy serwer bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="5eed5-123">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="5eed5-124">Tworzenie bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="5eed5-124">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="5eed5-125">Tworzy nową bazę danych z powitania serwera bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="5eed5-125">Creates a new database with hello SQL Database Server.</span></span> |
| [<span data-ttu-id="5eed5-126">AZ aplikacji sieci Web config appsettings zestawu</span><span class="sxs-lookup"><span data-stu-id="5eed5-126">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="5eed5-127">Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="5eed5-127">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="5eed5-128">Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="5eed5-128">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5eed5-129">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="5eed5-129">Next steps</span></span>

<span data-ttu-id="5eed5-130">Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5eed5-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5eed5-131">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="5eed5-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
