---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Połącz pamięci podręcznej redis tooa aplikacji sieci web | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Połącz pamięci podręcznej redis tooa aplikacji sieci web"
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
ms.openlocfilehash: b911e6643591b8f07aeb64d4d62876c0fa156a8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-redis-cache"></a>Połączenie pamięci podręcznej redis tooa aplikacji sieci web

W tym scenariuszu dowiesz się, jak toocreate Azure redis pamięci podręcznej i aplikacji sieci web platformy Azure. Następnie zostanie Połącz hello redis pamięci podręcznej toohello web app przy użyciu ustawień aplikacji.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/connect-to-redis/connect-to-redis.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia redis toocreate grupę zasobów aplikacji sieci web i wszystkie powiązane zasoby pamięci podręcznej. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi App Service. Przypomina farmy serwerów aplikacji sieci web platformy Azure. |
| [Tworzenie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp#create) | Tworzenie aplikacji sieci web platformy Azure. |
| [Tworzenie pamięci podręcznej redis az](https://docs.microsoft.com/en-us/cli/azure/redis#create) | Utwórz nowe wystąpienie pamięci podręcznej Redis. Jest to, gdzie będą przechowywane dane hello. |
| [klucze listy az redis](https://docs.microsoft.com/en-us/cli/azure/redis#list-keys) | Wyświetla listę hello klucze dostępu dla wystąpienia pamięci podręcznej redis hello. |
| [AZ aplikacji sieci Web config appsettings zestawu](https://docs.microsoft.com/cli/azure/webapp/config/appsettings#set) | Tworzy lub aktualizuje ustawienia aplikacji dla aplikacji sieci web platformy Azure. Ustawienia aplikacji są widoczne jako zmienne środowiskowe dla aplikacji. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).
