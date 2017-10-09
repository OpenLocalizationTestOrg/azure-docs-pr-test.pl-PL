---
title: aaaRedeploy maszyn wirtualnych systemu Linux na platformie Azure | Dokumentacja firmy Microsoft
description: "Jak problemy z maszyn wirtualnych systemu Linux tooredeploy w Azure toomitigate połączenia SSH."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
tags: azure-resource-manager,top-support-issue
ms.assetid: e9530dd6-f5b0-4160-b36b-d75151d99eb7
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: support-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/23/2017
ms.author: iainfou
ms.openlocfilehash: 9adfd1b11f262d362133366b2bba5e69c70c9b82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="redeploy-linux-virtual-machine-toonew-azure-node"></a>Należy ponownie wdrożyć toonew maszyny wirtualnej systemu Linux platformy Azure węzła
Ponowne rozmieszczanie hello maszyny Wirtualnej może pomóc w pokonywaniu trudności Rozwiązywanie problemów z SSH lub aplikacja dostęp do maszyny wirtualnej systemu Linux tooa (VM) na platformie Azure. Podczas ponownego wdrażania maszyny Wirtualnej przenosi do nowego węzła tooa hello maszyny Wirtualnej w ramach hello infrastruktury platformy Azure i uprawnień go ponownie. Opcje konfiguracji i skojarzonych zasobów są zachowywane. W tym artykule opisano sposób tooredeploy a maszyny Wirtualnej przy użyciu wiersza polecenia platformy Azure lub hello portalu Azure.

> [!NOTE]
> Po ponownego wdrażania maszyny Wirtualnej, dysku tymczasowym hello zostaną utracone i dynamicznych adresów IP skojarzonych z interfejsu sieci wirtualnej zostały zaktualizowane. 

Można wdrożyć ponownie Maszynę wirtualną przy użyciu jednej z hello następujące opcje. Wystarczy tylko jeden tooredeploy opcji toochoose maszyny Wirtualnej:

- [Interfejs wiersza polecenia platformy Azure 2.0](#azure-cli-20)
- [Interfejs wiersza polecenia platformy Azure 1.0](#azure-cli-10)
- [Witryna Azure Portal](#using-azure-portal)

## <a name="use-hello-azure-cli-20"></a>Użyj hello Azure CLI 2.0
Najnowsza wersja hello instalacji [Azure CLI 2.0](/cli/azure/install-az-cli2) i zaloguj się za pomocą konta Azure tooan [logowania az](/cli/azure/#login).

Wdrożenie maszyny Wirtualnej z [ponownego wdrażania maszyny wirtualnej az](/cli/azure/vm#redeploy). powitania po wdraża ponownie przykład Witaj maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:

```azurecli
az vm redeploy --resource-group myResourceGroup --name myVM 
```

## <a name="use-hello-azure-cli-10"></a>Użyj hello Azure CLI w wersji 1.0
Zainstaluj hello [najnowsze Azure CLI 1.0](../../cli-install-nodejs.md), zaloguj się za tooan konto platformy Azure i upewnij się, że jesteś w trybie Menedżera zasobów (`azure config mode arm`).

powitania po wdraża ponownie przykład Witaj maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:

```azurecli
azure vm redeploy --resource-group myResourceGroup --vm-name myVM 
```

[!INCLUDE [virtual-machines-common-redeploy-to-new-node](../../../includes/virtual-machines-common-redeploy-to-new-node.md)]

## <a name="next-steps"></a>Następne kroki
Jeśli występują problemy dotyczące łączenia tooyour maszyny Wirtualnej, można znaleźć pomoc w [Rozwiązywanie problemów z połączeniami SSH](troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) lub [szczegółowe kroki rozwiązywania problemów SSH](detailed-troubleshoot-ssh-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Jeśli nie można uzyskać dostęp do aplikacji działających na maszynie Wirtualnej, możesz przeczytać [aplikacji Rozwiązywanie problemów z](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

