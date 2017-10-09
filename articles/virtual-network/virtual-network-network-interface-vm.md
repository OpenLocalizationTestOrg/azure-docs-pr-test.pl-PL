---
title: "Usuń tooor interfejsów sieciowych aaaAdd z maszyn wirtualnych platformy Azure | Dokumentacja firmy Microsoft"
description: "Dowiedz się, jak usunąć tooor interfejsów sieciowych tooadd interfejsów sieciowych z maszyn wirtualnych."
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
ms.date: 07/25/2017
ms.author: jdial
ms.openlocfilehash: eb564b94932b9242f29bc23234b08b0c76ac23a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="add-network-interfaces-tooor-remove-from-virtual-machines"></a>Dodaj interfejsy sieciowe tooor usunąć z maszyny wirtualne

Dowiedz się, jak tooadd istniejącej sieci interfejsu podczas tworzenia maszyny Wirtualnej lub dodawanie lub usuwanie interfejsów sieciowych z istniejącej maszyny Wirtualnej w hello zatrzymane (cofnięciu przydziału) stanu. Interfejs sieciowy umożliwia toocommunicate Azure maszyny wirtualnej (VM) z Internetem, Azure i lokalnymi zasobami. Maszyna wirtualna może mieć jeden lub więcej interfejsów sieciowych. 

Tooadd, należy zmienić lub usunąć adresy IP dla karty sieciowej, przeczytaj hello [zarządzania adresami IP interfejsu sieci](virtual-network-network-interface-addresses.md) artykułu. Jeśli potrzebujesz toocreate, zmienianie lub usuwanie interfejsów sieciowych, przeczytaj hello [Zarządzanie interfejsów sieciowych](virtual-network-network-interface.md) artykułu.

## <a name="before"></a>Przed rozpoczęciem

Wykonaj następujące zadania, przed wykonaniem dowolnej kroków w żadnej sekcji tego artykułu hello:

