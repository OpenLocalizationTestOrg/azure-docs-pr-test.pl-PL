---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - mapy domeny niestandardowej aplikacji sieci web tooa | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - mapy aplikacji sieci web tooa domeny niestandardowej"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 5ac4a680-cc73-4578-bcd6-8668c08802c2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 49d6be092e438a63c0a43e3207080ca4cd5ff3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="map-a-custom-domain-tooa-web-app"></a>Mapa aplikacji sieci web tooa domeny niestandardowej

Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie mapuje `www.<yourdomain>` tooit.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-custom-domain/configure-custom-domain.sh?highlight=3 "Map a custom domain tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi App Service. |
| [Tworzenie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp#create) | Tworzenie aplikacji sieci web platformy Azure. |
| [Dodaj az nazwy hosta z konfiguracji aplikacji sieci Web](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | Mapuje aplikacji sieci web tooa domeny niestandardowej. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).
