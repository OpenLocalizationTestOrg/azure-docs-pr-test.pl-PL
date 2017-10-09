---
title: "aaaConfigure adresów IP dla interfejsu sieci platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak zmienić tooadd i Usuń prywatne i publiczne adresy IP dla karty sieciowej."
services: virtual-network
documentationcenter: na
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
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 1e5ea6c65d93be9b1fda5d807500a0823c94c89c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-change-or-remove-ip-addresses-for-an-azure-network-interface"></a>Dodawanie, zmienianie lub usuwanie adresów IP dla interfejsu sieci platformy Azure

Dowiedz się, jak zmienić tooadd i usuń publiczne i prywatne adresy IP dla karty sieciowej. Prywatne adresy IP przypisane interfejsu sieciowego tooa włączyć toocommunicate maszynę wirtualną z innych zasobów w sieci wirtualnej platformy Azure i połączone sieci. Prywatny adres IP umożliwia także komunikacji wychodzącej toohello Internet przy użyciu nieprzewidywalne adresu IP. A [publicznego adresu IP](virtual-network-public-ip-address.md) przypisane tooa interfejsu sieciowego umożliwia komunikacji przychodzącej tooa maszyny wirtualnej na podstawie hello Internet. adres Hello umożliwia także komunikacji wychodzącej z toohello maszyny wirtualnej hello Internet przy użyciu wartości prognozowanych adresu IP. Aby uzyskać więcej informacji, zobacz [Opis połączeń wychodzących na platformie Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json). 

Toocreate, należy zmienić lub usunąć interfejsu sieciowego, przeczytaj hello [Zarządzanie interfejsu sieciowego](virtual-network-network-interface.md) artykułu. Jeśli potrzebujesz interfejsy sieciowe tooadd tooor interfejsów sieciowych Usuń z maszyny wirtualnej, przeczytaj hello [Dodawanie lub usuwanie interfejsów sieciowych](virtual-network-network-interface-vm.md) artykułu. 


## <a name="before-you-begin"></a>Przed rozpoczęciem

Wykonaj następujące zadania, przed wykonaniem dowolnej kroków w żadnej sekcji tego artykułu hello:

