---
title: "Azure CLI skrypt przykładowy — tworzenie aplikacji funkcja do wykonania niekorzystającą | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie aplikacji funkcja do wykonania bez serwera"
services: functions
documentationcenter: functions
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 0e221db6-ee2d-4e16-9bf6-a456cd05b6e7
ms.service: functions
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 04/11/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 37046967bd5ab0d797d1c66690db7200fb4805e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-function-app-for-serverless-execution"></a>Tworzenie aplikacji funkcja do wykonania bez serwera

Ten przykładowy skrypt tworzy aplikację funkcji Azure to kontener dla funkcji. Funkcja aplikacji jest tworzony przy użyciu [planu zużycia](../functions-scale.md#consumption-plan), który jest odpowiedni dla obciążeń niekorzystającą sterowane zdarzeniami.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

Ten skrypt tworzy aplikacji funkcji platformy Azure przy użyciu [planu zużycie](../functions-scale.md#consumption-plan).

[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/create-function-app-consumption/create-function-app-consumption.sh "Tworzenie funkcji platformy Azure w planie zużycie")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Każde polecenie w tabeli łącza do dokumentacji określonego polecenia. Ten skrypt używa następujących poleceń:

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie konta magazynu az](/cli/azure/storage/account#create) | Tworzy konto magazynu Azure. |
| [Utwórz az functionapp](https://docs.microsoft.com/cli/azure/functionapp#create) | Tworzy funkcję platformy Azure. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów wiersza polecenia funkcji platformy Azure można znaleźć w [dokumentacji usługi Azure Functions](../functions-cli-samples.md).
