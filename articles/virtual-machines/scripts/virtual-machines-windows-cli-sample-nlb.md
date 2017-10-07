---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — Utwórz Maszynę wirtualną systemu Windows Server 2016 z równoważeniem obciążenia Sieciowego | Dokumentacja firmy Microsoft"
description: "Azure CLI skrypt przykładowy — Utwórz Maszynę wirtualną systemu Windows Server 2016 z równoważeniem obciążenia Sieciowego"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: aaaac0c2cc32ce0cac21417926399d848bd6fa09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a>Ruch Równoważenie obciążenia między maszynami wirtualnymi wysokiej dostępności

Ten przykładowy skrypt tworzy wszystko, co jest potrzebne toorun kilka maszyny wirtualnej systemu Ubuntu skonfigurowany w wysokiej dostępności i załadować zrównoważonym konfiguracji. Po uruchamianie skryptu hello, będzie mieć trzy maszyny wirtualne, połączone tooan zestawu dostępności Azure i jest dostępny za pośrednictwem usługi równoważenia obciążenia Azure.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-windows-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Hello uruchom następujące polecenie, grupy zasobów hello tooremove, maszyny Wirtualnej i wszystkich powiązanych zasobów.

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, maszyny wirtualnej zestawu dostępności, usługi równoważenia obciążenia i wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Tworzenie sieci wirtualnej sieci az](https://docs.microsoft.com/cli/azure/network/vnet#create) | Tworzy sieć wirtualna platformy Azure i podsieć. |
| [Tworzenie sieci az publicznego ip](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Tworzy publiczny adres IP z statyczny adres IP i skojarzonej nazwy DNS. |
| [Utwórz równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb#create) | Tworzy Azure Usługa równoważenia obciążenia sieciowego (NLB). |
| [Utwórz sondowania równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Tworzy badanie równoważenia obciążenia Sieciowego. Sonda równoważenia obciążenia Sieciowego jest używane toomonitor każdej maszyny Wirtualnej w zestawie równoważenia obciążenia Sieciowego hello. Jeśli żadnej maszyny Wirtualnej staje się niedostępny, ruch nie jest kierowany toohello maszyny Wirtualnej. |
| [Utwórz regułę równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Tworzy regułę równoważenia obciążenia Sieciowego. W tym przykładzie jest tworzona reguła dla portu 80. Ruch HTTP dociera hello równoważenia obciążenia Sieciowego, jest kierowany tooport 80 jednej z maszyn wirtualnych hello hello zestawu równoważenia obciążenia Sieciowego. |
| [Utwórz az sieci lb ruchu przychodzącego translatora adresów sieciowych — reguł](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Tworzy regułę równoważenia obciążenia Sieciowego translatora adresów sieciowych (NAT).  Reguły NAT mapować port hello portu tooa równoważenia obciążenia Sieciowego na maszynie Wirtualnej. W tym przykładzie tworzona jest reguła NAT dla tooeach ruchu SSH maszyny Wirtualnej w zestawie równoważenia obciążenia Sieciowego hello.  |
| [Tworzenie grupy nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg#create) | Tworzy sieciową grupę zabezpieczeń (NSG), czyli granicę zabezpieczeń między hello internet i hello maszyny wirtualnej. |
| [Tworzenie reguły nsg sieci az](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Tworzy grupy NSG tooallow reguły ruchu przychodzącego. W tym przykładzie port 22 jest otwarty dla ruchu protokołu SSH. |
| [Utwórz az kart interfejsu sieciowego](https://docs.microsoft.com/cli/azure/network/nic#create) | Tworzy karty sieci wirtualnej i dołącza go w sieci wirtualnej toohello, podsieci i NSG. |
| [Tworzenie maszyny wirtualnej az zestawu dostępności](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Tworzy zestaw dostępności. Zestawy dostępności upewnij się, czas działania aplikacji poprzez rozłożenie zasobów fizycznych hello maszyny wirtualnej tak, aby w przypadku niepowodzenia hello cały zestaw nie jest wykonywane. |
| [Tworzenie maszyny wirtualnej az](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Tworzy maszynę wirtualną hello i łączy go toohello karty sieciowej, sieć wirtualną, podsieci i NSG. To polecenie określa również toobe obrazu maszyny wirtualnej hello używane i poświadczenia administracyjne.  |
| [Usuwanie grupy az](https://docs.microsoft.com/cli/azure/vm/extension#set) | Usuwa grupę zasobów, w tym wszystkich zagnieżdżonych zasobów. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Windows Azure](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
