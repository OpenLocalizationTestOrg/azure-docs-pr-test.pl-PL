---
title: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web z pamięci podręcznej redis | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — łączenie aplikacji sieci web z pamięci podręcznej redis"
services: appservice
documentationcenter: appservice
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: bc8345b2-8487-40c6-a91f-77414e8688e6
ms.service: app-service
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 06/19/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: b697c8508a6c3422b6b0d0ca36843a9c884b505f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-web-app-to-a-redis-cache"></a>Łączenie aplikacji sieci web z pamięci podręcznej redis

W tym scenariuszu dowiesz się, jak tworzyć pamięć podręczna Azure redis i aplikacji sieci web platformy Azure. Następnie połączy pamięć podręczna redis do aplikacji sieci web, przy użyciu ustawień aplikacji.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[główne](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "pamięć podręczna Redis Azure")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń, aby utworzyć grupę zasobów, aplikacji sieci web, redis pamięci podręcznej i wszystkie powiązane zasoby. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi App Service. Przypomina farmy serwerów aplikacji sieci web platformy Azure. |
| [Tworzenie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp#create) | Tworzenie aplikacji sieci web platformy Azure. |
| [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) | Utwórz nowe wystąpienie pamięci podręcznej Redis. Jest to, gdzie będą przechowywane dane. |
| [klucze listy az redis](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | Wyświetla klucze dostępu do wystąpienia pamięci podręcznej redis. |
| [AZ aplikacji sieci Web config appsettings zestawu](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure. Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).
