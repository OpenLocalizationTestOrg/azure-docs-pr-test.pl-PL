---
title: "aaaCreate, zmienić lub usunąć sieć wirtualną platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak toocreate, zmienić lub usunąć sieci wirtualnej na platformie Azure."
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
ms.openlocfilehash: 7dfe6632753182eae2a13bb0327f03f75e03d057
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-virtual-network"></a>Tworzenie, zmienianie lub usuwanie sieci wirtualnej

Dowiedz się, jak toocreate i usuwania wirtualnych ustawienia sieci i zmianę, jak serwery DNS i adres IP spacji dla istniejącej sieci wirtualnej.

Sieć wirtualna jest reprezentację sieci w chmurze hello. Sieć wirtualna jest logiczną izolacją hello Azure chmurze, która jest dedykowany tooyour subskrypcji platformy Azure. Dla każdej sieci wirtualnej, utworzony można:
- Wybierz tooassign przestrzeni adresowej. Przestrzeń adresową składa się z jednego lub więcej zakresów adresów, które są zdefiniowane przy użyciu notacji Classless Inter-Domain Routing (CIDR), takich jak 10.0.0.0/16.
- Wybierz serwer DNS platformy Azure hello toouse lub użyć serwera DNS. Wszystkie zasoby, które są połączone toohello sieci wirtualnej są przypisywane tej nazwy tooresolve serwerów DNS w sieci wirtualnej hello.
- Segment hello sieci wirtualnej do podsieci, każda z własną zakres adresów w obrębie hello przestrzeni adresowej sieci wirtualnej hello. jak toocreate, zmiany i usunięcia podsieci, zobacz toolearn [Dodawanie, zmienianie lub usuń podsieci](virtual-network-manage-subnet.md).

W tym artykule opisano, jak toocreate, zmienianie i usuwanie sieci wirtualnych za pomocą modelu wdrażania usługi Azure Resource Manager hello.

## <a name="before"></a>Przed rozpoczęciem

Przed rozpoczęciem powitalne zadań, które są opisane w tym artykule ukończyć powitalnych następujące wymagania wstępne:

