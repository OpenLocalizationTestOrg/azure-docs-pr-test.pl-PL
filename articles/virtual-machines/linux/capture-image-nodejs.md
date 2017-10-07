---
title: aaaCapture toouse Azure maszyny Wirtualnej systemu Linux jako szablon | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocapture i obraz opartych na systemie Linux Azure maszynę wirtualną (VM) utworzone za pomocą modelu wdrażania usługi Azure Resource Manager hello."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e608116f-f478-41be-b787-c2ad91b5a802
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 877eee5c842bebe80e755c2240cdaaef4ade6ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="capture-a-linux-virtual-machine-running-on-azure"></a>Przechwytywanie maszyny wirtualnej systemu Linux działających na platformie Azure
Wykonaj kroki hello w tym artykule toogeneralize i przechwycenia maszyny wirtualnej systemu Linux platformy Azure (VM) w modelu wdrażania usługi Resource Manager hello. Uogólnienie hello maszyny Wirtualnej, Usuń konto osobiste informacje i przygotować toobe wirtualna hello użyty jako obraz. Można następnie przechwytywania obrazów uogólniony wirtualny dysk twardy (VHD) do hello systemu operacyjnego, dysków VHD dla dysków dołączonych danych i [szablonu usługi Resource Manager](../../azure-resource-manager/resource-group-overview.md) o nowych wdrożeniach maszyny Wirtualnej. W tym artykule szczegółowo sposób obrazu toocapture maszyny Wirtualnej o hello Azure CLI 1.0 dla maszyny Wirtualnej za pomocą niezarządzanych dysków. Możesz również [Przechwytywanie maszyny Wirtualnej za pomocą dysków zarządzanych Azure z hello Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Zarządzane dyski są obsługiwane przez hello platformy Azure i nie wymagają żadnych toostore przygotowania lub lokalizacji je. Aby uzyskać więcej informacji, zobacz temat [Omówienie usługi Azure Managed Disks](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

toocreate maszyn wirtualnych przy użyciu obrazu hello, skonfiguruj zasobów sieciowych dla każdej nowej maszyny Wirtualnej i użyj hello toodeploy szablonu (pliku notacji obiektu JavaScript lub formatu JSON,) z hello przechwyconych obrazów dysków VHD. W ten sposób można replikować maszyny Wirtualnej z bieżącej konfiguracji oprogramowania, podobnie toohello używać obrazów w hello Azure Marketplace.

> [!TIP]
> Jeśli toocreate kopię istniejącej maszyny Wirtualnej systemu Linux jej stanem specjalne tworzenia kopii zapasowej i debugowania, zobacz [utworzenie kopii maszyny wirtualnej systemu Linux działających na platformie Azure](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). I tooupload wirtualnego dysku twardego z lokalnej maszyny Wirtualnej systemu Linux, zobacz [przekazywanie i Utwórz Maszynę wirtualną systemu Linux na podstawie obrazu niestandardowego dysku](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).  

## <a name="cli-versions-toocomplete-hello-task"></a>Zadanie hello toocomplete wersje interfejsu wiersza polecenia
Można ukończyć powitalnych zadań przy użyciu jednej z hello następujące wersje interfejsu wiersza polecenia:

- [Azure CLI 1.0](#before-you-begin) — nasze interfejsu wiersza polecenia dla hello classic i zasobów zarządzania wdrażania modeli (w tym artykule)
- [Azure CLI 2.0](capture-image.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -naszej nowej generacji interfejsu wiersza polecenia dla modelu wdrażania zarządzania zasobów hello

## <a name="before-you-begin"></a>Przed rozpoczęciem
Upewnij się, czy zostały spełnione następujące wymagania wstępne hello:

* **Maszyna wirtualna platformy Azure utworzonych w modelu wdrażania usługi Resource Manager hello** — Jeśli nie utworzono Maszynę wirtualną systemu Linux, możesz użyć hello [portalu](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), hello [interfejsu wiersza polecenia Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), lub [Resource Manager szablony](create-ssh-secured-vm-from-template.md). 
  
    Skonfiguruj hello maszyny Wirtualnej, zgodnie z potrzebami. Na przykład [Dodaj dyski danych](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), stosowania aktualizacji i zainstalować aplikacje. 
* **Azure CLI** -Install hello [interfejsu wiersza polecenia Azure](../../cli-install-nodejs.md) na komputerze lokalnym.

## <a name="step-1-remove-hello-azure-linux-agent"></a>Krok 1: Usuń agenta systemu Linux Azure hello
Najpierw uruchom hello **agenta waagent** z hello **deprovision** parametru na powitania maszyny Wirtualnej systemu Linux. To polecenie usuwa pliki i hello toomake danych gotowe do uogólnianie maszyny Wirtualnej. Aby uzyskać więcej informacji, zobacz hello [Podręcznik użytkownika agenta systemu Linux Azure](../windows/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

1. Połącz tooyour maszyny Wirtualnej systemu Linux przy użyciu klienta SSH.
2. W oknie SSH hello wpisz następujące polecenie hello:
   
    ```bash
    sudo waagent -deprovision+user
    ```
   > [!NOTE]
   > Tylko Uruchom to polecenie na maszynie Wirtualnej, który ma toocapture jako obraz. Nie gwarantuje obrazu hello jest brany pod uwagę wszystkie informacje poufne lub nadaje się do ponownej dystrybucji.
 
3. Typ **y** toocontinue. Możesz dodać hello **-wymusić** tooavoid parametr ten krok potwierdzenia.
4. Po zakończeniu wykonywania polecenia hello wpisz **zakończyć**. Ten krok powoduje zamknięcie powitania klienta SSH.

## <a name="step-2-capture-hello-vm"></a>Krok 2: Przechwytywanie hello maszyny Wirtualnej
Użyj hello toogeneralize wiersza polecenia platformy Azure i przechwytywania hello maszyny Wirtualnej. Poniższe przykłady w hello Zastąp przykładowe nazwy parametrów własne wartości. Przykład nazwy parametru zawierają **myResourceGroup**, **myVnet**, i **myVM**.

1. Z komputera lokalnego, otwórz hello wiersza polecenia platformy Azure i [tooyour logowania subskrypcji platformy Azure](../../xplat-cli-connect.md). 
2. Upewnij się, że jesteś w trybie Menedżera zasobów.
   
    ```azurecli
    azure config mode arm
    ```
3. Zamknij maszynę Wirtualną, która już anulowana za pomocą następującego polecenia hello hello:
   
    ```azurecli
    azure vm deallocate -g myResourceGroup -n myVM
    ```
4. Generalize hello maszyny Wirtualnej z hello następujące polecenie:
   
    ```azurecli
    azure vm generalize -g myResourceGroup -n myVM
    ```
5. Teraz uruchom hello **przechwytywania maszyna wirtualna platformy azure** polecenia, które przechwytywania hello maszyny Wirtualnej. W hello poniższy przykład, wirtualne dyski twarde są przechwytywane z obrazu hello nazwy zaczyna się od **MyVHDNamePrefix**i hello **-t** opcja określa szablon toohello ścieżki **MyTemplate.json**. 
   
    ```azurecli
    azure vm capture -g myResourceGroup -n myVM -p myVHDNamePrefix -t myTemplate.json
    ```
   
   > [!IMPORTANT]
   > pliki VHD obrazu Hello tworzone domyślnie hello używać tego samego konta magazynu, który hello oryginalna maszyna wirtualna. Użyj hello *tego samego konta magazynu* hello toostore wirtualne dyski twarde dla wszelkie nowe maszyny wirtualne, Utwórz hello obrazu. 

6. Lokalizacja hello toofind przechwyconego obrazu szablonu JSON hello otwarty w edytorze tekstów. W hello **storageProfile**, Znajdź hello **uri** z hello **obrazu** znajduje się w hello **systemu** kontenera. Na przykład hello identyfikatora URI obrazu dysku systemu operacyjnego hello przypomina zbyt`https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`

## <a name="step-3-create-a-vm-from-hello-captured-image"></a>Krok 3: Tworzenie maszyny Wirtualnej z hello przechwycony obraz
Teraz za pomocą obrazu hello toocreate szablonu maszyny Wirtualnej systemu Linux. Te kroki pokazują, jak toouse hello wiersza polecenia platformy Azure i hello szablon pliku JSON przechwycone toocreate hello maszyny Wirtualnej w nowej sieci wirtualnej.

### <a name="create-network-resources"></a>Utwórz zasoby sieciowe
Szablon hello toouse, należy najpierw tooset sieci wirtualnej i karty Sieciowej dla nowej maszyny Wirtualnej. Zaleca się tworzenie grupy zasobów dla tych zasobów w hello miejsce przechowywania obrazu maszyny Wirtualnej. Uruchom polecenia podobne toohello po, zastępując nazwy zasobów i odpowiednie lokalizacji platformy Azure ("centralus" w tych poleceniach):

```azurecli
azure group create myResourceGroup1 -l "centralus"

azure network vnet create myResourceGroup1 myVnet -l "centralus"

azure network vnet subnet create myResourceGroup1 myVnet mySubnet

azure network public-ip create myResourceGroup1 myPublicIP -l "centralus"

azure network nic create myResourceGroup1 myNIC -k mySubnet -m myVnet -p myPublicIP -l "centralus"
```

### <a name="get-hello-id-of-hello-nic"></a>Pobierz hello identyfikator hello karty Sieciowej
toodeploy maszyny Wirtualnej z obrazu hello przy użyciu hello JSON zapisane podczas przechwytywania, należy hello identyfikator hello karty sieciowej. Go uzyskać, uruchamiając następujące polecenie hello:

```azurecli
azure network nic show myResourceGroup1 myNIC
```

Witaj **identyfikator** w hello dane wyjściowe są podobne zbyt`/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic`

### <a name="create-a-vm"></a>Tworzenie maszyny wirtualnej
Teraz hello uruchom następujące polecenie toocreate maszyny Wirtualnej z hello przechwycony obraz maszyny Wirtualnej. Użyj hello **-f** szablon toohello ścieżki hello toospecify parametru JSON plik zostanie zapisany.

```azurecli
azure group deployment create myResourceGroup1 MyDeployment -f MyTemplate.json
```

W danych wyjściowych polecenia hello są toosupply zostanie wyświetlony monit o nowe nazwę maszyny Wirtualnej, nazwa użytkownika administratora hello i hasło, a hello identyfikator hello karty Sieciowej, którą utworzono wcześniej.

```bash
info:    Executing command group deployment create
info:    Supply values for hello following parameters
vmName: myNewVM
adminUserName: myAdminuser
adminPassword: ********
networkInterfaceId: /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resource Groups/myResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
```

następujące przykładowe Hello pokazuje, zobacz pomyślne wdrożenie:

```bash
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment xxxxxxx
+ Waiting for deployment toocomplete
data:    DeploymentName     : MyDeployment
data:    ResourceGroupName  : MyResourceGroup1
data:    ProvisioningState  : Succeeded
data:    Timestamp          : xxxxxxx
data:    Mode               : Incremental
data:    Name                Type          Value

data:    ------------------  ------------  -------------------------------------

data:    vmName              String        myNewVM

data:    vmSize              String        Standard_D1

data:    adminUserName       String        myAdminuser

data:    adminPassword       SecureString  undefined

data:    networkInterfaceId  String        /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/MyResourceGroup1/providers/Microsoft.Network/networkInterfaces/myNic
info:    group deployment create command OK
```

### <a name="verify-hello-deployment"></a>Sprawdź hello wdrożenia
Teraz SSH toohello maszyny wirtualnej utworzone tooverify hello wdrażania i uruchamiania przy użyciu hello nowej maszyny Wirtualnej. tooconnect za pośrednictwem protokołu SSH, znaleźć adres IP hello hello maszyny Wirtualnej utworzonej, uruchamiając następujące polecenie hello:

```azurecli
azure network public-ip show myResourceGroup1 myPublicIP
```

Hello publiczny adres IP jest wyświetlany w danych wyjściowych polecenia hello. Domyślnie połączenie toohello maszyny Wirtualnej systemu Linux przez SSH na port 22.

## <a name="create-additional-vms"></a>Utwórz dodatkowe maszyny wirtualne
Użyj hello przechwycone toodeploy obrazu i szablon dodatkowe maszyny wirtualne, wykonując kroki hello w powyższej sekcji hello. Inne opcje toocreate maszyn wirtualnych z obrazu hello obejmują przy użyciu szablonu Szybki Start lub uruchomione hello **tworzenia maszyny wirtualnej azure** polecenia.

### <a name="use-hello-captured-template"></a>Użyj szablonu przechwyconych hello
toouse hello przechwycony obraz i szablonu, wykonaj następujące kroki, (szczegóły w powyższej sekcji hello):

* Upewnij się, że obraz maszyny Wirtualnej jest w hello tego samego konta magazynu, który jest hostem wirtualnego dysku twardego maszyny Wirtualnej.
* Skopiuj plik JSON szablonu hello i określ unikatową nazwę dysku systemu operacyjnego hello hello nowej maszyny Wirtualnej wirtualnego dysku twardego (lub wirtualne dyski twarde). Na przykład w hello **storageProfile**w obszarze **wirtualnego dysku twardego**w **uri**, określ unikatową nazwę dla hello **osDisk** wirtualnego dysku twardego, podobne zbyt`https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`
* Utwórz kartę Sieciową w obu hello tej samej lub innej sieci wirtualnej.
* Przy użyciu pliku JSON hello zmodyfikować szablon, Utwórz wdrożenie w grupie zasobów hello, w którym zdefiniować hello sieci wirtualnej.

### <a name="use-a-quickstart-template"></a>Szablon szybkiego startu
Jeśli chcesz skonfigurować automatycznie po utworzeniu maszyny Wirtualnej z obrazu hello sieci hello tych zasobów można określić w szablonie. Na przykład, zobacz hello [101 maszyny wirtualnej użytkownika obrazu z szablonu](https://github.com/Azure/azure-quickstart-templates/tree/master/101-vm-from-user-image) z usługi GitHub. Ten szablon tworzy Maszynę wirtualną z obrazu niestandardowego i hello niezbędne sieci wirtualnej, publiczny adres IP i zasobów kart interfejsu Sieciowego. Przewodnik przy użyciu szablonu hello hello portalu Azure, zobacz [jak toocreate maszynę wirtualną z obrazu niestandardowego za pomocą szablonu usługi Resource Manager](http://codeisahighway.com/how-to-create-a-virtual-machine-from-a-custom-image-using-an-arm-template/).

### <a name="use-hello-azure-vm-create-command"></a>Użyj hello azure vm Utwórz polecenie
Zazwyczaj jest najprostszym toouse toocreate szablon Menedżera zasobów maszyny Wirtualnej z obrazu hello. Można jednak utworzyć hello wirtualna *imperatively* przy użyciu hello **tworzenia maszyny wirtualnej platformy azure** z hello **-Q** (**— urn obrazu**) parametru . Jeśli ta metoda również przekazać hello **-d** (**systemu operacyjnego —-dysk-dysk vhd**) parametru toospecify hello lokalizację pliku VHD hello systemu operacyjnego dla hello nowej maszyny Wirtualnej. Ten plik musi znajdować się w kontenerze wirtualne dyski twarde hello hello konta magazynu, którym jest przechowywany plik wirtualnego dysku twardego obraz powitania. Witaj polecenia kopie hello wirtualnego dysku twardego dla hello nowej maszyny Wirtualnej automatycznie toohello **wirtualne dyski twarde** kontenera.

Przed uruchomieniem **tworzenia maszyny wirtualnej azure** z obrazem hello ukończyć hello następujące kroki:

1. Utwórz grupę zasobów lub istniejącej grupy zasobów dla wdrożenia hello zidentyfikować.
2. Utwórz publiczny zasobu adresu IP i zasobu kart hello nowej maszyny Wirtualnej. Kroki toocreate sieci wirtualnej publiczny adres IP i kart przy użyciu interfejsu wiersza polecenia, hello uzyskać wcześniej w tym artykule. (**tworzenia maszyny wirtualnej azure** można również utworzyć karty Sieciowej, ale należy toopass dodatkowe parametry dla sieci wirtualnej i podsieci.)

Następnie uruchom polecenie, które przekazuje identyfikatorów URI tooboth hello nowego pliku wirtualnego dysku twardego systemu operacyjnego i hello istniejącego obrazu. W tym przykładzie rozmiar Standard_A1 zostanie utworzona maszyna wirtualna w regionie wschodnie stany USA hello.

```azurecli
azure vm create -g myResourceGroup1 -n myNewVM -l eastus -y Linux \
-z Standard_A1 -u myAdminname -p myPassword -f myNIC \
-d "https://xxxxxxxxxxxxxx.blob.core.windows.net/vhds/MyNewVHDNamePrefix.vhd" \
-Q "https://xxxxxxxxxxxxxx.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.vhd"
```

Opcje dodatkowe polecenia, można uruchomić `azure help vm create`.

## <a name="next-steps"></a>Następne kroki
toomanage maszyn wirtualnych z hello interfejsu wiersza polecenia, zobacz zadań hello w [wdrażania i zarządzania maszynami wirtualnymi przy użyciu szablonów usługi Azure Resource Manager i hello Azure CLI](create-ssh-secured-vm-from-template.md).

