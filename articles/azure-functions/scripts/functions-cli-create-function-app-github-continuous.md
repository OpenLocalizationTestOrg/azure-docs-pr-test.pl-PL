---
title: "aaaCreate aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub | Dokumentacja firmy Microsoft"
description: "Tworzenie aplikacji funkcji i wdrażanie kodu funkcji z usługi GitHub"
services: functions
ms.service: functions
keywords: 
ms.devlang: azurecli
author: syntaxc4
ms.author: cfowler
ms.date: 04/27/2017
ms.topic: sample
ms.custom: mvc
ms.openlocfilehash: 4d44204b899b32af464260db51ed98bcf00eb2bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-app-service"></a>Utwórz usługę aplikacji

Ten przykładowy skrypt tworzy aplikacji funkcji przy użyciu hello [planu zużycie](../functions-scale.md#consumption-plan) z jego powiązanych zasobów i stale wdraża kodu funkcji z repozytorium GitHub. W tym przykładzie należy:

* Repozytorium GitHub z kodem funkcje, które ma uprawnienia administracyjne.
* A [osobistych dostępu tokenu (PAWEŁ)](https://help.github.com/articles/creating-an-access-token-for-command-line-use) na koncie usługi GitHub.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

Ten przykład tworzy aplikację funkcji platformy Azure i wdraża kod funkcji z usługi GitHub.

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/deploy-function-app-with-function-github-continuous/deploy-function-app-with-function-github-continuous.sh?highlight=3-4 "Azure Service")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji. Ten skrypt używa następujących hello:

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie konta magazynu az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi App Service. |
| [Utwórz az functionapp](https://docs.microsoft.com/cli/azure/appservice/web#delete) |
| [Konfiguracja kontroli źródła programu az usługi aplikacji sieci web](https://docs.microsoft.com/cli/azure/appservice/web/source-control#config) | Kojarzy aplikacji funkcji za pomocą Git lub repozytorium Mercurial. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w hello [dokumentacji usługi Azure Functions](../functions-cli-samples.md).
