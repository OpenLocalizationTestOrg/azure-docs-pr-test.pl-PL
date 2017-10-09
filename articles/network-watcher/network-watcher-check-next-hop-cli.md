---
title: "Następny przeskok aaaFind z Azure sieci obserwatora następnego przeskoku - Azure CLI 2.0 | Dokumentacja firmy Microsoft"
description: "W tym artykule opisano, jak i można znaleźć jakie hello następnego przeskoku typu jest przy użyciu adresu ip następnego przeskoku przy użyciu wiersza polecenia platformy Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0700c274-3e0d-4dca-acfa-3ceac8990613
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 77c2bde51274bd5c64e7a2467f95139af620ca30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="find-out-what-hello-next-hop-type-is-using-hello-next-hop-capability-in-azure-network-watcher-using-azure-cli-20"></a>Dowiedz się hello Typ następnego przeskoku jest przy użyciu możliwości następnego przeskoku hello w obserwatora sieciowego Azure używa interfejsu wiersza polecenia platformy Azure w wersji 2.0

> [!div class="op_single_selector"]
> - [Witryna Azure Portal](network-watcher-check-next-hop-portal.md)
> - [PowerShell](network-watcher-check-next-hop-powershell.md)
> - [Interfejs wiersza polecenia 1.0](network-watcher-check-next-hop-cli-nodejs.md)
> - [Interfejs wiersza polecenia 2.0](network-watcher-check-next-hop-cli.md)
> - [Interfejs API Azure REST](network-watcher-check-next-hop-rest.md)

Następny przeskok jest funkcją obserwatora sieciowego, która umożliwia określenie hello uzyskać typ następnego przeskoku hello i adresu IP na podstawie określonej maszyny wirtualnej. Ta funkcja jest przydatna przy określaniu, jeśli ruchu wychodzącego maszyny wirtualnej są przesyłane za pośrednictwem bramy, Internetu lub sieci wirtualne tooget tooits docelowego.

W tym artykule wykorzystano naszej nowej generacji interfejsu wiersza polecenia model wdrażania hello zasobów management, Azure CLI 2.0, który jest dostępny dla systemu Windows, Mac i Linux.

Witaj tooperform kroków w tym artykule, należy za[zainstalować hello interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI)](https://docs.microsoft.com/en-us/cli/azure/install-az-cli2).

## <a name="before-you-begin"></a>Przed rozpoczęciem

W tym scenariuszu użyje hello Azure CLI toofind hello Typ następnego przeskoku i adres IP.

W tym scenariuszu przyjęto zostały już wykonane kroki hello [utworzyć obserwatora sieciowego](network-watcher-create.md) toocreate obserwatora sieciowego. Scenariusz Hello również założono, że grupa zasobów o prawidłową maszynę wirtualną istnieje toobe używane.

## <a name="scenario"></a>Scenariusz

Scenariusz Hello omówione w tym artykule używa następnego przeskoku, funkcja obserwatora sieciowego, który znajduje się typ następnego przeskoku hello i adres IP dla każdego zasobu. odwiedź stronę toolearn więcej informacji na temat następnego przeskoku [następnego przeskoku omówienie](network-watcher-next-hop-overview.md).


## <a name="get-next-hop"></a>Pobierz następnego skoku

tooget hello następnego przeskoku nazywamy hello `az network watcher show-next-hop` polecenia cmdlet. Grupa zasobów hello polecenia cmdlet hello obserwatora sieciowego, hello NetworkWatcher maszynę wirtualną identyfikator, źródłowego adresu IP i docelowy adres IP jest przekazywana. W tym przykładzie hello docelowy adres IP jest tooa maszyny Wirtualnej w innej sieci wirtualnej. Między dwiema sieciami wirtualnymi hello jest bramy sieci wirtualnej.

Jeśli nie zostało jeszcze, instalowania i konfigurowania hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login). Następnie uruchom następujące polecenie hello:

```azurecli
az network watcher show-next-hop --resource-group <resourcegroupName> --vm <vmNameorID> --source-ip <source-ip> --dest-ip <destination-ip>

```

> [!NOTE]
Jeśli hello maszyna wirtualna ma wiele kart sieciowych i przesyłanie dalej IP jest włączona na żadnym z hello kart sieciowych, hello parametru karty Sieciowej (-i identyfikator karty sieciowej) musi być określona. W przeciwnym razie jest opcjonalne.

## <a name="review-results"></a>Przejrzyj wyniki

Po zakończeniu hello wyniki są dostarczane. oraz hello typ zasobu, który jest zwracany jest adres IP następnego przeskoku Hello.

```azurecli
{
    "nextHopIpAddress": null,
    "nextHopType": "Internet",
    "routeTableId": "System Route"
}
```

Witaj Poniższa lista zawiera aktualnie dostępne wartości Typ następnego przeskoku hello:

**Typ następnego przeskoku**

* Internet
* VirtualAppliance
* VirtualNetworkGateway
* VnetLocal
* HyperNetGateway
* VnetPeering
* Brak

## <a name="next-steps"></a>Następne kroki

Dowiedz się, jak tooreview ustawieniami grupy zabezpieczeń sieci programowo, odwiedzając [NSG inspekcji z obserwatora sieciowego](network-watcher-nsg-auditing-powershell.md)
