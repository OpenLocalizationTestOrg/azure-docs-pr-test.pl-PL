---
title: "aaaCreate sieci wirtualnej platformy Azure (klasyczną) z wieloma podsieciami | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate sieci wirtualnej (wdrożenia klasyczne) z wieloma podsieciami na platformie Azure."
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: jdial
ms.custom: 
ms.openlocfilehash: cc7b9ad08d5c26dba09584762bedf614d2847032
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-classic-with-multiple-subnets"></a>Tworzenie sieci wirtualnej (wdrożenia klasyczne) z wieloma podsieciami

> [!IMPORTANT]
> Platforma Azure ma dwa [różne modele wdrażania](../azure-resource-manager/resource-manager-deployment-model.md?toc=%2fazure%2fvirtual-network%2ftoc.json) do tworzenia i pracy z zasobami: Resource Manager i model klasyczny. W tym artykule omówiono przy użyciu hello klasycznego modelu wdrażania. Firma Microsoft zaleca utworzenie większości nowych sieci wirtualnych za pomocą hello [Resource Manager](virtual-networks-create-vnet-arm-pportal.md) modelu wdrażania.

W tym samouczku Dowiedz się, jak toocreate Podstawowa sieć wirtualna platformy Azure (klasyczne) ma oddzielne podsieci publiczne i prywatne. Można utworzyć zasobów platformy Azure, takich jak maszyny wirtualne i usługi w chmurze w podsieci. Zasoby utworzone w sieciach wirtualnych (klasyczne) może komunikować się ze sobą oraz z zasobami w sieci wirtualnej podłączonej tooa innych sieci.

Dowiedz się więcej na temat wszystkich [sieci wirtualnej](virtual-network-manage-network.md) i [podsieci](virtual-network-manage-subnet.md) ustawienia.

