---
title: "aaaCreate równorzędna sieci wirtualnej platformy Azure - Resource Manager — tej samej subskrypcji | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi utworzone za pomocą Menedżera zasobów istnieje w hello sam subskrypcji platformy Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 026bca75-2946-4c03-b4f6-9f3c5809c69a
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: jdial;narayan;annahar
ms.openlocfilehash: c2d24fdc8103c09c3bfb8e59be12e301d9e9a55a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-peering---resource-manager-same-subscription"></a>Tworzenie sieci wirtualnej równorzędna - Resource Manager tej samej subskrypcji

Z tego samouczka dowiesz się toocreate sieci wirtualnej komunikacji równorzędnej między sieciami wirtualnymi utworzone za pomocą Menedżera zasobów. Obie sieci wirtualne istnieją w hello sam subskrypcji. Witaj komunikacji równorzędnej dwa zasoby umożliwia sieci wirtualnych w różnych sieciach wirtualnych toocommunicate ze sobą z tej samej przepustowości i opóźnień tak, jakby hello zasoby były hello tej samej sieci wirtualnej. Dowiedz się więcej o [równorzędna sieci wirtualnej](virtual-network-peering-overview.md). 

Witaj toocreate kroki sieci wirtualnej komunikacji równorzędnej są różne, w zależności od tego, czy hello sieci wirtualne są w hello tych samych lub różnych subskrypcji i które [modelu wdrożenia usługi Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) hello sieci wirtualne są tworzone za pomocą. Dowiedz się, jak toocreate a wirtualnych sieci równorzędna w innych sytuacjach, klikając hello scenariusza z hello w poniższej tabeli:

|Model wdrażania platformy Azure  | Subskrypcja platformy Azure  |
|--------- |---------|
|[Obie usługi Resource Manager](create-peering-different-subscriptions.md) |Różne|
|[Jeden Resource Manager, co classic](create-peering-different-deployment-models.md) |tym samym|
|[Jeden Resource Manager, co classic](create-peering-different-deployment-models-subscriptions.md) |Różne|

Nie można utworzyć sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnej wdrożone za pośrednictwem hello klasycznego modelu wdrażania. Element równorzędny sieci wirtualnej można tworzyć tylko między dwiema sieciami wirtualnych, które istnieją w hello sam region platformy Azure. Jeśli potrzebujesz sieci wirtualnych tooconnect zarówno utworzonych za pomocą hello klasycznego modelu wdrażania lub istnieje w różnych regionach platformy Azure, można użyć Azure [bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) tooconnect hello sieci wirtualnych. 

