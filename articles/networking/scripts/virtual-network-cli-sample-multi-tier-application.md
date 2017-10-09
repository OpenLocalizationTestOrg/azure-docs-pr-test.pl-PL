---
title: "aaaAzure interfejsu wiersza polecenia skryptu przykładowe — tworzenie sieci dla aplikacji wielowarstwowych | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — tworzenie sieci wirtualnej dla aplikacji wielowarstwowych."
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>Tworzenie sieci dla aplikacji wielowarstwowych

Ten przykładowy skrypt tworzy sieć wirtualną z podsieci frontonu i zaplecza. Podsieci frontonu toohello ruchu jest ograniczony tooHTTP i SSH, podczas toohello ruchu podsieci wewnętrznej jest ograniczona tooMySQL, port 3306. Po uruchamianie skryptu hello masz dwie maszyny wirtualne, w każdej podsieci, którą można wdrożyć serwera sieci web i MySQL oprogramowania.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a>Przykładowy skrypt


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa powitania po toocreate poleceń, grupy zasobów, sieci wirtualnej i grup zabezpieczeń sieci. Każde polecenie w dokumentacji konkretnego toocommand łącza tabeli hello.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet#create) | Tworzy sieć wirtualna platformy Azure i podsieci frontonu. |
| [Utwórz podsieć sieci az](/cli/azure/network/vnet/subnet#create) | Tworzy podsieć zaplecza. |
| [Tworzenie sieci az publicznego ip](/cli/azure/network/public-ip#create) | Tworzy publicznego adresu IP adres tooaccess hello maszyny Wirtualnej na podstawie hello Internet. |
| [Utwórz az kart interfejsu sieciowego](/cli/azure/network/nic#create) | Tworzy interfejsy sieci wirtualnej i dołącza je podsieci sieci wirtualnej toohello frontonu i zaplecza. |
| [Tworzenie grupy nsg sieci az](/cli/azure/network/nsg#create) | Tworzy grupy zabezpieczeń sieci (NSG), które są skojarzone toohello podsieci frontonu i zaplecza. |
| [Tworzenie reguły nsg sieci az](/cli/azure/network/nsg/rule#create) |Tworzy reguły NSG, które zezwala lub blokuje określone porty toospecific podsieci. |
| [Tworzenie maszyny wirtualnej az](/cli/azure/vm#create) | Tworzy maszyny wirtualne i dołącza tooeach karty Sieciowej maszyny Wirtualnej. To polecenie określa również toouse obrazu maszyny wirtualnej hello i poświadczenia administracyjne. |
| [Usuwanie grupy az](/cli/azure/group#delete) | Usuwa grupę zasobów i wszystkie zasoby, które zawiera. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](/cli/azure/overview).

Dodatkowe przykłady skryptów sieci interfejsu wiersza polecenia można znaleźć w hello [Azure Przegląd dokumentacji](../cli-samples.md)
