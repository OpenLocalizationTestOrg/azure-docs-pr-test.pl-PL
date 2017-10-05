---
title: "Azure CLI przykładowym skrypcie - kierować ruchem wysoką dostępność aplikacji | Dokumentacja firmy Microsoft"
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
ms.openlocfilehash: 0593d063a4935d02aae124d83b62b11e37aa3c33
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-for-high-availability-of-applications"></a>Kierować ruchem wysoką dostępność aplikacji

Ten skrypt tworzy grupę zasobów, dwa planów usługi aplikacji, dwie aplikacje sieci web, profilu Menedżera ruchu i dwa punkty końcowe Menedżera ruchu. Menedżer ruchu kieruje ruch do aplikacji w jednym regionie jako regionu podstawowego, a w regionie pomocniczym, gdy aplikacja w regionie podstawowym jest niedostępny. Przed wykonaniem skryptu, należy zmienić wartości MyWebApp, MyWebAppL1 i MyWebAppL2 unikatowych wartości na platformie Azure. Po uruchomieniu skryptu, można uzyskać dostępu do aplikacji w regionie podstawowym z mywebapp.trafficmanager.net adresu URL.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[główne](../../../cli_scripts/traffic-manager/direct-traffic-for-increased-application-availability/direct-traffic-for-increased-application-availability.sh "kierować ruchem w celu zapewnienia wysokiej dostępności")]


## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Po uruchomieniu przykładowym skrypcie, wykonaj polecenie może służyć do usunięcia grupy zasobów, aplikacji usługi app Service i wszystkie powiązane zasoby.

```azurecli
az group delete --name myResourceGroup1 --yes
az group delete --name myResourceGroup2 --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa następujących poleceń do utworzenia grupy zasobów, aplikacji sieci web profilu Menedżera ruchu i wszystkie powiązane zasoby. Każde polecenie w tabeli łącza do dokumentacji określonego polecenia.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie planu usług aplikacji az](https://docs.microsoft.com/cli/azure/appservice/plan#create) | Tworzy plan usługi App Service. Przypomina farmy serwerów aplikacji sieci web platformy Azure. |
| [Utwórz az appservice w sieci web](https://docs.microsoft.com/cli/azure/appservice/web#create) | Tworzy aplikację sieci web platformy Azure w ramach planu usługi aplikacji. |
| [Utwórz profil Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) | Tworzy profil Menedżera ruchu Azure. |
| [Tworzenie punktu końcowego Menedżera ruchu sieciowego az](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) | Dodaje punkt końcowy profilu Menedżera ruchu Azure. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji dotyczących interfejsu wiersza polecenia Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Dodatkowe przykłady skryptów aplikacji usługi interfejsu wiersza polecenia można znaleźć w [Azure Networking dokumentacji](../cli-samples.md).
