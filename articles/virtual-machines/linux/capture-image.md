---
title: "Obraz maszyny wirtualnej systemu Linux na platformie Azure przy użyciu interfejsu wiersza polecenia 2.0 aaaCapture | Dokumentacja firmy Microsoft"
description: "Przechwyć obraz maszyny Wirtualnej Azure toouse wdrożeń masowej przy użyciu hello Azure CLI 2.0."
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 07/10/2017
ms.author: cynthn
ms.openlocfilehash: 9558332a86186b282775097428df462709373012
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-image-of-a-virtual-machine-or-vhd"></a>Jak toocreate obraz maszyny wirtualnej lub wirtualnego dysku twardego

<!-- generalize, image - extended version of hello tutorial-->

toocreate wiele kopii toouse maszyny wirtualnej (VM) na platformie Azure, przechwytywania obrazu hello maszyny Wirtualnej lub hello wirtualnego dysku twardego systemu operacyjnego. toocreate obrazu, należy usunąć informacje osobiste konto, dzięki czemu bezpieczniejsze toodeploy wiele razy. W hello następujące kroki, anulowanie zastrzeżenia istniejącej maszyny Wirtualnej, deallocate i tworzenie obrazu. Można użyć tego obrazu toocreate maszyn wirtualnych w dowolnej grupie zasobów w ramach subskrypcji.

Jeśli chcesz toocreate kopię istniejącej maszyny Wirtualnej systemu Linux tworzenia kopii zapasowej i debugowania lub przekazanie specjalne dysku VHD systemu Linux z lokalnej maszyny Wirtualnej, zobacz [przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie obrazu niestandardowego dysku](upload-vhd.md).  

Można również użyć **pakujący** toocreate konfiguracji niestandardowej. Aby uzyskać więcej informacji na temat używania pakujący, zobacz [jak obrazy maszyny wirtualnej systemu Linux toocreate pakujący toouse w programie Azure](build-image-with-packer.md).


## <a name="before-you-begin"></a>Przed rozpoczęciem
Upewnij się, czy zostały spełnione następujące wymagania wstępne hello:

* Należy maszyny Wirtualnej platformy Azure utworzonych w modelu wdrażania usługi Resource Manager hello za pomocą dysków zarządzanych. Jeśli nie utworzono Maszynę wirtualną systemu Linux, możesz użyć hello [portal](quick-create-portal.md), hello [interfejsu wiersza polecenia Azure](quick-create-cli.md), lub [szablonów Resource Manager](create-ssh-secured-vm-from-template.md). Skonfiguruj hello maszyny Wirtualnej, zgodnie z potrzebami. Na przykład [Dodaj dyski danych](add-disk.md), stosowania aktualizacji i zainstalować aplikacje. 

