---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - Bind niestandardowych aplikacji funkcji tooa certyfikatu SSL | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie interfejsu wiersza polecenia Azure — wiązanie niestandardowych SSL certyfikatu tooa funkcji aplikacji na platformie Azure"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a>Powiąż niestandardowych aplikacji funkcji tooa certyfikat protokołu SSL

Ten przykładowy skrypt tworzy aplikacji funkcji w usłudze App Service z powiązane zasoby, a następnie powiązania certyfikatu SSL hello tooit nazwy domeny niestandardowej. Dla tego przykładu należy:

* Dostęp do strony konfiguracji DNS rejestratora domen tooyour.
* Nieprawidłowa. Plik PFX i jego hasło dla hello SSL certyfikatów można mają tooupload i ich powiązania.

toobind certyfikatu SSL w planie usługi aplikacji, a nie w planie zużycia, należy utworzyć aplikację funkcji.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy certyfikaty SSL toobind wymagane planu usługi aplikacji. |
| [Utwórz az functionapp]() | Tworzy aplikację funkcji. |
| [Dodaj nazwę az usługi aplikacji sieci web konfiguracji hosta](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Mapuje aplikacji funkcji toohello domeny niestandardowej. |
| [AZ usługi aplikacji sieci web config ssl przekazywania](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | Przekazanie aplikacji funkcja tooa certyfikatu SSL. |
| [powiązania ssl config az usługi aplikacji sieci web](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | Wiąże przekazanej aplikacji funkcji tooa certyfikatu SSL. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service]().
