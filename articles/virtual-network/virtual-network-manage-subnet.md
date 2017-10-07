---
title: "aaaAdd, zmienić lub usunąć podsieć sieci wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak tooadd, zmienić lub usunąć podsieć sieci wirtualnej na platformie Azure."
services: virtual-network
documentationcenter: na
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
ms.date: 05/10/2017
ms.author: jdial
ms.openlocfilehash: 0d6d813b7e2fc52a00a87f6c6714ab5b7ca589ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-delete-a-virtual-network-subnet"></a>Dodawanie, zmienianie lub usuwanie podsieć sieci wirtualnej

Dowiedz się, jak tooadd, zmienić lub usunąć podsieć sieci wirtualnej. 

Jeśli nie znasz z sieciami wirtualnymi, aby dodać, zmienić lub usunąć podsieć, zaleca się przeczytanie [Omówienie usługi Azure Virtual Network](virtual-networks-overview.md) i [tworzenie, zmienianie lub usuwanie sieci wirtualnej](virtual-network-manage-network.md). Wszystkie zasoby Azure wdrożony w sieci wirtualnej są wdrażane w podsieci sieci wirtualnej. Na ogół wiele podsieci są tworzone w ramach sieci wirtualnej do:
- **Filtrować ruch między podsieciami**. Możesz zastosować sieci zabezpieczeń grupy toosubnets toofilter przychodzący i wychodzący ruch dla wszystkich zasobów (np. maszyny wirtualne), znajdujące się w sieci wirtualnej hello sieciowy. więcej informacji o toolearn, toocreate sieciową grupę zabezpieczeń, zobacz temat [Utwórz grupy zabezpieczeń sieci](virtual-networks-create-nsg-arm-pportal.md).
- **Kontrolowanie routing między podsieciami**. Azure tworzy trasy domyślne, tak aby ruch jest automatycznie przesyłany między podsieciami. Trasy domyślne Azure można zastąpić, tworząc trasy zdefiniowane przez użytkownika. toolearn więcej informacji na temat trasy zdefiniowane przez użytkownika, zobacz [utworzyć trasy zdefiniowane przez użytkownika](virtual-network-create-udr-arm-ps.md). 

W tym artykule opisano, jak tooadd, zmienianie i usuwanie podsieci dla sieci wirtualnych, które zostały utworzone przy użyciu modelu wdrażania usługi Azure Resource Manager hello.
 
## <a name="before"></a>Przed rozpoczęciem

Przed rozpoczęciem powitalne zadań, które są opisane w tym artykule ukończyć powitalnych następujące wymagania wstępne:

