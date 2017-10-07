---
title: "aaaCreate niestandardowych obrazów maszyn wirtualnych z hello Azure CLI | Dokumentacja firmy Microsoft"
description: "Samouczek — Tworzenie niestandardowego obrazu maszyny Wirtualnej przy użyciu hello wiersza polecenia platformy Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/21/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 217a993c0c1d48939b74108ac6c5f7a1a619416c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-image-of-an-azure-vm-using-hello-cli"></a>Tworzenie niestandardowego obrazu maszyny Wirtualnej platformy Azure przy użyciu hello interfejsu wiersza polecenia

Niestandardowe obrazy są takie jak obrazy marketplace, ale można je utworzyć samodzielnie. Niestandardowe obrazy mogą być używane toobootstrap konfiguracje, takie jak wstępnego ładowania aplikacji, konfiguracji aplikacji i inne konfiguracje systemu operacyjnego. W tym samouczku utworzysz własnego niestandardowego obrazu maszyny wirtualnej platformy Azure. Omawiane kwestie:

> [!div class="checklist"]
> * Anulowanie zastrzeżenia i generalize maszyny wirtualne
> * Tworzenie obrazu niestandardowego
> * Utwórz maszynę Wirtualną z obrazu niestandardowego
> * Wyświetlanie listy wszystkich obrazów hello w ramach subskrypcji
> * Usuń obraz


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Jeśli wybierz tooinstall i użyj interfejsu wiersza polecenia hello lokalnie, w tym samouczku wymaga działają hello Azure CLI w wersji 2.0.4 lub nowszej. Uruchom `az --version` toofind hello wersji. Jeśli potrzebujesz tooinstall lub uaktualniania, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="before-you-begin"></a>Przed rozpoczęciem

Poniższe kroki Hello szczegółowo tootake istniejącej maszyny Wirtualnej i włącz go do wielokrotnego użytku niestandardowego obrazu, który służy toocreate nowych wystąpień maszyny Wirtualnej.

przykład Witaj toocomplete w tym samouczku, musi mieć istniejącej maszyny wirtualnej. Jeśli to konieczne, to [przykładowym skrypcie](../scripts/virtual-machines-linux-cli-sample-create-vm-nginx.md) można utworzyć. Podczas pracy nad hello samouczek, Zastąp maszyny Wirtualnej i grupy zasobów hello nazwy w razie potrzeby.

## <a name="create-a-custom-image"></a>Tworzenie obrazu niestandardowego

toocreate obrazu maszyny wirtualnej, należy tooprepare hello wirtualna anulowania obsługi, dealokowanie, a następnie oznaczenie hello źródłowej maszyny Wirtualnej, ponieważ uogólniony. Raz hello, który został przygotowany maszyny Wirtualnej, można utworzyć obrazu.

### <a name="deprovision-hello-vm"></a>Anulowanie zastrzeżenia hello maszyny Wirtualnej 

Cofanie zastrzegania stanowi uogólnienie hello maszyny Wirtualnej przez usunięcie informacji na temat określonego komputera. To generalizacji ułatwia toodeploy możliwych wiele maszyn wirtualnych za pomocą pojedynczego obrazu. Podczas anulowania obsługi, nazwa hosta hello jest resetowany zbyt*localhost.localdomain*. Klucze hosta SSH, konfiguracje wskazują hasła głównego i buforowanych dzierżaw DHCP również są usuwane.

Witaj toodeprovision maszyny Wirtualnej, użyj agenta maszyny Wirtualnej Azure hello (agenta waagent). agent maszyny Wirtualnej Azure Hello jest zainstalowany na powitania maszyny Wirtualnej i zarządza interakcji z hello Kontroler sieci szkieletowej Azure i udostępniania. Aby uzyskać więcej informacji, zobacz hello [Podręcznik użytkownika agenta systemu Linux Azure](agent-user-guide.md).

