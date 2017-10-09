---
title: "aaaAzure maszyn wirtualnych systemu Linux i usługi Azure Storage | Dokumentacja firmy Microsoft"
description: "Zawiera opis usługi Azure Standard i Magazyn w warstwie Premium i zarówno zarządzane i niezarządzane dysków z maszyn wirtualnych systemu Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: d364c69e-0bd1-4f80-9838-bbc0a95af48c
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 2/7/2017
ms.author: rasquill
ms.openlocfilehash: d34441698a4e59721847685099e5fb3aa378c597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-storage"></a>Magazyn Azure i maszyny Wirtualnej systemu Linux
Magazyn Azure to rozwiązanie magazynu hello w chmurze dla nowoczesnych aplikacji, które polegają na trwałości, dostępności i skalowalności toomeet hello potrzeb klientów.  W toomaking dodanie go możliwe dla deweloperów toobuild aplikacji na dużą skalę toosupport nowych scenariuszy, Azure Storage stanowi również podstawowy magazyn hello maszyn wirtualnych platformy Azure.

## <a name="managed-disks"></a>Managed Disks

Maszyny wirtualne platformy Azure są teraz dostępne za pomocą [dysków zarządzanych Azure](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), co pozwala toocreate możesz maszyn wirtualnych bez tworzenia lub zarządzanie żadnego [konta usługi Azure Storage](../../storage/common/storage-introduction.md) samodzielnie. Możesz określić, czy Premium lub standardowego magazynu i dysku hello jak duże powinny być, i Azure utworzy hello dysków maszyny Wirtualnej. Maszyny wirtualne z dyskami zarządzane mają wiele ważnych funkcji, w tym:

- Obsługa automatycznego skalowania. Azure tworzy hello dysków i zarządza hello źródłowego magazynu toosupport się too10, 000 dysków na subskrypcję.
- Zwiększenie niezawodności z zestawami dostępności. Azure zapewnia, że dyski maszyny Wirtualnej są automatycznie odizolowane od siebie nawzajem w obrębie zestawów dostępności.
- Kontrola dostępu zwiększona. Dyski zarządzanych ujawnia różnych operacji kontrolowane przez [based kontroli dostępu (RBAC)](../../active-directory/role-based-access-control-what-is.md).