Można użyć hello [portalu Azure](#portal), hello Azure [interfejsu wiersza polecenia](#cli) (CLI) Azure [PowerShell](#powershell), lub [szablonu usługi Azure Resource Manager](#template) toocreate sieci wirtualnej komunikacji równorzędnej. Kliknij dowolny z hello poprzedniego narzędzia łącza toogo, bezpośrednio toohello kroki tworzenia sieci wirtualnej komunikacji równorzędnej narzędzie wyboru.

## <a name="portal"></a>Utwórz równorzędna - portalu Azure

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
4. Wykonaj kroki od 2 do 3 ponownie określanie hello następujące wartości w kroku 3:
    - **Nazwa**: *myVnet2*
    - **Przestrzeń adresowa**: *10.1.0.0/16*
    - **Nazwa podsieci**: *domyślne*
    - **Zakres adresów podsieci**: *10.1.0.0/24*
    - **Subskrypcja**: Wybierz subskrypcję
    - **Grupa zasobów**: Wybierz **Użyj istniejącego** i wybierz *myResourceGroup*
    - **Lokalizacja**: *wschodnie stany USA*
5. W hello **wyszukiwania zasobów** pole u góry hello hello portalu, typ *myResourceGroup*. Kliknij przycisk **myResourceGroup** po wyświetleniu w wynikach wyszukiwania hello. Zostanie wyświetlony blok hello **myresourcegroup** grupy zasobów. Grupa zasobów Hello zawiera Witaj dwie sieci wirtualne utworzone w poprzednich krokach.
6. Kliknij przycisk **myVNet1**.
7. W hello **myVnet1** bloku, który jest wyświetlany, kliknij przycisk **komunikacji równorzędnych** z hello pionowy listy opcji na powitania po lewej stronie powitania bloku.
8. W hello **myVnet1 - komunikacji równorzędnych** bloku, które wystąpiły, kliknij przycisk **+ Dodaj**
9. W hello **równorzędna Dodaj** bloku, zostanie wyświetlone, wprowadź, lub wybierz hello następujące opcje, a następnie kliknij **OK**:
     - **Nazwa**: *myVnet1ToMyVnet2*
     - **Model wdrażania sieci wirtualnej**: Wybierz **Resource Manager**. 
     - **Subskrypcja**: Wybierz subskrypcję
     - **Sieć wirtualna**: kliknij **wybierz sieć wirtualną**, następnie kliknij przycisk **myVnet2**.
     - **Zezwalaj na dostęp do sieci wirtualnej:** upewnij się, że **włączone** jest zaznaczone.
    W tym samouczku są używane żadne inne ustawienia. Przeczytaj toolearn dotyczące wszystkich ustawień komunikacji równorzędnej, [Zarządzanie komunikacji równorzędnych sieci wirtualnych](virtual-network-manage-peering.md#create-a-peering).
10. Po kliknięciu przycisku **OK** w poprzednim kroku hello hello **równorzędna Dodaj** bloku zamyka i zobacz hello **myVnet1 - komunikacji równorzędnych** ponownie blok. Po kilku sekundach hello równorzędna utworzonego pojawia się w bloku hello. **Zainicjowane** ma na liście hello **RÓWNORZĘDNA stan** kolumny dla hello **myVnet1ToMyVnet2** równorzędna zostanie utworzony. Już połączyć za pomocą Vnet1 tooVnet2, ale teraz musi równorzędnego myVnet2 toomyVnet1. równorzędna Hello należy utworzyć w obu kierunkach tooenable zasobów w toocommunicate sieci wirtualnych hello ze sobą.
11. Wykonaj kroki 5 – 10 ponownie dla myVnet2.  Nazwa hello równorzędna *myVnet2ToMyVnet1*.
12. Kilka sekund po kliknięciu przycisku **OK** toocreate hello komunikacji równorzędnej dla MyVnet2, hello **myVnet2ToMyVnet1** równorzędna właśnie utworzony znajduje się **połączony** w hello  **Komunikacja RÓWNORZĘDNA stan** kolumny.
13. Wykonaj kroki 5-7 ponownie dla MyVnet1. Witaj **RÓWNORZĘDNA stan** dla hello **myVnet1ToVNet2** komunikacji równorzędnej jest teraz również **połączony**. równorzędna Hello zostanie pomyślnie nawiązane po **połączony** w hello **RÓWNORZĘDNA stan** kolumny dla obu sieci wirtualnych w komunikacji równorzędnej hello.
14. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
15. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello etapami hello [zasoby zostaną usunięte](#delete-portal) sekcji tego artykułu.

Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="cli"></a>Utwórz równorzędna - wiersza polecenia platformy Azure

Witaj następującego skryptu:

- Wymaga hello Azure CLI w wersji 2.0.4 lub nowszej. Wersja hello toofind, uruchom hello `az --version` polecenia. Jeśli potrzebujesz tooupgrade, zobacz [zainstalować Azure CLI 2.0]( /cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json).
- Działanie powłoki Bash. Aby wyświetlić opcje uruchamiania skryptów wiersza polecenia platformy Azure na kliencie systemu Windows, zobacz [działający w systemie Windows hello Azure CLI](../virtual-machines/windows/cli-options.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Zamiast instalowania hello interfejsu wiersza polecenia i jego zależności, możesz użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. Kliknij przycisk hello **wypróbuj** przycisku na powitania skrypt, który pozostaje zgodne z regułami, które wywołuje powłoki chmury, który loguje się użytkownik może zalogować się tooyour konto platformy Azure z. tooexecute hello skrypt, kliknij przycisk hello **kopiowania** przycisk i Wklej zawartość hello w chmurze powłoki.

1. Utwórz grupę zasobów i dwie sieci wirtualne.

    ```azurecli-interactive
    #!/bin/bash

    # Variables for common values used throughout hello script.
    rgName="myResourceGroup"
    location="eastus"

    # Create a resource group.
    az group create \
      --name $rgName \
      --location $location

    # Create virtual network 1.
    az network vnet create \
      --name myVnet1 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.0.0.0/16

    # Create virtual network 2.
    az network vnet create \
      --name myVnet2 \
      --resource-group $rgName \
      --location $location \
      --address-prefix 10.1.0.0/16
    ```

2. Tworzenie sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnymi hello.
 
    ```azurecli-interactive
    # Get hello id for VNet1.
    vnet1Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet1 \
      --query id --out tsv)

    # Get hello id for VNet2.
    vnet2Id=$(az network vnet show \
      --resource-group $rgName \
      --name myVnet2 \
      --query id \
      --out tsv)

    # Peer VNet1 tooVNet2.
    az network vnet peering create \
      --name myVnet1ToMyVnet2 \
      --resource-group $rgName \
      --vnet-name myVnet1 \
      --remote-vnet-id $vnet2Id \
      --allow-vnet-access

    # Peer VNet2 tooVNet1.
    az network vnet peering create \
      --name myVnet2ToMyVnet1 \
      --resource-group $rgName \
      --vnet-name myVnet2 \
      --remote-vnet-id $vnet1Id \
      --allow-vnet-access
    ```

3. Po wykonaniu skryptu hello, przejrzyj komunikacji równorzędnych powitania dla każdej sieci wirtualnej. 

    ```azurecli-interactive
    az network vnet peering list \
      --resource-group myResourceGroup \
      --vnet-name myVnet1 \
      --output table
    ```
    
    Poprzednie polecenie hello ponownie uruchomić, zastępując *myVnet1* z *myVnet2*. dane wyjściowe Hello obu polecenia pokazuje **połączony** w hello **PeeringState** kolumny.

     Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

4. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
5. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-cli) w tym artykule.


## <a name="powershell"></a>Utwórz równorzędna — PowerShell

1. Zainstaluj najnowszą wersję hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu. Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. toostart sesję programu PowerShell Przejdź zbyt**Start**, wprowadź **powershell**, a następnie kliknij przycisk **programu PowerShell**.
3. W programie PowerShell Zaloguj tooAzure wprowadzając hello `login-azurermaccount` polecenia. Zaloguj się przy użyciu konta Hello musi mieć hello toocreate niezbędne uprawnienia sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
4. Utwórz grupę zasobów i dwie sieci wirtualne. skrypt hello tooexecute, następujące hello kopii skryptu, wklej go do programu PowerShell, a następnie naciśnij `Enter` po ostatnim wierszu hello jest wyświetlany na ekranie powitania:

    ```powershell
    # Variables for common values used throughout hello script.
    $rgName='myResourceGroup'
    $location='eastus'

    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name $rgName `
      -Location $location

    # Create virtual network 1.
    $vnet1 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet1' `
      -AddressPrefix '10.0.0.0/16' `
      -Location $location

    # Create virtual network 2.
    $vnet2 = New-AzureRmVirtualNetwork `
      -ResourceGroupName $rgName `
      -Name 'myVnet2' `
      -AddressPrefix '10.1.0.0/16' `
      -Location $location
    ```

5. Tworzenie sieci wirtualnej komunikacji równorzędnej między dwiema sieciami wirtualnymi hello. Następujące hello kopii skryptu, Wklej tooPowerShell i naciśnij klawisz `Enter` po ostatnim wierszu hello jest wyświetlany na ekranie powitania:
    ```powershell
    # Peer VNet1 tooVNet2.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet1ToMyVnet2' `
      -VirtualNetwork $vnet1 `
      -RemoteVirtualNetworkId $vnet2.Id

    # Peer VNet2 tooVNet1.
    Add-AzureRmVirtualNetworkPeering `
      -Name 'myVnet2ToMyVnet1' `
      -VirtualNetwork $vnet2 `
      -RemoteVirtualNetworkId $vnet1.Id
    ```
6. tooreview hello podsieci sieci wirtualnej hello, kopiowania hello następujące polecenia, Wklej tooPowerShell, a następnie naciśnij `Enter`:

    ```powershell
    Get-AzureRmVirtualNetworkPeering `
      -ResourceGroupName myResourceGroup `
      -VirtualNetworkName myVnet1 `
      | Format-Table VirtualNetworkName, PeeringState
    ```

    Poprzednie polecenie hello ponownie uruchomić, zastępując *myVnet1* z *myVnet2*. dane wyjściowe Hello obu polecenia pokazuje **połączony** w hello **PeeringState** kolumny.
7. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
8. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-powershell) w tym artykule.

Dowolnych zasobów platformy Azure, utworzone w każdej sieci wirtualnej są teraz możliwe toocommunicate ze sobą za pośrednictwem ich adresy IP. Jeśli używasz domyślnego rozwiązania Azure nazwy dla sieci wirtualnych hello, hello zasoby w sieciach wirtualnych hello nie są możliwe tooresolve nazw w sieciach wirtualnych hello. Jeśli chcesz nazwy tooresolve między sieciami wirtualnymi w komunikacji równorzędnej, należy utworzyć serwer DNS. Dowiedz się, jak tooset się [rozpoznawanie nazw przy użyciu serwera DNS](virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server).

## <a name="template"></a>Utwórz równorzędna - szablonu usługi Resource Manager

1. Odwołanie [tworzenie sieci wirtualnej komunikacji równorzędnej](https://azure.microsoft.com/resources/templates/201-vnet-to-vnet-peering) szablonu usługi Resource Manager. Instrukcje znajdują się z szablonem hello wdrażania szablonu hello przy użyciu hello portalu Azure, programu PowerShell lub hello wiersza polecenia platformy Azure. Dziennik w narzędziu toowhichever, wybierz szablon hello toodeploy przy użyciu konta, które ma hello toocreate niezbędnych uprawnień sieci wirtualnej komunikacji równorzędnej. Zobacz hello [uprawnienia](#permissions) sekcji tego artykułu, aby uzyskać szczegółowe informacje.
2. **Opcjonalne**: Chociaż tworzenia maszyn wirtualnych nie została uwzględniona w tym samouczku, można utworzyć maszynę wirtualną w każdej sieci wirtualnej i połączyć z jednej maszyny wirtualnej toohello innych, toovalidate łączności.
3. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello etapami hello [zasoby zostaną usunięte](#delete) hello sekcji tego artykułu, za pomocą portalu Azure, programu PowerShell lub hello wiersza polecenia platformy Azure.

## <a name="permissions"></a>Uprawnienia

konta Hello się, że używasz toocreate sieci wirtualnej komunikacji równorzędnej musi mieć hello ról lub uprawnień. Na przykład jeśli zostały równorzędna dwie sieci wirtualne o nazwach VNet1 i VNet2, Twoje konto musi zostać przypisane hello następujące minimalne roli lub uprawnienia dla każdej sieci wirtualnej:
    
|Sieć wirtualna|Rola|Uprawnienia|
|---|---|---|
|VNet1|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/virtualNetworkPeerings/write|
|VNet2|[Współautor sieci](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor)|Microsoft.Network/virtualNetworks/peer|

Dowiedz się więcej o [wbudowane role](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) i przypisywanie uprawnień określonych zbyt[role niestandardowe](../active-directory/role-based-access-control-custom-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json) (tylko Resource Manager).

## <a name="delete"></a>Usuwanie zasobów
Po zakończeniu tego samouczka można toodelete hello zasobów, utworzony w samouczek hello w celu uniknięcia opłat użycie. Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów, które znajdują się w grupie zasobów hello.

### <a name="delete-portal"></a>Azure portal

1. W polu wyszukiwania portalu hello wpisz **myResourceGroup**. W wynikach wyszukiwania powitania kliknij **myResourceGroup**.
2. Na powitania **myResourceGroup** bloku, kliknij przycisk hello **usunąć** ikony.
3. Usuwanie hello tooconfirm, w hello **hello typu nazwa grupy zasobów** wprowadź **myResourceGroup**, a następnie kliknij przycisk **usunąć**.

### <a name="delete-cli"></a>Interfejs wiersza polecenia platformy Azure

Wprowadź hello następujące polecenie:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>Środowiska PowerShell

Wprowadź hello następujące polecenie:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -force
```

## <a name="next-steps"></a>Następne kroki

- Należy dokładnie zapoznać się z ważne [ograniczenia komunikacji równorzędnej sieci wirtualnej i zachowania](virtual-network-manage-peering.md#requirements-and-constraints) przed utworzeniem sieci wirtualnej komunikacji równorzędnej w środowisku produkcyjnym należy używać.
- Więcej informacji na temat wszystkich [sieci wirtualnej komunikacji równorzędnej ustawienia](virtual-network-manage-peering.md#create-a-peering).
- Dowiedz się, jak za[tworzenie koncentratora i gwiazda topologii sieci](/azure/architecture/reference-architectures/hybrid-networking/hub-spoke?toc=%2fazure%2fvirtual-network%2ftoc.json#vnet-peering) z sieci wirtualnej komunikacji równorzędnej.
