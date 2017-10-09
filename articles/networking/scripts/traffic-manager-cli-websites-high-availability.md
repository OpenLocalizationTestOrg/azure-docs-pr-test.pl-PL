---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia - kierować ruchem wysoką dostępność aplikacji | Dokumentacja firmy Microsoft"
description: "Azure CLI przykładowym skrypcie - kierować ruchem wysoką dostępność aplikacji"
services: traffic-manager
documentationcenter: traffic-manager
author: KumudD
manager: timlt
editor: tysonn
tags: azure-infrastructure
ms.assetid: 
ms.service: traffic-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: traffic-manager
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 2142c8bbec1dffc2f12b5500df142a429393a145
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Kierować ruchem wysoką dostępność aplikacji

Ten skrypt tworzy grupę zasobów, dwa planów usługi aplikacji, dwie aplikacje sieci web, profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu. Menedżera ruchu kieruje ruch toohello aplikacji w jeden region jako hello regionu podstawowego, a region pomocniczy toohello, gdy aplikacja hello w regionie podstawowym hello jest niedostępna. Przed wykonaniem skryptu hello, musisz zmienić hello MyWebApp, MyWebAppL1 i MyWebAppL2 wartości toounique wartości w obrębie platformy Azure. Po uruchomieniu skryptu hello, można uzyskać dostępu do aplikacji hello w regionie podstawowym hello z hello mywebapp.trafficmanager.net adresu URL.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "Route traffic for high availability")]


## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Po uruchomieniu przykładowym skrypcie hello hello wykonaj polecenie może być grupy zasobów hello tooremove używanych aplikacji usługi app Service i wszystkie powiązane zasoby.

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, aplikacji sieci web, profilu Menedżera ruchu, a wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi App Service. Przypomina farmy serwerów aplikacji sieci web platformy Azure. |
| [Utwórz az appservice w sieci web](https://docs.microsoft.com/cli/azure/appservice/web#create) | Tworzy aplikację sieci web platformy Azure w ramach hello planu usługi aplikacji. |
| [Utwórz profil Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Tworzy profil Menedżera ruchu Azure. |
| [Tworzenie punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Dodaje tooan punktu końcowego profilu Menedżera ruchu Azure. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w hello [Azure Networking dokumentacji](../cli-samples.md).
