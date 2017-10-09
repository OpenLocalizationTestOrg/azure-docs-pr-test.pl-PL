---
title: "aaaCreate, zmienić lub usunąć interfejs sieci platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jakie interfejs sieciowy jest i jak toocreate, zmienić ustawienia i usunąć jeden."
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
ms.openlocfilehash: dcb6cdbd73bc0d0ca4efb9d972d370cf2d54abb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="create-change-or-delete-a-network-interface"></a>Tworzenie, zmienianie lub usuwanie interfejsu sieciowego

Dowiedz się, jak toocreate, Zmień ustawienia i usunąć interfejsu sieciowego. Interfejs sieciowy umożliwia toocommunicate maszyny wirtualnej platformy Azure z Internetu, Azure i lokalnymi zasobami. Podczas tworzenia maszyny wirtualnej z wykorzystaniem hello portalu Azure, portalu hello tworzy jeden interfejs sieciowy z ustawieniami domyślnymi dla Ciebie. Zamiast tego mogą wybrać toocreate interfejsów sieciowych za pomocą ustawień niestandardowych i Dodaj jeden lub więcej sieci interfejsy tooa maszynę wirtualną podczas jej tworzenia. Można również ustawienia interfejsu sieciowego domyślne toochange dla istniejącego interfejsu sieciowego. W tym artykule opisano sposób toocreate interfejsu sieciowego z użyciem ustawień niestandardowych, zmień istniejące ustawienia, takie jak przypisywanie (sieciowej grupy zabezpieczeń) filtru sieci, przypisanie podsieci, ustawienia serwera DNS i przesyłanie dalej IP i usunąć interfejsu sieciowego.

Tooadd, należy zmienić lub usunąć adresy IP dla karty sieciowej, przeczytaj hello [adresów IP zarządzanie](virtual-network-network-interface-addresses.md) artykułu. Jeśli konieczne tooadd interfejsów sieciowych lub usuwanie interfejsów sieciowych z maszyn wirtualnych, przeczytaj hello [Dodawanie lub usuwanie interfejsów sieciowych](virtual-network-network-interface-vm.md) artykułu.


## <a name="before-you-begin"></a>Przed rozpoczęciem

Wykonaj następujące zadania, przed wykonaniem dowolnej kroków w żadnej sekcji tego artykułu hello:

