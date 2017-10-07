---
title: "aaaEnable lub wyłączenie monitorowania maszyny Wirtualnej Azure"
description: "Opisuje sposób tooEnable lub Wyłącz monitorowanie maszyny Wirtualnej Azure"
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
ms.openlocfilehash: 39c2211e4e5f3ad364513b52c5acc70c00b432fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-or-disable-azure-vm-monitoring"></a>Włącz lub Wyłącz monitorowanie maszyna wirtualna platformy Azure

W tej sekcji opisano, jak tooenable lub wyłączania monitorowania na wirtualnej maszyny działających na platformie Azure. Można włączyć lub wyłączyć monitorowanie za pomocą portalu hello lub interfejsu wiersza polecenia platformy Azure dla komputerów Mac, Linux i Windows (hello Azure CLI).

> [!IMPORTANT]
> Ten dokument zawiera opis wersji 2.3 hello diagnostycznych rozszerzenia systemu Linux, która została wycofana. Wersja 2.3 będzie obsługiwana do 30 czerwca 2018.
>
> Zamiast tego można włączyć w wersji 3.0 hello rozszerzenia diagnostyczne systemu Linux. Aby uzyskać więcej informacji, zobacz [hello dokumentacji](./diagnostic-extension.md).

## <a name="enable--disable-monitoring-through-hello-azure-portal"></a>Włącz / Wyłącz monitorowanie za pomocą hello portalu Azure

Umożliwia monitorowanie maszyny Wirtualnej Azure, która zapewnia dane dotyczące wystąpienia w okresach 1 minutę. (dotyczy zmiany magazynu). Dane diagnostyczne szczegółowe jest dostępna dla hello maszyny Wirtualnej w portalu wykresy hello lub za pośrednictwem hello interfejsu API. Domyślnie portalu Azure umożliwia oparta na hoście monitorowanie określonych metryk. Umożliwia monitorowanie pomiarów w maszynie Wirtualnej podczas powitalne maszyna wirtualna jest uruchomiona lub zatrzymana.

* Otwórz hello Azure w portalu [https://portal.azure.com](https://portal.azure.com).
* Lewy pasek nawigacyjny hello kliknij maszyn wirtualnych.
* W przypadku hello listy maszyn wirtualnych należy wybrać wystąpienie uruchamiania i zatrzymywana. zostanie otwarty blok "Maszyny wirtualnej" Hello.
* Kliknij pozycję wszystkie ustawienia.
* Kliknij pozycję Diagnostyka.
* Zmień stan tooOn lub wyłączona. Możesz również wybrać na tym poziomie hello bloku monitorowania szczegóły chcesz tooenable dla maszyny wirtualnej.

![Włącz / Wyłącz monitorowanie za pomocą hello portalu Azure.][1]

## <a name="enable--disable-monitoring-with-azure-cli"></a>Włącz / Wyłącz monitorowanie za pomocą interfejsu wiersza polecenia platformy Azure

tooenable monitorowanie dla maszyny Wirtualnej platformy Azure.

* Utwórz plik (nazwanych takich jak PrivateConfig.json):

```json
{
        "storageAccountName":"hello storage account tooreceive data",
        "storageAccountKey":"hello key of hello account"
}
```

* Włącz rozszerzenia hello za pomocą wiersza polecenia platformy Azure.

```azurecli
azure vm extension set myvm LinuxDiagnostic Microsoft.OSTCExtensions 2.3 --private-config-path PrivateConfig.json
```

Aby uzyskać więcej informacji, zobacz [przy użyciu rozszerzenia diagnostycznych Linux tooMonitor maszyny Wirtualnej systemu Linux na wydajność i danych diagnostycznych](classic/diagnostic-extension-v2.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json).

<!--Image references-->
[1]: ./media/vm-monitoring/portal-enable-disable.png