- W przypadku nowych tooworking z sieciami wirtualnymi, firma Microsoft zaleca przejrzenie wykonywania hello w [tworzenie sieci wirtualnej platformy Azure pierwsze](virtual-network-get-started-vnet-subnet.md). Tego ćwiczenia ułatwiają zapoznanie się ze sieci wirtualnych.
- toolearn dotyczących ograniczeń dla sieci wirtualnej, przejrzyj [limity Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).
- Zaloguj się w portalu Azure toohello, hello narzędzia wiersza polecenia platformy Azure (Azure CLI) lub Azure PowerShell przy użyciu konta platformy Azure. Jeśli nie masz konta platformy Azure, należy zarejestrować się w celu [bezpłatnego konta wersji próbnej](https://azure.microsoft.com/free).
- Jeśli planujesz toouse toocomplete hello zadania opisane w tym artykule poleceń programu PowerShell, należy najpierw [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello poleceń cmdlet programu Azure PowerShell zainstalowane. Wprowadź tooget pomocy dla poleceń programu PowerShell w przykładach hello `get-help <command> -full`.
- Jeśli planujesz toouse toocomplete hello zadania opisane w tym artykule polecenia interfejsu wiersza polecenia Azure, należy najpierw [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję interfejsu wiersza polecenia Azure zainstalowany hello. Wprowadź tooget pomoc dotyczącą poleceń interfejsu wiersza polecenia Azure `az <command> --help`.


## <a name="create-vnet"></a>Tworzenie sieci wirtualnej

toocreate sieci wirtualnej:

1. Zaloguj się toohello [portal](https://portal.azure.com) przy użyciu konta, do którego przypisano uprawnienia roli współautora sieci hello (co najmniej) dla Twojej subskrypcji. toolearn więcej informacji o przypisywaniu tooaccounts ról i uprawnień, zobacz [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. Kliknij przycisk **nowy** > **sieci** > **sieci wirtualnej**.
3. Na powitania **sieci wirtualnej** bloku w hello **wybierz model wdrożenia** pozostaw **Resource Manager** zaznaczone, a następnie kliknij przycisk **Utwórz**.
4. Na powitania **Utwórz sieć wirtualną** bloku, wprowadź lub wybierz wartości hello następujące ustawienia, a następnie kliknij przycisk **Utwórz**:
    - **Nazwa**: hello nazwa musi być unikatowa w hello [grupy zasobów](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) wybranej sieci wirtualnej hello toocreate w. Nie można zmienić nazwy hello, po utworzeniu sieci wirtualnej hello. Wraz z upływem czasu, można utworzyć wiele sieci wirtualnych. Nazewnictwa sugestii, zobacz [konwencje nazewnictwa](/azure/architecture/best-practices/naming-conventions.md?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions). Po konwencji nazewnictwa może sprawić, że jej łatwiejsze toomanage wiele sieci wirtualnych.
    - **Przestrzeń adresowa**: Określ hello przestrzeń adresów w notacji CIDR. przestrzeń adresowa Hello zdefiniowanych można publicznych lub prywatnych (RFC 1918). Czy przestrzeń adresowa hello można zdefiniować jako publicznych lub prywatnych, przestrzeni adresowej hello jest dostępny tylko w ramach sieci wirtualnej hello, z połączonych sieci wirtualnych i sieciami lokalnymi połączyły toohello sieci wirtualnej. Nie można dodać następujące przestrzenie adresowe hello:
        - 224.0.0.0/4 (multiemisji)
        - 255.255.255.255/32 (emisji)
        - 127.0.0.0/8 (sprzężenie zwrotne)
        - 169.254.0.0/16 (Link-local)
        - 168.63.129.16/32 (wewnętrzny serwer DNS)

      Mimo że można zdefiniować tylko jedną przestrzeń adresową, podczas tworzenia sieci wirtualnej hello, możesz dodać więcej przestrzenie adresowe po utworzeniu sieci wirtualnej hello. toolearn tooadd adres miejsce tooan istniejącej sieci wirtualnej, zobacz [Dodaj lub Usuń przestrzeń adresową](#add-address-spaces) w tym artykule.

      >[!WARNING]
      >Jeśli sieć wirtualna ma przestrzeni adresów, które nakładają się z inną siecią wirtualną sieć lub lokalnie, nie można połączyć Witaj dwie sieci. Przed zdefiniowaniem przestrzeń adresową, czy należy rozważyć może sieci wirtualne sieci wirtualnej tooother tooconnect hello lub sieci lokalnej w hello przyszłych.
      >
      >

    - **Nazwa podsieci**: hello nazwy podsieci muszą być unikatowe w ramach sieci wirtualnej hello. Nie można zmienić nazwy podsieci hello, po utworzeniu hello podsieci. Hello portal wymaga zdefiniowania w jednej podsieci po utworzeniu sieci wirtualnej, nawet jeśli sieć wirtualna nie jest wymagane toohave żadnych podsieci. W portalu hello można zdefiniować tylko jedną podsieć, podczas tworzenia sieci wirtualnej. Możesz dodać więcej sieci wirtualnej toohello podsieci później, po utworzeniu sieci wirtualnej hello. Zobacz tooadd podsieci sieci wirtualnej w tooa, [Utwórz podsieć](virtual-network-manage-subnet.md#create-subnet) w [tworzenie, zmienianie i usuwanie podsieci](virtual-network-manage-subnet.md). Można utworzyć sieci wirtualnej, który ma wiele podsieci przy użyciu wiersza polecenia platformy Azure lub programu PowerShell.

      >[!TIP]
      >Czasami Administratorzy utworzyć różne podsieci toofilter lub kontroli ruchu, routing między podsieciami hello. Przed zdefiniowaniem podsieci, należy wziąć pod uwagę demonstrujący mają toofilter i kierować ruchem między podsieci. toolearn więcej informacji na temat filtrowania ruchu między podsieciami, zobacz [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md). Azure automatycznie trasy ruch między podsieciami, ale można zastąpić trasy domyślne platformy Azure. toolearn toooverride Azure domyślne routingu ruchu w podsieci, zobacz [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md).
      >

    - **Zakres adresów podsieci**: hello zakres musi być w przestrzeni adresowej hello wprowadzono hello sieci wirtualnej. Witaj zakres najmniejszą można określić jest /29, co umożliwia osiem adresów IP podsieci hello. Azure rezerw hello najpierw i ostatniego adresu w każdej podsieci dla zgodności protokołu. Trzy dodatkowe adresy są zarezerwowane do użycia usługi Azure. W związku z tym sieci wirtualnej z zakresem adresów podsieci /29 zawiera tylko trzy można używać adresów IP. Jeśli planujesz tooconnect Brama sieci wirtualnej tooa sieci VPN, należy utworzyć podsieć bramy. Dowiedz się więcej o [zagadnienia dotyczące zakresu określonego adresu podsieci bramy](../vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md?toc=%2fazure%2fvirtual-network%2ftoc.json#gwsub). Zakres adresów hello można zmienić po utworzeniu podsieci hello określonych warunkach. toolearn toochange zakres adresów podsieci, zobacz temat [zmienić ustawienia podsieci](#change-subnet) w [Dodawanie, zmienianie lub usuń podsieci](virtual-network-manage-subnet.md).
    - **Subskrypcja**: Wybierz [subskrypcji](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). Nie można użyć hello tej samej sieci wirtualnej w więcej niż jedną subskrypcją platformy Azure. Można jednak połączyć sieć wirtualną w jednej sieci toovirtual subskrypcji w innych subskrypcji. tooconnect sieci wirtualnych w ramach różnych subskrypcji, użyj bramy sieci VPN platformy Azure lub sieci wirtualnej komunikacji równorzędnej. Dowolnym zasobem Azure połączyć z sieci wirtualnej toohello musi być w hello tej samej subskrypcji co sieć wirtualna hello.
    - **Grupa zasobów**: Wybierz istniejący [grupy zasobów](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-groups) lub Utwórz nową. Zasobów platformy Azure połączyć z sieci wirtualnej toohello może znajdować się w hello tej samej grupie zasobów co sieć wirtualna hello lub w innej grupie zasobów.
    - **Lokalizacja**: wybierz pozycję Azure [lokalizacji](https://azure.microsoft.com/regions/), znanej również jako regionu. Sieć wirtualna może być w tylko jednej lokalizacji platformy Azure. Można jednak połączyć sieć wirtualną w jednej lokalizacji tooa sieci wirtualnej w innej lokalizacji przy użyciu bramy sieci VPN. Dowolnym zasobem Azure połączyć z sieci wirtualnej toohello musi być w hello tej samej lokalizacji co sieć wirtualna hello.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia platformy Azure|[Tworzenie sieci wirtualnej sieci az](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nowy AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name = "view-vnet"></a>Widok sieci wirtualnych i ustawień

sieci wirtualne tooview i ustawienia:

1. Zaloguj się toohello [portal](https://portal.azure.com) przy użyciu konta, do którego przypisano uprawnienia roli współautora sieci hello (co najmniej) dla Twojej subskrypcji. toolearn więcej informacji o przypisywaniu tooaccounts ról i uprawnień, zobacz [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. W polu wyszukiwania portalu hello wpisz **sieci wirtualnych**. W wynikach wyszukiwania powitania kliknij **sieci wirtualnych**.
3. Na powitania **sieci wirtualnych** bloku, kliknij hello sieć wirtualna, która ma tooview ustawienia.
4. Witaj następujące ustawienia są wyświetlane na powitania bloku dla sieci wirtualnej hello wybranych:
    - **Omówienie**: zawiera informacje o sieci wirtualnej hello, w tym przestrzeń adresową i serwery DNS. Witaj Poniższy zrzut ekranu przedstawia hello Przegląd ustawień sieci wirtualnej o nazwie **MyVNet**:

        ![Omówienie interfejsu sieciowego](./media/virtual-network-manage-network/vnet-overview.png)

      Na powitania **omówienie** bloku można przenieść sieć wirtualną tooa innej subskrypcji lub grupy zasobów. toolearn toomove sieci wirtualnej, zobacz temat [przenoszenia zasobów tooa innej grupie zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json). Artykuł Hello zawiera listę wymagań wstępnych i sposobu toomove zasobów za pomocą hello portalu Azure, programu PowerShell i interfejsu wiersza polecenia Azure. Wszystkie zasoby, które są połączone toohello sieci wirtualnej, należy przenieść z hello sieci wirtualnej.
    - **Przestrzeń adresowa**: znajdują się przestrzeni adresowych hello przypisanych toohello sieci wirtualnej. toolearn jak ukończyć tooadd i Usuń przestrzeń adresową, hello kroki w [Dodaj lub Usuń przestrzeń adresową](#address-spaces) w tym artykule.
    - **Połączone urządzenia**: wymienione są wszystkie zasoby, które są połączone toohello sieci wirtualnej. W hello zrzut ekranu poprzedzającym trzy interfejsy sieciowe i jeden moduł równoważenia obciążenia są toohello połączonych sieci wirtualnej. Są wyświetlane wszystkie nowe zasoby, tworzenie i łączenie toohello sieci wirtualnej. Jeśli usuniesz z zasobem, który został toohello połączonych sieci wirtualnej, nie będzie widoczny na liście hello.
    - **Podsieci**: Lista podsieci, które istnieją w ramach sieci wirtualnej hello jest wyświetlany. toolearn jak tooadd i Usuń podsieć, zobacz [Utwórz podsieć](virtual-network-manage-subnet.md#create-subnet) i [usunąć podsieć](virtual-network-manage-subnet.md#delete-subnet) w [Dodawanie, zmienianie lub usuń podsieci](virtual-network-manage-subnet.md).
    - **Serwery DNS**: można określić, czy hello Azure wewnętrznego serwera DNS lub niestandardowy serwer DNS udostępnia rozpoznawanie nazw dla urządzeń, które są połączone toohello sieci wirtualnej. Po utworzeniu sieci wirtualnej przy użyciu portalu Azure hello serwerów DNS platformy Azure są używane do rozpoznawania nazw w sieci wirtualnej domyślnie. serwery DNS hello toomodify, pełną hello kroki opisane w temacie [Dodawanie, zmienianie i usuwanie serwera DNS](#dns-servers) w tym artykule.
    - **Komunikacji równorzędnych**: Jeśli istnieją istniejącego komunikacji równorzędnych w subskrypcji hello, są one wyświetlane tutaj. Można wyświetlać ustawienia dla istniejącego komunikacji równorzędnych, lub utworzyć, zmienić lub usunąć komunikacji równorzędnych. toolearn więcej informacji na temat komunikacji równorzędnych, zobacz [równorzędna sieci wirtualnej](virtual-network-peering-overview.md).
    - **Właściwości**: Wyświetla ustawienia o hello sieci wirtualnej, w tym identyfikator zasobu hello sieci wirtualnej i hello subskrypcji platformy Azure jest.
    - **Diagram**: hello diagram zawiera wizualną reprezentację wszystkich urządzeń, które są połączone toohello sieci wirtualnej. Hello diagram ma niektóre najważniejsze informacje na temat hello urządzeń. toomanage urządzenia, w tym widoku diagramu powitania kliknij hello urządzenie.
    - **Typowe ustawienia Azure**: toolearn więcej informacji na temat typowych ustawień platformy Azure, zobacz hello następujących informacji:
        *   [Dziennik aktywności](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs)
        *   [Kontrola dostępu (IAM)](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control)
        *   [Tagi](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags)
        *   [Blokady](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
        *   [Skrypt automatyzacji](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group)

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia platformy Azure|[Pokaż sieci wirtualnej sieci az](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVirtualNetwork](/powershell/module/azurerm.network/get-azurermvirtualnetwork/?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="add-address-spaces"></a>Dodaj lub Usuń przestrzeń adresową

Można dodawać i usuwać przestrzeni adresów sieci wirtualnej. Przestrzeń adresowa musi być określony w notacji CIDR i nie może nakładać się z innymi obszarami adresów w obrębie hello sam sieci wirtualnej. przestrzenie adresowe Hello zdefiniowanych można publicznych lub prywatnych (RFC 1918). Czy przestrzeń adresowa hello można zdefiniować jako publicznych lub prywatnych, przestrzeni adresowej hello jest dostępny tylko w ramach sieci wirtualnej hello, z połączonych sieci wirtualnych i sieciami lokalnymi połączyły toohello sieci wirtualnej. Nie można dodać następujące przestrzenie adresowe hello:

- 224.0.0.0/4 (multiemisji)
- 255.255.255.255/32 (emisji)
- 127.0.0.0/8 (sprzężenie zwrotne)
- 169.254.0.0/16 (Link-local)
- 168.63.129.16/32 (wewnętrzny serwer DNS)

tooadd lub Usuń przestrzeń adresową:

1. Zaloguj się toohello [portal](https://portal.azure.com) przy użyciu konta, do którego przypisano uprawnienia roli współautora sieci hello (co najmniej) dla Twojej subskrypcji. toolearn więcej informacji o przypisywaniu tooaccounts ról i uprawnień, zobacz [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. W polu wyszukiwania portalu hello wpisz **sieci wirtualnych**. W wynikach wyszukiwania hello, wybierz **sieci wirtualnych**.
3. Na powitania **sieci wirtualnych** bloku, kliknij sieć wirtualną hello, dla którego chcesz tooadd lub Usuń przestrzeń adresową.
4. Na powitania wirtualnych sieci bloku, w obszarze **ustawienia**, kliknij przycisk **przestrzeni adresów**.
5. W bloku hello hello przestrzeni adresowej wykonaj jedną z hello następujące opcje:
    - **Dodaj przestrzeń adresową**: Wprowadź hello nowych przestrzeni adresowej. przestrzeń adresowa Hello nie nakłada się na istniejącą przestrzeń adresową, która jest zdefiniowana dla sieci wirtualnej hello.
    - **Usuń przestrzeń adresową**: kliknij prawym przyciskiem myszy na przestrzeń adresową, a następnie kliknij przycisk **Usuń**. Jeśli podsieć istnieje w przestrzeni adresowej hello, nie można usunąć hello przestrzeni adresowej. tooremove przestrzeń adresową, należy najpierw usunąć wszystkie podsieci (i wszystkie zasoby, które są połączone toohello podsieci) który istnieje w przestrzeni adresowej hello.
6. Kliknij pozycję **Zapisz**.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia platformy Azure|Resource Manager|[Aktualizacja sieci wirtualnej sieci az](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="dns-servers"></a>Dodawanie, zmienianie lub usuwanie serwera DNS

Zarejestruj wszystkich maszyn wirtualnych, które są połączone toohello sieci wirtualnej przy użyciu serwerów DNS hello określonych dla sieci wirtualnej hello. Również użyć hello określony serwer DNS do rozpoznawania nazw. Każdego interfejsu sieciowego (NIC) na maszynie wirtualnej może mieć własne ustawienia serwera DNS. Jeśli karta sieciowa ma swoje własne ustawienia serwera DNS, zastępują one hello ustawienia serwera DNS dla sieci wirtualnej hello. toolearn więcej informacji na temat ustawień DNS kart interfejsu Sieciowego, zobacz [interfejsu zadań i ustawień sieci](virtual-network-network-interface.md#change-dns-servers). toolearn więcej informacji na temat rozpoznawanie nazwy dla maszyn wirtualnych i wystąpień ról w usługach w chmurze Azure, zobacz [rozpoznawanie nazw dla maszyn wirtualnych i wystąpień roli](virtual-networks-name-resolution-for-vms-and-role-instances.md). tooadd, Zmień lub Usuń serwer DNS:

1. Zaloguj się toohello [portal](https://portal.azure.com) przy użyciu konta, do którego przypisano uprawnienia roli współautora sieci hello (co najmniej) dla Twojej subskrypcji. toolearn więcej informacji o przypisywaniu tooaccounts ról i uprawnień, zobacz [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. W polu wyszukiwania portalu hello wpisz **sieci wirtualnych**. W wynikach wyszukiwania hello, wybierz **sieci wirtualnych**.
3. Na powitania **sieci wirtualnych** bloku, kliknij hello sieci wirtualnej ma toochange ustawień DNS.
4. Na powitania wirtualnych sieci bloku, w obszarze **ustawienia**, kliknij przycisk **serwerów DNS**.
5. Wybierz jedną z hello następujące opcje w bloku hello, który wyświetla listę serwerów DNS:
    - **Domyślne (zakładając Azure)**: wszystkie nazwy zasobów i prywatnych adresów IP są automatycznie zarejestrowane toohello serwerów usługi Azure DNS. Można rozwiązać nazwy między wszystkie zasoby, które są połączone toohello tej samej sieci wirtualnej. Nie można użyć tej opcji tooresolve nazwy w sieciach wirtualnych. tooresolve nazwy sieci wirtualnej, należy użyć niestandardowego serwera DNS.
    - **Niestandardowe**: można dodać jeden lub więcej serwerów, zapasowej toohello Azure ograniczyć sieci wirtualnej. toolearn więcej informacji na temat limity serwera DNS, zobacz [limity Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#virtual-networking-limits-classic). Masz hello następujące opcje:
        - **Dodaj adres**: dodaje listy serwerów DNS powitania serwera tooyour sieci wirtualnej. Ta opcja również rejestruje powitania serwera DNS przy użyciu platformy Azure. Jeśli serwer DNS został już zarejestrowany przy użyciu platformy Azure, można wybrać tego serwera DNS na liście hello.
        - **Usuń adres**: kliknij przycisk Dalej toohello serwera tooremove, **X**. Usuwanie serwera hello usuwa hello serwer tylko z tej listy sieci wirtualnej. Serwer DNS Hello pozostaje zarejestrowane w usłudze Azure dla innych toouse sieci wirtualnych.
        - **Zmień kolejność adresów serwerów DNS**: należy wyświetlić listę serwerów DNS w hello tooverify Popraw kolejności dla danego środowiska. Listy serwera DNS są używane w kolejności hello one określone. Nie działają jako Instalator okrężnego. Jeśli hello pierwszego serwera DNS na liście hello jest osiągalna, hello klient korzysta z tego serwera DNS, niezależnie od tego, czy serwer DNS hello działa prawidłowo. Usuń wszystkie hello serwery DNS, które są wyświetlane, a następnie dodaj je ponownie w kolejności hello.
        - **Zmień adres**: zaznacz serwer DNS hello hello liście, a następnie wprowadź nową nazwę hello.
6. Kliknij pozycję **Zapisz**.
7. Ponowne uruchomienie maszyn wirtualnych hello, które są toohello połączenia wirtualnej sieci, więc są przypisane hello nowych ustawień serwera DNS. Maszyny wirtualne nadal toouse swoje bieżące ustawienia DNS do czasu ich ponownego uruchomienia.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia platformy Azure|[Aktualizacja sieci wirtualnej sieci az](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="delete-vnet"></a>Usunąć sieci wirtualnej

Tylko wtedy, gdy nie ma żadnych tooit połączonych zasobów, można usunąć sieci wirtualnej. W przypadku zasobów połączonych tooany podsieci w sieci wirtualnej hello, należy najpierw usunąć hello zasoby, które są połączone tooall podsieci w sieci wirtualnej hello. Hello kroki należy wykonać toodelete zasobu zależy od zasobu hello. jak odczytu toodelete zasoby, które są połączone toosubnets toolearn hello dokumentacji dla każdego typu zasobu ma toodelete. toodelete sieci wirtualnej:

1. Zaloguj się toohello [portal](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. toolearn więcej informacji o przypisywaniu tooaccounts ról i uprawnień, zobacz [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. W polu wyszukiwania portalu hello wpisz **sieci wirtualnych**. W wynikach wyszukiwania powitania kliknij **sieci wirtualnych**.
3. Na powitania **sieci wirtualnych** bloku, wybierz hello sieci wirtualnej ma toodelete.
4. W bloku sieci wirtualnej hello tooconfirm, że nie istnieją żadne urządzenia podłączone toohello sieci wirtualnej, w obszarze **ustawienia**, kliknij przycisk **urządzeń podłączonych**. W przypadku połączonych urządzeń, należy je usunąć przed usunięciem sieci wirtualnej hello. Jeśli nie ma żadnych podłączonych urządzeń, kliknij przycisk **omówienie**.
5. U góry hello hello bloku, kliknij przycisk hello **usunąć** ikony.
6. Usuwanie hello tooconfirm hello sieci wirtualnej, kliknij przycisk **tak**.


**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia platformy Azure|[Usuń sieć wirtualną sieć platformy Azure](/cli/azure/network/vnet?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Remove-AzureRmVirtualNetwork](/powershell/module/azurerm.network/remove-azurermvirtualnetwork?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="next-steps"></a>Następne kroki

- toocreate maszyny Wirtualnej, a następnie połącz go tooa sieci wirtualnej, zobacz [utworzyć sieć wirtualną i połączyć maszyny wirtualne](virtual-network-get-started-vnet-subnet.md#create-vms).
- toofilter ruch sieciowy między podsieciami sieci wirtualnej, zobacz [Utwórz grupy zabezpieczeń sieci](virtual-networks-create-nsg-arm-pportal.md).
- toopeer sieci wirtualnej tooanother sieci wirtualnej, zobacz [tworzenie sieci wirtualnej komunikacji równorzędnej](virtual-network-create-peering.md#portal).
- Zobacz toolearn o możliwości podłączenia sieci wirtualnej sieci lokalnej tooan [o bramy sieci VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#diagrams).
