---
title: "aaaCreate wirtualnej Azure sieci komunikacji równorzędnej — różne modele wdrażania — tej samej subskrypcji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi została utworzona za pośrednictwem różnych wdrożenia usługi Azure modeli, które istnieją w hello sam subskrypcji platformy Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: 365156d651c9042ed52baeb15bf629fcc5329af8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---different-deployment-models-same-subscription"></a>Tworzenie sieci wirtualnej równorzędna — różne modele wdrażania, tej samej subskrypcji 

Z tego samouczka dowiesz się toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi utworzone przez różne modele wdrażania. Obie sieci wirtualne istnieją w hello sam subskrypcji. Witaj komunikacji równorzędnej dwa zasoby umożliwia sieci wirtualnych w różnych sieciach wirtualnych toocommunicate ze sobą z tej samej przepustowości i opóźnień tak, jakby hello zasoby były hello tej samej sieci wirtualnej. Dowiedz się więcej o [równorzędna sieci wirtualnej](virtual-network-peering-overview.md). 

Witaj toocreate kroki sieci wirtualnej komunikacji równorzędnej są różne, w zależności od tego, czy hello sieci wirtualne są w hello tych samych lub różnych subskrypcji i które [modelu wdrożenia usługi Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sieci wirtualne są tworzone za pomocą. Dowiedz się, jak toocreate a wirtualnych sieci równorzędna w innych sytuacjach, klikając hello scenariusza z hello w poniższej tabeli:

|Model wdrażania platformy Azure  | Subskrypcja platformy Azure  |
|--------- |---------|
|[Obie usługi Resource Manager](virtual-network-create-peering.md) |tym samym|
|[Obie usługi Resource Manager](create-peering-different-subscriptions.md) |Różne|
|[Jeden Resource Manager, co classic](create-peering-different-deployment-models-subscriptions.md) |Różne|

Nie można utworzyć sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnej wdrożone za pośrednictwem hello klasycznego modelu wdrażania. Element równorzędny sieci wirtualnej można tworzyć tylko między dwiema sieciami wirtualnych, które istnieją w hello sam region platformy Azure. Jeśli potrzebujesz sieci wirtualnych tooconnect zarówno utworzonych za pomocą hello klasycznego modelu wdrażania lub istnieje w różnych regionach platformy Azure, można użyć Azure [bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sieci wirtualnych. 

Można użyć hello [portalu Azure](#portal), hello Azure [interfejsu wiersza polecenia](#cli) (CLI) lub Azure [PowerShell](#powershell) toocreate sieci wirtualnej komunikacji równorzędnej. Kliknij dowolny z hello poprzedniego narzędzia łącza toogo, bezpośrednio toohello kroki tworzenia sieci wirtualnej komunikacji równorzędnej narzędzie wyboru.

## <a name="cli"></a>Utwórz równorzędna - portalu

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com). Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
2. Kliknij przycisk **+ nowy**, kliknij przycisk **sieci**, następnie kliknij przycisk **sieci wirtualnej**.
3. W hello **Utwórz sieć wirtualną** bloku, wprowadź, lub wybierz wartości dla hello następujące ustawienia, a następnie kliknij **Utwórz**:
    - **Nazwa**: *myVnet1*
    - **Przestrzeń adresowa**: *10.0.0.0/16*
    - **Nazwa podsieci**: *domyślne*
    - **Zakres adresów podsieci**: *10.0.0.0/24*
    - **Subskrypcja**: Wybierz subskrypcję
    - **Grupa zasobów**: Wybierz **Utwórz nowy** , a następnie wprowadź *myResourceGroup*
    - **Lokalizacja**: *wschodnie stany USA*
4. Kliknij przycisk **+ nowy**. W hello **hello wyszukiwania Marketplace** wpisz *sieci wirtualnej*. Kliknij przycisk **sieci wirtualnej** po wyświetleniu w wynikach wyszukiwania hello. 
5. W hello **sieci wirtualnej** bloku, wybierz opcję **klasycznego** w hello **wybierz model wdrożenia** , a następnie kliknij przycisk **Utwórz**.
6. W hello **Utwórz sieć wirtualną** bloku, wprowadź, lub wybierz wartości dla hello następujące ustawienia, a następnie kliknij **Utwórz**:
    - **Nazwa**: *myVnet2*
    - **Przestrzeń adresowa**: *10.1.0.0/16*
    - **Nazwa podsieci**: *domyślne*
    - **Zakres adresów podsieci**: *10.1.0.0/24*
    - **Subskrypcja**: Wybierz subskrypcję
    - **Grupa zasobów**: Wybierz **Użyj istniejącego** i wybierz *myResourceGroup*
    - **Lokalizacja**: *wschodnie stany USA*
7. W hello **wyszukiwania zasobów** pole u góry hello hello portalu, typ *myResourceGroup*. Kliknij przycisk **myResourceGroup** po wyświetleniu w wynikach wyszukiwania hello. Zostanie wyświetlony blok hello **myresourcegroup** grupy zasobów. Grupa zasobów Hello zawiera Witaj dwie sieci wirtualne utworzone w poprzednich krokach.
8. Kliknij przycisk **myVNet1**.
9. W hello **myVnet1** bloku, który jest wyświetlany, kliknij przycisk **komunikacji równorzędnych** z hello pionowy listy opcji na powitania po lewej stronie powitania bloku.
10. W hello **myVnet1 - komunikacji równorzędnych** bloku, które wystąpiły, kliknij przycisk **+ Dodaj**
11. W hello **równorzędna Dodaj** bloku, zostanie wyświetlone, wprowadź, lub wybierz hello następujące opcje, a następnie kliknij **OK**:
     - **Nazwa**: *myVnet1ToMyVnet2*
     - **Model wdrażania sieci wirtualnej**: Wybierz **klasycznego**. 
     - **Subskrypcja**: Wybierz subskrypcję
     - **Sieć wirtualna**: kliknij **wybierz sieć wirtualną**, następnie kliknij przycisk **myVnet2**.
     - **Zezwalaj na dostęp do sieci wirtualnej:** upewnij się, że **włączone** jest zaznaczone.
    W tym samouczku są używane żadne inne ustawienia. Przeczytaj toolearn dotyczące wszystkich ustawień komunikacji równorzędnej, [Zarządzanie komunikacji równorzędnych sieci wirtualnych](virtual-network-manage-peering.md#create-a-peering).
12. Po kliknięciu przycisku **OK** w poprzednim kroku hello hello **równorzędna Dodaj** bloku zamyka i zobacz hello **myVnet1 - komunikacji równorzędnych** ponownie blok. Po kilku sekundach hello równorzędna utworzonego pojawia się w bloku hello. **Połączone** ma na liście hello **RÓWNORZĘDNA stan** kolumny dla hello **myVnet1ToMyVnet2** równorzędna zostanie utworzony.

    Witaj równorzędna zostanie ustanowione. Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
13. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
14. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello etapami hello [zasoby zostaną usunięte](#delete-portal) sekcji tego artykułu.

## <a name="cli"></a>Utwórz równorzędna - wiersza polecenia platformy Azure

1. [Zainstaluj](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello Azure CLI 1.0 toocreate hello sieć wirtualna (klasyczna).
2. Otwórz sesję polecenia, a następnie zaloguj się przy użyciu hello tooAzure `azure login` polecenia.
3. Uruchom hello interfejsu wiersza polecenia w trybie zarządzania usługami, wprowadzając hello `azure config mode asm` polecenia.
4. Wprowadź hello następujące polecenia toocreate hello sieć wirtualna (klasyczna):
 
    ```azurecli
    azure network vnet create --vnet myVnet2 --address-space 10.1.0.0 --cidr 16 --location "East US"
    ```

5. Utwórz grupę zasobów i sieć wirtualną (Resource Manager). Można użyć hello CLI w wersji 1.0 lub 2.0 ([zainstalować](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json)). W tym samouczku hello 2.0 interfejsu wiersza polecenia jest używane toocreate hello sieci wirtualnej (Resource Manager), ponieważ 2.0 musi być używane toocreate hello komunikacji równorzędnej. Wykonanie hello następujących bash skryptu interfejsu wiersza polecenia z komputera lokalnego z hello CLI 2.0.4 lub nowszej. Opcje uruchamiania bash CLI skrypty w kliencie systemu Windows, temacie [działający w systemie Windows hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Można również uruchomić hello skryptu za pomocą hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. Kliknij przycisk hello **wypróbuj** przycisku na powitania skrypt, który pozostaje zgodne z regułami, które wywołuje powłoki chmury, który loguje się użytkownik może zalogować się tooyour konto platformy Azure z. tooexecute hello skrypt, kliknij przycisk hello **kopiowania** przycisk i Wklej zawartość hello w chmurze powłoki, naciśnij klawisz `Enter`.

    ```azurecli-interactive
    #!/bin/bash

    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus

    # Create hello virtual network (Resource Manager).
    az network vnet create \
      --name myVnet1 \
      --resource-group myResourceGroup \
      --location eastus \
      --address-prefix 10.0.0.0/16
    ```

6. Tworzenie sieci wirtualnej komunikacji równorzędnej między Witaj dwie sieci wirtualne utworzone za pośrednictwem hello różne modele wdrażania. Skopiuj powitania po Edytor tekstu tooa skryptu na komputerze. Zastąp `<subscription id>` z Twojego identyfikatora subskrypcji. Jeśli nie znasz identyfikator subskrypcji, wprowadź hello `az account show` polecenia. Witaj wartość **identyfikator** w hello jest identyfikator subskrypcji Wklej hello zmodyfikować skrypt w sesji interfejsu wiersza polecenia tooyour, a następnie naciśnij klawisz `Enter`.

    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group myResourceGroup \
      --name myVnet1 \
      --query id --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --remote-vnet-id /subscriptions/<subscription id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2 \
      --allow-vnet-access
    ```
7. Po wykonaniu skryptu hello, przejrzyj hello komunikacji równorzędnej dla sieci wirtualnej hello (Resource Manager). Kopiuj hello następujące polecenia, wklej go w sesji interfejsu wiersza polecenia i naciśnij klawisz `Enter`:

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    przedstawia dane wyjściowe Hello **połączony** w hello **PeeringState** kolumny. 

    Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).
8. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
9. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-cli) w tym artykule.

## <a name="powershell"></a>Utwórz równorzędna — PowerShell

1. Zainstaluj najnowszą wersję hello PowerShell hello [Azure](https://www.powershellgallery.com/packages/Azure) i [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułów. Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Uruchom sesję programu PowerShell.
3. W programie PowerShell Zaloguj tooAzure wprowadzając hello `Add-AzureAccount` polecenia.
4. toocreate sieci wirtualnej (wdrożenia klasyczne) przy użyciu programu PowerShell, należy utworzyć nową, lub zmodyfikować istniejący plik konfiguracji sieci. Dowiedz się, jak za[eksportu, aktualizować i importowanie plików konfiguracyjnych sieci](virtual-networks-using-network-configuration-file.md). Witaj pliku powinny zawierać następujące hello **VirtualNetworkSite** elementu dla sieci wirtualnej hello używane w tym samouczku:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importowanie pliku konfiguracji sieci zmienione może spowodować zmiany tooexisting sieciami wirtualnymi (klasyczne) w ramach subskrypcji. Upewnij się, tylko dodać hello poprzedniej sieci wirtualnej i nie zmienić lub usunąć istniejące sieci wirtualnych z subskrypcji. 
5. Zaloguj się za tooAzure toocreate hello sieci wirtualnej (Resource Manager), wprowadzając hello `login-azurermaccount` polecenia. Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
6. Utwórz grupę zasobów i sieć wirtualną (Resource Manager). Skopiuj skrypt hello, wklej go do programu PowerShell i naciśnij klawisz `Enter`.

    ```powershell
    # Create a resource group.
      New-AzureRmResourceGroup -Name myResourceGroup -Location eastus

    # Create hello virtual network (Resource Manager).
      $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location eastus
    ```

7. Tworzenie sieci wirtualnej komunikacji równorzędnej między Witaj dwie sieci wirtualne utworzone za pośrednictwem hello różne modele wdrażania. Skopiuj powitania po Edytor tekstu tooa skryptu na komputerze. Zastąp `<subscription id>` z Twojego identyfikatora subskrypcji. Jeśli nie znasz identyfikator subskrypcji, wprowadź hello `Get-AzureRmSubscription` tooview polecenia go. Witaj wartość **identyfikator** w hello zwrócone dane wyjściowe są Twojego identyfikatora subskrypcji. skrypt hello tooexecute, hello kopiowania zmodyfikować skrypt w edytorze tekstów, kliknij prawym przyciskiem myszy w sesji programu PowerShell i naciśnij klawisz `Enter`.

    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name myVnet1ToMyVnet2 `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId /subscriptions/<subscription Id>/resourceGroups/Default-Networking/providers/Microsoft.ClassicNetwork/virtualNetworks/myVnet2
    ```

8. Po wykonaniu skryptu hello, przejrzyj hello komunikacji równorzędnej dla sieci wirtualnej hello (Resource Manager). Kopiuj hello następujące polecenia, wklej go w sesji programu PowerShell i naciśnij klawisz `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    przedstawia dane wyjściowe Hello **połączony** w hello **PeeringState** kolumny.

    Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

9. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
10. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-powershell) w tym artykule.
 
## <a name="permissions"></a>Uprawnienia

konta Hello się, że używasz toocreate sieci wirtualnej komunikacji równorzędnej musi mieć hello ról lub uprawnień. Na przykład jeśli zostały równorzędna dwie sieci wirtualne o nazwach myVnet1 i myVnet2, Twoje konto musi zostać przypisane hello następujące minimalne roli lub uprawnienia dla każdej sieci wirtualnej:
    
|Sieć wirtualna|Model wdrażania|Rola|Uprawnienia|
|---|---|---|---|
|myVnet1|Resource Manager|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
| |Wdrożenie klasyczne|[Współautor klasycznej sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Nie dotyczy|
|myVnet2|Resource Manager|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|
||Wdrożenie klasyczne|[Współautor klasycznej sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#classic-network-contributor)|Microsoft.ClassicNetwork/virtualNetworks/peer|

Dowiedz się więcej o [wbudowane role](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) i przypisywanie uprawnień określonych zbyt[role niestandardowe](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (tylko Resource Manager).

## <a name="delete"></a>Usuwanie zasobów
Po zakończeniu tego samouczka można toodelete hello zasobów, utworzony w samouczek hello w celu uniknięcia opłat użycie. Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów, które znajdują się w grupie zasobów hello.

### <a name="delete-portal"></a>Azure portal

1. W polu wyszukiwania portalu hello wpisz **myResourceGroup**. W wynikach wyszukiwania powitania kliknij **myResourceGroup**.
2. Na powitania **myResourceGroup** bloku, kliknij przycisk hello **usunąć** ikony.
3. Usuwanie hello tooconfirm, w hello **hello typu nazwa grupy zasobów** wprowadź **myResourceGroup**, a następnie kliknij przycisk **usunąć**.

### <a name="delete-cli"></a>Interfejs wiersza polecenia platformy Azure

1. Hello Azure CLI 2.0 toodelete hello sieci wirtualnej (Resource Manager) za pomocą hello następujące polecenie:

    ```azurecli-interactive
    az group delete --name myResourceGroup --yes
    ```

2. Hello Azure CLI 1.0 toodelete hello sieć wirtualna (klasyczna) za pomocą następującego polecenia hello:

    ```azurecli
    azure config mode asm

    azure network vnet delete --vnet myVnet2 --quiet
    ```

### <a name="delete-powershell"></a>Środowiska PowerShell

1. Wprowadź hello następujące polecenia toodelete hello sieci wirtualnej (Resource Manager):

    ```powershell
    Remove-AzureRmResourceGroup -Name myResourceGroup -Force
    ```

2. toodelete hello sieci wirtualnej (wdrożenia klasyczne) przy użyciu programu PowerShell, należy zmodyfikować istniejący plik konfiguracji sieci. Dowiedz się, jak za[eksportu, aktualizować i importowanie plików konfiguracyjnych sieci](virtual-networks-using-network-configuration-file.md). Usuń hello następującego elementu VirtualNetworkSite dla sieci wirtualnej hello używane w tym samouczku:

    ```xml
    <VirtualNetworkSite name="myVnet2" Location="East US">
      <AddressSpace>
        <AddressPrefix>10.1.0.0/16</AddressPrefix>
      </AddressSpace>
      <Subnets>
        <Subnet name="default">
          <AddressPrefix>10.1.0.0/24</AddressPrefix>
        </Subnet>
      </Subnets>
    </VirtualNetworkSite>
    ```

    > [!WARNING]
    > Importowanie pliku konfiguracji sieci zmienione może spowodować zmiany tooexisting sieciami wirtualnymi (klasyczne) w ramach subskrypcji. Upewnij się, tylko Usuń hello poprzedniej sieci wirtualnej, a nie zmienić lub usunąć innych istniejących sieci wirtualnej z subskrypcji. 

## <a name="next-steps"></a>Następne kroki

- Należy dokładnie zapoznać się z ważne [ograniczenia komunikacji równorzędnej sieci wirtualnej i zachowania](virtual-network-manage-peering.md#requirements-and-constraints) przed utworzeniem sieci wirtualnej komunikacji równorzędnej w środowisku produkcyjnym należy używać.
- Więcej informacji na temat wszystkich [sieci wirtualnej komunikacji równorzędnej ustawienia](virtual-network-manage-peering.md#create-a-peering).
- Dowiedz się, jak za[tworzenie koncentratora i gwiazda topologii sieci](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) z sieci wirtualnej komunikacji równorzędnej.
