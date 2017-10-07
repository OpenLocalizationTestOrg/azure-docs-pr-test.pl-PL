---
title: "aaaCreate funkcji Azure, która łączy tooan bazy danych Azure rozwiązania Cosmos | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Tworzenie funkcji platformy Azure, łączącego tooan bazy danych Azure rozwiązania Cosmos"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: functions
ms.assetid: 
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 04/20/2017
ms.author: rachelap
ms.custom: mvc
ms.openlocfilehash: 0fbc1ebec2dfd480e0cf3ca64f9febcec8af9a04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-function-that-connects-tooan-azure-cosmos-db"></a>Tworzenie funkcji platformy Azure, łączącego tooan bazy danych Azure rozwiązania Cosmos

Ten przykładowy skrypt tworzy aplikacji funkcji platformy Azure i łączy tooan bazy danych Azure rozwiązania Cosmos w bazie danych.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

Ten przykład tworzy aplikację funkcji platformy Azure i dodaje DB rozwiązania Cosmos punktu końcowego i dostępu do klucza tooapp ustawień.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/create-function-app-connect-to-cosmos-db/create-function-app-connect-to-cosmos-db.sh "Create an Azure Function that connects tooan Azure Cosmos DB")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia

Po uruchomieniu przykładowym skrypcie hello hello wykonaj polecenie może być grupa zasobów hello tooremove używanych, i wszystkich powiązanych zasobów.

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [AZ logowania](https://docs.microsoft.com/cli/azure/#login) | TooAzure logowania. |
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Utwórz grupę zasobów z lokalizacji |
| [Tworzenie konta magazynu az](https://docs.microsoft.com/cli/azure/storage/account) | Tworzenie konta magazynu |
| [Utwórz az functionapp](https://docs.microsoft.com/cli/azure/functionapp#create) | Utwórz nową aplikację funkcji |
| [Utwórz az usługi documentdb](https://docs.microsoft.com/cli/azure/documentdb#create) | Utwórz bazę danych usługi documentdb |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/group#delete) | Czyszczenie |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w hello [dokumentacji usługi Azure Functions](../functions-cli-samples.md).




