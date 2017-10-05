---
title: "Przykładowym skrypcie interfejsu wiersza polecenia Azure — wiązanie SSL niestandardowych certyfikatów aplikacji funkcja | Dokumentacja firmy Microsoft"
description: "Przykładowym skrypcie interfejsu wiersza polecenia Azure — wiązanie niestandardowe certyfikat SSL do aplikacji funkcji na platformie Azure"
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
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a>Powiązania niestandardowego certyfikatu SSL do aplikacji — funkcja

Ten przykładowy skrypt tworzy aplikacji funkcji w usłudze App Service z powiązane zasoby, a następnie wiąże certyfikatu SSL z niestandardowej nazwy domeny. Dla tego przykładu należy:

* Dostęp do strony konfiguracji DNS rejestratora domen.
* Nieprawidłowa. Plik PFX i jego hasło dla certyfikatu SSL chcesz przekazać i ich powiązania.

Aby powiązać certyfikatu SSL, można utworzyć aplikacji funkcji w planie usługi aplikacji, a nie w planie zużycia.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli zdecydujesz się zainstalować interfejs wiersza polecenia i korzystać z niego lokalnie, ten temat będzie wymagał interfejsu wiersza polecenia platformy Azure w wersji 2.0 lub nowszej. Uruchom polecenie `az --version`, aby dowiedzieć się, jaka wersja jest używana. Jeśli konieczna będzie instalacja lub uaktualnienie, zobacz [Instalowanie interfejsu wiersza polecenia platformy Azure 2.0]( /cli/azure/install-azure-cli). 

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[główne](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "wiązania niestandardowego certyfikatu SSL w aplikacji sieci web")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi aplikacji wymaganej do powiązania certyfikatów SSL. |
| [Utwórz az functionapp]() | Tworzy aplikację funkcji. |
| [Dodaj nazwę az usługi aplikacji sieci web konfiguracji hosta](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | Mapuje niestandardową domenę do funkcji aplikacji. |
| [AZ usługi aplikacji sieci web config ssl przekazywania](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | Przekazuje certyfikat SSL do aplikacji funkcji. |
| [powiązania ssl config az usługi aplikacji sieci web](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | Wiąże aplikacji funkcji przekazano certyfikat SSL. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [dokumentacji usługi Azure App Service]().