- Przejrzyj hello [Azure ogranicza](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artykuł na temat limitów dla publicznych i prywatnych adresów IP.
- Zaloguj się za toohello Azure [portal](https://portal.azure.com), Azure interfejsu wiersza polecenia (CLI) lub Azure PowerShell przy użyciu konta platformy Azure. Jeśli nie masz jeszcze konta platformy Azure, należy zarejestrować się w celu [bezpłatnego konta wersji próbnej](https://azure.microsoft.com/free).
- Jeśli przy użyciu programu PowerShell poleceń toocomplete zadania w tym artykule [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello apletów poleceń programu hello Azure PowerShell. tooget Pomoc dla poleceń programu PowerShell, wraz z przykładami, wpisz `get-help <command> -full`.
- Jeśli przy użyciu interfejsu wiersza polecenia platformy Azure (CLI) polecenia toocomplete zadania w tym artykule [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello Azure CLI zainstalowane. tooget pomocy dla poleceń interfejsu wiersza polecenia, wpisz `az <command> --help`. Zamiast instalowania hello interfejsu wiersza polecenia i jego wymagania wstępne można użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. toouse hello powłoki chmury kliknij hello powłoki chmury **> _** u góry hello hello [portal](https://portal.azure.com).

## <a name="add-ip-addresses"></a>Dodaj adresy IP

Można dodać jako wiele [prywatnej](#private) i [publicznego](#public) [IPv4](#ipv4) adresy niezbędne tooa interfejsu sieciowego, w ramach limitów hello na liście hello [limity Azure ](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artykułu. Nie można użyć tooadd portalu hello istniejącego interfejsu sieciowego IPv6 adres tooan (chociaż podczas tworzenia hello interfejsu sieciowego, można użyć portalu tooadd hello prywatnego interfejsu sieciowego tooa adres IPv6). Możesz użyć programu PowerShell lub hello tooone adres tooadd prywatnej IPv6 interfejsu wiersza polecenia [dodatkowej konfiguracji IP](#secondary) (o ile istnieją żadnych istniejących dodatkowej konfiguracji IP) dla istniejącej sieci interfejsu, który nie jest dołączony tooa wirtualnego maszyny. Nie można użyć dowolnego narzędzia tooadd publicznego interfejsu sieciowego tooa adres IPv6. Zobacz [IPv6](#ipv6) szczegółowe informacje o przy użyciu adresów IPv6. 

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *interfejsy sieciowe*. Gdy **interfejsy sieciowe** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **interfejsy sieciowe** bloku, który jest wyświetlany, kliknij przycisk ma adres tooadd IPv4 dla interfejsu sieciowego hello.
4. Kliknij przycisk **konfiguracje adresów IP** w hello **ustawienia** części bloku hello interfejsu sieciowego hello wybrane.
5. Kliknij przycisk **+ Dodaj** w bloku hello, którego kliknięcie spowoduje otwarcie dla konfiguracji adresów IP.
6. Określ hello poniżej, a następnie kliknij przycisk **OK** tooclose hello **konfiguracji IP dodać** bloku:

    |Ustawienie|Wymagana?|Szczegóły|
    |---|---|---|
    |Nazwa|Tak|Musi być unikatowa dla interfejsu sieciowego hello|
    |Typ|Tak|Ponieważ w przypadku dodawania istniejącego interfejsu sieciowego IP konfiguracji tooan i każdego interfejsu sieciowego musi mieć [głównej](#primary) jest jedyną opcją konfiguracji adresów IP, **dodatkowej**.|
    |Metoda przypisywania adresu prywatnego adresu IP|Tak|[**Dynamiczne** ](#dynamic) adresy można zmienić, jeśli hello maszyny wirtualnej zostanie ponownie uruchomiony po o w hello zatrzymane (cofnięciu przydziału) stanu. Azure przypisuje adres z hello przestrzeni adresowej interfejsu sieciowego hello podsieci hello jest połączony. [**Statyczne** ](#static) adresy nie są zwalniane aż do usunięcia hello interfejsu sieciowego. Określ adres IP z zakresu przestrzeni adresów podsieci hello, który nie jest obecnie używany przez inną konfigurację adresu IP.|
    |Publiczny adres IP|Nie|**Wyłączone:** zasobu bez publicznego adresu IP jest obecnie skojarzony toohello konfiguracji adresu IP. **Włączone:** wybierz istniejący adres IPv4 publicznego adresu IP lub Utwórz nową. toolearn jak toocreate publiczny adres IP, przeczytaj hello [publicznego adresu IP, adresy](virtual-network-public-ip-address.md#create-a-public-ip-address) artykułu.|
7. Ręcznie Dodaj dodatkowej prywatnego adresu IP adresów toohello systemu operacyjnego maszyny wirtualnej, wykonując instrukcje hello hello [przypisać wiele adresów IP systemów operacyjnych maszyny toovirtual](virtual-network-multiple-ip-addresses-portal.md#os-config) artykułu. Zobacz [prywatnej](#private) adresów IP dla uwagi przed dodaniem ręcznie systemu operacyjnego maszyny wirtualnej tooa adresów IP. Nie dodawaj żadnych publicznego adresu IP adresów toohello systemu operacyjnego maszyny wirtualnej.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Tworzenie kart sieciowych az ip-config](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Dodaj AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/add-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-ip-address-settings"></a>Zmień ustawienia adresu IP

Metoda przydziału hello toochange adres IPv4, zmień hello statyczny adres IPv4, może być konieczne lub hello zmian publicznego adresu IP przypisane tooa interfejsu sieciowego. Jeśli chcesz zmienić hello prywatny adres IPv4 dodatkowej konfiguracji adresu IP skojarzonego z dodatkowy interfejs sieciowy na maszynie wirtualnej (Dowiedz się więcej o [interfejsów sieciowych podstawowych i pomocniczych](virtual-network-network-interface-vm.md#about)), miejsce hello wirtualnego maszyny do hello zatrzymane (cofnięciu przydziału) stanu przed ukończeniem hello następujące kroki: 

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *interfejsy sieciowe*. Gdy **interfejsy sieciowe** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **interfejsy sieciowe** bloku, który jest wyświetlany, kliknij przycisk hello interfejsu sieciowego mają tooview lub zmienić ustawienia adresu IP.
4. Kliknij przycisk **konfiguracje adresów IP** w hello **ustawienia** części bloku hello interfejsu sieciowego hello wybrane.
5. Kliknij pozycję Konfiguracja IP hello ma toomodify z listy hello w bloku hello, którego kliknięcie spowoduje otwarcie dla konfiguracji adresów IP.
6. Zmień hello ustawienia, zgodnie z potrzebami, za pomocą hello informacji o ustawieniach hello w kroku 6 hello [Dodaj konfigurację IP](#create-ip-config) sekcji tego artykułu. Kliknij przycisk **zapisać** tooclose hello bloku do konfiguracji protokołu IP hello zostało zmienione.

>[!NOTE]
>Jeśli hello podstawowy interfejs sieciowy ma wielu konfiguracji adresów IP i zmień hello prywatnego adresu IP hello podstawową konfigurację protokołu IP, należy ręcznie ponownie przypisać hello podstawowych i pomocniczych IP adresów toohello interfejsu sieciowego w systemie Windows (nie wymagany dla systemu Linux). toomanually przypisać interfejsu sieciowego tooa adresów IP w ramach systemu operacyjnego, przeczytaj hello [przypisać wiele adresów IP maszyny toovirtual](virtual-network-multiple-ip-addresses-portal.md#os-config) artykułu. Zobacz [prywatnej](#private) adresów IP dla uwagi przed dodaniem ręcznie systemu operacyjnego maszyny wirtualnej tooa adresów IP. Nie dodawaj żadnych publicznego adresu IP adresów toohello systemu operacyjnego maszyny wirtualnej.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Aktualizacja konfiguracji adresu ip karty sieciowej sieci az](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Zestaw AzureRMNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="remove-ip-addresses"></a>Usuń adresy IP

Możesz usunąć [prywatnej](#private) i [publicznego](#public) adresów IP z karty sieciowej, ale interfejs sieci zawsze musi mieć co najmniej jednego prywatnego tooit przypisany adres IPv4.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *interfejsy sieciowe*. Gdy **interfejsy sieciowe** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **interfejsy sieciowe** bloku, który jest wyświetlany, kliknij przycisk tooremove adresy IP z interfejsu sieciowego hello.
4. Kliknij przycisk **konfiguracje adresów IP** w hello **ustawienia** części bloku hello interfejsu sieciowego hello wybrane.
5. Kliknij prawym przyciskiem myszy [dodatkowej](#secondary) konfiguracji protokołu IP (nie można usunąć hello [głównej](#primary) konfiguracji) mają toodelete, kliknij przycisk **usunąć**, następnie kliknij przycisk **tak**  tooconfirm hello usunięcia. Jeśli konfiguracja hello ma zasób publicznego adresu IP skojarzonego tooit, zasobów hello jest oddzielona od konfiguracji IP hello, ale hello zasobów nie zostanie usunięta.
6. Zamknij hello **konfiguracje adresów IP** bloku.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Usuwanie konfiguracji adresu ip karty sieciowej sieci az](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Usuń AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/remove-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="ip-configurations"></a>Konfiguracje adresów IP

[Prywatne](#private) i (opcjonalnie) [publicznego](#public) adresy IP są przypisywane tooone lub więcej konfiguracje adresów IP przypisanych tooa interfejsu sieciowego. Istnieją dwa typy konfiguracji adresu IP:

### <a name="primary"></a>Podstawowy

Każdy interfejs sieciowy jest przypisany jedną podstawową konfigurację protokołu IP. Podstawową konfigurację protokołu IP:

- Ma [prywatnej](#private) [IPv4](#ipv4) tooit adres przypisany. Nie można przydzielić prywatnej [IPv6](#ipv6) adres tooa podstawową konfigurację protokołu IP.
- Może być również [publicznego](#public) tooit przypisany adres IPv4. Nie można przypisać publicznej konfiguracji adresów IPv6 tooa podstawowy lub pomocniczy IP. Możesz natomiast, przypisz IPv6 publiczny adres usługi równoważenia obciążenia Azure tooan, które można załadować równoważenie ruchu tooa maszynę wirtualną w prywatny adres IPv6. Aby uzyskać więcej informacji, zobacz [szczegółowe informacje i ograniczenia dotyczące IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations).

### <a name="secondary"></a>Pomocniczy

Ponadto tooa podstawową konfigurację protokołu IP, karty sieciowej może być zero lub więcej dodatkowej konfiguracji IP przypisanych tooit. Dodatkowej konfiguracji adresu IP:

- Musi mieć prywatnych tooit przypisany adres IPv4 lub IPv6. Jeśli hello adresu IPv6, hello interfejsu sieciowego może mieć tylko jedną konfigurację adresu IP dodatkowej. Jeśli hello adres IPv4, hello interfejsu sieciowego może mieć wielu dodatkowej konfiguracji adresów IP przypisanych tooit. toolearn więcej informacji na temat liczby prywatnych i publicznych adresów IPv4 można przypisać tooa interfejsu sieciowego, zobacz hello [Azure ogranicza](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artykułu.  
- Mogą także mieć publicznego tooit przypisany adres IPv4, jeśli hello prywatnego adresu IP jest protokół IPv4. Hello prywatnego adresu IP w przypadku protokołu IPv6, nie można przypisać z publicznego IPv4 lub IPv6 adres toohello konfiguracji IP. Przypisywanie wielu interfejsu sieciowego tooa adresów IP jest takie jak przydatne w scenariuszach:
    - Hostowanie wielu witryn sieci Web lub usług z różnymi adresami IP i certyfikatami SSL na jednym serwerze.
    - Maszyna wirtualna, służąc jako urządzenie wirtualne sieci, takie jak Zapora lub Usługa równoważenia obciążenia.
    - żadnego z adresów IPv4 prywatny dla każdego z puli zaplecza modułu równoważenia obciążenia Azure tooan interfejsów sieciowych hello hello Hello tooadd możliwości. W ciągu ostatnich hello tylko hello podstawowy adres IPv4 dla interfejsu sieci podstawowej hello można było dodać tooa puli zaplecza. toolearn więcej informacji na temat sposobu tooload saldo konfiguracji z wieloma IPv4 Zobacz hello [wielu konfiguracji adresów IP równoważenia obciążenia](../load-balancer/load-balancer-multiple-ip.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu. 
    - tooload możliwości Hello równoważenie jeden interfejs sieciowy tooa przypisany adres IPv6. toolearn więcej informacji na temat sposobu tooload saldo tooa prywatnego adresu IPv6, zobacz hello [adresy IPv6 równoważenia obciążenia](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.


## <a name="address-types"></a>Typy adresów

Witaj następujące typy tooan adresy IP można przypisać [konfiguracji IP](#ip-configurations):

### <a name="private"></a>Prywatne

Prywatne [IPv4](#ipv4) adresy włączyć toocommunicate maszynę wirtualną z innych zasobów w sieci wirtualnej lub innych połączonych sieciach. Maszyny wirtualnej nie może być przekazywane ruchu przychodzącego, ani można hello maszyny wirtualnej komunikowania się wychodzące z prywatnej [IPv6](#ipv6) adres, z jednym wyjątkiem. Maszyny wirtualne mogą komunikować się z modułem równoważenia obciążenia Azure hello przy użyciu adresu IPv6. Aby uzyskać więcej informacji, zobacz [szczegółowe informacje i ograniczenia dotyczące IPv6](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#details-and-limitations). 

Domyślnie serwery Azure DHCP hello przypisać hello prywatny adres IPv4 dla hello [podstawową konfigurację protokołu IP](#primary) hello sieci interfejsu toohello interfejsu sieciowego w systemie operacyjnym maszyny wirtualnej hello. O ile to konieczne, należy nigdy nie ręcznie ustawić hello adres IP interfejsu sieciowego w systemie operacyjnym maszyny wirtualnej hello. 

> [!WARNING]
> Jeśli tooa dołączony hello adres IPv4 ustawione jako hello podstawowy adres IP interfejsu sieciowego w systemie operacyjnym maszyny wirtualnej kiedykolwiek różni się od hello toohello podstawową konfigurację protokołu IP interfejsu sieci podstawowej hello przypisany prywatny adres IPv4 w przypadku maszyny wirtualnej w systemie Azure zostaną utracone maszyny wirtualnej toohello łączności.

Istnieją scenariusze, w których jest konieczne toomanually zestaw hello adres IP interfejsu sieciowego w systemie operacyjnym maszyny wirtualnej hello. Na przykład należy ręcznie ustawić hello głównych i dodatkowych adresów IP w systemie operacyjnym Windows podczas dodawania wielu tooan adresów IP maszyny wirtualnej platformy Azure. Dla maszyny wirtualnej systemu Linux konieczne może być toomanually zestaw hello dodatkowych adresów IP. Zobacz [adresów IP Dodaj system operacyjny maszyny Wirtualnej tooa](virtual-network-multiple-ip-addresses-portal.md#os-config) szczegółowe informacje. Po ustawieniu ręcznie hello adresu IP w ramach systemu operacyjnego hello, zalecane jest zawsze przypisać konfiguracji IP toohello hello adresów dla karty sieciowej, za pomocą metody przydziału statyczne (zamiast dynamicznych) hello. Przypisywanie adresu hello za pomocą metody statycznej hello zapewnia hello adres nie ulega zmianie w obrębie platformy Azure. Jeśli kiedykolwiek zajdzie toochange hello adres przypisany tooan konfiguracji adresu IP, jest zalecane możesz:

1. Maszyna wirtualna tooensure hello jest uzyskiwania adresu z serwerów Azure DHCP hello, zmień przydział hello wstecz tooDHCP adres IP hello w ramach systemu operacyjnego hello i maszyny wirtualnej hello ponownego uruchomienia.
2. Zatrzymaj (deallocate) hello maszyny wirtualnej.
3. Zmienianie adresu IP hello do konfiguracji protokołu IP hello w obrębie platformy Azure.
4. Uruchom maszynę wirtualną hello.
5. [Ręczne konfigurowanie](virtual-network-multiple-ip-addresses-portal.md#os-config) hello dodatkowej toomatch adresów w ramach systemu operacyjnego hello (a także hello podstawowego adresu IP w systemie Windows) adresu IP, ustaw w obrębie platformy Azure.
 
Wykonując hello poprzednie kroki hello prywatnego adresu IP adres przypisany toohello interfejsu sieciowego w systemie Azure i w systemie operacyjnym maszyny wirtualnej, pozostają takie same hello. Śledź tookeep którego maszyn wirtualnych w ramach subskrypcji ręcznie ustawiono adresy IP w ramach systemu operacyjnego, należy rozważyć dodanie Azure [tag](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags) toohello maszyn wirtualnych. Można na przykład "przypisywanie adresów IP: statyczny", na przykład. W ten sposób hello maszyn wirtualnych można łatwo znaleźć w ramach subskrypcji ręcznie ustawionych hello adres IP w ramach systemu operacyjnego hello.

Ponadto tooenabling toocommunicate maszynę wirtualną z innych zasobów w ramach tego samego lub połączonych sieci wirtualnych, prywatnego adresu IP również adres powitalne umożliwia toohello wychodzących toocommunicate Internet maszyny wirtualnej. Połączenia wychodzące są źródłowego adresu sieci przetłumaczyła nieprzewidywalne publicznego adresu IP tooan platformy Azure. więcej informacji na temat Azure wychodzące połączenie z Internetem, przeczytaj hello toolearn [Azure wychodzące połączenie z Internetem](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu. Nie można komunikować się maszyny wirtualnej dla ruchu przychodzącego tooa prywatnego adresu IP z hello Internet.

### <a name="public"></a>Publiczne

Publiczne adresy IP umożliwiają maszyny wirtualnej tooa połączenia przychodzącego z hello Internet. Połączenia wychodzące toohello Internet używać przewidywalną adresu IP. Zobacz [Opis połączeń wychodzących na platformie Azure](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) szczegółowe informacje. Może przypisać publicznej konfiguracji IP tooan adresu IP, ale nie są wymagane. Jeśli nie przypisano publiczny maszyny wirtualnej tooa adres IP, nadal mogą komunikować się wychodzących toohello Internetem przy użyciu prywatnego adresu IP. więcej informacji na temat publiczne adresy IP, przeczytaj hello toolearn [publicznego adresu IP](virtual-network-public-ip-address.md) artykułu.

Istnieją ograniczenia toohello liczba prywatnych i publicznych adresów IP, że można przypisać tooa interfejsu sieciowego. Aby uzyskać więcej informacji, przeczytaj hello [Azure ogranicza](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) artykułu.

> [!NOTE]
> Azure tłumaczy maszynę wirtualną prywatnego adresu IP adres tooa publicznego adresu IP. W związku z tym nie rozpoznaje wszystkie publiczne adresy IP przypisane tooit hello systemu operacyjnego, więc nie ma żadnych tooever muszą ręcznie przypisać publicznego adresu IP w ramach systemu operacyjnego hello.

## <a name="assignment-methods"></a>Metody przydziału

Publiczne i prywatne adresy IP są przypisywane, przy użyciu hello następujące metody przypisania:

### <a name="dynamic"></a>Dynamiczny

Prywatne IPv4 i IPv6 (opcjonalnie) adresy są przypisywane domyślnie. Dynamiczne adresy można zmienić, gdy maszyna wirtualna hello są umieszczane w hello zatrzymana stanu (cofnięciu przydziału), a następnie uruchomić. Jeśli nie chcesz toochange adresy IPv4 dla okresu hello hello maszyny wirtualnej, przypisz adresy hello za pomocą metody statycznej hello. Można przypisać tylko prywatnego adresu IPv6 przy użyciu metody dynamiczne przydzielanie hello. Nie można przypisać publicznej konfiguracji adresów IPv6 tooan IP przy użyciu jednej z metod.

### <a name="static"></a>Statyczny

Adresy przypisywane przy użyciu metody statycznej hello nie należy zmieniać dopóki maszyna wirtualna zostanie usunięta. Interfejs sieciowy hello podsieci hello jest ręcznie przypisać prywatnej IPv4 adres tooan konfiguracji statycznych adresów IP w przestrzeni adresowej hello. (Opcjonalnie) można przypisać publicznych lub prywatnych IPv4 adres tooan konfiguracji statycznych adresów IP. Nie można przypisać publicznych lub prywatnych IPv6 adres tooan konfiguracji statycznych adresów IP. toolearn więcej informacji na temat sposobu Azure przypisuje statyczne publiczne adresy IPv4, zobacz hello [publicznego adresu IP](virtual-network-public-ip-address.md) artykułu.

## <a name="ip-address-versions"></a>Wersji adresu IP

Można określić następujące wersje podczas przypisywania adresów hello:

### <a name="ipv4"></a>IPv4

Każdy interfejs sieciowy musi mieć jeden [głównej](#primary) konfiguracji adresów IP z przypisanym [prywatnej](#private) [IPv4](#ipv4) adres. Można dodać jeden lub więcej [dodatkowej](#secondary) konfiguracje adresów IP, każdy mieć IPv4 prywatnych i (opcjonalnie) IPv4 [publicznego](#public) adresu IP.

### <a name="ipv6"></a>Protokół IPv6

Można przypisać prywatnego zero lub jeden [IPv6](#ipv6) adres tooone dodatkowej konfiguracji IP interfejsu sieciowego. Interfejs sieciowy Hello nie może mieć żadnych istniejących dodatkowej konfiguracji adresu IP. Nie można dodać konfiguracji IP przy użyciu adresu IPv6 przy użyciu portalu hello. Za pomocą programu PowerShell lub hello tooadd CLI konfigurację IP prywatnej IPv6 adres tooan istniejącego interfejsu sieciowego. Interfejs sieciowy Hello nie może być dołączone tooan istniejącej maszyny Wirtualnej.

> [!NOTE]
> Chociaż można utworzyć interfejs sieciowy z adresów IPv6 za pomocą portalu hello, nie można dodać istniejącej sieci interfejsu tooa nowej lub istniejącej maszyny wirtualnej, za pomocą portalu hello. Użyj programu PowerShell lub hello Azure CLI 2.0 toocreate interfejsu sieciowego za pomocą prywatnego adresu IPv6, a następnie dołączyć interfejsu sieciowego hello, podczas tworzenia maszyny wirtualnej. Nie można dołączyć karty sieciowej, za pomocą prywatnego adresu IPv6 przypisany tooit tooan istniejącej maszyny wirtualnej. Nie można dodać prywatnej konfiguracji adresów IPv6 tooan IP dla dowolnego interfejsu sieci tooa maszyny wirtualnej przy użyciu dowolnego narzędzia (portal, interfejsu wiersza polecenia lub środowiska PowerShell).

Nie można przypisać publicznej konfiguracji adresów IPv6 tooa podstawowy lub pomocniczy IP.

## <a name="next-steps"></a>Następne kroki
toocreate maszynę wirtualną z różnymi konfiguracjami IP, przeczytaj hello następujące artykuły:

|Zadanie|Narzędzie|
|---|---|
|Tworzenie maszyny wirtualnej z wieloma kartami sieciowymi|[Interfejs wiersza polecenia](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [środowiska PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Tworzenie jednej maszyny Wirtualnej karty Sieciowej z wielu adresów IPv4|[Interfejs wiersza polecenia](virtual-network-multiple-ip-addresses-cli.md), [środowiska PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Tworzenie jednej maszyny Wirtualnej karty Sieciowej za pomocą prywatnego adresu IPv6 (za równoważenia obciążenia Azure)|[Interfejs wiersza polecenia](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [szablonu usługi Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
