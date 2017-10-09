---
title: "aaaCreate i zarządzania maszynami wirtualnymi w usłudze DevTest Labs z wiersza polecenia platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate Azure DevTest Labs toouse i zarządzania maszynami wirtualnymi Azure CLI 2.0"
services: devtest-lab,virtual-machines
documentationcenter: na
author: lisawong19
manager: douge
editor: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/19/2017
ms.author: liwong
ms.openlocfilehash: 98ea3aa7b2489bff61971573aaf584984cd811e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-virtual-machines-with-devtest-labs-using-hello-azure-cli"></a>Tworzenie i zarządzanie maszynami wirtualnymi z DevTest Labs przy użyciu hello wiersza polecenia platformy Azure
To szybki start przeprowadzi użytkownika przez proces tworzenia, uruchamiania, połączenie, aktualizowanie i czyszczenia komputera Programowanie w laboratorium. 

Przed rozpoczęciem:

* Jeśli laboratorium nie został utworzony, można znaleźć instrukcje [tutaj](devtest-lab-create-lab.md).

* [Zainstaluj interfejs wiersza polecenia 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). toostart, uruchom az toocreate logowania połączenia z platformą Azure. 

## <a name="create-and-verify-hello-virtual-machine"></a>Tworzenie i sprawdź hello maszyny wirtualnej 
Utwórz maszynę Wirtualną z obrazu z witryny marketplace z ssh uwierzytelniania.
```azurecli
az lab vm create --lab-name sampleLabName --resource-group sampleLabResourceGroup --name sampleVMName --image "Ubuntu Server 16.04 LTS" --image-type gallery --size Standard_DS1_v2 --authentication-type  ssh --generate-ssh-keys --ip-configuration public 
```
> [!NOTE]
> Umieść hello **grupy zasobów w laboratorium** nazwie w hello — parametr grupy zasobów.
>

Toocreate Maszynę wirtualną przy użyciu formuły, należy użyć hello — parametr formuły w [tworzenia maszyny wirtualnej laboratorium az](https://docs.microsoft.com/cli/azure/lab/vm#create).


Sprawdź, czy ten hello maszyny Wirtualnej jest dostępna.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand 'properties($expand=ComputeVm,NetworkInterface)' --query '{status: computeVm.statuses[0].displayStatus, fqdn: fqdn, ipAddress: networkInterface.publicIpAddress}'
```
```json
{
  "fqdn": "lisalabvm.southcentralus.cloudapp.azure.com",
  "ipAddress": "13.85.228.112",
  "status": "Provisioning succeeded"
}
```

## <a name="start-and-connect-toohello-virtual-machine"></a>Rozpoczęcie i połączenie toohello maszyny wirtualnej
Uruchom Maszynę wirtualną.
```azurecli
az lab vm start --lab-name sampleLabName --name sampleVMName --resource-group sampleLabResourceGroup
```
> [!NOTE]
> Umieść hello **grupy zasobów w laboratorium** nazwie w hello — parametr grupy zasobów.
>

Połącz tooa maszyny Wirtualnej: [SSH](../virtual-machines/linux/mac-create-ssh-keys.md) lub [pulpitu zdalnego](../virtual-machines/windows/connect-logon.md).
```bash
ssh userName@ipAddressOrfqdn 
```

## <a name="update-hello-virtual-machine"></a>Maszyna wirtualna hello aktualizacji
Zastosuj tooa artefaktów maszyny Wirtualnej.
```azurecli
az lab vm apply-artifacts --lab-name  sampleLabName --name sampleVMName  --resource-group sampleResourceGroup  --artifacts @/artifacts.json
```

```json
[
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-java",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-install-nodejs",
    "parameters": []
  },
  {
    "artifactId": "/artifactSources/public repo/artifacts/linux-apt-package",
    "parameters": [
      {
        "name": "packages",
        "value": "abcd"
      },
      {
        "name": "update",
        "value": "true"
      },
      {
        "name": "options",
        "value": ""
      }
    ]
  } 
]
```

Lista dostępnych w laboratorium hello artefaktów.
```azurecli
az lab vm show --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup --expand "properties(\$expand=artifacts)" --query 'artifacts[].{artifactId: artifactId, status: status}'
```
```json
{
  "artifactId": "/subscriptions/abcdeftgh1213123/resourceGroups/lisalab123RG822645/providers/Microsoft.DevTestLab/labs/lisalab123/artifactSources/public repo/artifacts/linux-install-nodejs",
  "status": "Succeeded"
}
```

## <a name="stop-and-delete-hello-virtual-machine"></a>Zatrzymaj i Usuń maszynę wirtualną hello    
Zatrzymaj Maszynę wirtualną.
```azurecli
az lab vm stop --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

Usuń Maszynę wirtualną.
```azurecli
az lab vm delete --lab-name sampleLabName --name sampleVMName --resource-group sampleResourceGroup
```

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]