> [!WARNING]
> Sieci wirtualne (klasyczne) są natychmiast usuwane przez Azure podczas [subskrypcja została wyłączona](../billing/billing-subscription-become-disable.md?toc=%2fazure%2fvirtual-network%2ftoc.json#you-reached-your-spending-limit). Sieci wirtualne (klasyczne) są usuwane niezależnie od tego, czy istnieje zasobów w sieci wirtualnej hello. Jeśli później ponownie włączysz hello subskrypcji, zasobów, które były dostępne w sieci wirtualnej hello muszą zostać ponownie utworzone.

Sieć wirtualna (klasyczna) można utworzyć za pomocą hello [portalu Azure](#portal), hello [Azure interfejsu wiersza polecenia (CLI) 1.0](#azure-cli), lub [PowerShell](#powershell).

## <a name="portal"></a>Portal

1. W przeglądarce sieci Web, przejdź do pozycji toohello [portalu Azure](https://portal.azure.com). Zaloguj się za pomocą programu [konta Azure](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#account). Jeśli nie masz konta platformy Azure, możesz zarejestrować się w celu [bezpłatnej wersji próbnej](https://azure.microsoft.com/offers/ms-azr-0044p).
2. Kliknij przycisk **+ nowy** w portalu hello.
3. Wprowadź *sieci wirtualnej* w hello **hello wyszukiwania portalu Marketplace** u góry hello hello **nowy** wyświetlonym bloku.  Kliknij przycisk **sieci wirtualnej** po wyświetleniu w wynikach wyszukiwania hello.
4. Wybierz **klasycznego** w hello **wybierz model wdrożenia** polu w hello **sieci wirtualnej** bloku, zostanie wyświetlone, następnie kliknij przycisk **Utwórz**. 
5. Wprowadź następujące wartości na powitania hello **Utwórz sieć wirtualną (klasyczne)** bloku, a następnie kliknij przycisk **Utwórz**:

    |Ustawienie|Wartość|
    |---|---|
    |Nazwa|myVnet|
    |Przestrzeń adresowa|10.0.0.0/16|
    |Nazwa podsieci|Publiczne|
    |Zakres adresów podsieci|10.0.0.0/24|
    |Grupa zasobów|Pozostaw **Utwórz nowy** zaznaczone, a następnie wprowadź **myResourceGroup**.|
    |Subskrypcji i lokalizacji|Wybierz subskrypcji i lokalizacji.

    Jeśli nowy tooAzure, Dowiedz się więcej o [grup zasobów](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group), [subskrypcje](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription), i [lokalizacje](https://azure.microsoft.com/regions) (nazywana także tooas *regionów*).
4. W portalu hello można utworzyć tylko jedną podsieć, podczas tworzenia sieci wirtualnej. W tym samouczku utworzysz drugiej podsieci po utworzeniu sieci wirtualnej hello. Później można utworzyć zasoby internetowe dostępny w hello **publicznego** podsieci. Można także utworzyć zasoby, które nie są dostępne z hello Internet w hello **prywatnej** podsieci. toocreate hello drugiej podsieci, wprowadź **myVnet** w hello **wyszukiwania zasobów** pole u góry hello hello strony. Kliknij przycisk **myVnet** po wyświetleniu w wynikach wyszukiwania hello.
5. Kliknij przycisk **podsieci** (w hello **ustawienia** sekcji) na powitania **Utwórz sieć wirtualną (klasyczne)** wyświetlonym bloku.
6. Kliknij przycisk **+ Dodaj** na powitania **myVnet - podsieci** wyświetlonym bloku.
7. Wprowadź **prywatnej** dla **nazwa** na powitania **Dodaj podsieć** bloku. Wprowadź **10.0.1.0/24** dla **zakres adresów**.  Kliknij przycisk **OK**.
8. Na powitania **myVnet - podsieci** bloku widać hello **publicznego** i **prywatnej** podsieci, które zostały utworzone.
9. **Opcjonalne**: po zakończeniu tego samouczka, może być toodelete hello zasoby, które zostały utworzone, tak aby nie wiąże się z opłatami użycia:
    - Kliknij przycisk **omówienie** na powitania **myVnet** bloku.
    - Kliknij przycisk hello **usunąć** ikonę na powitania **myVnet** bloku.
    - Usuwanie hello tooconfirm, kliknij przycisk **tak** w hello **sieci wirtualnej Usuń** pole.

## <a name="azure-cli"></a>Interfejs wiersza polecenia platformy Azure

1. Możesz albo [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](../cli-install-nodejs.md?toc=%2fazure%2fvirtual-network%2ftoc.json), lub użyj hello interfejsu wiersza polecenia w hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. tooget pomocy dla poleceń interfejsu wiersza polecenia, wpisz `azure <command> --help`. 
2. Zaloguj się za tooAzure przy użyciu polecenia hello znajdujący się w sesji interfejsu wiersza polecenia. Jeśli klikniesz przycisk **wypróbuj** w poniższym polu hello, otwiera powłokę chmury. Możesz zalogować się w tooyour subskrypcji platformy Azure, bez konieczności wprowadzania hello następujące polecenie:

    ```azurecli-interactive
    azure login
    ```

3. powitalne tooensure interfejsu wiersza polecenia jest w trybie zarządzania usługami, wprowadź hello następujące polecenie:

    ```azurecli-interactive
    azure config mode asm
    ```

4. Utwórz sieć wirtualną z prywatnej podsieci:

    ```azurecli-interactive
    azure network vnet create --vnet myVnet --address-space 10.0.0.0 --cidr 16  --subnet-name Private --subnet-start-ip 10.0.0.0 --subnet-cidr 24 --location "East US"
    ```

5. Utwórz publiczny podsieci w sieci wirtualnej hello:

    ```azurecli-interactive
    azure network vnet subnet create --name Public --vnet-name myVnet --address-prefix 10.0.1.0/24
    ```    
    
6. Przejrzyj hello sieci wirtualnej i podsieci:

    ```azurecli-interactive
    azure network vnet show --vnet myVnet
    ```

7. **Opcjonalne**: może być toodelete hello zasoby, które zostały utworzone po zakończeniu tego samouczka, dzięki czemu nie wiąże się z opłatami użycia:

    ```azurecli-interactive
    azure network vnet delete --vnet myVnet --quiet
    ```

> [!NOTE]
> Chociaż nie można określić toocreate grupy zasobów sieci wirtualnej (wdrożenia klasyczne) za pomocą interfejsu wiersza polecenia hello, platforma Azure tworzy hello sieci wirtualnej w grupie zasobów o nazwie *sieci domyślne*.

## <a name="powershell"></a>PowerShell

1. Zainstaluj najnowszą wersję hello PowerShell hello [Azure](https://www.powershellgallery.com/packages/Azure) modułu. Jeśli jesteś tooAzure nowego środowiska PowerShell, zobacz [Omówienie programu Azure PowerShell](/powershell/azure/overview?toc=%2fazure%2fvirtual-network%2ftoc.json).
2. Uruchom sesję programu PowerShell.
3. W programie PowerShell Zaloguj tooAzure wprowadzając hello `Add-AzureAccount` polecenia.
4. Zmień poniżej hello ścieżkę i nazwę pliku, zgodnie z potrzebami, a następnie wyeksportować do istniejącego pliku konfiguracji sieci:

    ```powershell
    Get-AzureVNetConfig -ExportToFile c:\azure\NetworkConfig.xml
    ```

5. toocreate sieci wirtualnej z podsieciami publiczne i prywatne, użyj dowolnej hello tooadd Edytor tekstu **VirtualNetworkSite** elementem pliku konfiguracji sieci toohello.

    ```xml
    <VirtualNetworkSite name="myVnet" Location="East US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/16</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Private">
            <AddressPrefix>10.0.0.0/24</AddressPrefix>
          </Subnet>
          <Subnet name="Public">
            <AddressPrefix>10.0.1.0/24</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    ```

    Przejrzyj hello pełne [schemat pliku konfiguracji sieci](https://msdn.microsoft.com/library/azure/jj157100.aspx).

6. Importowanie pliku konfiguracji sieci hello:

    ```powershell
    Set-AzureVNetConfig -ConfigurationPath c:\azure\NetworkConfig.xml
    ```

    > [!WARNING]
    > Importowanie pliku konfiguracji sieci zmienione może spowodować zmiany tooexisting sieciami wirtualnymi (klasyczne) w ramach subskrypcji. Upewnij się, tylko dodać hello poprzedniej sieci wirtualnej i nie zmienić lub usunąć istniejące sieci wirtualnych z subskrypcji. 

7. Przejrzyj hello sieci wirtualnej i podsieci:

    ```powershell
    Get-AzureVNetSite -VNetName "myVnet"
    ```

8. **Opcjonalne**: może być toodelete hello zasoby, które zostały utworzone po zakończeniu tego samouczka, dzięki czemu nie wiąże się z opłatami użycia. toodelete hello sieci wirtualnej, pełną kroki 4 – 6 ponownie, ten czas hello usuwania **VirtualNetworkSite** element dodanej w kroku 5.
 
> [!NOTE]
> Chociaż nie można określić toocreate grupy zasobów sieci wirtualnej (wdrożenia klasyczne) przy użyciu programu PowerShell, platforma Azure tworzy hello sieci wirtualnej w grupie zasobów o nazwie *sieci domyślne*.

---

## <a name="next-steps"></a>Następne kroki

- Zobacz toolearn o wszystkich sieci wirtualnej i ustawienia podsieci [Zarządzanie sieciami wirtualnymi](virtual-network-manage-network.md) i [Zarządzanie podsieci sieci wirtualnej](virtual-network-manage-subnet.md). Istnieją różne opcje dotyczące korzystania z sieci wirtualnych i podsieci w środowisku produkcyjnym wymagania różnych toomeet środowiska.
- toofilter dla ruchu przychodzącego i wychodzącego ruchu w podsieci, tworzenie i stosowanie [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) toosubnets.
- Utwórz [Windows](../virtual-machines/windows/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Linux](../virtual-machines/linux/classic/createportal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) maszyny wirtualnej, a następnie podłącz je tooan istniejącej sieci wirtualnej.
- tooconnect dwie sieci wirtualne w tej samej lokalizacji platformy Azure Witaj, Utwórz [sieci wirtualnej komunikacji równorzędnej](create-peering-different-deployment-models.md) między sieciami wirtualnymi hello. Można elementu równorzędnego sieci wirtualnej tooa sieci wirtualnej (Resource Manager) (klasyczne), ale nie można utworzyć komunikacji równorzędnej między dwiema sieciami wirtualnymi (klasyczny).
- Połączyć sieć lokalną tooan hello w sieci wirtualnej przy użyciu [bramy sieci VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Azure ExpressRoute](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md?toc=%2fazure%2fvirtual-network%2ftoc.json) obwodu.