* Należy również toohave hello najnowszych [Azure CLI 2.0](/cli/azure/install-az-cli2) zainstalowane i zalogować się przy użyciu konta Azure tooan [logowania az](/cli/azure/#login).

## <a name="quick-commands"></a>Szybkie polecenia

Uproszczona wersja tego tematu, testowania, obliczenia lub informacje o maszynach wirtualnych na platformie Azure, dla [utworzyć niestandardowy obraz maszyny Wirtualnej platformy Azure przy użyciu interfejsu wiersza polecenia hello](tutorial-custom-images.md).


## <a name="step-1-deprovision-hello-vm"></a>Krok 1: Hello Deprovision maszyny Wirtualnej
Możesz anulowanie zastrzeżenia hello maszyny Wirtualnej za pomocą agenta maszyny Wirtualnej Azure hello, toodelete maszyny określonych plików i danych. Użyj hello `waagent` z hello *-deprovision + użytkownika* parametru w źródle maszyny Wirtualnej systemu Linux. Aby uzyskać więcej informacji, zobacz hello [Podręcznik użytkownika agenta systemu Linux Azure](../windows/agent-user-guide.md).

1. Połącz tooyour maszyny Wirtualnej systemu Linux przy użyciu klienta SSH.
2. W oknie SSH hello wpisz następujące polecenie hello:
   
    ```bash
    sudo waagent -deprovision+user
    ```
<br>
   > [!NOTE]
   > Tylko Uruchom to polecenie na maszynie Wirtualnej, który ma toocapture jako obraz. Nie gwarantuje obrazu hello jest brany pod uwagę wszystkie informacje poufne lub nadaje się do ponownej dystrybucji. Witaj *+ użytkownika* parametru spowoduje również usunięcie hello ostatnie konto użytkownika elastycznie. Jeśli poświadczenia konta tookeep w hello maszyny Wirtualnej, należy użyć *-deprovision* tooleave hello konta w miejscu.
 
3. Typ **y** toocontinue. Możesz dodać hello **-wymusić** tooavoid parametr ten krok potwierdzenia.
4. Po zakończeniu wykonywania polecenia hello wpisz **zakończyć**. Ten krok powoduje zamknięcie powitania klienta SSH.

## <a name="step-2-create-vm-image"></a>Krok 2: Tworzenie obrazu maszyny Wirtualnej
Jak uogólniony przy użyciu hello Azure CLI 2.0 toomark hello maszyny Wirtualnej, a następnie przechwycić obraz powitania. Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają *myResourceGroup*, *myVnet*, i *myVM*.

1. Cofnięcie przydziału hello maszynę Wirtualną, która anulowana z [deallocate wirtualna az](/cli//azure/vm#deallocate). Witaj poniższy przykład cofa alokację hello maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup*:
   
    ```azurecli
    az vm deallocate \
      --resource-group myResourceGroup \
      --name myVM
    ```

2. Znacznik hello maszyny Wirtualnej, ponieważ uogólniony z [generalize wirtualna az](/cli//azure/vm#generalize). Witaj następujący przykład znaczniki Witaj Witaj maszyny Wirtualnej o nazwie *myVM* hello grupy zasobów o nazwie *myResourceGroup* jako uogólniony:
   
    ```azurecli
    az vm generalize \
      --resource-group myResourceGroup \
      --name myVM
    ```

3. Teraz utworzyć obraz powitania zasobu maszyny Wirtualnej z [tworzenia obrazu az](/cli//azure/image#create). Witaj poniższy przykład tworzy obraz o nazwie *myImage* hello grupy zasobów o nazwie *myResourceGroup* przy użyciu hello zasobu maszyny Wirtualnej o nazwie *myVM*:
   
    ```azurecli
    az image create \
      --resource-group myResourceGroup \
      --name myImage --source myVM
    ```
   
   > [!NOTE]
   > Witaj obrazu jest tworzony w hello same grupy zasobów jako źródło maszyny Wirtualnej. Maszyny wirtualne można tworzyć w dowolnej grupie zasobów w ramach subskrypcji z tego obrazu. Z punktu widzenia zarządzania możesz toocreate grupy zasobów dla określonych zasobów maszyny Wirtualnej i obrazów.

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Krok 3: Tworzenie maszyny Wirtualnej z hello przechwycony obraz
Utwórz maszynę Wirtualną przy użyciu obrazu hello zostały utworzone z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Witaj poniższy przykład tworzy Maszynę wirtualną o nazwie *myVMDeployed* z obrazu hello o nazwie *myImage*:

```azurecli
az vm create \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --image myImage\
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```

### <a name="creating-hello-vm-in-another-resource-group"></a>Tworzenie hello maszyny Wirtualnej w innej grupie zasobów 

Maszyny wirtualne można utworzyć na podstawie obrazu w dowolnej grupie zasobów w ramach subskrypcji. toocreate Maszynę wirtualną w innej grupie zasobów niż obraz powitania Określ hello zasobów pełny identyfikator tooyour obrazu. Użyj [listy obrazów az](/cli/azure/image#list) tooview listy obrazów. Witaj danych wyjściowych jest toohello podobnie poniższy przykład:

```json
"id": "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage",
   "location": "westus",
   "name": "myImage",
```

Witaj poniższym przykładzie użyto [tworzenia maszyny wirtualnej az](/cli/azure/vm#create) toocreate Maszynę wirtualną w innej grupie zasobów niż obraz źródłowy hello, określając identyfikator zasobu obrazu hello:

```azurecli
az vm create \
   --resource-group myOtherResourceGroup \
   --name myOtherVMDeployed \
   --image "/subscriptions/guid/resourceGroups/MYRESOURCEGROUP/providers/Microsoft.Compute/images/myImage" \
   --admin-username azureuser \
   --ssh-key-value ~/.ssh/id_rsa.pub
```


## <a name="step-4-verify-hello-deployment"></a>Krok 4: Weryfikowanie wdrażania hello

Teraz SSH toohello maszyny wirtualnej utworzone tooverify hello wdrażania i uruchamiania przy użyciu hello nowej maszyny Wirtualnej. tooconnect za pośrednictwem protokołu SSH, Znajdź hello adres IP lub nazwa FQDN maszyny wirtualnej z [az maszyny wirtualnej pokazu](/cli/azure/vm#show):

```azurecli
az vm show \
   --resource-group myResourceGroup \
   --name myVMDeployed \
   --show-details
```

## <a name="next-steps"></a>Następne kroki
Możesz utworzyć wiele maszyn wirtualnych z obrazu maszyny Wirtualnej źródłowego. Jeśli potrzebujesz toomake zmiany tooyour obrazu: 

- Utwórz maszynę Wirtualną z obrazu.
- Upewnij się, wszystkie aktualizacje i zmiany konfiguracji.
- Wykonaj hello ponownie kroki toodeprovision, deallocate generalize i tworzenie obrazu.
- Skorzystaj z tego nowego obrazu dla przyszłych wdrożeń. W razie potrzeby usuń hello oryginalnego obrazu.

Aby uzyskać więcej informacji na temat zarządzania maszyn wirtualnych z hello interfejsu wiersza polecenia, zobacz [Azure CLI 2.0](/cli/azure/overview).