- Dowiedz się więcej o ile interfejsów sieciowych rozmiar każdego z systemami Linux i maszyny Wirtualnej systemu Windows obsługuje przeglądając hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykuły rozmiary maszyny Wirtualnej.
- Zaloguj się za toohello Azure [portal](https://portal.azure.com), Azure interfejsu wiersza polecenia (CLI) lub Azure PowerShell przy użyciu konta platformy Azure. Jeśli nie masz jeszcze konta platformy Azure, należy zarejestrować się w celu [bezpłatnego konta wersji próbnej](https://azure.microsoft.com/free).
- Jeśli przy użyciu programu PowerShell poleceń toocomplete zadania w tym artykule [Instalowanie i konfigurowanie programu Azure PowerShell](/powershell/azureps-cmdlets-docs?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello apletów poleceń programu hello Azure PowerShell. tooget Pomoc dla poleceń programu PowerShell, wraz z przykładami, wpisz `get-help <command> -full`.
- Jeśli przy użyciu interfejsu wiersza polecenia platformy Azure (CLI) polecenia toocomplete zadania w tym artykule [Instalowanie i Konfigurowanie interfejsu wiersza polecenia Azure hello](/cli/azure/install-azure-cli?toc=%2fazure%2fvirtual-network%2ftoc.json). Upewnij się, że masz najnowszą wersję hello hello Azure CLI zainstalowane. tooget pomocy dla poleceń interfejsu wiersza polecenia, wpisz `az <command> --help`. Zamiast instalowania hello interfejsu wiersza polecenia i jego wymagania wstępne można użyć hello powłoki chmury Azure. Hello powłoki chmury Azure jest bezpłatna powłoki Bash, który można uruchomić bezpośrednio z poziomu hello portalu Azure. Ma ona hello Azure CLI wstępnie zainstalowane i skonfigurowane toouse z Twoim kontem. toouse hello powłoki chmury kliknij hello powłoki chmury **> _** u góry hello hello [portal](https://portal.azure.com).

## <a name="about"></a>O interfejsami sieciowymi i maszyny wirtualne

Możesz dodać (Dołącz) istniejącego tooa interfejsu sieciowego maszyny Wirtualnej po utworzeniu hello maszyny Wirtualnej, pod warunkiem hello interfejsu sieciowego nie jest obecnie dołączony tooanother maszyny Wirtualnej. Interfejs sieciowy, aby dodać lub usunąć (odłączyć) sieci interfejsu toofrom istniejącej maszyny Wirtualnej, pod warunkiem hello maszyny Wirtualnej w hello zatrzymaniu stanu (cofnięciu przydziału). Jeśli tworzysz Maszynę wirtualną przy użyciu hello portalu Azure, portalu hello tworzy interfejs sieciowy z ustawieniami domyślnymi. Hello portal nie umożliwiają:

- Określ istniejące tooadd interfejsu sieciowego podczas tworzenia hello maszyny Wirtualnej
- Tworzenie maszyny wirtualnej z wieloma interfejsami sieciowymi
- Określ nazwę dla interfejsu sieciowego hello (hello portal tworzy interfejs sieciowy hello z domyślną nazwą)

Wszystkie atrybuty poprzedniej hello, które nie mogą używać portalu hello dla można użyć programu Azure PowerShell lub toocreate CLI hello karty sieciowej lub maszyny Wirtualnej. Przed wykonaniem zadań hello w hello następujące sekcje zawierają informacje, należy wziąć pod uwagę następujące hello ograniczenia i zachowania:

- Co najmniej dwa interfejsy sieci obsługuje wszystkich rozmiarów maszyn wirtualnych, ale niektóre rozmiarów maszyn wirtualnych obsługuje więcej niż dwa interfejsy sieciowe. W hello poza niektórych maszyn wirtualnych rozmiary obsługiwane tylko jeden interfejs sieciowy. toolearn obsługuje każdego rozmiaru maszyny Wirtualnej, jak wiele interfejsów sieciowych odczytu hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykuły rozmiary maszyny Wirtualnej. 
- W ciągu ostatnich hello interfejsy sieciowe mogło zostać tylko dodano tooVMs, obsługuje wiele interfejsów sieciowych, który został utworzony za pomocą co najmniej dwa interfejsy sieciowe. Nie można dodać tooa interfejsu sieciowego maszyny Wirtualnej, który został utworzony z jeden interfejs sieciowy, nawet jeśli hello rozmiar maszyny Wirtualnej obsługuje wiele interfejsów sieciowych. Z drugiej strony interfejsy sieciowe można tylko usunąć z maszyny Wirtualnej z co najmniej trzech interfejsów sieciowych, ponieważ maszyny wirtualne utworzone z co najmniej dwa interfejsy sieci zawsze toohave co najmniej dwa interfejsy sieciowe. Żadna z tych warunków ograniczających już stosowane. Można teraz utworzyć Maszynę wirtualną z dowolnej liczby interfejsów sieciowych (w górę liczbę toohello obsługiwaną przez hello rozmiar maszyny Wirtualnej) i dodawać i usuwać dowolna liczba interfejsów sieciowych (ze stanu maszyn wirtualnych w hello zatrzymane (cofnięciu przydziału)), jak długo hello wirtualna zawsze ma co najmniej jeden interfejs sieciowy.
- Domyślnie program hello pierwszy interfejsu sieciowego na maszynie wirtualnej jest zdefiniowany jako hello *głównej* interfejsu sieciowego. Wszystkie interfejsy sieciowe inne hello maszyny Wirtualnej są *dodatkowej* interfejsów sieciowych.
- Podstawowych interfejsów sieciowych przypisanych przez serwery Azure DHCP hello brama domyślna, ale nie są dodatkowych interfejsów sieciowych. Ponieważ dodatkowych interfejsów sieciowych nie są przypisane bramę domyślną, nie mogli komunikować się z zasobami spoza ich podsieci domyślnie. tooenable dodatkowych interfejsów sieciowych w toocommunicate maszyny Wirtualnej systemu Windows, z zasobami spoza ich podsieci, Dodaj system operacyjny toohello tras za pomocą hello `route add` polecenia z wiersza polecenia systemu Windows. Dla maszyn wirtualnych systemu Linux ponieważ hello domyślne zachowanie używa słabe hosta routingu, zaleca się ograniczanie ruchu dla interfejsów sieciowych dodatkowej tooa pojedynczej podsieci. Jeśli łączność poza hello podsieci jest wymagana dla dodatkowych interfejsów sieciowych, włącz na podstawie zasad routingu tooensure ten ruch przychodzący i wychodzący ruch używa hello sam sieci interfejsu.
- Domyślnie ruch wychodzący z maszyny Wirtualnej jest wysłane z adresu IP hello powitalne przypisane toohello podstawową konfigurację protokołu IP hello podstawowy interfejs sieciowy. Możesz kontrolować, który adres IP jest używana dla ruchu wychodzącego w ramach systemu operacyjnego hello maszyny Wirtualnej, ale domyślnie jest za pośrednictwem hello podstawowy interfejs sieciowy.
- W hello poza wszystkich maszyn wirtualnych w ramach hello tego samego zestawu dostępności były wymagane toohave, które interfejsy sieciowe jednego lub wielu. Maszyny wirtualne z dowolnej liczby sieci, z którą interfejsy teraz może istnieć w hello tego samego zestawu dostępności, numer toohello obsługiwane przez hello rozmiar maszyny Wirtualnej. Można dodawać tylko ustawić po utworzeniu jednak dostępności tooan maszyny Wirtualnej. więcej informacji na temat zestawów dostępności, przeczytaj hello toolearn [Zarządzanie hello dostępność maszyn wirtualnych na platformie Azure](../virtual-machines/windows/manage-availability.md?toc=%2fazure%2fvirtual-network%2ftoc.json#configure-multiple-virtual-machines-in-an-availability-set-for-redundancy) artykułu.
- Gdy interfejsy sieciowe w hello tej samej maszyny Wirtualnej może być połączone toodifferent podsieci w sieci wirtualnej, wszystkie interfejsy sieciowe hello muszą być połączone toohello tej samej sieci wirtualnej.
- Możesz dodać dowolnego adresu IP dla żadnej konfiguracji adresu IP z żadnej puli zaplecza modułu równoważenia obciążenia Azure tooan interfejsu sieci podstawowej lub dodatkowej. W ciągu ostatnich hello tylko hello podstawowego adresu IP hello podstawowy interfejs sieciowy może zostać dodany tooa puli zaplecza. więcej informacji na temat adresów IP i konfiguracje, przeczytaj hello toolearn [Dodaj, Zmień lub Usuń adresy IP](virtual-network-network-interface-addresses.md) artykułu.
- Usuwanie maszyny Wirtualnej nie powoduje usunięcia hello interfejsów sieciowych, które są dołączone tooit. Po usunięciu maszyny Wirtualnej hello interfejsy sieciowe są odłączone od hello maszyny Wirtualnej. Można dodać toodifferent interfejsów sieciowych hello maszyn wirtualnych, lub usuń je.
- Jeśli interfejs sieciowy ma prywatnej tooit przypisany adres IPv6, możesz dołączyć go tooa maszyny Wirtualnej podczas tworzenia hello maszyny Wirtualnej. Nie można dołączyć karty sieciowej z przypisanego adresu IPv6 tooa maszyny Wirtualnej, po utworzeniu hello maszyny Wirtualnej. Jeśli podczas tworzenia maszyny wirtualnej można dołączyć karty sieciowej z przypisany prywatny adres IPv6, można dołączać sieci interfejsu toohello maszyny wirtualnej, niezależnie od tego, jak wiele interfejsów sieciowych obsługuje hello rozmiar maszyny Wirtualnej. Zobacz [sieci adresów IP interfejsu](virtual-network-network-interface-addresses.md) toolearn więcej informacji o przypisaniu IP adresów toonetwork interfejsów.

## <a name="vm-create"></a>Dodaj istniejący tooa interfejsy sieciowe nowej maszyny Wirtualnej

Podczas tworzenia maszyny Wirtualnej za pośrednictwem portalu hello hello portal tworzy interfejs sieciowy z ustawieniami domyślnymi i dołącza go toohello maszyny Wirtualnej dla Ciebie. Nie można dodać istniejącego tooa interfejsy sieciowe nowej maszyny Wirtualnej, lub utworzyć Maszynę wirtualną z wieloma interfejsami sieciowymi przy użyciu hello portalu Azure. Można wykonać obie czynności przy użyciu hello interfejsu wiersza polecenia lub środowiska PowerShell. Można dodać jako wiele sieci jako hello rozmiar maszyny Wirtualnej, które tworzysz obsługuje interfejsy tooa maszyny Wirtualnej. toolearn więcej informacji na temat liczby sieci interfejsy każdego obsługuje rozmiar maszyny Wirtualnej, przeczytaj hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykuły rozmiary maszyny Wirtualnej. Interfejsy sieciowe Hello dodać tooa maszyny Wirtualnej nie może być aktualnie tooanother dołączona maszyna wirtualna. więcej informacji na temat tworzenia interfejsów sieciowych, przeczytaj hello toolearn [Zarządzanie interfejsów sieciowych](virtual-network-network-interface.md#create-a-network-interface) artykułu.

> [!WARNING]
> Jeśli interfejs sieciowy ma prywatnego adresu IPv6 przypisany tooit, maszynę wirtualną toohello interfejs sieci hello można tylko dodać podczas tworzenia maszyny wirtualnej hello. Nie można dołączyć więcej niż jednej maszyny wirtualnej toohello interfejs sieci podczas tworzenia maszyny wirtualnej hello, lub po hello utworzeniu maszyny wirtualnej, tak długo, jak adres IPv6 jest przypisany maszyny wirtualnej tooa tooa sieci interfejsu. Zobacz [sieci adresów IP interfejsu](virtual-network-network-interface-addresses.md) toolearn więcej informacji o przypisaniu IP adresów toonetwork interfejsów.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Tworzenie maszyny wirtualnej az](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#create)|
|PowerShell|[Nowe AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-add-nic"></a>Dodaj istniejące tooan interfejsu sieciowego istniejącej maszyny Wirtualnej

Można dodać jako wiele sieci tooa interfejsy maszyny Wirtualnej jako hello rozmiar maszyny Wirtualnej w przypadku dodawania toosupports interfejsów sieciowych. toolearn obsługuje każdego rozmiaru maszyny Wirtualnej, jak wiele interfejsów sieciowych odczytu hello [Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) lub [Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-network%2ftoc.json) artykuły rozmiary maszyny Wirtualnej. Hello ma tooadd toomust interfejsu sieciowego obsługuje hello liczba interfejsów sieciowych mają tooadd i muszą być pisane hello zatrzymana maszyny Wirtualnej (cofnięciu przydziału) stanu. Interfejsy sieciowe Hello ma tooadd aktualnie nie może być dołączone tooanother maszyny Wirtualnej. Nie można dodać istniejącej maszyny Wirtualnej przy użyciu portalu Azure hello tooan interfejsów sieciowych. Interfejsy sieciowe tooadd tooan istniejącej maszyny Wirtualnej, należy użyć hello interfejsu wiersza polecenia lub środowiska PowerShell. 

> [!WARNING]
> Jeśli interfejs sieciowy ma prywatnego adresu IPv6 przypisany tooit, nie można dodać tooan istniejącej maszyny wirtualnej. Można tylko dodać karty sieciowej z przypisaną prywatnej IPv6 adres tooa maszyny wirtualnej, podczas tworzenia maszyny wirtualnej. Zobacz [sieci adresów IP interfejsu](virtual-network-network-interface-addresses.md) toolearn więcej informacji o przypisaniu IP adresów toonetwork interfejsów.

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Dodaj kartę sieciową maszyny wirtualnej az](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#add) (odwołanie) lub [szczegółowe kroki](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-a-vm)|
|PowerShell|[Dodaj AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (odwołanie) lub [szczegółowe kroki](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#add-a-nic-to-an-existing-vm)|

## <a name="vm-view-nic"></a>Wyświetlanie interfejsów sieciowych do maszyny Wirtualnej

Można wyświetlić hello toolearn maszyny Wirtualnej tooa obecnie podłączonych interfejsów sieci o konfiguracji każdego interfejsu sieciowego i przypisywane adresy IP hello tooeach interfejsu sieciowego. 

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) z kontem, które jest przypisaną rolę właściciela, współautora lub współautora sieci powitania dla Twojej subskrypcji. Zobacz toolearn więcej informacji o przypisywaniu tooaccounts ról [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *maszyn wirtualnych*. Gdy **maszyn wirtualnych** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **maszyn wirtualnych** bloku, który jest wyświetlany, kliknij nazwę hello hello ma tooview interfejsów sieciowych do maszyny Wirtualnej.
4. W hello **ustawienia** sekcji hello maszyny wirtualnej wyświetlonym bloku dla hello maszyna wirtualna została wybrana, kliknij przycisk **interfejsy sieciowe**. toolearn o ustawienia interfejsu sieciowego i w jaki sposób toochange ich, przeczytaj hello [Zarządzanie interfejsów sieciowych](virtual-network-network-interface.md) artykułu. toolearn dotyczące dodawania, zmieniania lub usuwania adresy IP przypisane tooa interfejsu sieciowego, zobacz [adresów IP zarządzanie](virtual-network-network-interface-addresses.md).

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Pokaż wirtualna az](/cli/azure/vm?toc=%2fazure%2fvirtual-network%2ftoc.json#show)|
|PowerShell|[Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm?toc=%2fazure%2fvirtual-network%2ftoc.json)|

## <a name="vm-remove-nic"></a>Usunąć interfejsu sieciowego z maszyny Wirtualnej

Witaj maszyna wirtualna ma tooremove (lub odłączyć) karty sieciowej z musi być w hello zatrzymana (cofnięciu przydziału) i musi mieć co najmniej dwa interfejsy podłączonych tooit. Możesz usunąć wszelkie interfejsu sieciowego, ale hello wirtualna zawsze musi mieć co najmniej jeden tooit interfejsu sieciowego. Jeśli usuniesz podstawowy interfejs sieciowy Azure przypisuje interfejsu sieciowego toohello atrybut podstawowy hello, która została toohello dołączona maszyna wirtualna hello najdłuższym. 

1. Zaloguj się za toohello [portalu Azure](https://portal.azure.com) z kontem, które jest przypisaną rolę właściciela, współautora lub współautora sieci powitania dla Twojej subskrypcji. Zobacz toolearn więcej informacji o przypisywaniu tooaccounts ról [wbudowanych ról dla kontroli dostępu opartej na rolach na platformie Azure](../active-directory/role-based-access-built-in-roles.md?toc=%2fazure%2fvirtual-network%2ftoc.json#network-contributor).
2. W polu hello, które zawiera tekst hello *wyszukiwania zasobów* u góry hello hello portalu Azure, wpisz *maszyn wirtualnych*. Gdy **maszyn wirtualnych** pojawia się w wynikach wyszukiwania hello, kliknij ją.
3. W hello **maszyn wirtualnych** bloku, który jest wyświetlany, kliknij nazwę hello hello ma tooremove karty sieciowej dla maszyny Wirtualnej.
4. W hello **ustawienia** sekcji hello maszyny wirtualnej wyświetlonym bloku dla hello maszyna wirtualna została wybrana, kliknij przycisk **interfejsy sieciowe**. toolearn o ustawienia interfejsu sieciowego i w jaki sposób toochange ich, przeczytaj hello [Zarządzanie interfejsów sieciowych](virtual-network-network-interface.md) artykułu. toolearn dotyczące dodawania, zmieniania lub usuwania adresy IP przypisane tooa interfejsu sieciowego, zobacz [adresów IP zarządzanie](virtual-network-network-interface-addresses.md).
5. W bloku interfejsów sieci hello, który pojawia się, kliknij przycisk hello **...**  toohello rogu hello interfejsu sieciowego, które mają toodetach.
6. Kliknij przycisk **odłączyć**. Jeśli istnieje tylko jedna maszyna wirtualna toohello interfejsu sieciowego, hello **Detach** opcja jest niedostępna. Kliknij przycisk **tak** w wyświetlonym oknie potwierdzenia hello.

**Polecenia**

|Narzędzie|Polecenie|
|---|---|
|Interfejs wiersza polecenia|[Usuń kartę sieciową maszyny wirtualnej az](/cli/azure/vm/nic?toc=%2fazure%2fvirtual-network%2ftoc.json#remove) (odwołanie) lub [szczegółowe kroki](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-a-vm)|
|PowerShell|[Usuń AzureRMVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface?toc=%2fazure%2fvirtual-network%2ftoc.json) (odwołanie) lub [szczegółowe kroki](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json#remove-a-nic-from-an-existing-vm)|

## <a name="next-steps"></a>Następne kroki
toocreate Maszynę wirtualną z wieloma interfejsami sieciowymi lub adresy IP, przeczytaj hello następujące artykuły:

**Polecenia**

|Zadanie|Narzędzie|
|---|---|
|Tworzenie maszyny wirtualnej z wieloma kartami sieciowymi|[Interfejs wiersza polecenia](../virtual-machines/linux/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [środowiska PowerShell](../virtual-machines/windows/multiple-nics.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
|Tworzenie jednej maszyny Wirtualnej karty Sieciowej z wielu adresów IPv4|[Interfejs wiersza polecenia](virtual-network-multiple-ip-addresses-cli.md), [środowiska PowerShell](virtual-network-multiple-ip-addresses-powershell.md)|
|Tworzenie jednej maszyny Wirtualnej karty Sieciowej za pomocą prywatnego adresu IPv6 (za równoważenia obciążenia Azure)|[Interfejs wiersza polecenia](../load-balancer/load-balancer-ipv6-internet-cli.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [PowerShell](../load-balancer/load-balancer-ipv6-internet-ps.md?toc=%2fazure%2fvirtual-network%2ftoc.json), [szablonu usługi Azure Resource Manager](../load-balancer/load-balancer-ipv6-internet-template.md?toc=%2fazure%2fvirtual-network%2ftoc.json)|
