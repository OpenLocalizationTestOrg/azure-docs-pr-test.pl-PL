---
title: "kod zarządzany platformy Azure na dysku dla kopii zapasowej aaaCopy | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate kopię toouse Azure zarządzanych dysku dla dysku z powrotem się lub rozwiązywania problemów problemy."
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 2/6/2017
ms.author: rasquill
ms.openlocfilehash: 41b91c2d68eb5be9c493a66be5f7d085a70450d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a>Utwórz kopię plik VHD przechowywany jako dysk zarządzane Azure przy użyciu migawek zarządzane
Migawki zarządzane dysku do utworzenia kopii zapasowej lub tworzenie dysku zarządzanego z migawki hello i dołącz je tooa test maszyny wirtualnej tootroubleshoot. Zarządzane migawki jest kopią pełnej w momencie zarządzane dysku maszyny Wirtualnej. Tworzy kopię tylko do odczytu z wirtualnego dysku twardego i, domyślnie zapisuje go jako dysk standardowy zarządzane. 

Aby uzyskać informacje o cenach, zobacz [cennik usługi Azure Storage](https://azure.microsoft.com/pricing/details/managed-disks/). <!--Add link tootopic or blog post that explains managed disks. -->

Użyj albo hello Azure portalu lub hello Azure CLI 2.0 tootake migawkę hello dysku zarządzanego.

## <a name="use-azure-cli-20-tootake-a-snapshot"></a>Użyj tootake Azure CLI 2.0 migawki

> [!NOTE] 
> Witaj poniższy przykład wymaga hello Azure CLI 2.0 zainstalowany, a zalogowany do konta platformy Azure.

Witaj poniższej procedurze pokazano, jak tooobtain i wykonaj migawkę zarządzanych systemu operacyjnego na dysku za pomocą hello `az snapshot create` z hello `--source-disk` parametru. Hello poniższym przykładzie założono, że istnieje maszyna wirtualna o nazwie `myVM` utworzone za pomocą zarządzanego dysku systemu operacyjnego w hello `myResourceGroup` grupy zasobów.

```azure-cli
# take hello disk id with which toocreate a snapshot
osDiskId=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
az snapshot create -g myResourceGroup --source "$osDiskId" --name osDisk-backup
```

dane wyjściowe Hello powinny wyglądać mniej więcej tak:

```json
{
  "accountType": "Standard_LRS",
  "creationData": {
    "createOption": "Copy",
    "imageReference": null,
    "sourceResourceId": null,
    "sourceUri": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/disks/osdisk_6NexYgkFQU",
    "storageAccountId": null
  },
  "diskSizeGb": 30,
  "encryptionSettings": null,
  "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup/providers/Microsoft.Compute/snapshots/osDisk-backup",
  "location": "westus",
  "name": "osDisk-backup",
  "osType": "Linux",
  "ownerId": null,
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "tags": null,
  "timeCreated": "2017-02-06T21:27:10.172980+00:00",
  "type": "Microsoft.Compute/snapshots"
}
```

## <a name="use-azure-portal-tootake-a-snapshot"></a>Użyj tootake portalu Azure migawki 

1. Zaloguj się toohello [portalu Azure](https://portal.azure.com).
2. Począwszy od lewej górnej powitania kliknij **nowy** i wyszukaj **migawki**.
3. W bloku migawki powitania kliknij **Utwórz**.
4. Wprowadź **nazwa** hello migawki.
5. Wybierz istniejący [grupy zasobów](../../azure-resource-manager/resource-group-overview.md#resource-groups) lub nazwa typu hello nowej. 
6. Wybierz centrum danych Azure lokalizacji.  
7. Aby uzyskać **dysku źródłowego**, wybierz hello toosnapshot dysku zarządzanego.
8. Wybierz hello **typ konta** toouse toostore hello migawki. Firma Microsoft zaleca **Standard_LRS** chyba że ma być przechowywane na dysku wysokiej wydajności.
9. Kliknij przycisk **Utwórz**.

Jeśli planujesz toouse hello migawki toocreate dysku zarządzanego dołączyć maszynę Wirtualną, która wymaga wydajnych toobe, użyj parametru hello `--sku Premium_LRS` z hello `az snapshot create` polecenia. Spowoduje to utworzenie migawki hello tak, aby była przechowywana jako dysk zarządzane Premium. Dysków zarządzanych w warstwie Premium działać lepiej, ponieważ są dysków półprzewodnikowych (SSD), ale są droższe niż dyski standardowe (HDD).


