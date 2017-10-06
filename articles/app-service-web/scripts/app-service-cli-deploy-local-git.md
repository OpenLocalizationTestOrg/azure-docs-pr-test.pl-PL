---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git | Dokumentacja firmy Microsoft"
description: "Przykładowy skrypt interfejsu wiersza polecenia Azure — tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 048f98aa-f708-44cb-9b9e-953f67dc6da8
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 5ad75394c40025d8941282eabeaf34c19c72ee1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-and-deploy-code-from-a-local-git-repository"></a>Tworzenie aplikacji sieci web i wdrażanie kodu z lokalnego repozytorium Git

Ten przykładowy skrypt tworzy aplikację sieci web w usłudze App Service z powiązane zasoby, a następnie wdraża kodu aplikacji sieci web w lokalnym repozytorium Git.


[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym temacie wymaga, że uruchamiasz hello Azure CLI w wersji 2.0 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/deploy-local-git/deploy-local-git.sh?highlight=3-5 "Create a web app and deploy code from a local Git repository")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi App Service. |
| [Tworzenie aplikacji sieci Web az](https://docs.microsoft.com/cli/azure/webapp#create) | Tworzenie aplikacji sieci web platformy Azure. |
| [ustawiono użytkownika wdrożenia aplikacji sieci Web az](https://review.docs.microsoft.com/cli/azure/webapp/deployment/user#set) | Ustawia poświadczenia wdrożenia na poziomie konta hello usługi aplikacji. |
| [Źródło wdrożenia az aplikacji sieci Web — config lokalnej — git](https://review.docs.microsoft.com/cli/azure/webapp/deployment/source#config-local-git) | Tworzy konfiguracji kontroli źródła dla lokalnego repozytorium Git. |
| [AZ przeglądania aplikacji sieci Web](https://docs.microsoft.com/cli/azure/webapp#browse) | Otwórz aplikację sieci web platformy Azure w przeglądarce. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [dokumentacji usługi Azure App Service](../app-service-cli-samples.md).
