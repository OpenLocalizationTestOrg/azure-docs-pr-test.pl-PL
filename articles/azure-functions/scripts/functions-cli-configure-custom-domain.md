---
title: "Azure CLI przykładowym skrypcie - mapy niestandardową domenę do aplikacji funkcji | Dokumentacja firmy Microsoft"
description: "Przykład skryptu usługi Azure CLI — mapy niestandardową domenę do aplikacji funkcji na platformie Azure."
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d127e347-7581-47d7-b289-e0f51f2fbfbc
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/01/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 6fcea6d32f9dd25b0fafb4f895f60d8320ac9df8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="map-a-custom-domain-to-a-function-app"></a>Zamapować niestandardową domenę do aplikacji funkcji

Ten przykładowy skrypt tworzy aplikacji funkcji z powiązanych zasobów, a następnie mapuje `www.<yourdomain>` do niego. Do mapowania na domenę niestandardową, należy utworzyć aplikacji funkcji w planie usługi aplikacji, a nie w planie zużycia. Środowisko Azure Functions obsługuje tylko mapowania domeny niestandardowej przy użyciu rekordu A.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli). 


## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/configure-custom-domain/configure-custom-domain.sh?highlight=3 "zamapować niestandardową domenę do aplikacji funkcji")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie konta magazynu az](https://docs.microsoft.com/cli/azure/storage/account#create) | Tworzy wymagane przez aplikację funkcja konto magazynu. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi aplikacji potrzebne do mapowania domeny niestandardowej. |
| [Utwórz az functionapp]() | Tworzy aplikację funkcji. |
| [Dodaj nazwę az usługi aplikacji sieci web konfiguracji hosta](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Mapuje domeny niestandardowej aplikacji funkcji. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów funkcji interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure Functions]().
