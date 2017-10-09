---
title: "aaaAzure chmury powłoki (wersja zapoznawcza) — Szybki Start | Dokumentacja firmy Microsoft"
description: "Szybki Start dla hello powłoki chmury Azure"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>Szybki Start dotyczące używania hello powłoki chmury Azure

Ten dokument zawiera szczegóły jak toouse hello Azure Cloud powłoki w hello [portalu Azure](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Uruchom powłokę chmury
1. Uruchom **powłoki chmury** z hello górnym menu nawigacyjnym hello portalu Azure <br>
![](media/shell-icon.png)
2. Wybierz toocreate subskrypcja konta magazynu i udział plików na platformę Azure
3. Wybierz opcję "Utwórz magazyn"

> [!TIP]
> Azure CLI 2.0 są automatycznie uwierzytelniani w każdym sesssion.

### <a name="set-your-subscription"></a>Ustaw swoją subskrypcję
1. Subskrypcje listy, do których masz dostęp do: <br>
`az account list`
2. Ustaw preferowany subskrypcji: <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> Subskrypcja zostanie zapamiętany dla przyszłych sesji przy użyciu `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Tworzenie grupy zasobów
Utwórz nową grupę zasobów w WestUS o nazwie "MyRG": <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Tworzenie maszyny wirtualnej z systemem Linux
Tworzenie maszyny Wirtualnej systemu Ubuntu w nowej grupy zasobów. Hello Azure CLI 2.0 utworzy kluczy SSH i hello konfiguracji maszyny Wirtualnej z nimi. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> Witaj tooauthenticate klucze publiczne i prywatne używane maszyny Wirtualnej są umieszczane w `/User/.ssh/id_rsa` i `/User/.ssh/id_rsa.pub` przez Azure CLI 2.0 domyślnie. Folderu .ssh jest utrwalona w obrazie 5 GB na udział dołączonych plików na platformę Azure.

Nazwa użytkownika na tej maszynie Wirtualnej zostanie nazwy użytkownika używane w chmurze powłoki ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>SSH do maszyny Wirtualnej systemu Linux
1. Wyszukaj nazwę maszyny Wirtualnej na pasku wyszukiwania portalu Azure hello
2. Kliknij przycisk "Połącz", a następnie uruchom:`ssh username@ipaddress`

![](media/sshcmd-copy.png)

Podczas ustanawiania połączenia SSH hello, powinna zostać wyświetlona hello Ubuntu powitalnej wiersza.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Czyszczenie 
Usunięcie grupy zasobów i wszystkie zasoby w niej: <br>
Uruchom polecenie `az group delete -n MyRG`

## <a name="next-steps"></a>Następne kroki
[Dowiedz się więcej o trwałych magazynu w chmurze powłoki](persisting-shell-storage.md) <br>
[Więcej informacji na temat usługi Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) <br>
[Więcej informacji na temat usługi Magazyn plików Azure](../storage/files/storage-files-introduction.md) <br>