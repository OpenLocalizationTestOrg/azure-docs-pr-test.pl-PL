---
title: "sieć wirtualna platformy Azure z wieloma podsieciami aaaCreate | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnej z wieloma podsieciami na platformie Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ad679a4-a959-4e48-a317-d9f5655a442b
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/26/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: 0f56fa6ac24537d33b8e217f5b03f387826ab487
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-multiple-subnets"></a>Tworzenie sieci wirtualnej z wieloma podsieciami

W tym samouczku Dowiedz się, jak toocreate podstawowe sieci wirtualnej platformy Azure, która ma oddzielne podsieci publiczne i prywatne. W podsieci można utworzyć zasobów platformy Azure, takich jak maszyny wirtualne, środowiska usługi aplikacji, zestawy skalowania maszyny wirtualnej, Azure HDInsight i usługi w chmurze. Zasoby w sieci wirtualne mogą komunikować się ze sobą oraz z zasobami w sieci wirtualnej podłączonej tooa innych sieci.

Witaj poniższe sekcje zawierają czy możesz zrobić toocreate sieć wirtualną przy użyciu hello [portalu Azure](#portal), hello interfejsu wiersza polecenia platformy Azure ([interfejsu wiersza polecenia Azure](#azure-cli)), [programu Azure PowerShell ](#powershell)i [szablonu usługi Azure Resource Manager](#resource-manager-template). wynik Hello jest hello sam, niezależnie od tego narzędzia, których można użyć sieci wirtualnej hello toocreate. Kliknij sekcję narzędzia łącze toogo toothat hello samouczka. Dowiedz się więcej na temat wszystkich [sieci wirtualnej](virtual-network-manage-network.md) i [podsieci](virtual-network-manage-subnet.md) ustawienia.

W tym artykule przedstawiono kroki toocreate sieć wirtualną przy użyciu modelu wdrażania Menedżera zasobów hello, czyli hello model wdrażania, które firma Microsoft zaleca używanie podczas tworzenia nowej sieci wirtualnej. Jeśli potrzebujesz toocreate sieć wirtualna (klasyczna), zobacz [utworzyć sieć wirtualną (klasyczne)](create-virtual-network-classic.md). Jeśli nie masz doświadczenia w obsłudze modele wdrażania platformy Azure, zobacz [modele wdrażania zrozumieć Azure](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json).

## <a name="portal"></a>Azure portal

1. W przeglądarce sieci Web, przejdź do pozycji toohello [portalu Azure](https://portal.azure.com). Zaloguj się za pomocą programu [konta Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Jeśli nie masz konta platformy Azure, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).
2. W portalu powitania kliknij **+ nowy** > **sieci** > **sieci wirtualnej**.
3. Na powitania **Utwórz sieć wirtualną** bloku, wprowadź następujące wartości hello, a następnie kliknij przycisk **Utwórz**:

    |Ustawienie|Wartość|
    |---|---|
    |Nazwa|myVnet|
    |Przestrzeń adresowa|10.0.0.0/16|
    |Nazwa podsieci|Publiczne|
    |Zakres adresów podsieci|10.0.0.0/24|
    |Grupa zasobów|Pozostaw **Utwórz nowy** zaznaczone, a następnie wprowadź **myResourceGroup**.|
    |Subskrypcji i lokalizacji|Wybierz subskrypcji i lokalizacji.

    Jeśli nowy tooAzure, Dowiedz się więcej o [grup zasobów](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subskrypcje](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), i [lokalizacje](https://azure.microsoft.com/regions) (nazywana także tooas *regionów*).
4. W portalu hello można utworzyć tylko jedną podsieć, podczas tworzenia sieci wirtualnej. W tym samouczku utworzysz drugiej podsieci po utworzeniu sieci wirtualnej hello. Później można utworzyć zasoby internetowe dostępny w hello **publicznego** podsieci. Można także utworzyć zasoby, które nie są dostępne z hello Internet w hello **prywatnej** podsieci. toocreate hello drugiej podsieci, w hello **wyszukiwania zasobów** polu u góry hello hello strony, wprowadź **myVnet**. W wynikach wyszukiwania powitania kliknij **myVnet**. Jeśli masz wiele sieci wirtualnych, z hello tej samej nazwie w ramach subskrypcji, sprawdź hello grupy zasobów, które znajdują się w każdej sieci wirtualnej. Upewnij się, kliknij przycisk hello **myVnet** Wyszukaj wynik, który ma grupy zasobów hello **myResourceGroup**.
5. Na powitania **myVnet** bloku, w obszarze **ustawienia**, kliknij przycisk **podsieci**.
6. Na powitania **myVnet - podsieci** bloku, kliknij przycisk **+ podsieci**.
7. Na powitania **Dodaj podsieć** bloku dla **nazwa**, wprowadź **prywatnej**. Aby uzyskać **zakres adresów**, wprowadź **10.0.1.0/24**.  Kliknij przycisk **OK**.
8. Na powitania **myVnet - podsieci** bloku, przejrzyj hello podsieci. Zostanie wyświetlony hello **publicznego** i **prywatnej** podsieci, które zostały utworzone.
9. **Opcjonalnie:** toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-portal) w tym artykule.

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

Polecenia interfejsu wiersza polecenia platformy Azure są hello takie same, czy można wykonywać polecenia hello z systemu Windows, Linux lub macOS. Jednak ma różnic skryptów powłoki systemu operacyjnego. skrypt Hello hello następujące kroki wykonuje powłoki Bash. 

1. [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello Azure CLI zainstalowane. tooget pomocy dla poleceń interfejsu wiersza polecenia, wpisz `az <command> --help`. Zamiast instalowania hello interfejsu wiersza polecenia i jego wymagania wstępne można użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Witaj powłoki chmury ma hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. toouse hello powłoki chmury kliknij hello powłoki chmury (**> _**) u góry hello hello [portal](https://portal.azure.com) lub po prostu kliknij hello *wypróbuj* przycisk hello kroków, które należy wykonać. 
2. Jeśli uruchomiony lokalnie hello interfejsu wiersza polecenia, zaloguj się za tooAzure z hello `az login` polecenia. Jeśli używasz hello powłoki chmury, użytkownik jest już zalogowany.
3. Witaj przeglądu następującego skryptu i jego komentarzami. W przeglądarce Skopiuj skrypt hello i wklej go do sesji interfejsu wiersza polecenia:

    ```azurecli-interactive
    #!/bin/bash
    
    # Create a resource group.
    az group create \
      --name myResourceGroup \
      --location eastus
    
    # Create a virtual network with one subnet named Public.
    az network vnet create \
      --name myVnet \
      --resource-group myResourceGroup \
      --subnet-name Public
    
    # Create an additional subnet named Private in hello virtual network.
    az network vnet subnet create \
      --name Private \
      --address-prefix 10.0.1.0/24 \
      --vnet-name myVnet \
      --resource-group myResourceGroup
    ```
    
4. Po zakończeniu skryptu hello uruchomiona, przejrzyj podsieci hello hello sieci wirtualnej. Skopiuj hello następujące polecenie, a następnie wklej go do sesji interfejsu wiersza polecenia:

    ```azurecli
    az network vnet subnet list --resource-group myResourceGroup --vnet-name myVnet --output table
    ```

5. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-cli) w tym artykule.

## <a name="powershell"></a>PowerShell

1. Zainstaluj najnowszą wersję hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu. Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. W sesji programu PowerShell Zaloguj tooAzure z Twojej [konta Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account) przy użyciu hello `login-azurermaccount` polecenia.

3. Witaj przeglądu następującego skryptu i jego komentarzami. W przeglądarce Skopiuj skrypt hello i wklej go do sesji programu PowerShell:

    ```powershell
    # Create a resource group.
    New-AzureRmResourceGroup `
      -Name myResourceGroup `
      -Location eastus
    
    # Create hello public and private subnets.
    $Subnet1 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Public `
      -AddressPrefix 10.0.0.0/24
    $Subnet2 = New-AzureRmVirtualNetworkSubnetConfig `
      -Name Private `
      -AddressPrefix 10.0.1.0/24
    
    # Create a virtual network.
    $Vnet=New-AzureRmVirtualNetwork `
      -ResourceGroupName myResourceGroup `
      -Location eastus `
      -Name myVnet `
      -AddressPrefix 10.0.0.0/16 `
      -Subnet $Subnet1,$Subnet2
    ```

4. podsieci hello tooreview hello sieci wirtualnej, skopiuj hello następujące polecenie, a następnie wkleić ją w sesji programu PowerShell:

    ```powershell
    $Vnet.subnets | Format-Table Name, AddressPrefix
    ```

5. **Opcjonalne**: toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello czynnościach w ramach [zasoby zostaną usunięte](#delete-powershell) w tym artykule.

## <a name="resource-manager-template"></a>Szablon usługi Resource Manager

Sieć wirtualną można wdrożyć za pomocą szablonu usługi Azure Resource Manager. toolearn więcej informacji na temat szablonów, zobacz [co to jest Menedżer zasobów](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#template-deployment). Szablon hello tooaccess i toolearn o jego parametrów, zobacz hello [utworzyć sieć wirtualną z dwiema podsieciami](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) szablonu. Witaj szablonu można wdrożyć przy użyciu hello [portal](#template-portal), [interfejsu wiersza polecenia Azure](#template-cli), lub [PowerShell](#template-powershell).

**Opcjonalnie:** toodelete hello zasobów, które możesz utworzyć w tym samouczku, pełną hello kroków w dowolnym podsekcjach [zasoby zostaną usunięte](#delete) w tym artykule.

### <a name="template-portal"></a>Azure portal

1. W przeglądarce otwórz hello [strony szablonu](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets).
2. Kliknij przycisk hello **wdrażanie tooAzure** przycisku. Jeśli jeszcze nie zalogowano tooAzure, zaloguj się na ekranie logowania do portalu Azure hello, który pojawia się.
3. Zaloguj się przy użyciu portalu toohello Twojego [konta Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Jeśli nie masz konta platformy Azure, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).
4. Wprowadź następujące wartości parametrów hello hello:

    |Parametr|Wartość|
    |---|---|
    |Subskrypcja|Wybierz subskrypcję|
    |Grupa zasobów|myResourceGroup|
    |Lokalizacja|Wybierz lokalizację|
    |Nazwa sieci wirtualnej|myVnet|
    |Prefiks adresu sieci wirtualnej|10.0.0.0/16|
    |Subnet1Prefix|10.0.0.0/24|
    |Subnet1Name|Publiczne|
    |Subnet2Prefix|10.0.1.0/24|
    |Subnet2Name|Prywatne|

5. Akceptuję toohello warunków i postanowień, a następnie kliknij przycisk **zakupu** sieci wirtualnej hello toodeploy.

### <a name="template-cli"></a>Interfejs wiersza polecenia platformy Azure

1. [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello Azure CLI zainstalowane. tooget pomocy dla poleceń interfejsu wiersza polecenia, wpisz `az <command> --help`. Zamiast instalowania hello interfejsu wiersza polecenia i jego wymagania wstępne można użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Witaj powłoki chmury ma hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. toouse hello powłoki chmury kliknij hello powłoki chmury **> _** u góry hello hello [portal](https://portal.azure.com), lub po prostu kliknij hello **wypróbuj** przycisk hello kroków, które należy wykonać. 
2. Jeśli uruchomiony lokalnie hello interfejsu wiersza polecenia, zaloguj się za tooAzure z hello `az login` polecenia. Jeśli używasz hello powłoki chmury, użytkownik jest już zalogowany.
3. toocreate grupę zasobów dla sieci wirtualnej hello kopiowania hello następujące polecenie i wklej go do sesji interfejsu wiersza polecenia:

    ```azurecli-interactive
    az group create --name myResourceGroup --location eastus
    ```
    
4. Witaj szablonu można wdrożyć przy użyciu jednej z hello następujące opcje parametrów:
    - **Domyślne wartości parametrów**. Wprowadź hello następujące polecenie:
    
        ```azurecli-interactive
        az group deployment create --resource-group myResourceGroup --name VnetTutorial --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json`
        ```
    - **Wartości parametrów niestandardowych**. Pobierz i zmodyfikować szablon hello przed wdrożeniem hello szablonu. Możesz również wdrażanie szablonu hello przy użyciu parametrów wiersza polecenia hello lub wdrażanie szablonu hello przy użyciu pliku oddzielne parametrów. pliki szablonów i parametry toodownload hello, kliknij przycisk hello **Przejdź w serwisie GitHub** przycisk na powitania [utworzyć sieć wirtualną z dwiema podsieciami](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) strony szablonu. W usłudze GitHub kliknij hello **azuredeploy.parameters.json** lub **azuredeploy.json** pliku. Następnie kliknij przycisk hello **Raw** przycisk toodisplay hello pliku. W przeglądarce skopiuj zawartość hello hello pliku. Zapisz plik tooa zawartość hello na tym komputerze. Można zmodyfikować wartości parametrów hello w szablonie hello, lub wdrażanie szablonu hello przy użyciu pliku oddzielne parametrów.  

    więcej informacji o toolearn, jak szablony toodeploy za pomocą tych metod, wpisz `az group deployment create --help`.

### <a name="template-powershell"></a>Środowiska PowerShell

1. Zainstaluj najnowszą wersję hello PowerShell hello [AzureRm](https://www.powershellgallery.com/packages/AzureRM/) modułu. Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. W sesji programu PowerShell, toosign przy użyciu programu [konta Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account), wprowadź `login-azurermaccount`.
3. toocreate grupę zasobów dla sieci wirtualnej hello, wprowadź następujące polecenie hello:

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location eastus
    ```
    
4. Witaj szablonu można wdrożyć przy użyciu jednej z hello następujące opcje parametrów:
    - **Domyślne wartości parametrów**. Wprowadź hello następujące polecenie:
    
        ```powershell
        New-AzureRmResourceGroupDeployment -Name VnetTutorial -ResourceGroupName myResourceGroup -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vnet-two-subnets/azuredeploy.json
        ```
        
    - **Wartości parametrów niestandardowych**. Pobierz i zmodyfikować hello szablon przed jego wdrożeniem. Możesz również wdrażanie szablonu hello przy użyciu parametrów wiersza polecenia hello lub wdrażanie szablonu hello przy użyciu pliku oddzielne parametrów. pliki szablonów i parametry toodownload hello, kliknij przycisk hello **Przejdź w serwisie GitHub** przycisk na powitania [utworzyć sieć wirtualną z dwiema podsieciami](https://azure.microsoft.com/resources/templates/101-vnet-two-subnets/) strony szablonu. W usłudze GitHub kliknij hello **azuredeploy.parameters.json** lub **azuredeploy.json** pliku. Następnie kliknij przycisk hello **Raw** przycisk toodisplay hello pliku. W przeglądarce skopiuj zawartość hello hello pliku. Zapisz plik tooa zawartość hello na tym komputerze. Można zmodyfikować wartości parametrów hello w szablonie hello, lub wdrażanie szablonu hello przy użyciu pliku oddzielne parametrów.  

    więcej informacji o toolearn, jak szablony toodeploy za pomocą tych metod, wpisz `Get-Help New-AzureRmResourceGroupDeployment`. 

## <a name="delete"></a>Usuwanie zasobów

Po zakończeniu tego samouczka można toodelete hello zasoby, które zostały utworzone, tak aby nie wiąże się z opłatami użycia. Usunięcie grupy zasobów powoduje usunięcie wszystkich zasobów, które znajdują się w grupie zasobów hello.

### <a name="delete-portal"></a>Azure portal

1. W polu wyszukiwania portalu hello wpisz **myResourceGroup**. W wynikach wyszukiwania powitania kliknij **myResourceGroup**.
2. Na powitania **myResourceGroup** bloku, kliknij przycisk hello **usunąć** ikony.
3. Usuwanie hello tooconfirm, w hello **hello typu nazwa grupy zasobów** wprowadź **myResourceGroup**, a następnie kliknij przycisk **usunąć**.

### <a name="delete-cli"></a>Interfejs wiersza polecenia platformy Azure

W sesji interfejsu wiersza polecenia wprowadź hello następujące polecenie:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

### <a name="delete-powershell"></a>Środowiska PowerShell

W sesji programu PowerShell wprowadź następujące polecenie hello:

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a>Następne kroki

- Zobacz toolearn o wszystkich sieci wirtualnej i ustawienia podsieci [Zarządzanie sieciami wirtualnymi](virtual-network-manage-network.md#view-vnet) i [Zarządzanie podsieci sieci wirtualnej](virtual-network-manage-subnet.md#create-subnet). Istnieją różne opcje dotyczące korzystania z sieci wirtualnych i podsieci w środowisku produkcyjnym wymagania różnych toomeet środowiska.
- toofilter dla ruchu przychodzącego i wychodzącego ruchu w podsieci, tworzenie i stosowanie [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) toosubnets.
- Utwórz [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) maszyny wirtualnej, a następnie podłącz je tooan istniejącej sieci wirtualnej.
- tooconnect dwie sieci wirtualne w tej samej lokalizacji platformy Azure Witaj, Utwórz [sieci wirtualnej komunikacji równorzędnej](virtual-network-peering-overview.md) między sieciami wirtualnymi hello.
- Połączyć sieć lokalną tooan hello w sieci wirtualnej przy użyciu [bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) obwodu.