Cennik dysków zarządzanych różni się od tego niezarządzane dysków. Informacje, zobacz [cennik i rozliczenia dla dysków zarządzanych](../windows/managed-disks-overview.md#pricing-and-billing).

Możesz przekonwertować istniejące maszyny wirtualne korzystające z dysków toouse zarządzane niezarządzane dysków z [konwersji maszyny wirtualnej az](/cli/azure/vm#convert). Aby uzyskać więcej informacji, zobacz [jak tooconvert Maszynę wirtualną systemu Linux z niezarządzanych dyski dysków zarządzanych tooAzure](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Niezarządzane dysku nie można przekonwertować na dysków zarządzanych, jeśli na koncie magazynu, lub w dowolnym momencie zostały zaszyfrowane za pomocą dysku niezarządzane hello [szyfrowanie usługi Magazyn Azure (SSE)](../../storage/common/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Witaj kroki opisane szczegółowo sposób tootooconvert niezarządzanych dysków, które są lub były na koncie magazynu zaszyfrowanych:

- Skopiuj hello wirtualny dysk twardy (VHD) z [rozpoczęcia kopiowania obiektu blob magazynu az](/cli/azure/storage/blob/copy#start) tooa konta magazynu, który nigdy nie został włączony dla szyfrowanie usługi Magazyn Azure.
- Utwórz maszynę Wirtualną, która używa dysków zarządzanych i określić tego pliku wirtualnego dysku twardego w trakcie tworzenia w programie [tworzenia maszyny wirtualnej az](/cli/azure/vm#create), lub
- Dołącz hello skopiować wirtualny dysk twardy z [dołączyć dysku maszyny wirtualnej az](/cli/azure/vm/disk#attach) dyskach zarządzanych tooa maszyny Wirtualnej z systemem.


## <a name="azure-storage-standard-and-premium"></a>Usługi Azure Storage: Standardowa i Premium
Maszyny wirtualne platformy Azure — czy za pomocą dysków zarządzanych lub niezarządzanych — mogą być wbudowane w system dyski magazynu w warstwie standardowa lub premium magazynu dysków. Korzystając z portalu toochoose hello maszyny Wirtualnej należy przełączyć listy rozwijanej na powitania **podstawy** tooview ekranu dysków zarówno warstwy standardowa i premium. Jeśli włączono tooSSD, tylko magazyn w warstwie premium włączone maszyny wirtualne będą wyświetlane, wszystkich kopii przez SSD dysków.  Gdy włączono tooHDD, standardowy magazyn z włączonym obsługiwanej przez wirowania dysków maszyn wirtualnych są wyświetlane, wraz z maszyn wirtualnych przez SSD magazyn w warstwie premium.

Podczas tworzenia maszyny Wirtualnej z hello `azure-cli` , możesz wybrać standard i premium w przypadku wybrania hello rozmiar maszyny Wirtualnej za pomocą hello `-z` lub `--vm-size` flagi interfejsu wiersza polecenia.

## <a name="creating-a-vm-with-a-managed-disk"></a>Tworzenie maszyny Wirtualnej z dyskiem zarządzanym

Witaj poniższy przykład wymaga hello Azure CLI 2.0, które można [zainstalować tutaj](/cli/azure/install-azure-cli).

Najpierw utwórz hello toomanage grupy zasobów zasoby z [Tworzenie grupy az](/cli/azure/group#create):

```azurecli
az group create --location westus --name myResourceGroup
```

Teraz utworzyć hello maszyny Wirtualnej z [tworzenia maszyny wirtualnej az](/cli/azure/vm#create). Określ unikatową `--public-ip-address-dns-name` argumentu, jako `mypublicdns` prawdopodobnie jest zajęty.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns
```

Witaj w poprzednim przykładzie tworzy Maszynę wirtualną z dysków zarządzanych w ramach konta magazynu w warstwie standardowa. toouse konto magazynu w warstwie Premium, Dodaj hello `--storage-sku Premium_LRS` argumentu, takich jak hello poniższy przykład:

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns \
    --storage-sku Premium_LRS
```

## <a name="standard-storage"></a>Standard Storage
Standardowy magazyn Azure to hello domyślny typ magazynu.  Standardowy magazyn jest ekonomiczne przy zachowaniu wydajności.  

## <a name="premium-storage"></a>Premium Storage
Usługa Azure Premium Storage oferuje obsługę wysokiej wydajności i małych opóźnieniach dysku dla maszyn wirtualnych uruchomionych/O wykonujących obciążeń. Dysków dla maszyny wirtualnej (VM) korzystające z magazynu Premium przechowywania danych na dyskach półprzewodnikowych (SSD). Można przeprowadzić migrację aplikacji maszyny Wirtualnej dyski tooAzure magazyn w warstwie Premium tootake zaletą hello szybkości i wydajności tych dysków.

Funkcje magazynu Premium:

* Dyski magazynu Premium: Usługa Azure Premium Storage obsługuje dyski maszyn wirtualnych, które mogą być dołączone tooDS, DSv2 lub maszynach wirtualnych platformy Azure serii GS.
* Premium stronicowych obiektów Blob: Magazyn w warstwie Premium obsługuje Azure stronicowe obiekty BLOB, które są używane toohold trwałe dysków na maszynach wirtualnych Azure (VM).
* Magazyn lokalnie nadmiarowy Premium: Konta Premium Storage tylko obsługuje lokalnie nadmiarowego magazynu (LRS) jako opcję replikacji hello i przechowuje trzy kopie danych hello w pojedynczym regionie.
* [Magazyn w warstwie Premium](../../storage/common/storage-premium-storage.md)

## <a name="premium-storage-supported-vms"></a>Magazyn w warstwie Premium są obsługiwane maszyny wirtualne
Magazyn w warstwie Premium obsługuje serii DS, DSv2 serii, serie GS i maszynach wirtualnych Azure serii Fs (VM). Z magazynu Premium obsługiwanych maszyn wirtualnych służy dysków magazynu w wersjach Standard i Premium. Ale nie można używać dysków Premium Storage z serii maszyn wirtualnych, które nie są zgodne magazyn w warstwie Premium.

Poniżej przedstawiono dystrybucje systemu Linux hello, który mamy zweryfikować z magazyn w warstwie Premium.

| Dystrybucja | Wersja | Obsługiwane jądra |
| --- | --- | --- |
| Ubuntu |12.04 |3.2.0-75.110+ |
| Ubuntu |14.04 |3.13.0-44.73+ |
| Debian |7.x, 8.x |3.16.7-ckt4-1+ |
| SLES |SLES 12 |3.12.36-38.1+ |
| SLES |SLES 11 Z DODATKIEM SP4 |3.0.101-0.63.1+ |
| CoreOS |584.0.0+ |3.18.4+ |
| Centos |6.5, 6.6, 6.7, 7.0, 7.1 |3.10.0-229.1.2.el7+ |
| RHEL |6.8+, 7.2+ | |

## <a name="azure-file-storage"></a>Magazyn plików Azure
Magazyn plików Azure oferuje udziały plików w chmurze hello przy użyciu standardowego protokołu SMB hello. Przy użyciu plików Azure można migrować aplikacje dla przedsiębiorstw, które są oparte na tooAzure serwerów plików. Aplikacje działające na platformie Azure można łatwo zainstalować udziały plików z systemem Linux maszyn wirtualnych platformy Azure. I hello najnowszej wersji z pliku magazynu, można zainstalować udział plików z aplikacji lokalnej, która obsługuje protokół SMB 3.0.  Ponieważ udziały plików są udziałami SMB, możesz uzyskiwać do nich dostęp za pośrednictwem interfejsów API systemu plików standardowych.

Magazyn plików jest oparty na tej samej technologii jako magazyn obiektów Blob, tabel i kolejek, więc magazyn plików oferuje hello dostępności, trwałości, skalowalność i nadmiarowość geograficzna który jest wbudowanych w platformy Azure storage hello hello. Aby uzyskać więcej informacji o cele wydajności magazynu plików i limity Zobacz cele dotyczące wydajności i skalowalności magazynu Azure.

* [Jak toouse magazyn plików Azure z systemem Linux](../../storage/files/storage-how-to-use-files-linux.md)

## <a name="hot-storage"></a>Magazynu gorącego
Warstwa magazynu gorącego Azure Hello jest zoptymalizowana pod kątem przechowywania danych często uzyskuje się dostęp.  Magazynu gorącego jest hello domyślny typ magazynu magazynów obiektów blob.

## <a name="cool-storage"></a>Magazynu chłodnego
Warstwa magazynu chłodnego Azure Hello jest zoptymalizowana pod kątem przechowywania danych, których rzadko uzyskuje się dostęp i długotrwałe. Przykładowe przypadki użycia do magazynu chłodnego obejmują kopii zapasowych, zawartości multimedialnej danych naukowych, zgodności i archiwizowania danych. Ogólnie rzecz biorąc dane, które rzadko jest dostępny jest idealne kandydatem do magazynu chłodnego.

|  | Warstwa magazynu gorącego | Warstwa magazynu chłodnego |
|:--- |:---:|:---:|
| Dostępność |99,9% |99% |
| Dostępność (odczyty RA-GRS) |99,99% |99,9% |
| Opłaty za zużycie |Wyższe koszty magazynowania |Niższe koszty magazynowania |
| Niższe dostępu |Wyższy dostępu | |
| i koszty transakcji |i koszty transakcji | |

## <a name="redundancy"></a>Nadmiarowość
Witaj danych platformy Microsoft Azure konto magazynu jest zawsze replikowane tooensure trwałości i wysokiej dostępności, spotkania hello umowy SLA magazynu platformy Azure, nawet w powierzchnię hello przejściowych awarii sprzętu.

Podczas tworzenia konta magazynu musi wybierz jedną z hello następujące opcje replikacji:

* Magazyn lokalnie nadmiarowy (LRS)
* Magazyn strefowo nadmiarowy (ZRS)
* Magazyn geograficznie nadmiarowy (GRS)
* Magazyn geograficznie nadmiarowy dostępny do odczytu (RA-GRS)

### <a name="locally-redundant-storage"></a>Magazyn lokalnie nadmiarowy
Magazyn lokalnie nadmiarowy (LRS) replikuje dane w regionie hello, w którym utworzono konto magazynu. trwałość toomaximize, każde żądanie dotyczące danych na koncie magazynu są replikowane trzy razy. Te trzy repliki każdego znajdują się w oddzielnych błędów domen i domen uaktualnienia.  Żądanie pomyślnie zwraca tylko wtedy, gdy został zapisany tooall trzy repliki.

### <a name="zone-redundant-storage"></a>Magazyn strefowo nadmiarowy
Magazyn strefowo nadmiarowy (ZRS) replikuje dane między dwoma toothree urządzeń, w jednym lub dwóch regionach, zapewniając większą trwałość niż magazyn LRS. Jeśli Twoje konto magazynu ZRS włączone, dane są trwałe nawet w przypadku hello awarii w jednej hello urządzeń.

### <a name="geo-redundant-storage"></a>Magazyn geograficznie nadmiarowy
Magazyn geograficznie nadmiarowy (GRS) replikuje regionu dodatkowej tooa danych będącego setki odległości od regionu podstawowego hello. Jeśli konto magazynu ma GRS włączone, dane są trwałe nawet w przypadku hello pełną regionalnej awarii lub awarii, w których hello regionu podstawowego nie jest możliwe do odzyskania.

### <a name="read-access-geo-redundant-storage"></a>Dostęp do odczytu magazynu geograficznie nadmiarowego
Dostęp do odczytu magazynu geograficznie nadmiarowego (RA-GRS) pozwala zwiększyć dostępność dla konta magazynu, dostarczając danych toohello dostęp tylko do odczytu w lokalizacji dodatkowej hello, oprócz replikacji toohello dwóch regionach podał grs w warstwie. W przypadku hello dane będą niedostępne w regionie podstawowym hello aplikacji może odczytywać dane z regionu pomocniczego hello.

Dla nowości w Zobacz nadmiarowość magazynu Azure:

* [Replikacja usługi Azure Storage](../../storage/common/storage-redundancy.md)

## <a name="scalability"></a>Skalowalność
Usługa Azure Storage jest skalowalna na ogromną skalę, więc można przechowywać i przetwarzać setki terabajtów danych toosupport hello danych big data scenariusze analizy naukowych, finansowych i aplikacji. Możesz także przechowywać hello niewielkich ilości danych wymagane dla małych firm witryny sieci Web. Gdy Twoje potrzeby zmniejszą, płacisz tylko za hello dane, które są przechowywane. Obecnie Magazyn Azure przechowuje dziesiątki bilionów unikatowych obiektów klienckich i obsługuje średnio miliony żądań na sekundę.

W przypadku kont magazynu w warstwie standardowa: konta standard storage ma maksymalna całkowita liczba żądań liczba IOPS 20 000. Witaj całkowita IOPS wszystkich dysków maszyny wirtualnej w ramach konta magazynu w warstwie standardowa nie może przekraczać ten limit.

Dla kont premium magazynu: Konto magazynu w warstwie premium ma maksymalną przepustowość łączna liczba 50 GB/s. Witaj ogólnej przepustowości we wszystkich dysków maszyny Wirtualnej nie może przekraczać ten limit.

## <a name="availability"></a>Dostępność
Firma Microsoft gwarantuje, że co najmniej 99,99% (99,9% Warstwa dostępu chłodna) czas hello, firma Microsoft będzie pomyślnie przetwarzania żądań tooread danych z magazynu geograficznie nadmiarowego geograficznie dostęp do odczytu (RA-GRS) kont, pod warunkiem, że nie prób tooread dane z regionu podstawowego hello ponowione w regionie pomocniczym hello.

Firma Microsoft gwarantuje, że co najmniej 99,9% (99% Warstwa dostępu chłodna) czas hello, firma Microsoft będzie pomyślnie proces żąda danych tooread z lokalnie nadmiarowego magazynu (LRS), strefy magazyn geograficznie nadmiarowy (ZRS) i konta magazynu geograficznie nadmiarowego magazynu (GRS).

Firma Microsoft gwarantuje, że co najmniej 99,9% (99% Warstwa dostępu chłodna) czas hello, firma Microsoft będzie pomyślnie proces żąda toowrite danych tooLocally magazyn geograficznie nadmiarowy (LRS), strefy nadmiarowego magazynu (ZRS) i z magazynu geograficznie nadmiarowego kont magazynu (GRS) oraz dostęp do odczytu geograficznie nadmiarowego Konta magazynu (RA-GRS).

* [SLA platformy Azure dla magazynu](https://azure.microsoft.com/support/legal/sla/storage/v1_1/)

## <a name="regions"></a>Regiony
Azure jest ogólnie dostępna w regionach 30 wokół Witaj świecie i ogłosiła plany 4 dodatkowe regionów. Ekspansji jest priorytet dla platformy Azure, ponieważ umożliwia ona naszym klientom tooachieve większą wydajność i obsługuje on ich wymagań i preferencji dotyczących danych lokalizacji.  Azures najnowsze toolaunch region jest w Niemczech.

Hello Niemcy Microsoft Cloud zapewnia toohello zróżnicowanych opcji już dostępne dla usługi Microsoft Cloud w Europie, tworzenie zwiększenie możliwości innowacji i wzrostu gospodarczego dla dużej podlegającymi ochronie partnerów i klientów w Niemczech, Hello Europejskiej Unii i hello Europejskiego wolnego handlu skojarzenia (ESWH).

Dane klienta w tych nowych centrów danych w Magdeburgu i Frankfurt, odbywa się pod kontrolą hello zarządca danych, międzynarodowej T-systemy niezależnie od firmy niemieckim i zależnym Telekom marki. Firmy Microsoft komercyjnych usług chmurowych w tych centrach danych odpowiednia przepisy dotyczące obsługi danych, tooGerman i zapewniają klientom dodatkowe opcje z jak i gdzie dane są przetwarzane.

* [Mapa regionów platformy Azure](https://azure.microsoft.com/regions/)

## <a name="security"></a>Bezpieczeństwo
Usługa Azure Storage zapewnia rozbudowany zestaw funkcji zabezpieczeń, które razem umożliwiają deweloperom toobuild bezpiecznych aplikacji. samo konto magazynu Hello mogą być chronione przy użyciu kontroli dostępu opartej na rolach i Azure Active Directory. Dane mogą być chronione przesyłanych między aplikacją a Azure za pomocą szyfrowania po stronie klienta, HTTPS lub SMB 3.0. Dane można ustawić toobe automatycznie szyfrowane podczas zapisywane tooAzure magazynu przy użyciu szyfrowania usługi magazynu (SSE). Systemu operacyjnego i dysków z danymi używanych przez maszyny wirtualne można ustawić toobe zaszyfrowane za pomocą szyfrowania dysków Azure. Obiekty danych toohello delegowanego dostępu w usłudze Azure Storage można otrzymać za pomocą sygnatury dostępu współdzielonego.

### <a name="management-plane-security"></a>Zarządzanie płaszczyzny zabezpieczeń
płaszczyzny zarządzania Hello składa się z toomanage zasoby używane hello konta magazynu. W tej sekcji będziesz omawianiu modelu wdrażania usługi Azure Resource Manager hello i jak toocontrol kontroli dostępu opartej na rolach (RBAC) toouse uzyskują dostęp do kont magazynu tooyour. Firma Microsoft będzie również porozmawiać na temat zarządzania kluczami konta magazynu i w jaki sposób tooregenerate je.

### <a name="data-plane-security"></a>Zabezpieczenia warstwy danych
W tej sekcji wyjaśniono zezwalania na dostęp toohello rzeczywiste dane obiektów na koncie magazynu obiektów blob, plików, kolejek i tabel, przy użyciu sygnatury dostępu współdzielonego i przechowywane zasad dostępu. Omówimy SAS poziomu usług i poziomie konta sygnatury dostępu Współdzielonego. Firma Microsoft sekcji omówiono również, jak toolimit dostępu tooa określonego adresu IP (lub zakres adresów IP), jak używany protokół hello toolimit tooHTTPS i jak toorevoke a Shared Access Signature nie oczekuje na tooexpire.

## <a name="encryption-in-transit"></a>Szyfrowanie podczas przesyłania
W tej sekcji omówiono sposób toosecure danych podczas transferu do lub z usługi Azure Storage. Będzie omawianiu hello zalecane użycie protokołu HTTPS i hello szyfrowania używany przez protokół SMB 3.0 do udziały plików platformy Azure. Firma Microsoft będzie także Spójrz na szyfrowanie po stronie klienta, co umożliwia tooencrypt hello dane przed przeniesieniem do magazynu w aplikacji klienckiej i toodecrypt powitania po przeniesieniu poza magazynu.

## <a name="encryption-at-rest"></a>Szyfrowanie magazynowanych
Zostanie omawianiu szyfrowanie usługi Magazyn (SSE) i jak można ją włączyć dla konta magazynu, co powoduje blokowe, stronicowe obiekty BLOB i uzupełnialnych obiektów blob, są szyfrowane automatycznie, gdy zapisywane tooAzure magazynu. Ponadto przedstawiono sposób użycia szyfrowania dysków Azure i Poznaj podstawowe różnice hello i przypadków szyfrowania dysku i SSE i szyfrowania po stronie klienta. Krótko przedstawiono zgodności ze standardem FIPS dla Stanów Zjednoczonych Komputery dla instytucji rządowych.

* [Przewodnik po zabezpieczeniach magazynu Azure](../../storage/common/storage-security-guide.md)

## <a name="temporary-disk"></a>Tymczasowe dysku
Każda maszyna wirtualna zawiera dysku tymczasowym. dysku tymczasowym Hello zapewnia krótkoterminowy magazyn dla aplikacji i procesów i jest zamierzone tooonly przechowywania danych, takich jak pliki strony lub wymiany. Dane na dysku tymczasowym hello mogą zostać utracone podczas [zdarzenia konserwacji](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) lub gdy użytkownik [ponownego wdrażania maszyny Wirtualnej](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Podczas standardowego ponowne uruchomienie hello maszyny Wirtualnej ma utrwalić danych hello na powitania tymczasowej stacji.

W przypadku maszyn wirtualnych systemu Linux, dysk hello jest zwykle **/dev/sdb** sformatowany i jest zainstalowany za**katalogu/mnt** przez hello agenta systemu Linux platformy Azure. Hello rozmiar dysku tymczasowym hello zależy od rozmiaru hello hello maszyny wirtualnej. Aby uzyskać więcej informacji, zobacz [rozmiary maszyn wirtualnych systemu Linux](sizes.md).

Aby uzyskać więcej informacji o używaniu dysku tymczasowym hello Azure, zobacz [opis hello tymczasowej stacji na maszynach wirtualnych Azure firmy Microsoft](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="cost-savings"></a>Oszczędności
* [Koszt magazynowania](https://azure.microsoft.com/pricing/details/storage/)
* [Kalkulator magazynu koszt](https://azure.microsoft.com/pricing/calculator/?service=storage)

## <a name="storage-limits"></a>Limity magazynu
* [Ograniczenia usługi magazynu](../../azure-subscription-service-limits.md#storage-limits)
