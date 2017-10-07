---
title: aaaCreate, zmienianie lub usuwanie publicznego adresu IP platformy Azure | Dokumentacja firmy Microsoft
description: "Dowiedz się, jak toocreate, zmienić lub usunąć publicznego adresu IP."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bb71abaf-b2d9-4147-b607-38067a10caf6
ms.service: virtual-network
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: jdial
ms.openlocfilehash: 0f2578e8661c8f33419b896debcfa0ba1b41fc5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-public-ip-address"></a>Tworzenie, zmienianie lub usuwanie publicznego adresu IP

Dowiedz się więcej o publicznego adresu IP adresów i jak toocreate, zmienianie i usuwanie jednego. Publiczny adres IP jest zasób o jego ustawienia można skonfigurować. Przypisywanie publicznego tooother adres IP zasobów platformy Azure umożliwia:
- Liczba przychodzących tooresources łączności Internet, takich jak Azure maszyn wirtualnych (VM), zestawy skalowania maszyny wirtualnej Azure, Brama sieci VPN platformy Azure, bramy aplikacji i usług równoważenia obciążenia Azure internetowy. Zasoby platformy Azure nie mogą otrzymywać komunikacji przychodzącej hello Internet bez przypisanej publicznego adresu IP. Podczas niektórych zasobów platformy Azure są z założenia dostępne za pośrednictwem publicznych adresów IP, inne zasoby musi mieć publicznych adresów IP przypisanych toobe toothem dostępny z Internetu hello.
- Łączność wychodząca toohello Internet przy użyciu wartości prognozowanych adresu IP. Na przykład maszyny wirtualne mogą komunikować się wychodzących toohello Internet bez publicznego tooit przypisany adres IP, ale jej adres jest adresem sieci przetłumaczyła Azure tooan nieprzewidywalne publiczny adres. Przypisywanie zasobu tooa publicznego adresu IP pozwala tooknow, który adres IP jest używana dla połączenia wychodzącego hello. Chociaż przewidywalne, można zmienić adres hello, w zależności od wybranej metody przypisania hello. Aby uzyskać więcej informacji, zobacz [tworzenie publicznego adresu IP](#create-a-public-ip-address). więcej informacji na temat połączenia wychodzące z zasobów platformy Azure, przeczytaj hello toolearn [zrozumieć połączeń wychodzących](../load-balancer/load-balancer-outbound-connections.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykułu.

## <a name="before-you-begin"></a>Przed rozpoczęciem

Wykonaj następujące zadania, przed wykonaniem dowolnej kroków w żadnej sekcji tego artykułu hello:

- Przejrzyj hello [Azure ogranicza](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artykuł na temat limitów dla publicznych adresów IP.
- Zaloguj się za toohello Azure [portal](https://portal.azure.com), Azure interfejsu wiersza polecenia (CLI) lub Azure PowerShell przy użyciu konta platformy Azure. Jeśli nie masz jeszcze konta platformy Azure, należy zarejestrować się w celu [bezpłatnego konta wersji próbnej](https://azure.microsoft.com/free).
- Jeśli przy użyciu programu PowerShell poleceń toocomplete zadania w tym artykule [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello apletów poleceń programu hello Azure PowerShell. tooget Pomoc dla poleceń programu PowerShell, wraz z przykładami, wpisz `get-help <command> -full`.
- Jeśli przy użyciu interfejsu wiersza polecenia platformy Azure (CLI) polecenia toocomplete zadania w tym artykule [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello Azure CLI zainstalowane. tooget pomocy dla poleceń interfejsu wiersza polecenia, wpisz `az <command> --help`. Zamiast instalowania hello interfejsu wiersza polecenia i jego wymagania wstępne można użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. toouse hello powłoki chmury kliknij hello powłoki chmury **> _** u góry hello hello [portal](https://portal.azure.com).

Publiczne adresy IP ma nominalnego opłat. Cennik hello tooview odczytu hello [cennik adres IP](https://azure.microsoft.com/pricing/details/ip-addresses) strony. 

## <a name="create-a-public-ip-address"></a>Tworzenie publicznego adresu IP

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *publicznego adresu ip*. Gdy **publicznego adresu IP, adresy** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. Kliknij przycisk **+ Dodaj** w hello **publicznego adresu IP** wyświetlonym bloku.
4. Wprowadź lub wybierz wartości dla następujących ustawień w hello hello **tworzenie publicznego adresu IP** bloku, zostanie wyświetlone, następnie kliknij przycisk **Utwórz**:

    |Ustawienie|Wymagana?|Szczegóły|
    |---|---|---|
    |Nazwa|Tak|Nazwa Hello musi być unikatowa w ramach grupy zasobów hello, którą wybierzesz.|
    |Wersji protokołu IP|Tak| Wybierz IPv4 lub IPv6. Podczas gdy IPv4 publiczne adresy mogą być przypisane tooseveral zasobów platformy Azure, publiczny adres IP protokołu IPv6 można przypisać tylko tooan internetowy modułu równoważenia obciążenia. Moduł równoważenia obciążenia Hello może zrównoważyć obciążenie IPv6 ruchu tooAzure maszyn wirtualnych. Dowiedz się więcej o [maszyny toovirtual ruch IPv6 równoważenia obciążenia](../load-balancer/load-balancer-ipv6-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json).
    |Przypisywanie adresów IP|Tak|**Dynamiczne:** dynamicznych adresów są przypisane tylko po hello publiczny adres IP jest skojarzony tooa karty Sieciowej podłączony tooa maszyny Wirtualnej i hello maszyna wirtualna jest uruchomiona na powitania po raz pierwszy. Dynamiczne adresy można zmienić, gdy hello hello maszyny Wirtualnej karty Sieciowej jest dołączony toois zatrzymane (cofnięciu przydziału). pozostaje adres Hello hello sam hello maszyny Wirtualnej jest ponowny rozruch lub zatrzymana (ale nie cofnięciu przydziału). **Statyczne:** przypisywania adresów statycznych po utworzeniu hello publicznego adresu IP. Statyczne adresy nie nie zmiany, nawet jeśli hello maszyny Wirtualnej jest umieszczany w hello zatrzymane (cofnięciu przydziału) stanu. adres Hello zwolnieniu tylko po usunięciu hello karty Sieciowej. Metoda przydziału hello można zmienić po utworzeniu hello karty Sieciowej. W przypadku wybrania protokołu IPv6 dla hello **IP w wersji**, Metoda przydziału dostępne tylko hello jest **dynamiczne**.|
    |Limit czasu bezczynności (w minutach)|Nie|Ile minut tookeep Otwórz połączenie TCP lub HTTP bez polegania na komunikaty utrzymywania aktywności toosend klientów. W przypadku wybrania protokołu IPv6 dla **IP w wersji**, nie można zmienić tej wartości. |
    |Etykieta nazwy DNS|Nie|Musi być unikatowa w obrębie hello lokalizacji platformy Azure, Utwórz nazwę hello (za pośrednictwem wszystkie subskrypcje i wszystkich klientów). Hello Azure publicznej usługi DNS automatycznie rejestruje hello nazwy i adresu IP, aby mogli łączyć z tooa zasobów o nazwie hello. Dołącza Azure *location.cloudapp.azure.com* (Jeśli lokalizacja jest lokalizacją hello wybrania) nazwa toohello podasz toocreate hello w pełni kwalifikowana nazwa DNS. Jeśli wybierzesz toocreate obie wersje adres hello tą samą nazwą DNS jest przypisany tooboth hello IPv4 i IPv6. Hello usługa Azure DNS zawiera zarówno IPv4 A i IPv6 AAAA rejestruje nazwę i odpowiada zarówno rekordy po wyszukiwana jest nazwa DNS hello. powitania klienta wybiera które adresu (IPv4 lub IPv6) toocommunicate z.|
    |Utwórz adres IPv6 (lub IPv4)|Nie| Określa, czy jest wyświetlany IPv6 lub protokół IPv4 jest zależna od wybierz dla **IP w wersji**. Na przykład w przypadku wybrania **IPv4** dla **IP w wersji**, **IPv6** jest wyświetlany w tym miejscu.
    |Nazwa (tylko widoczne, gdy zaznaczono hello **utworzyć adres IPv6 (lub IPv4)** wyboru)|Tak, w przypadku wybrania hello **utworzyć IPv6** (lub IPv4) pole wyboru.|Witaj nazwa musi być inna niż nazwa hello wprowadzeniu hello najpierw **nazwa** na tej liście. Jeśli wybierzesz toocreate adres IPv6 i IPv4, hello portal tworzy dwa oddzielne zasoby publicznych adresów IP adres, z każdej wersji adresu IP przypisany tooit.|
    |Przypisywanie adresów IP (tylko widoczne, gdy zaznaczono hello **utworzyć adres IPv6 (lub IPv4)** wyboru)|Tak, w przypadku wybrania hello **utworzyć IPv6** (lub IPv4) pole wyboru.|Jeśli pole wyboru hello **utworzyć adres IPv4**, można wybrać metodę przypisania. Jeśli pole wyboru hello **utworzyć adres IPv6**, nie można wybrać metodę przypisania jako musi być **dynamiczne**.|
    |Subskrypcja|Tak|Musi istnieć w hello sam [subskrypcji](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription) jako zasób hello ma tooassociate hello publiczny adres IP.|
    |Grupa zasobów|Tak|Może istnieć w hello tego samego lub innego, [grupy zasobów](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) jako zasób hello ma tooassociate hello publiczny adres IP.|
    |Lokalizacja|Tak|Musi istnieć w hello sam [lokalizacji](https://azure.microsoft.com/regions), nazywana także tooas region jako zasób hello ma tooassociate hello publiczny adres IP.|

**Polecenia**

Chociaż hello portal udostępnia hello opcja toocreate dwa zasoby publicznych adresów IP address (jeden adres IPv4 i IPv6 jeden), hello następujących poleceń programu PowerShell i interfejsu wiersza polecenia Utwórz jeden zasób z adresem dla jednej wersji adresu IP lub hello innych. Jeśli chcesz, aby dwa zasoby publicznych adresów IP address, jeden dla każdej wersji adresu IP, należy uruchomić polecenie hello dwukrotnie, określenia innej nazwy i wersje hello zasoby publicznych adresów IP. 

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Tworzenie sieci az publicznego ip](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nowe AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress)|

## <a name="view-change-settings-for-or-delete-a-public-ip-address"></a>Wyświetlanie, zmieniać ustawienia lub usuwanie publicznego adresu IP

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *publicznego adresu ip*. Gdy **publicznego adresu IP, adresy** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **publicznego adresu IP, adresy** bloku, który jest wyświetlany, kliknij nazwę hello hello publicznego adresu IP ma tooview, Zmień ustawienia lub usunąć.
4. W bloku hello wyświetlonym hello publicznego adresu IP, pełną spośród hello następujące opcje w zależności od tego, czy ma być tooview, usuń lub zmień hello publicznego adresu IP.
    - **Widok**: hello **omówienie** części bloku hello przedstawia ustawień klucza publicznego adresu IP hello, takich jak hello interfejs sieciowy związany z nim zbyt (Jeśli adres hello jest skojarzony tooa interfejsu sieciowego). Hello portal nie wyświetla wersję hello adresu hello (IPv4 lub IPv6). informacje o wersji hello tooview, hello Użyj programu PowerShell lub interfejsu wiersza polecenia polecenie tooview hello publicznego adresu IP. Wersja adresów IP hello jest protokół IPv6, hello przypisany adres nie jest wyświetlana przez hello portal, programu PowerShell lub hello interfejsu wiersza polecenia. 
    - **Usuń**: toodelete hello publicznego adresu IP, kliknij przycisk **usunąć** w hello **omówienie** sekcji hello bloku. Jeśli adres hello jest obecnie skojarzony tooan konfiguracji protokołu IP, nie można usunąć. Jeśli adres hello jest obecnie skojarzony z konfiguracją, kliknij przycisk **Utwórz skojarzenie** toodissociate hello adres z hello konfiguracji protokołu IP.
    - **Zmień**: kliknij **konfiguracji**. Zmień ustawienia za pomocą informacji hello w kroku 4 hello [tworzenie publicznego adresu IP](#create-a-public-ip-address) sekcji tego artykułu. przypisania hello toochange z toodynamic statycznego adresu IPv4, należy najpierw skojarzenie hello publiczny adres IPv4 z hello konfiguracji adresu IP, który jest ona skojarzona. Można zmienić toodynamic metoda przydziału hello i kliknij przycisk **skojarzyć** toohello adres IP hello tooassociate tego samego adresu IP konfiguracji, innej konfiguracji lub należy pozostawić Usunięto skojarzenie. publiczny adres IP w hello toodissociate **omówienie** , kliknij przycisk **Utwórz skojarzenie**.

>[!WARNING]
>Zmiana metody przypisywania hello z toodynamic statycznych, utracisz hello adresu IP, któremu przypisano publiczny adres IP toohello. Podczas hello Azure publicznych serwerów DNS Obsługa mapowanie między statyczne lub dynamiczne adresy i wszelkie etykieta nazwy DNS (Jeśli zdefiniowany jest jeden), dynamicznego adresu IP można zmienić, gdy hello maszyny Wirtualnej zostanie uruchomiony po w hello zatrzymania stanu (cofnięciu przydziału). adres hello tooprevent zmianę, Przypisz statyczny adres IP.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[AZ sieci publicznego adresu ip listy](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#list) toolist publiczne adresy IP, [az sieci publicznego adresu ip Pokazywanie](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#show) ustawienia tooshow; [az sieci ip publicznego aktualizacji](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#update) tooupdate; [usunąć publicznej sieci az ip](/cli/azure/network/public-ip?toc=%2fazure%2fvirtual-network%2ftoc.json#delete) toodelete|
|PowerShell|[Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) tooretrieve publicznego adresu IP adres obiektu i wyświetlić jej ustawienia [AzureRmPublicIpAddress zestaw](/powershell/resourcemanager/azurerm.network/set-azurermpublicipaddress?toc=%2fazure%2fvirtual-network%2ftoc.json) ustawienia tooupdate; [AzureRmPublicIpAddress Usuń](/powershell/module/azurerm.network/remove-azurermpublicipaddress) toodelete|

## <a name="next-steps"></a>Następne kroki
Podczas tworzenia hello następujących zasobów platformy Azure, przypisz publicznych adresów IP:

- [Windows](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Linux](../virtual-machines/linux/quick-create-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json) maszyny wirtualne
- [Moduł równoważenia obciążenia Azure połączonych z Internetem](../load-balancer/load-balancer-get-started-internet-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Brama aplikacji Azure](../application-gateway/application-gateway-create-gateway-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Połączenie lokacja lokacja za pomocą bramy sieci VPN platformy Azure](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
- [Zestaw skali maszyny wirtualnej platformy Azure](../virtual-machine-scale-sets/virtual-machine-scale-sets-portal-create.md?toc=%2fazure%2fvirtual-network%2ftoc.json)
