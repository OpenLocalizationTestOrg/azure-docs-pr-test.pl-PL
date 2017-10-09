---
title: "aaaWindows maszyn wirtualnych — omówienie | Dokumentacja firmy Microsoft"
description: "Dowiedz się więcej na temat tworzenia maszyn wirtualnych z systemem Windows na platformie Azure oraz zarządzania nimi."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Omówienie maszyn wirtualnych z systemem Windows na platformie Azure

Usługa Azure Virtual Machines (VM) to jeden z wielu [skalowalnych zasobów obliczeniowych dostępnych na żądanie](../../app-service-web/choose-web-site-cloud-service-vm.md), które są oferowane na platformie Azure. Zwykle możesz wybrać Maszynę wirtualną, gdy potrzebujesz większej kontroli nad środowiskiem obliczeniowych hello niż hello zaoferowania inne opcje. Ten artykuł zawiera informacje o kwestiach, jakie należy rozważyć przed przystąpieniem do tworzenia maszyny wirtualnej. Opisano w nim także tworzenie maszyny wirtualnej i zarządzanie nią.

Zapewnia maszyny Wirtualnej Azure hello swobodne korzystanie z wirtualizacji bez konieczności toobuy i obsługa sprzętu fizycznego hello który uruchamia go. Jednak nadal potrzebujesz hello toomaintain maszyny Wirtualnej, wykonując zadania, takie jak konfigurowanie, poprawki i instalowanie oprogramowania hello na nim.

Z maszyn wirtualnych na platformie Azure można korzystać na różne sposoby. Przykłady to:

* **Projektowania i testowania** — maszyny wirtualne Azure oferują szybki i łatwy sposób toocreate komputera o określonej konfiguracji wymaganych toocode i testowania aplikacji.
* **Aplikacje w chmurze hello** — ponieważ żądanie aplikacji mogą się zmieniać, może uniemożliwić toorun punktu widzenia ekonomii prawidłowym go na maszynie Wirtualnej na platformie Azure. Jeśli zajdzie potrzeba użycia dodatkowych maszyn wirtualnych, wystarczy je opłacić. Gdy dodatkowe maszyny staną się zbędne, można je wyłączyć.
* **Rozszerzony datacenter** — maszyn wirtualnych w sieci wirtualnej platformy Azure mogą być łatwo sieci połączonych tooyour organizacji.

