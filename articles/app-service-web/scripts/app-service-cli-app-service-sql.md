---
title: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web z bazy danych SQL | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web z bazy danych SQL"
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
ms.openlocfilehash: ec5e22bfacc12a89f1fb5882487df4829369777c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-sql-database"></a><span data-ttu-id="bf5fc-103">Łączenie aplikacji sieci web z bazy danych SQL</span><span class="sxs-lookup"><span data-stu-id="bf5fc-103">Connect a web app to a SQL database</span></span>

<span data-ttu-id="bf5fc-104">W tym scenariuszu dowiesz się, jak utworzyć bazę danych Azure SQL i aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-104">In this scenario you will learn how to create an Azure SQL database and an Azure web app.</span></span> <span data-ttu-id="bf5fc-105">Następnie zostaną połączone z bazą danych SQL do aplikacji sieci web, przy użyciu ustawień aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-105">Then you will link the SQL database to the web app using app settings.</span></span>


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="bf5fc-106">Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="bf5fc-107">Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="bf5fc-108">Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="bf5fc-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="bf5fc-109">Przykładowy skrypt</span><span class="sxs-lookup"><span data-stu-id="bf5fc-109">Sample script</span></span>

<span data-ttu-id="bf5fc-110">[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "bazy danych SQL")]</span><span class="sxs-lookup"><span data-stu-id="bf5fc-110">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="bf5fc-111">Wyjaśnienie skryptu</span><span class="sxs-lookup"><span data-stu-id="bf5fc-111">Script explanation</span></span>

<span data-ttu-id="bf5fc-112">Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, aplikacji sieci web, bazy danych SQL i wszystkie powiązane zasoby.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-112">This script uses the following commands to create a resource group, web app, SQL database and all related resources.</span></span> <span data-ttu-id="bf5fc-113">Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bf5fc-114">Polecenie</span><span class="sxs-lookup"><span data-stu-id="bf5fc-114">Command</span></span> | <span data-ttu-id="bf5fc-115">Uwagi</span><span class="sxs-lookup"><span data-stu-id="bf5fc-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bf5fc-116">Tworzenie grupy az</span><span class="sxs-lookup"><span data-stu-id="bf5fc-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="bf5fc-117">Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="bf5fc-118">Tworzenie planu usług aplikacji az</span><span class="sxs-lookup"><span data-stu-id="bf5fc-118">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="bf5fc-119">Tworzy plan usługi App Service.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-119">Creates an App Service plan.</span></span> <span data-ttu-id="bf5fc-120">Przypomina farmy serwerów aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-120">This is like a server farm for your Azure web app.</span></span> |
| [<span data-ttu-id="bf5fc-121">Tworzenie aplikacji sieci Web az</span><span class="sxs-lookup"><span data-stu-id="bf5fc-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="bf5fc-122">Tworzenie aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="bf5fc-123">Utwórz az programu sql server</span><span class="sxs-lookup"><span data-stu-id="bf5fc-123">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="bf5fc-124">Tworzy serwer bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-124">Creates a SQL Database Server.</span></span>  |
| [<span data-ttu-id="bf5fc-125">Tworzenie bazy danych sql az</span><span class="sxs-lookup"><span data-stu-id="bf5fc-125">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="bf5fc-126">Tworzy nową bazę danych z serwera bazy danych SQL.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-126">Creates a new database with the SQL Database Server.</span></span> |
| [<span data-ttu-id="bf5fc-127">AZ aplikacji sieci Web config appsettings zestawu</span><span class="sxs-lookup"><span data-stu-id="bf5fc-127">az webapp config appsettings set</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | <span data-ttu-id="bf5fc-128">Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-128">Creates or updates an app setting for an Azure web app.</span></span> <span data-ttu-id="bf5fc-129">Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji.</span><span class="sxs-lookup"><span data-stu-id="bf5fc-129">App settings are exposed as environment variables for your app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bf5fc-130">Następne kroki</span><span class="sxs-lookup"><span data-stu-id="bf5fc-130">Next steps</span></span>

<span data-ttu-id="bf5fc-131">Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="bf5fc-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bf5fc-132">Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="bf5fc-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