Połącz tooyour maszyny Wirtualnej przy użyciu protokołu SSH i hello Uruchom polecenie toodeprovision hello maszyny Wirtualnej. Z hello `+user` argument, hello ostatnie konto użytkownika elastycznie i wszelkie powiązane dane, również zostaną usunięte. Zamień adres IP przykład hello hello publicznego adresu IP maszyny Wirtualnej.

Toohello SSH maszyny Wirtualnej.
```bash
ssh azureuser@52.174.34.95
```
Anulowanie zastrzeżenia hello maszyny Wirtualnej.

```bash
sudo waagent -deprovision+user -force
```
Zamknij sesję SSH hello.

```bash
exit
```

### <a name="deallocate-and-mark-hello-vm-as-generalized"></a>Cofnięcie przydziału i oznacz hello maszyny Wirtualnej, ponieważ uogólniony

toocreate obraz powitania maszyny Wirtualnej musi toobe alokację. Cofnięcie przydziału hello maszynę Wirtualną przy użyciu [deallocate wirtualna az](/cli//azure/vm#deallocate). 
   
```azurecli-interactive 
az vm deallocate --resource-group myResourceGroup --name myVM
```

Wreszcie, Ustaw stan hello hello maszyny Wirtualnej jako uogólniony z [generalize wirtualna az](/cli//azure/vm#generalize) wówczas hello platformy Azure traktował hello maszyny Wirtualnej został uogólniony. Można tworzyć tylko obraz z ogólnych maszyny Wirtualnej.
   
```azurecli-interactive 
az vm generalize --resource-group myResourceGroup --name myVM
```

### <a name="create-hello-image"></a>Utworzyć obraz powitania

Teraz można utworzyć obraz powitania maszyny Wirtualnej za pomocą [tworzenia obrazu az](/cli//azure/image#create). Witaj poniższy przykład tworzy obraz o nazwie *myImage* z maszyny Wirtualnej o nazwie *myVM*.
   
```azurecli-interactive 
az image create \
    --resource-group myResourceGroup \
    --name myImage \
    --source myVM
```
 
## <a name="create-vms-from-hello-image"></a>Tworzenie maszyn wirtualnych z hello obrazu

Teraz, gdy masz obrazu można utworzyć jeden lub więcej nowych maszyn wirtualnych na podstawie hello obrazu przy użyciu [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMfromImage* z obrazu hello o nazwie *myImage*.

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVMfromImage \
    --image myImage \
    --admin-username azureuser \
    --generate-ssh-keys
```

## <a name="image-management"></a>Zarządzanie obrazami 

Oto kilka przykładów typowych zadań zarządzania obrazu i w jaki sposób toocomplete ich przy użyciu hello wiersza polecenia platformy Azure.

Wyświetl listę wszystkich obrazów według nazwy w formacie tabeli.

```azurecli-interactive 
az image list \
  --resource-group myResourceGroup
```

Usuń obraz. W tym przykładzie usuwa hello obrazu o nazwie *myOldImage* z hello *myResourceGroup*.

```azurecli-interactive 
az image delete \
    --name myOldImage \
    --resource-group myResourceGroup
```

## <a name="next-steps"></a>Następne kroki

W tym samouczku utworzony niestandardowy obraz maszyny Wirtualnej. W tym samouczku omówiono:

> [!div class="checklist"]
> * Anulowanie zastrzeżenia i generalize maszyny wirtualne
> * Tworzenie obrazu niestandardowego
> * Utwórz maszynę Wirtualną z obrazu niestandardowego
> * Wyświetlanie listy wszystkich obrazów hello w ramach subskrypcji
> * Usuń obraz

Przejdź dalej toolearn samouczka toohello o wysokiej dostępności maszyny wirtualnej.

> [!div class="nextstepaction"]
> [Tworzenie maszyn wirtualnych wysokiej dostępności](tutorial-availability-sets.md).

