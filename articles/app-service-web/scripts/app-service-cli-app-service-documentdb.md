---
title: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web do bazy danych rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web do bazy danych rozwiązania Cosmos"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bbbdbc42-efb5-4b4f-8ba6-c03c9d16a7ea
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: ff5e7a794033cc51120831e09b055a86affb28a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-cosmos-db"></a>Łączenie aplikacji sieci web do bazy danych rozwiązania Cosmos

W tym scenariuszu dowiesz się, jak utworzyć konto bazy danych rozwiązania Cosmos Azure i aplikacji sieci web platformy Azure. Następnie połączy DB rozwiązania Cosmos w aplikacji sieci web przy użyciu ustawień aplikacji.


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/connect-to-documentdb/connect-to-documentdb.sh "bazy danych Azure rozwiązania Cosmos")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń w celu utworzenia grupy zasobów, aplikacji sieci web, bazy danych rozwiązania Cosmos i wszystkich powiązanych zasobów. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi App Service. Przypomina farmy serwerów aplikacji sieci web platformy Azure. |
| [Tworzenie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp#create) | Tworzenie aplikacji sieci web platformy Azure. |
| [Utwórz az cosmosdb](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#create) | Tworzy konto DB rozwiązania Cosmos. Jest to, gdzie będą przechowywane dane. |
| [AZ cosmosdb listy kluczy](https://docs.microsoft.com/en-us/cli/azure/cosmosdb#list-keys) | Wyświetla klucze dostępu dla określonego konta DB rozwiązania Cosmos. |
| [AZ aplikacji sieci Web config appsettings zestawu](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure. Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).
