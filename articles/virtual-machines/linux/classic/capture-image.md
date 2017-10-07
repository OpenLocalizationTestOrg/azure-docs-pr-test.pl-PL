---
title: aaaCapture obrazu maszyny wirtualnej systemu Linux | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocapture obraz opartych na systemie Linux Azure maszynę wirtualną (VM) utworzony z hello klasycznego modelu wdrażania."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17d7ffee-a58e-4290-9de1-64c3cf1ddc05
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 33c4059d5bb919a86bdc3492abca540750f365ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocapture-a-classic-linux-virtual-machine-as-an-image"></a>Jak toocapture klasyczne maszyny wirtualnej systemu Linux jako obrazu
> [!IMPORTANT]
> Platforma Azure ma dwa różne modele wdrażania do tworzenia i pracy z zasobami: [Resource Manager i Model Klasyczny](../../../resource-manager-deployment-model.md). W tym artykule omówiono przy użyciu klasycznego modelu wdrożenia hello. Firma Microsoft zaleca, aby większości nowych wdrożeń korzystać hello modelu Resource Manager. Dowiedz się, jak za[wykonaj te czynności przy użyciu modelu Resource Manager hello](../capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

W tym artykule opisano sposób toocapture klasycznego Azure maszynę wirtualną (VM) systemem Linux jako obrazu toocreate innych maszyn wirtualnych. Ten obraz zawiera hello dysku systemu operacyjnego i dysków z danymi dołączone toohello maszyny Wirtualnej. Nie ma wśród nich konfiguracji sieci, więc należy tooconfigure które po utworzeniu hello inne maszyny Wirtualnej z obrazu hello.

Magazyny Azure hello obrazu w obszarze **obrazów**, oraz wszystkie obrazy zostały przekazane. Aby uzyskać więcej informacji na temat obrazów, zobacz [o obrazy maszyny wirtualnej na platformie Azure][About Virtual Machine Images in Azure].

## <a name="before-you-begin"></a>Przed rozpoczęciem
Tych krokach przyjęto założenie, że zostało już utworzone przy użyciu klasycznego modelu wdrożenia hello i hello skonfigurowanego systemu operacyjnego, dołączanie wszystkich dysków danych maszyny Wirtualnej platformy Azure. Toocreate maszyny Wirtualnej, należy przeczytać [jak tooCreate maszyny wirtualnej systemu Linux][How tooCreate a Linux Virtual Machine].

## <a name="capture-hello-virtual-machine"></a>Przechwytywanie maszyny wirtualnej hello
1. [Połącz toohello wirtualna](../mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) przy użyciu klienta SSH wybranych przez użytkownika.
2. W oknie SSH hello wpisz następujące polecenie hello. Witaj dane wyjściowe z `waagent` mogą się nieco różnić w zależności od wersji hello tego narzędzia:

    ```bash
    sudo waagent -deprovision+user
    ```

    Witaj poprzednie polecenie prób tooclean hello system i nie była odpowiednia dla reprovisioning. Tę operację wykonuje hello następujące zadania:

   * Usuwa kluczy SSH hosta (jeśli Provisioning.RegenerateSshHostKeyPair "y" w pliku konfiguracyjnym hello)
   * Czyści konfiguracji serwera nazw w /etc/resolv.conf
   * Usuwa hello `root` hasło użytkownika w tle/etc / (jeśli Provisioning.DeleteRootPassword "y" w pliku konfiguracyjnym hello)
   * Usunięcie buforowanych dzierżaw klientów DHCP
   * Resetuje hosta toolocalhost.localdomain nazwy
   * Usuwa hello ostatnie konto użytkownika elastycznie (uzyskane z /var/lib/waagent) **i skojarzone dane**.

     > [!NOTE]
     > Cofanie zastrzegania usuwa pliki i dane za "generalize" hello obrazu. Tylko Uruchom to polecenie na maszynie Wirtualnej, który ma toocapture jako nowy szablon obrazu. Nie gwarantuje obrazu hello jest brany pod uwagę wszystkie informacje poufne lub nadaje się do strony toothird ponownej dystrybucji.

3. Typ **y** toocontinue. Możesz dodać hello `-force` tooavoid parametr ten krok potwierdzenia.
4. Typ **zakończenia** tooclose hello SSH klienta.

   > [!NOTE]
   > Witaj pozostałych kroków założono, że masz już [zainstalowane hello Azure CLI](../../../cli-install-nodejs.md) na komputerze klienckim. Można również wykonać wszystkie hello następujące kroki w hello [portalu Azure](http://portal.azure.com).

5. Na swoim komputerze klienckim otwórz okno wiersza polecenia platformy Azure i tooyour logowania subskrypcji platformy Azure. Aby uzyskać więcej informacji, przeczytaj [połączyć tooan subskrypcji platformy Azure z hello Azure CLI](../../../xplat-cli-connect.md).

   > [!NOTE]
   > W portalu Azure hello Zaloguj się w portalu toohello.

6. Upewnij się, że jesteś w trybie zarządzania usługami:

    ```azurecli
    azure config mode asm
    ```

7. Zamknij maszynę Wirtualną, która jest już anulowana hello. Witaj poniższy przykład zamyka hello maszyny Wirtualnej o nazwie `myVM`:

    ```azurecli
    azure vm shutdown myVM
    ```
   Jeśli to konieczne, można wyświetlić listę hello wszystkie maszyny wirtualne utworzone w ramach subskrypcji przy użyciu`azure vm list`

   > [!NOTE]
   > Jeśli używasz hello portalu Azure wybierz hello maszyny Wirtualnej i kliknij przycisk **zatrzymać** zamknie hello maszyny Wirtualnej.

8. Po zatrzymaniu hello maszyny Wirtualnej Przechwyć obraz powitania. następujące przechwytywania przykład Hello hello maszyny Wirtualnej o nazwie `myVM` i tworzy uogólniony obraz o nazwie `myNewVM`:

    ```azurecli
    azure vm capture -t myVM myNewVM
    ```

    Witaj `-t` podpolecenia usuwa hello oryginalna maszyna wirtualna.

    > [!NOTE]
    > W portalu Azure hello, można przechwycić obraz, wybierając **obrazu** menu hello koncentratora. Potrzebujesz następujących informacji o obrazie hello hello toosupply: Nazwa grupy zasobów, lokalizacji, typu systemu operacyjnego i ścieżki do magazynu obiektów blob.

9. Nowy obraz powitania jest teraz dostępna w hello listy obrazów, które mogą być tooconfigure używanej żadnej nowej maszyny Wirtualnej. Możesz je wyświetlić przy użyciu polecenia hello:

   ```azurecli
   azure vm image list
   ```

   Na powitania [portalu Azure](http://portal.azure.com), w hello pojawi się nowy obraz powitania **obrazów maszyn wirtualnych (klasyczne)** należący toohello **obliczeniowe** usług. Dostęp można uzyskać **obrazów maszyn wirtualnych (klasyczne)** klikając _więcej usług_ u dołu hello hello Azure Usługa listy, a następnie sprawdzając w hello **obliczeniowe** usług.   

   ![Pomyślne przechwytywania obrazu](./media/capture-image/VMCapturedImageAvailable.png)

## <a name="next-steps"></a>Następne kroki
Obraz powitania jest gotowy toobe używane toocreate maszyn wirtualnych. Możesz użyć polecenia interfejsu wiersza polecenia Azure hello `azure vm create` i nazwa obrazu hello dostaw został utworzony. Aby uzyskać więcej informacji, zobacz [hello Using Azure CLI z klasycznego modelu wdrożenia](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).

Można również użyć hello [portalu Azure](http://portal.azure.com) toocreate niestandardowych maszyny Wirtualnej za pomocą hello **obrazu** — metoda i wybierając hello obrazu utworzonego. Aby uzyskać więcej informacji, zobacz [jak tooCreate wirtualna niestandardowe][How tooCreate a Custom Virtual Machine].

**Zobacz też:** [Podręcznik użytkownika Azure agenta systemu Linux](../agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[About Virtual Machine Images in Azure]:../../virtual-machines-linux-classic-about-images.md
[How tooCreate a Custom Virtual Machine]:create-custom.md
[How tooAttach a Data Disk tooa Virtual Machine]:attach-disk.md
[How tooCreate a Linux Virtual Machine]:create-custom.md
