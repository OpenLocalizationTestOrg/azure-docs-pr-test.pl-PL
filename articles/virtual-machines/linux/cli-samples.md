---
title: "aaaAzure przykłady interfejsu wiersza polecenia | Dokumentacja firmy Microsoft"
description: "Przykłady Azure CLI"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/08/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 776c947e6daca564242fc77b0527dcb124fa057d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-linux-virtual-machines"></a>Przykładów dla interfejsu wiersza polecenia platformy Azure dla maszyn wirtualnych systemu Linux

Witaj Poniższa tabela zawiera linki toobash skrypty utworzone przy użyciu interfejsu wiersza polecenia Azure hello.

| | |
|---|---|
|**Tworzenie maszyn wirtualnych**||
| [Utwórz maszynę wirtualną](./../scripts/virtual-machines-linux-cli-sample-create-vm-quick-create.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy maszynę wirtualną systemu Linux z minimalną konfiguracją. |
| [Utwórz maszynę wirtualną w pełni skonfigurowany](./../scripts/virtual-machines-linux-cli-sample-create-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy grupę zasobów, maszyny wirtualnej i wszystkie powiązane zasoby.|
| [Tworzenie maszyn wirtualnych o wysokiej dostępności](./../scripts/virtual-machines-linux-cli-sample-nlb.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy kilka maszyny wirtualne o wysokiej dostępności i konfiguracji równoważenia obciążenia. |
| [Tworzenie maszyny Wirtualnej z włączoną Docker](./../scripts/virtual-machines-linux-cli-sample-create-docker-host.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy maszynę wirtualną, konfiguruje tę maszynę Wirtualną jako hosta Docker i uruchamia kontener NGINX. |
| [Tworzenie maszyny Wirtualnej, a następnie uruchom skrypt konfiguracji](./../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy maszynę wirtualną i używa hello Azure niestandardowego skryptu rozszerzenia tooinstall NGINX. |
| [Utwórz maszynę Wirtualną z WordPress zainstalowany](./../scripts/virtual-machines-linux-cli-sample-create-vm-wordpress.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy maszynę wirtualną i używa hello Azure niestandardowego skryptu rozszerzenia tooinstall WordPress. |
| [Utwórz maszynę Wirtualną z dyskiem zarządzanym systemu operacyjnego](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json) | Tworzy maszynę wirtualną, dołączając istniejący dysk zarządzane jako dysk systemu operacyjnego. |
| [Tworzenie maszyny Wirtualnej z migawki](./../scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Tworzy maszynę wirtualną z migawki, najpierw tworząc dysków zarządzanych z migawki, a następnie Trwa dołączanie nowego dysku zarządzanego hello jako dysk systemu operacyjnego. |
|**Zarządzanie magazynem**||
| [Tworzenie dysku zarządzanego z wirtualnego dysku twardego](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json) | Tworzy dysków zarządzanych z specjalne wirtualny dysk twardy jako dysk systemu operacyjnego lub dane wirtualnego dysku twardego jako dysk danych.  |
| [Tworzenie dysku zarządzanego z migawki](../scripts/virtual-machines-linux-cli-sample-create-managed-disk-from-snapshot.md?toc=%2fcli%2fmodule%2ftoc.json) | Tworzy dysków zarządzanych z migawki. |
| [Kopiowanie dysków zarządzanych w toosame lub innej subskrypcji](../scripts/virtual-machines-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Zarządzane kopii dysku toosame lub innej subskrypcji, ale w hello sam region jako element nadrzędny hello zarządzane dysku. 
| [Eksportowanie migawki co konto magazynu tooa wirtualnego dysku twardego](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-storage-account.md?toc=%2fcli%2fmodule%2ftoc.json) | Eksportuje zarządzanych migawki co konto magazynu tooa wirtualnego dysku twardego w innym regionie. |
| [Kopiowanie migawek toosame lub innej subskrypcji](../scripts/virtual-machines-linux-cli-sample-copy-snapshot-to-same-or-different-subscription.md?toc=%2fcli%2fmodule%2ftoc.json) | Kopie migawki toosame lub innej subskrypcji, ale w hello sam region jako hello nadrzędnego migawki. |
|**Maszyny wirtualne sieci**||
| [Bezpieczny ruch sieciowy między maszynami wirtualnymi](./../scripts/virtual-machines-linux-cli-sample-create-vm-nsg.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy dwie maszyny wirtualne, wszystkich powiązanych zasobów i grup zabezpieczeń sieci wewnętrznych i zewnętrznych (NSG). |
|**Bezpieczne maszyny wirtualne**||
| [Szyfrowanie dysków maszyny Wirtualnej i danych](./../scripts/virtual-machines-linux-cli-sample-encrypt-vm.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy usługi Azure Key Vault, klucz szyfrowania i nazwy głównej usługi, a następnie szyfruje maszyny Wirtualnej. |
|**Monitorowanie maszyn wirtualnych**||
| [Monitor maszyny Wirtualnej w usłudze Operations Management Suite](./../scripts/virtual-machines-linux-cli-sample-create-vm-oms.md?toc=%2fcli%2fazure%2ftoc.json) | Tworzy maszynę wirtualną, instaluje agenta Operations Management Suite hello i rejestruje hello maszyny Wirtualnej w obszarze roboczym pakietu OMS.  |
|**Rozwiązywanie problemów z maszyn wirtualnych**||
| [Rozwiązywanie problemów z dyskiem systemu operacyjnego maszyny wirtualne](./../scripts/virtual-machines-linux-cli-sample-mount-os-disk.md?toc=%2fcli%2fazure%2ftoc.json) | Instaluje dysk systemu operacyjnego hello z jednej maszyny Wirtualnej jako dysk z danymi w drugiej maszyny Wirtualnej. |
| | |
