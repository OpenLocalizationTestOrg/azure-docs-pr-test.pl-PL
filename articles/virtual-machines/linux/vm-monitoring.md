---
title: "Włączanie lub wyłączanie monitorowania maszyna wirtualna platformy Azure"
description: "Opisuje, jak włączyć lub wyłączyć monitorowanie maszyna wirtualna platformy Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: kmouss
manager: timlt
editor: 
ms.assetid: 6ce366d2-bd4c-4fef-a8f5-a3ae2374abcc
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/08/2016
ms.author: kmouss
ms.openlocfilehash: 9b2fe579113d6ca6bfd27d82eb9d4657657d44ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 07/11/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Włącz lub Wyłącz monitorowanie maszyna wirtualna platformy Azure

W tej sekcji opisano, jak włączyć lub wyłączyć monitorowanie w przypadku maszyn wirtualnych działających na platformie Azure. Można włączyć lub wyłączyć monitorowanie za pomocą portalu lub interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (Azure CLI).

> [!IMPORTANT]
> Ten dokument zawiera opis wersji 2.3 rozszerzenia diagnostyczne systemu Linux, która została wycofana. Wersja 2.3 będzie obsługiwana do 30 czerwca 2018.
>
> Zamiast tego można włączyć w wersji 3.0 rozszerzenia diagnostyczne systemu Linux. Aby uzyskać więcej informacji, zobacz [dokumentacji](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-the-azure-portal"></a>Włącz / Wyłącz monitorowanie za pomocą portalu Azure

Umożliwia monitorowanie maszyny Wirtualnej Azure, która zapewnia dane dotyczące wystąpienia w okresach 1 minutę. (dotyczy zmiany magazynu). Dane diagnostyczne szczegółowe jest dostępna dla maszyny Wirtualnej w portalu wykresy lub za pośrednictwem interfejsu API. Domyślnie portalu Azure umożliwia oparta na hoście monitorowanie określonych metryk. Umożliwia monitorowanie pomiarów w maszynie Wirtualnej uruchomionej maszyny Wirtualnej lub w stanie zatrzymania.

* Otwórz portal Azure w [https://portal.azure.com](https://portal.azure.com).
* Na lewym pasku nawigacyjnym kliknij maszyn wirtualnych.
* Na maszynach wirtualnych listy wybierz wystąpienie uruchamiania i zatrzymywana. Zostanie otwarty blok "Maszyny wirtualnej".
* Kliknij pozycję wszystkie ustawienia.
* Kliknij pozycję Diagnostyka.
* Zmiana stanu na włączony lub wyłączony. Można również wybrać w tym bloku poziom monitorowania szczegóły, które chcesz włączyć maszyny wirtualnej.

![Włącz / Wyłącz monitorowanie za pomocą portalu Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Włącz / Wyłącz monitorowanie za pomocą interfejsu wiersza polecenia platformy Azure

Aby włączyć monitorowanie dla maszyny Wirtualnej platformy Azure.

* Utwórz plik (nazwanych takich jak PrivateConfig.json):

```json
{
        "storageAccountName":"the storage account to receive data",
        "storageAccountKey":"the key of the account"
}
```

* Włącz rozszerzenia za pomocą wiersza polecenia platformy Azure.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Aby uzyskać więcej informacji, zobacz [przy użyciu systemu Linux diagnostycznych rozszerzenia Monitor systemu Linux VM wydajności i danych diagnostycznych](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