- W przypadku nowych tooworking z sieciami wirtualnymi, firma Microsoft zaleca przejrzenie wykonywania hello w [tworzenie sieci wirtualnej platformy Azure pierwsze](virtual-network-get-started-vnet-subnet.md). Tego ćwiczenia ułatwiają zapoznanie się ze sieci wirtualnych.
- toolearn dotyczących ograniczeń dla sieci wirtualnej, przejrzyj [limity Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Zaloguj się w portalu Azure toohello, hello narzędzia wiersza polecenia platformy Azure (Azure CLI) lub Azure PowerShell przy użyciu konta platformy Azure. Jeśli nie masz konta platformy Azure, należy zarejestrować się w celu [bezpłatnego konta wersji próbnej](https://azure.microsoft.com/free).
- Jeśli planujesz toouse toocomplete hello zadania opisane w tym artykule poleceń programu PowerShell, należy najpierw [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello poleceń cmdlet programu Azure PowerShell zainstalowane. Wprowadź tooget pomocy dla poleceń programu PowerShell w przykładach hello `get-help <command> -full`.
- Jeśli planujesz toouse toocomplete hello zadania opisane w tym artykule polecenia interfejsu wiersza polecenia Azure, należy albo:
    - [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję interfejsu wiersza polecenia Azure zainstalowany hello.
    - Użyj hello powłoki chmury Azure. Zamiast instalowania hello interfejsu wiersza polecenia i jego zależności, możesz użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. toouse hello powłoki chmury kliknij hello powłoki chmury (**> _**) ikona u góry hello hello portalu Azure. 

  Wprowadź tooget pomoc dotyczącą poleceń interfejsu wiersza polecenia Azure `az <command> --help`.

## <a name="create-subnet"></a>Dodaj podsieć

tooadd podsieci:

1. Zaloguj się toohello [portal](https://portal.azure.com) przy użyciu konta, do którego przypisano uprawnienia roli współautora sieci hello (co najmniej) dla Twojej subskrypcji. toolearn więcej informacji o przypisywaniu tooaccounts ról i uprawnień, zobacz [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. W polu wyszukiwania portalu hello wpisz **sieci wirtualnych**. W wynikach wyszukiwania powitania kliknij **sieci wirtualnych**.
3. Na powitania **sieci wirtualnych** bloku, kliknij hello sieci wirtualnej ma tooadd podsieć.
4. W bloku sieci wirtualnej hello, kliknij **podsieci**.
5. Kliknij przycisk **+ podsieci**.
6. Na powitania **Dodaj podsieć** bloku, wprowadź wartości dla hello następujące parametry:
    - **Nazwa**: hello nazwa musi być unikatowa w ramach sieci wirtualnej hello.
    - **Zakres adresów**: hello zakres musi być unikatowe w obrębie hello przestrzeni adresowej dla sieci wirtualnej hello. Witaj zakresu nie może nakładać się na inne zakresy adresów podsieci w sieci wirtualnej hello. należy określić przestrzeń adresową Hello przy użyciu notacji Classless Inter-Domain Routing (CIDR). Na przykład w sieci wirtualnej z 10.0.0.0/16 przestrzeni adresów, można zdefiniować przestrzeni adresowej podsieci 10.0.0.0/24. Witaj zakres najmniejszą można określić jest /29, co umożliwia osiem adresów IP podsieci hello. Azure rezerw hello najpierw i ostatniego adresu w każdej podsieci dla zgodności protokołu. Trzy dodatkowe adresy są zarezerwowane do użycia usługi Azure. W związku z tym Definiowanie podsieci z /29 adresów zakresu wyników w trzech można używać w hello podsieci adresów IP. Jeśli planujesz tooconnect Brama sieci wirtualnej tooa sieci VPN, należy utworzyć podsieć bramy. Dowiedz się więcej o [zagadnienia dotyczące zakresu określonego adresu podsieci bramy](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Zakres adresów hello można zmienić po dodaniu podsieci hello określonych warunkach. toolearn toochange zakres adresów podsieci, zobacz temat [zmienić ustawienia podsieci](#change-subnet) w tym artykule.
    - **Grupy zabezpieczeń sieci**: Opcjonalnie można skojarzyć istniejącą sieciową grupę zabezpieczeń z toocontrol podsieci hello filtrowanie hello podsieci ruchu przychodzącego i wychodzącego ruchu sieciowego. Witaj sieciowej grupy zabezpieczeń musi istnieć w hello sam subskrypcji i lokalizacji co sieć wirtualna hello. On również należy utworzyć przy użyciu modelu wdrażania usługi Resource Manager hello. więcej informacji o toolearn, toocreate sieciową grupę zabezpieczeń, zobacz temat [sieciowej grupy zabezpieczeń](virtual-networks-create-nsg-arm-pportal.md).
    - **Tabela tras**: Opcjonalnie można skojarzyć istniejącą tabelę tras z hello podsieci toocontrol ruchu sieciowego routingu tooother sieci. Witaj tabeli tras musi istnieć w hello sam subskrypcji i lokalizacji co sieć wirtualna hello. On również należy utworzyć przy użyciu modelu wdrażania usługi Resource Manager hello. więcej informacji o toolearn, tabele tras toocreate, zobacz temat [trasy zdefiniowane przez użytkownika](virtual-network-create-udr-arm-ps.md).
    - **Użytkownicy**: podsieci toohello dostępu można kontrolować za pomocą wbudowanych ról lub własne niestandardowe role. toolearn więcej informacji na temat przypisywania podsieci hello tooaccess ról i użytkowników, zobacz [Użyj roli przypisania toomanage dostępu tooyour Azure zasobów](../active-directory/role-based-access-control-configure.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-access).
7. tooadd hello podsieci toohello sieć wirtualna, która została wybrana, kliknij przycisk **OK**.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia platformy Azure|[Utwórz az podsieci sieci wirtualnej](/cli/azure/network/vnet/subnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nowy AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json), [AzureRmVirtualNetworkSubnetConfig Dodaj](/powershell/module/azurerm.network/add-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet"></a>Zmień ustawienia podsieci

Za zarządzanie zasobami, które znajdują się w podsieci, można zmienić grup zabezpieczeń sieci, tabele tras i podsieci tooa dostępu użytkownika. toolearn o tych ustawieniach w [Dodaj podsieć](#create-subnet), zobacz krok 6. Jeśli chcesz toochange hello przestrzeni adresowej podsieci, należy najpierw usunąć wszystkie zasoby, które znajdują się w podsieci hello. Hello kroki należy wykonać toodelete zasobu zależy od zasobu hello. toolearn jak typ, które mają toodelete toodelete zasoby, które znajdują się w podsieci, odczytu hello dokumentacji dla każdego zasobu. toochange hello zakres adresów w podsieci:

1. Zaloguj się toohello [portal](https://portal.azure.com) przy użyciu konta, do którego przypisano uprawnienia roli współautora sieci hello (co najmniej) dla Twojej subskrypcji. toolearn więcej informacji o przypisywaniu tooaccounts ról i uprawnień, zobacz [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. W polu wyszukiwania portalu hello wpisz **sieci wirtualnych**. W wynikach wyszukiwania powitania kliknij **sieci wirtualnych**.
3. Na powitania **sieci wirtualnych** bloku, kliknij przycisk hello sieci wirtualnej, dla której ma zostać toochange zakres adresów podsieci.
4. Kliknij przycisk hello podsieci, dla której ma zostać zakres adresów hello toochange.
5. W bloku podsieci hello w hello **zakres adresów** wprowadź hello nowy zakres adresów. zakres Hello muszą być unikatowe w przestrzeni adresowej hello hello sieci wirtualnej. Witaj zakresu nie może nakładać się na inne zakresy adresów podsieci w sieci wirtualnej hello. należy określić przestrzeń adresową Hello przy użyciu notacji CIDR. Na przykład w sieci wirtualnej z 10.0.0.0/16 przestrzeni adresów, można zdefiniować przestrzeni adresowej podsieci 10.0.0.0/24. Witaj zakres najmniejszą można określić jest /29, co umożliwia osiem adresów IP podsieci hello. Azure rezerw hello najpierw i ostatniego adresu w każdej podsieci dla zgodności protokołu. Trzy dodatkowe adresy są zarezerwowane do użycia usługi Azure. Dzięki temu podsieci z /29 zakres adresów zawiera trzy można używać adresów IP. Jeśli planujesz tooconnect Brama sieci wirtualnej tooa sieci VPN, należy utworzyć podsieć bramy. Dowiedz się więcej o [zagadnienia dotyczące zakresu określonego adresu podsieci bramy](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Zakres adresów hello można zmienić po utworzeniu podsieci hello określonych warunkach. toolearn toochange zakres adresów podsieci, zobacz temat [zmienić ustawienia podsieci](#change-subnet) w tym artykule.
6. Kliknij pozycję **Zapisz**.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia platformy Azure|[Aktualizacja podsieci sieci wirtualnej sieci az](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Zestaw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-subnet"></a>Usuń podsieć

Tylko wtedy, gdy nie ma żadnych zasobów w podsieci hello, można usunąć podsieci. Jeśli dostępne są zasoby w podsieci hello, musisz usunąć hello zasobów, które znajdują się w podsieci hello, aby można było usunąć hello podsieci. Hello kroki należy wykonać toodelete zasobu zależy od zasobu hello. toolearn jak typ, które mają toodelete toodelete zasoby, które znajdują się w podsieci, odczytu hello dokumentacji dla każdego zasobu. toodelete podsieci:

1. Zaloguj się toohello [portal](https://portal.azure.com) przy użyciu konta, do którego przypisano uprawnienia roli współautora sieci hello (co najmniej) dla Twojej subskrypcji. toolearn więcej informacji o przypisywaniu tooaccounts ról i uprawnień, zobacz [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. W polu wyszukiwania portalu hello wpisz **sieci wirtualnych**. W wynikach wyszukiwania powitania kliknij **sieci wirtualnych**.
3. Na powitania **sieci wirtualnych** bloku, kliknij przycisk hello sieci wirtualnej ma toodelete podsieci z.
4. Na powitania wirtualnych sieci bloku, w obszarze **ustawienia**, kliknij przycisk **podsieci**.
5. Chcesz toodelete na powitania listę podsieci, który znajduje się w bloku podsieci hello podsieci powitania kliknij prawym przyciskiem myszy, kliknij przycisk **usunąć**, a następnie kliknij przycisk **tak** toodelete hello podsieci.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia platformy Azure|[AZ sieci usunięcie sieci wirtualnej](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Usuń AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/remove-azurermvirtualnetworksubnetconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Następne kroki

toocreate maszynę wirtualną w podsieci, zobacz [tworzenie sieci wirtualnej i wdrażanie maszyn wirtualnych w podsieci hello](virtual-network-get-started-vnet-subnet.md#create-vms).
