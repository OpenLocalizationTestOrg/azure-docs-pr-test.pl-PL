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
# <a name="connect-a-web-app-tooa-sql-database"></a>Połącz z bazą danych SQL tooa aplikacji sieci web

W tym scenariuszu dowiesz się, jak toocreate bazy danych Azure SQL i usługi Azure web app. Następnie zostanie Połącz hello SQL bazy danych toohello web app przy użyciu ustawień aplikacji.


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-sql/connect-to-sql.sh?highlight=9-10 "SQL Database")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web, bazy danych SQL i wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi App Service. Przypomina farmy serwerów aplikacji sieci web platformy Azure. |
| [Tworzenie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp#create) | Tworzenie aplikacji sieci web platformy Azure. |
| [Utwórz az programu sql server](https://docs.microsoft.com/cli/azure/sql/server#create) | Tworzy serwer bazy danych SQL.  |
| [Tworzenie bazy danych sql az](https://docs.microsoft.com/cli/azure/sql/db#create) | Tworzy nową bazę danych z powitania serwera bazy danych SQL. |
| [AZ aplikacji sieci Web config appsettings zestawu](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure. Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).
