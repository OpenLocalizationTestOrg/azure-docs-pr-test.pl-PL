---
title: "aaaAzure przykładowym skrypcie interfejsu wiersza polecenia — wdrażanie hello stosu światła w zestawie skalowania Machin wirtualna Load-Balanced | Dokumentacja firmy Microsoft"
description: "Użyj skryptu niestandardowego rozszerzenia toodeploy hello stosu światła w przypadku obciążenia = skali maszyny wirtualnej ze zrównoważonym ustawiony na platformie Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a>Wdrażanie hello stosu światła w zestawie skalowania maszyn wirtualnych z równoważeniem obciążenia

W tym przykładzie tworzy zestaw skali maszyny wirtualnej i stosuje rozszerzenie, które działa na każdej maszynie wirtualnej w zestawie skalowania hello stosu światła hello toodeploy skryptu niestandardowego.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a>Przykładowy skrypt

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a>Połączenie

Użyj tego toosee kodu sposobu tooyour tooconnect maszyn wirtualnych i na skalę.

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a>Czyszczenie wdrożenia 

Uruchom hello następujące grupy zasobów hello tooremove polecenia, zestaw skali hello i maszyn wirtualnych oraz wszystkie powiązane zasoby.

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a>Wyjaśnienie skryptu

Ten skrypt używa hello następujące polecenia toocreate grupę zasobów, maszyny wirtualnej zestawu dostępności, usługi równoważenia obciążenia i wszystkie powiązane zasoby. Każde polecenie w tabeli hello łączy toocommand szczegółowej dokumentacji.

| Polecenie | Uwagi |
|---|---|
| [Tworzenie grupy az](https://docs.microsoft.com/cli/azure/group#create) | Tworzy grupę zasobów, w którym przechowywane są wszystkie zasoby. |
| [Utwórz az vmss](https://docs.microsoft.com/cli/azure/vmss#create) | Tworzy zestaw skali maszyny wirtualnej |
| [Utwórz regułę równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Dodaj punkt końcowy równoważeniem obciążenia |
| [Ustaw rozszerzenie vmss az](https://docs.microsoft.com/cli/azure/vmss/extension#set) | Tworzenie rozszerzenia hello, uruchamiany skryptu niestandardowego hello podczas wdrażania maszyny wirtualnej |
| [Aktualizacja vmss az-wystąpienia](https://docs.microsoft.com/cli/azure/vmss#update-instances) | Uruchom skrypt niestandardowych hello na hello wystąpień maszyn wirtualnych, które zostały wdrożone przed zastosowaniem hello rozszerzenia zestawu skali toohello. |
| [AZ vmss skali](https://docs.microsoft.com/cli/azure/vmss#scale) | Skalowanie w górę hello skali, dodając więcej wystąpień maszyny Wirtualnej. skryptu niestandardowego Hello jest uruchamiane na te, gdy są one wdrażane. |
| [Lista ip publicznej sieci az](https://docs.microsoft.com/cli/azure/network/public-ip#list) | Uzyskaj adresy IP hello hello maszyny wirtualne utworzone przez hello próbki. |
| [Pokaż równoważeniem obciążenia sieciowego az](https://docs.microsoft.com/cli/azure/network/lb#show) | Pobierz hello frontonu i zaplecza porty używane przez hello równoważenia obciążenia. |

## <a name="next-steps"></a>Następne kroki

Aby uzyskać więcej informacji na powitania wiersza polecenia platformy Azure, zobacz [dokumentacji interfejsu wiersza polecenia Azure](https://docs.microsoft.com/cli/azure/overview).

Przykłady skryptów CLI dodatkowe maszyny wirtualnej znajdują się w hello [dokumentacji maszyny Wirtualnej systemu Linux Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