Hello liczbę maszyn wirtualnych, które korzysta z aplikacji można skalować i limit toowhatever jest wymagane toomeet potrzeb.

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>Co należy toothink o przed utworzeniem maszyny Wirtualnej?
Podczas tworzenia infrastruktury aplikacji na platformie Azure należy zawsze wziąć pod uwagę wiele różnych [zagadnień projektowych](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Te aspekty maszyny wirtualnej są ważne toothink o przed rozpoczęciem:

* nazwy Hello zasobów aplikacji
* Witaj lokalizacji przechowywania hello zasobów
* rozmiar Hello hello maszyny Wirtualnej
* Maksymalna liczba maszyn wirtualnych, które można utworzyć Hello
* Uruchamia system operacyjny Hello hello maszyny Wirtualnej
* Konfiguracja Hello hello maszyny Wirtualnej po jego uruchomieniu
* Witaj hello, że maszyna wirtualna musi powiązanych zasobów

### <a name="naming"></a>Nazewnictwo
Maszyna wirtualna ma [nazwa](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooit przypisanej i nazwa komputera jest skonfigurowany jako część systemu operacyjnego hello. Nazwa Hello maszyny wirtualnej może być zapasowej too15 znaków.

Jeśli używasz dysku systemu operacyjnego hello Azure toocreate, hello nazwy komputera i nazwy maszyny wirtualnej hello są hello takie same. Jeśli użytkownik [przekazywanie i użycie własnego obrazu](upload-generalized-managed.md) który zawiera wcześniej skonfigurowany system operacyjny i przy jego użyciu toocreate maszynę wirtualną, hello nazwy mogą być różne. Firma Microsoft zaleca podczas przekazywania pliku obrazu, wykonanie hello nazwy komputera w systemie operacyjnym hello i nazwy maszyny wirtualnej hello hello takie same.

### <a name="locations"></a>Lokalizacje
Wszystkie zasoby utworzona na platformie Azure są rozproszone na wielu [regionów geograficznych](https://azure.microsoft.com/regions/) wokół hello world. Zwykle jest nazywany hello region **lokalizacji** podczas tworzenia maszyny Wirtualnej. Dla maszyny Wirtualnej hello Lokalizacja określa, gdzie hello wirtualne dyski twarde są przechowywane.

W poniższej tabeli zamieszczono niektóre sposoby hello, które można uzyskać listę dostępnych lokalizacji.

| Metoda | Opis |
| --- | --- |
| Azure Portal |Wybierz lokalizację z listy hello podczas tworzenia maszyny Wirtualnej. |
| Azure PowerShell |Użyj hello [Get-AzureRmLocation](/powershell/module/azurerm.resources/get-azurermlocation) polecenia. |
| Interfejs API REST |Użyj hello [listy lokalizacje](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations) operacji. |

### <a name="vm-size"></a>Rozmiar maszyny wirtualnej
Witaj [rozmiar](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) dostępnych hello maszyny Wirtualnej, którego używasz zależy od obciążenia hello, które mają toorun. rozmiar Hello wybierzesz określa czynników, takich jak zdolność zasilania, pamięci i miejsca do przetwarzania. System Azure oferuje szeroką gamę toosupport rozmiary wielu różnych zastosowań.

Azure opłat [cenę godzinową](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) na podstawie rozmiaru i systemu operacyjnego hello maszyny Wirtualnej. Za kolejne rozpoczęte godziny Azure opłat tylko w przypadku minut hello używane. Magazyn jest wyceniany oddzielnie; związane z nim opłaty są także pobierane osobno.

### <a name="vm-limits"></a>Limity maszyn wirtualnych
Subskrypcja ma domyślne [limity przydziału](../../azure-subscription-service-limits.md) w miejscu, które mogą wpłynąć na powitania wdrażania wielu maszyn wirtualnych dla projektu. bieżący limit Hello na podstawie subskrypcji na to 20 maszyn wirtualnych na region. Limity można zwiększyć, wypełniając bilet pomocy technicznej.

### <a name="operating-system-disks-and-images"></a>Dyski i obrazy z systemem operacyjnym
Użyj maszyn wirtualnych [wirtualnych dysków twardych (VHD)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore ich systemu operacyjnego (OS) i danych. Wirtualne dyski twarde są również używane dla obrazów hello, które można wybrać tooinstall systemu operacyjnego. 

Platforma Azure udostępnia wiele [obrazów marketplace](https://azure.microsoft.com/marketplace/virtual-machines/) toouse z różnych wersji i typów systemów operacyjnych Windows Server. Obrazy z Marketplace są oznaczone nazwą wydawcy i oferty, jednostką SKU i wersją (zwykle najnowszą). 

W poniższej tabeli zamieszczono niektóre sposób, w którym można znaleźć hello informacji o obrazie.

| Metoda | Opis |
| --- | --- |
| Azure Portal |wartości Hello są automatycznie określane automatycznie po wybraniu toouse obrazu. |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher) -Location "lokalizacja"<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer) -Location "lokalizacja" -Publisher "nazwa_wydawcy"<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku) -Location "lokalizacja" -Publisher "nazwa_wydawcy" -Offer "nazwa_oferty" |
| Interfejsy API REST |[Wyświetl listę wydawców obrazów](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<BR>[Wyświetl listę ofert obrazów](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<BR>[Wyświetl listę jednostek SKU obrazów](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) |

Możesz wybrać zbyt[przekazywanie i użycie własnego obrazu](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account) i po wykonaniu czynności nie są używane hello nazwę wydawcy, oferty i jednostki sku.

### <a name="extensions"></a>Rozszerzenia
[Rozszerzenia](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) maszyn wirtualnych udostępniają dodatkowe funkcje, z których można korzystać po wdrożeniu i do automatyzacji zadań.

Typowe zadania można realizować przy użyciu różnych rozszerzeń:

* **Uruchamianie niestandardowych skryptów** — Witaj [niestandardowe rozszerzenie skryptu](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) służy do konfigurowania obciążeń na powitania maszyny Wirtualnej, uruchamiając skrypt po hello maszyny Wirtualnej zostanie zainicjowana.
* **Wdrażanie i zarządzanie konfiguracjami** — Witaj [rozszerzenia konfiguracji żądanego stanu środowiska PowerShell (DSC)](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pomaga skonfigurować DSC na toomanage maszyny Wirtualnej konfiguracji i środowiskach.
* **Zbieranie danych diagnostycznych** — Witaj [rozszerzenia diagnostyki Azure](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) pomaga skonfigurować dane diagnostyczne toocollect wirtualna hello, które mogą być używane toomonitor hello kondycji aplikacji.

### <a name="related-resources"></a>Powiązane zasoby
Hello zasoby w tej tabeli są używane przez hello maszyny Wirtualnej i tooexist potrzebne lub można utworzyć po utworzeniu hello maszyny Wirtualnej.

| Zasób | Wymagany | Opis |
| --- | --- | --- |
| [Grupa zasobów](../../azure-resource-manager/resource-group-overview.md) |Tak |Witaj maszyny Wirtualnej muszą być zawarte w grupie zasobów. |
| [Konto magazynu](../../storage/common/storage-create-storage-account.md) |Tak |Witaj maszyny Wirtualnej musi toostore konta magazynu hello jej wirtualne dyski twarde. |
| [Sieć wirtualna](../../virtual-network/virtual-networks-overview.md) |Tak |Witaj maszyny Wirtualnej musi być członkiem sieci wirtualnej. |
| [Publiczny adres IP](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |Nie |Hello maszyna wirtualna może mieć publicznych tooremotely tooit przypisany adres IP, na do niego dostęp. |
| [Interfejs sieciowy](../../virtual-network/virtual-network-network-interface.md) |Tak |Witaj maszyny Wirtualnej musi toocommunicate interfejsu sieciowego hello w hello sieci. |
| [Dyski danych](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |Nie |Witaj maszyna wirtualna może zawierać możliwości magazynu tooexpand dysków danych. |

## <a name="how-do-i-create-my-first-vm"></a>Jak utworzyć maszynę wirtualną?
Można skorzystać z jednej z kilku opcji utworzenia maszyny wirtualnej. Wybór Hello, wprowadzone zależy od środowiska hello, które znajdują się w. 

Ta tabela zawiera informacje tooget Rozpoczęto tworzenie maszyny Wirtualnej.

| Metoda | Artykuł |
| --- | --- |
| Azure Portal |[Utwórz maszynę wirtualną z systemem Windows przy użyciu portalu hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Szablony |[Tworzenie maszyny wirtualnej z systemem Windows przy użyciu szablonu usługi Resource Manager](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[Tworzenie maszyny wirtualnej z systemem Windows przy użyciu programu PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Zestawy SDK klienta |[Wdrażanie zasobów Azure przy użyciu języka C#](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Interfejsy API REST |[Tworzenie lub aktualizowanie maszyny wirtualnej](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) |

Nikt tego nie lubi, ale czasem coś może pójść nie tak. Jeśli ta sytuacja występuje tooyou, przeglądać informacje hello w [problemy z wdrażaniem Rozwiązywanie problemów z Menedżera zasobów z tworzenia maszyny wirtualnej systemu Windows na platformie Azure](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>Jak zarządzać hello maszyny Wirtualnej, który został utworzony?
Maszynami wirtualnymi można zarządzać w portalu w przeglądarce internetowej, a także przy użyciu narzędzi wiersza polecenia z obsługą skryptów oraz bezpośrednio za pomocą interfejsów API. Niektórych typowych zadań zarządzania, które można wykonać są pobieranie informacji na temat maszyny Wirtualnej, logowanie tooa maszyn wirtualnych, zarządzania, dostępność i tworzenia kopii zapasowych.

### <a name="get-information-about-a-vm"></a>Uzyskiwanie informacji o maszynie wirtualnej
Ta tabela zawiera niektóre sposoby hello, który można pobrać informacji o maszynie Wirtualnej.

| Metoda | Opis |
| --- | --- |
| Azure Portal |W menu Centrum powitania kliknij **maszyn wirtualnych** a następnie wybierz z listy hello hello maszyny Wirtualnej. W bloku hello hello maszyny Wirtualnej masz dostęp do informacji toooverview, wartości ustawień i monitorowania metryki. |
| Azure PowerShell |Aby uzyskać informacji o używaniu maszyn wirtualnych toomanage programu PowerShell, zobacz [tworzenia i zarządzania maszynami wirtualnymi systemu Windows za pomocą modułu Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| Interfejs API REST |Użyj hello [informacji pobieranie maszyny Wirtualnej](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) operacji tooget informacji o maszynie Wirtualnej. |
| Zestawy SDK klienta |Aby dowiedzieć się, jak przy użyciu języka C# toomanage maszyn wirtualnych, zobacz [Zarządzanie maszynach wirtualnych platformy Azure przy użyciu usługi Azure Resource Manager i C#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |

### <a name="log-on-toohello-vm"></a>Zaloguj się na toohello maszyny Wirtualnej
W portalu Azure hello Użyj zbyt przycisk Połącz hello[rozpocząć sesję pulpitu zdalnego (RDP)](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Można czasami wystąpienia problemów podczas próby toouse połączenia zdalnego. Jeśli ta sytuacja występuje tooyou, zapoznaj się hello informacje pomocy w [tooan połączeń pulpitu zdalnego Rozwiązywanie problemów z Azure maszyny wirtualnej z systemem Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="manage-availability"></a>Zarządzanie dostępnością
Ważne jest, aby użytkownik toounderstand jak zbyt[zapewnić wysoką dostępność](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) aplikacji. Ta konfiguracja obejmuje tworzenie wielu tooensure maszyn wirtualnych z co najmniej jednym systemem.

Aby tooqualify Twojego wdrożenia dla naszych 99.95 wirtualna umową dotyczącą poziomu usług, należy toodeploy co najmniej dwie maszyny wirtualne z systemami obciążenie wewnątrz [zestawu dostępności](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Ta konfiguracja daje gwarancję, że maszyny wirtualne są rozproszone w wielu domenach błędów i wdrożone na hostach z różnymi okresami konserwacji. Pełna Hello [umowy SLA platformy Azure](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) wyjaśniono hello gwarancji dostępności Azure jako całość.

### <a name="back-up-hello-vm"></a>Wykonaj kopię zapasową hello maszyny Wirtualnej
A [magazyn usług odzyskiwania](../../backup/backup-introduction-to-azure-backup.md) jest tooprotect używanych danych i zasobów w usługach zarówno Azure Backup i Azure Site Recovery. Korzystając z magazynu usług odzyskiwania zbyt[wdrażania i zarządzania nimi kopii zapasowych maszyn wirtualnych wdrożonych przez Menedżera zasobów, przy użyciu programu PowerShell](../../backup/backup-azure-vms-automation.md). 

## <a name="next-steps"></a>Następne kroki
* Jeśli zamierzeniu toowork z maszyn wirtualnych systemu Linux, obejrzyj [Azure i Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Dowiedz się więcej o wytycznych hello wokół Konfigurowanie infrastruktury w hello [wskazówki infrastruktury Azure przykład](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