- Przejrzyj hello [Azure ogranicza](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits) toolearn artykułu na temat limitów dla interfejsów sieciowych.
- Zaloguj się za toohello Azure [portal](https://portal.azure.com), Azure interfejsu wiersza polecenia (CLI) lub Azure PowerShell przy użyciu konta platformy Azure. Jeśli nie masz jeszcze konta platformy Azure, należy zarejestrować się w celu [bezpłatnego konta wersji próbnej](https://azure.microsoft.com/free).
- Jeśli przy użyciu programu PowerShell poleceń toocomplete zadania w tym artykule [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello apletów poleceń programu hello Azure PowerShell. tooget Pomoc dla poleceń programu PowerShell, wraz z przykładami, wpisz `get-help <command> -full`.
- Jeśli przy użyciu interfejsu wiersza polecenia platformy Azure (CLI) polecenia toocomplete zadania w tym artykule [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello Azure CLI zainstalowane. tooget pomocy dla poleceń interfejsu wiersza polecenia, wpisz `az <command> --help`. Zamiast instalowania hello interfejsu wiersza polecenia i jego wymagania wstępne można użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. toouse hello powłoki chmury kliknij hello powłoki chmury **> _** u góry hello hello [portal](https://portal.azure.com).

## <a name="create-a-network-interface"></a>Tworzenie interfejsu sieciowego

Podczas tworzenia maszyny wirtualnej z wykorzystaniem hello portalu Azure, portalu hello tworzy interfejs sieciowy z ustawieniami domyślnymi dla Ciebie. Jeśli wolisz określić wszystkie ustawienia interfejsu sieciowego, można utworzyć niestandardowe ustawienia interfejsu sieciowego i dołączyć maszyny wirtualnej tooa interfejsu sieciowego hello podczas tworzenia maszyny wirtualnej hello (przy użyciu programu PowerShell lub interfejsu wiersza polecenia Azure hello). Można również utworzyć interfejsu sieciowego i dodać go tooan istniejącej maszyny wirtualnej (przy użyciu programu PowerShell lub hello Azure CLI). toolearn jak toocreate maszynę wirtualną z istniejącym sieci interfejsu lub tooadd do lub usuwanie interfejsów sieciowych z istniejących maszyn wirtualnych, przeczytaj hello [Dodawanie lub usuwanie interfejsów sieciowych](virtual-network-network-interface-vm.md) artykułu. Przed utworzeniem karty sieciowej, musisz mieć istniejące [sieci wirtualnej](virtual-networks-create-vnet-arm-pportal.md) w hello tej samej lokalizacji i subskrypcji można utworzyć interfejsu sieciowego w.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *interfejsy sieciowe*. Gdy **interfejsy sieciowe** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **interfejsy sieciowe** bloku, który jest wyświetlany, kliknij przycisk **+ Dodaj**.
4. W hello **interfejsu sieciowego Utwórz** bloku, zostanie wyświetlone, wprowadź, lub wybierz wartości dla hello następujące ustawienia, a następnie kliknij **Utwórz**:

    |Ustawienie|Wymagana?|Szczegóły|
    |---|---|---|
    |Nazwa|Tak|Nazwa Hello musi być unikatowa w ramach grupy zasobów hello, którą wybierzesz. Wraz z upływem czasu najprawdopodobniej będziesz mieć kilka interfejsów sieciowych w ramach subskrypcji platformy Azure. Witaj odczytu [konwencje nazewnictwa](/azure/architecture/best-practices/naming-conventions?toc=%2fazure%2fvirtual-network%2ftoc.json#naming-rules-and-restrictions) artykułu dla sugestie podczas tworzenia nazewnictwa toomake Konwencji Zarządzanie kilka interfejsów łatwiejsze sieciowych. Nie można zmienić nazwy Hello, po utworzeniu hello interfejsu sieciowego.|
    |Sieć wirtualna|Tak|Wybierz sieć wirtualną hello hello interfejsu sieciowego. Można przypisać tylko sieci interfejsu tooa siecią wirtualną, która istnieje na powitania sam subskrypcji i lokalizacji co hello interfejsu sieciowego. Po utworzeniu karty sieciowej nie można zmienić hello sieci wirtualnej, który jest przypisany do. Witaj maszyny wirtualnej, dodać toomust interfejsu sieciowego hello także istnieć w hello sam lokalizacji i subskrypcji jako hello interfejsu sieciowego.|
    |Podsieć|Tak|Wybierz podsieć w sieci wirtualnej hello wybrane. Można zmienić podsieci hello hello interfejsu sieciowego jest przypisany tooafter jest tworzona.|
    |Przypisanie prywatnego adresu IP|Tak| W tym ustawieniu, czy wybierana metoda przydziału hello hello adres IPv4. Wybierz jedną z hello następujące metody przypisania: **dynamicznej:** po wybraniu tej opcji Azure automatycznie przypisuje adres z hello przestrzeni adresowej podsieci hello wybrane. Azure może przypisać interfejsu sieciowego tooa inny adres, po uruchomieniu hello maszyny wirtualnej, w którym się po o w hello zatrzymane (cofnięciu przydziału) stanu. pozostaje adres Hello hello takie same, jeśli hello maszyny wirtualnej zostanie ponownie uruchomiony bez konieczności w hello zatrzymane (cofnięciu przydziału) stanu. **Statyczne:** po wybraniu tej opcji, należy ręcznie przypisać dostępne z adresu IP w przestrzeni adresowej hello podsieci hello wybrane. Statyczne adresy nie należy zmieniać dopóki je zmienić lub interfejs sieciowy hello jest usuwany. Metoda przydziału hello można zmienić po utworzeniu hello interfejsu sieciowego. Serwer Azure DHCP Hello przypisuje ten interfejs sieciowy toohello adresu w ramach systemu operacyjnego hello hello maszyny wirtualnej.|
    |Grupy zabezpieczeń sieci|Nie| Pozostaw ustawić także**Brak**, wybierz istniejący [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md), lub [Utwórz grupę zabezpieczeń sieci](virtual-networks-create-nsg-arm-pportal.md). Grupy zabezpieczeń sieci Włącz toofilter ruch sieciowy do i z karty sieciowej. Możesz zastosować zero lub jeden zabezpieczeń grupy tooa interfejs sieci. Zero lub jedną grupę zabezpieczeń sieci można również będą stosowane toohello podsieci hello sieciowej jest przypisany do. Gdy grupa zabezpieczeń sieci jest zastosowane tooa sieci i interfejsem sieciowym hello podsieci hello jest przypisany do, wystąpić czasami nieoczekiwane wyniki. interfejsy toonetwork zastosowane i podsieci, grup zabezpieczeń sieci tootroubleshoot odczytu hello [Rozwiązywanie problemów z grup zabezpieczeń sieci](virtual-network-nsg-troubleshoot-portal.md#nsg) artykułu.|
    |Subskrypcja|Tak|Wybierz jedną z platformy Azure [subskrypcje](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#subscription). Dołącz sieci interfejsu tooand hello sieć wirtualną można połączyć z maszyny wirtualnej Hello toomust istnieje w hello sam subskrypcji.|
    |Prywatny adres IP (IPv6)|Nie| Jeśli zaznaczysz to pole wyboru, adres IPv6 jest przypisany toohello interfejsu sieciowego, oprócz toohello adres IPv4 przypisany toohello interfejsu sieciowego. Zobacz hello [IPv6](#IPv6) sekcji tego artykułu, aby uzyskać ważne informacje na temat używania protokołu IPv6 z interfejsami sieciowymi. Nie można wybrać metodę przypisania hello adres IPv6. Jeśli wybierzesz tooassign adres IPv6 jest przypisany przy użyciu metody dynamicznej hello.
    |Nazwa IPv6 (pojawia się tylko wtedy, gdy hello **prywatny adres IP (IPv6)** jest zaznaczone pole wyboru) |Tak, jeśli hello **prywatny adres IP (IPv6)** jest zaznaczone pole wyboru.| Ta nazwa jest przypisany tooa dodatkowej konfiguracji IP interfejsu sieciowego hello. Dowiedz się więcej o konfiguracji adresów IP w hello [wyświetlić ustawienia interfejsu sieciowego](#view-network-interface-settings) sekcji tego artykułu.|
    |Grupa zasobów|Tak|Wybierz istniejący [grupy zasobów](../azure-glossary-cloud-terminology.md?toc=%2fazure%2fvirtual-network%2ftoc.json#resource-group) lub utwórz taki pakiet. Interfejs sieciowy może istnieć w hello takie same lub innej grupie zasobów, niż hello maszyny wirtualnej, dołączyć lub hello wirtualnych sieci, można je połączyć.|
    |Lokalizacja|Tak|Dołącz sieci interfejsu tooand hello sieć wirtualną można połączyć z maszyny wirtualnej Hello toomust istnieje w hello takie same [lokalizacji](https://azure.microsoft.com/regions), nazywana także tooas region.|

Hello portal nie zapewnia z tooassign opcji hello publicznego interfejsu sieciowego toohello adresów IP podczas tworzenia, chociaż portalu hello Utwórz publiczny adres IP i przypisz mu tooa interfejsu sieciowego, podczas tworzenia maszyny wirtualnej za pomocą portalu hello. toolearn jak tooadd sieci toohello publiczny adres IP interfejsu po tworzenia, odczytu hello [adresów IP zarządzanie](virtual-network-network-interface-addresses.md) artykułu. Jeśli chcesz toocreate interfejsu sieciowego z publicznym adresem IP, należy użyć hello interfejsu wiersza polecenia lub środowiska PowerShell toocreate hello interfejsu sieciowego.

>[!Note]
> Przypisuje Azure, MAC address toohello interfejsu sieciowego tylko po hello interfejsu sieciowego maszyny wirtualnej podłączone tooa i maszyny wirtualnej hello jest uruchamiane powitania po raz pierwszy. Nie można określić adres MAC hello że Azure przypisuje toohello interfejsu sieciowego. Witaj interfejsu sieciowego toohello pozostaje przypisany adres MAC, aż do usunięcia interfejsu sieciowego hello lub hello toohello podstawową konfigurację protokołu IP interfejsu sieci podstawowej hello przypisany prywatny adres IP zostanie zmieniona. więcej informacji na temat adresów IP i konfiguracje adresów IP, przeczytaj hello toolearn [adresów IP zarządzanie](virtual-network-network-interface-addresses.md) artykułu.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Utwórz az kart interfejsu sieciowego](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nowe AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|

## <a name="view-network-interface-settings"></a>Wyświetl ustawienia interfejsu sieciowego

Możesz wyświetlić i zmienić większość ustawień interfejsu sieciowego po jego utworzeniu.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *interfejsy sieciowe*. Gdy **interfejsy sieciowe** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **interfejsy sieciowe** bloku, który jest wyświetlany, kliknij przycisk hello interfejsu sieciowego mają tooview lub zmienić ustawienia.
4. Witaj następujące ustawienia są wymienione w hello wyświetlonym bloku hello interfejsu sieciowego, wybrane:
    - **Omówienie:** informacje na temat interfejsu sieciowego hello, takie jak hello adresy IP przypisane tooit, interfejsu sieciowego hello wirtualnego podsieci hello jest przypisany do i interfejsu sieciowego hello maszyny wirtualnej hello jest dołączony zbyt (Jeśli jest dołączony tooone). Witaj poniższej ilustracji przedstawiono hello omówienie ustawienia dla karty sieciowej o nazwie **mywebserver256**: ![omówienie interfejsu sieciowego](./media/virtual-network-network-interface/nic-overview.png) można przenieść sieci interfejsu tooa innej grupie zasobów lub Subskrypcja, klikając (**zmienić**) dalej toohello **grupy zasobów** lub **Nazwa subskrypcji**. Jeśli przenosisz hello interfejsu sieciowego, należy przenieść wszystkie interfejsu sieciowego zasobów toohello powiązanych z nim. Jeśli interfejs sieciowy hello jest dołączona tooa maszyny wirtualnej, na przykład, należy również przenieść hello maszyny wirtualnej i innych zasobów związanych z maszyny wirtualnej. toomove interfejsu sieciowego, przeczytaj hello [przenoszenia zasobów tooa nową grupę zasobów lub subskrypcji](../azure-resource-manager/resource-group-move-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json#use-portal) artykułu. Artykuł Hello zawiera listę wymagań wstępnych oraz sposób toomove zasobów przy użyciu hello portalu Azure, programu PowerShell i hello wiersza polecenia platformy Azure.
    - **Konfiguracje adresów IP:** prywatnych i publicznych adresów IPv4 i IPv6 przypisany tooIP konfiguracje są wyświetlane tutaj. Jeśli adres IPv6 jest przypisany tooan konfiguracji adresu IP, adres hello nie jest wyświetlany. Dowiedz się więcej o konfiguracji adresów IP i jak adresy IP tooadd i Usuń w hello [adresy IP, skonfiguruj dla interfejsu sieci platformy Azure](virtual-network-network-interface-addresses.md) artykułu. Przesyłanie dalej IP i przypisanie podsieci są również skonfigurowane w tej sekcji. więcej informacji na temat tych ustawień, przeczytaj hello toolearn [włączać lub wyłączać przesyłanie dalej IP](#enable-or-disable-ip-forwarding) i [zmienić przypisanie podsieci](#change-subnet-assignment) sekcje w tym artykule.
    - **Serwery DNS:** można określić, który serwer DNS interfejsu sieciowego jest przypisany przez hello serwerów Azure DHCP. Witaj interfejsu sieciowego może dziedziczyć ustawień hello z hello jest przypisany do interfejsu sieciowego hello sieci wirtualnej, lub mieć ustawienia niestandardowe, zastępuje ustawienie hello hello sieci wirtualnej jest przypisany do. toomodify, co jest wyświetlane, pełną hello etapami hello [serwerów DNS zmiany](#change-dns-servers) sekcji tego artykułu.
    - **Grupy zabezpieczeń sieci (NSG):** Wyświetla co grupa NSG jest skojarzona toohello interfejsu sieciowego (jeśli istnieje). Grupa NSG zawiera reguły ruchu przychodzącego i wychodzącego ruchu sieciowego toofilter hello interfejsu sieciowego. Jeśli grupa NSG jest skojarzony toohello interfejsu sieciowego, nazwę hello hello skojarzona grupa NSG jest wyświetlany. toomodify, co jest wyświetlane, pełną hello etapami hello [Zarządzanie skojarzenia grupy zabezpieczeń sieci](virtual-network-manage-nsg-arm-portal.md#manage-associations) artykułu.
    - **Właściwości:** Wyświetla ustawienia dotyczące hello interfejsu sieciowego, łącznie z jej adres MAC (pusty w przypadku hello interfejsu sieciowego nie jest dołączony tooa maszyny wirtualnej), a dla klucza hello istnieje w subskrypcji.
    - **Reguły efektywnym elementem systemu zabezpieczeń:** reguły zabezpieczeń są wyświetlane, jeśli interfejs sieciowy hello jest dołączona tooa uruchomienie maszyny wirtualnej, a grupa NSG jest skojarzona toohello interfejsu sieciowego i podsieci hello jest przypisany do. toolearn więcej informacji o to, co jest wyświetlane, przeczytaj hello [Rozwiązywanie problemów z grup zabezpieczeń sieci](virtual-network-nsg-troubleshoot-portal.md#nsg) artykułu. więcej informacji na temat grup NSG, przeczytaj hello toolearn [sieciowej grupy zabezpieczeń](virtual-networks-nsg.md) artykułu.
    - **Skuteczne tras:** wymienione są trasy, jeśli interfejs sieciowy hello jest dołączona tooa uruchomienie maszyny wirtualnej. trasy Hello są kombinacją trasy domyślne Azure hello, wszelkie trasy zdefiniowane przez użytkownika (przez) i wszelkie trasy protokołu BGP, które mogą wystąpić dla interfejsu sieciowego hello podsieci hello jest przypisany do. toolearn więcej informacji o to, co jest wyświetlane, przeczytaj hello [Rozwiązywanie problemów z tras](virtual-network-routes-troubleshoot-portal.md#view-effective-routes-for-a-network-interface) artykułu. więcej informacji na temat domyślnych Azure i Udr odczytu hello toolearn [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md) artykułu.
    - **Typowe ustawienia usługi Azure Resource Manager:** toolearn więcej informacji na temat typowych ustawień usługi Azure Resource Manager w celu odczytu hello [dziennik aktywności](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#activity-logs), [(IAM) kontroli dostępu](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#access-control), [tagów ](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-network%2ftoc.json#tags), [Blokuje](../azure-resource-manager/resource-group-lock-resources.md?toc=%2fazure%2fvirtual-network%2ftoc.json), i [skryptu automatyzacji](../azure-resource-manager/resource-manager-export-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json#export-the-template-from-resource-group) artykułów.

**Polecenia**

Jeśli adres IPv6 jest przypisany tooa interfejsu sieciowego, hello dane wyjściowe programu PowerShell zwraca hello fakt, że adres hello jest przypisany, ale nie zwraca hello przypisany adres. Podobnie, hello CLI zwraca hello fakt, że adres hello jest przypisane, ale zwraca *null* w danych wyjściowych dla adresu hello.

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Lista kart sieci az](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#list) tooview interfejsów sieciowych w subskrypcji hello; [Pokaż kart sieciowych az](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#show) tooview ustawienia interfejsu sieciowego|
|PowerShell|[Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) tooview interfejsy sieciowe hello subskrypcji lub Wyświetl ustawienia interfejsu sieciowego|

## <a name="change-dns-servers"></a>Zmień serwerów DNS

Serwer DNS Hello jest przypisywany przez hello interfejsu sieci toohello serwera Azure DHCP w ramach systemu operacyjnego hello maszyny wirtualnej. Serwer DNS Hello przypisany jest niezależnie od ustawienia serwera DNS hello interfejsu sieciowego. toolearn więcej informacji na temat ustawień rozpoznawania nazwy dla interfejsu sieciowego, zobacz [rozpoznawanie nazw dla maszyn wirtualnych](virtual-networks-name-resolution-for-vms-and-role-instances.md). Interfejs sieciowy Hello można hello ustawienia były dziedziczone z sieci wirtualnej hello, lub użyć własnych ustawień unikatowy, które przesłaniają ustawienia hello hello sieci wirtualnej.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *interfejsy sieciowe*. Gdy **interfejsy sieciowe** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **interfejsy sieciowe** bloku, który jest wyświetlany, kliknij przycisk hello interfejsu sieciowego mają tooview lub zmienić ustawienia.
4. W bloku hello wybranego interfejsu sieciowego powitania kliknij **serwerów DNS** w obszarze **ustawienia**.
5. Kliknij opcję:
    - **Dziedzicz sieci wirtualnej (ustawienie domyślne)**: Wybierz to tooinherit hello DNS serwera ustawienie zdefiniowany dla interfejsu sieciowego hello sieci wirtualnej hello jest przypisany do. Na poziomie sieci wirtualnej hello niestandardowy serwer DNS lub serwer DNS platformy Azure hello jest zdefiniowany. Witaj serwera DNS platformy Azure można rozwiązać nazwy hostów dla zasobów przydzielonych toohello tej samej sieci wirtualnej. Nazwa FQDN musi być używane tooresolve zasobów przydzielonych toodifferent sieci wirtualnych.
    - **Niestandardowe**: można skonfigurować własne nazwy DNS serwera tooresolve przez wiele sieci wirtualnych. Wprowadź adres IP hello powitania serwera ma toouse jako serwer DNS. Hello adres serwera DNS, które określisz przypisano tylko toothis interfejsu sieciowego i każdego ustawienia DNS interfejsu sieciowego hello sieci wirtualnej hello jest przypisany do zastąpień.
6. Kliknij pozycję **Zapisz**.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Aktualizacja kart sieciowych az](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Zestaw AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="enable-or-disable-ip-forwarding"></a>Włączać lub wyłączać przesyłanie dalej IP

Przesyłanie dalej IP umożliwia hello maszyny wirtualnej karty sieciowej jest dołączony do:
- Odbieranie ruchu sieciowego, które nie są przeznaczone dla jednego z adresów IP hello przypisanych tooany konfiguracji IP hello przypisanych toohello interfejsu sieciowego.
- Wyślij ruch sieciowy za pomocą adresu IP innego źródła niż hello jeden przypisany tooone konfiguracje adresów IP interfejsu sieciowego.

Ustawienie Hello musi być włączone dla każdego interfejsu sieciowego, który jest dołączony toohello maszyny wirtualnej, która odbiera ruch, który hello tooforward potrzeb maszyny wirtualnej. Maszyny wirtualnej może przekazywać ruch, czy ma ona wiele interfejsów sieciowych lub tooit interfejsu jednej sieci. Przesyłanie dalej IP jest ustawienie platformy Azure, maszyny wirtualnej hello musi również uruchomić aplikacji może tooforward hello ruchu, na przykład zapora, Optymalizacja sieci WAN i aplikacje równoważenia obciążenia. Maszyna wirtualna jest uruchomiona aplikacji sieciowych, hello maszyny wirtualnej jest często określonego tooas urządzenie sieci wirtualnej. Można wyświetlić listę wirtualnych urządzeń sieciowych toodeploy gotowy w hello [portalu Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/category/networking?page=1&subcategories=appliances). Przesyłanie dalej IP jest zwykle używany z tras zdefiniowanych przez użytkownika. więcej informacji na temat trasy zdefiniowane przez użytkownika, odczytać hello toolearn [trasy zdefiniowane przez użytkownika](virtual-networks-udr-overview.md) artykułu.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *interfejsy sieciowe*. Gdy **interfejsy sieciowe** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **interfejsy sieciowe** bloku, który jest wyświetlany, kliknij przycisk hello interfejsu sieciowego mają tooenable lub wyłączyć przekazywanie IP.
4. W bloku hello wybranego interfejsu sieciowego powitania kliknij **konfiguracje adresów IP** w hello **ustawienia** sekcji.
5. Kliknij przycisk **włączone** lub **wyłączone** ustawienie hello toochange (ustawienie domyślne).
6. Kliknij pozycję **Zapisz**.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Aktualizacja kart sieciowych az](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Zestaw AzureRmNetworkInterface](/powershell/module/azurerm.network/set-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="change-subnet-assignment"></a>Zmień przypisanie podsieci

Można zmienić podsieci hello, ale nie hello sieci wirtualnej, przypisane do karty sieciowej.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *interfejsy sieciowe*. Gdy **interfejsy sieciowe** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **interfejsy sieciowe** bloku, który jest wyświetlany, kliknij przycisk hello interfejsu sieciowego mają tooview lub zmienić ustawienia.
4. Kliknij przycisk **konfiguracje adresów IP** w obszarze **ustawienia** w bloku hello interfejsu sieciowego hello wybrane. Jeśli prywatne adresy IP dla konfiguracji IP wyświetlane **(statyczny)** toothem dalej, musisz zmienić hello IP address przypisania metody toodynamic, wykonując kroki hello, które należy wykonać. Wszystkich prywatnych adresów IP muszą przypisany za pomocą hello dynamiczne przydzielanie metody toochange hello podsieci przypisania hello interfejsu sieciowego. Jeśli adresy hello są przypisywane przy użyciu metody dynamicznej hello, nadal toostep pięć. Adresy IPv4, są przypisane przy użyciu metody statyczne przypisania hello, należy wykonać następujące kroki toochange hello przypisania metody toodynamic hello:
    - Kliknij pozycję Konfiguracja IP hello ma hello toochange IPv4 adres przypisania metodę z listy hello konfiguracje adresów IP.
    - W hello wyświetlonym bloku do konfiguracji protokołu IP powitania kliknij **dynamiczne** dla hello **przypisania** metody. Nie można przypisać adresów IPv6 za pomocą metody statyczne przypisania hello.
    - Kliknij pozycję **Zapisz**.
5. Wybierz podsieć hello ma tooconnect hello sieci interfejsu toofrom hello **podsieci** listy rozwijanej.
6. Kliknij pozycję **Zapisz**. Nowe dynamiczne adresy są przypisywane z zakresu adresów podsieci hello hello nowej podsieci. Po przypisaniu hello interfejsu tooa nowej podsieci, można przypisać statycznego adresu IPv4 z hello nowy zakres adresów podsieci po wybraniu. więcej informacji na temat Dodawanie, zmienianie i usuwanie adresów IP dla karty sieciowej, przeczytaj hello toolearn [adresów IP zarządzanie](virtual-network-network-interface-addresses.md) artykułu.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Aktualizacja konfiguracji adresu ip karty sieciowej sieci az](/cli/azure/network/nic/ip-config?toc=%2fazure%2fvirtual-network%2ftoc.json#update)|
|PowerShell|[Zestaw AzureRmNetworkInterfaceIpConfig](/powershell/module/azurerm.network/set-azurermnetworkinterfaceipconfig?toc=%2fazure%2fvirtual-network%2ftoc.json)|


## <a name="delete-a-network-interface"></a>Usunąć interfejsu sieciowego

Można usunąć interfejsu sieciowego, dopóki nie jest dołączony tooa maszyny wirtualnej. Jest dołączony tooa maszyny wirtualnej, należy stan maszyny wirtualnej w hello zatrzymane (cofnięciu przydziału) hello miejscu pierwszej, następnie odłączyć hello interfejsu sieciowego z maszyny wirtualnej hello, aby można było usunąć hello interfejsu sieciowego. toodetach interfejsu sieciowego z maszyny wirtualnej, pełną hello etapami hello [odłączyć interfejsu sieciowego z maszyny wirtualnej](virtual-network-network-interface-vm.md#vm-remove-nic) sekcji hello [Dodawanie lub usuwanie interfejsów sieciowych](virtual-network-network-interface-vm.md) artykułu. Trwa usuwanie maszyny wirtualnej Odłącza wszystkie tooit dołączone interfejsów sieci, ale nie powoduje usunięcia hello interfejsów sieciowych.

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) przy użyciu konta, czyli przypisane (co najmniej) uprawnienia roli współautora sieci powitania dla Twojej subskrypcji. Witaj odczytu [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor) więcej informacji na temat przypisywania ról i uprawnień tooaccounts toolearn artykułu.
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *interfejsy sieciowe*. Gdy **interfejsy sieciowe** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. Kliknij prawym przyciskiem myszy interfejs sieciowy hello toodelete i kliknij **usunąć**.
4. Kliknij przycisk **tak** tooconfirm usunięcie hello interfejsu sieciowego.

Po usunięciu interfejsu sieciowego, wszystkie MAC lub adresy IP przypisane tooit są wydawane.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Usuń kartę sieciową sieci az](/cli/azure/network/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#delete)|
|PowerShell|[Usuń AzureRmNetworkInterface](/powershell/module/azurerm.network/remove-azurermnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="next-steps"></a>Następne kroki
toocreate adresy maszynę wirtualną z wielu interfejsów sieciowych lub adres IP, przeczytaj hello następujące artykuły:

**Polecenia**

|Zadanie|Narzędzie|
|---|---|
|Tworzenie maszyny wirtualnej z wieloma kartami sieciowymi|[Interfejs wiersza polecenia](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [środowiska PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Tworzenie jednej maszyny Wirtualnej karty Sieciowej z wielu adresów IPv4|[Interfejs wiersza polecenia](virtual-network-multiple-ip-addresses-cli.md), [środowiska PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Tworzenie jednej maszyny Wirtualnej karty Sieciowej za pomocą prywatnego adresu IPv6 (za równoważenia obciążenia Azure)|[Interfejs wiersza polecenia](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [szablonu usługi Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
