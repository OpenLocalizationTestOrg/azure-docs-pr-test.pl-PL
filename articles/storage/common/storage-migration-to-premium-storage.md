---
title: aaaMigrating maszyn wirtualnych tooAzure magazyn w warstwie Premium | Dokumentacja firmy Microsoft
description: "Migrowanie istniejących tooAzure maszyn wirtualnych magazyn w warstwie Premium. Magazyn w warstwie Premium oferuje obsługę dysków o wysokiej wydajności i małych opóźnieniach/O wykonujących obciążeń uruchomionych na maszynach wirtualnych platformy Azure."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: 19aaf2b7594e570f5a964baa00958a7a8eaae97b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a>Migrowanie tooAzure magazyn w warstwie Premium (niezarządzany dysków)

> [!NOTE]
> W tym artykule opisano, jak toomigrate maszynę Wirtualną, która używa tooa niezarządzane standardowych dysków maszyny Wirtualnej używającej niezarządzanych dysków premium. Zaleca się używać dysków zarządzanych Azure dla maszyn wirtualnych i przekonwertowanie poprzedniej dysków toomanaged niezarządzane dysków. Zarządzane dyski dojścia hello źródłowego magazynu konta, dzięki czemu nie trzeba. Aby uzyskać więcej informacji, zobacz nasze [omówienie dysków zarządzanych](../../virtual-machines/windows/managed-disks-overview.md).
>

Usługa Azure Premium Storage oferuje obsługę wysokiej wydajności i małych opóźnieniach dysku dla maszyn wirtualnych uruchomionych/O wykonujących obciążeń. Zaletą hello szybkości i wydajności tych dysków może potrwać przy użyciu funkcji migracji aplikacji maszyny Wirtualnej dyski tooAzure magazyn w warstwie Premium.

przeznaczenie tego przewodnika Hello jest toohelp nowych użytkowników usługi Azure Premium Storage lepsze przygotowanie toomake przejścia z ich bieżącej tooPremium systemu magazynowania. Przewodnik Hello adresów trzy najważniejsze składniki hello tego procesu:

* [Planowanie hello tooPremium migracji magazynu](#plan-the-migration-to-premium-storage)
* [Przygotowanie i tooPremium kopiowania wirtualnych dysków twardych (VHD) magazynu](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [Utwórz maszynę wirtualną platformy Azure przy użyciu magazyn w warstwie Premium](#create-azure-virtual-machine-using-premium-storage)

Można dokonać migracji maszyn wirtualnych z innych platform tooAzure magazyn w warstwie Premium lub migracji istniejących maszyn wirtualnych platformy Azure z magazynu w warstwie standardowa tooPremium magazynu. W tym przewodniku opisano kroki dla obu dwa scenariusze. Wykonaj kroki hello określone w odpowiedniej sekcji hello w zależności od danego scenariusza.

> [!NOTE]
> Omówienie funkcji i cenowych Premium magazynu w warstwie Premium Storage można znaleźć: [magazynu o wysokiej wydajności dla obciążeń maszyny wirtualnej Azure](storage-premium-storage.md). Zaleca się migrowanie dyskami maszyny wirtualnej wymagające wysokiej tooAzure IOPS magazyn w warstwie Premium hello najlepszą wydajność aplikacji. Jeśli dysk nie wymaga wysokiej IOPS, przechowując go w Standard Storage, która przechowuje dane dysku maszyny wirtualnej na stacje dysków twardych (HDD) zamiast dysków SSD można ograniczyć koszty.
>

Kończenie procesu migracji hello w całości może wymagać dodatkowych akcji przed i po hello z krokami opisanymi w tym przewodniku. Przykładami konfigurowania sieci wirtualnych lub punktów końcowych lub wprowadzania zmian w kodzie aplikacji hello sam wymagające przestój w aplikacji. Te akcje są unikatowe tooeach aplikacji i należy je ukończyć wraz z hello z krokami opisanymi w tej przewodnik toomake hello pełne przejście tooPremium magazynu jako bezproblemowe, jak to możliwe.

## <a name="plan-the-migration-to-premium-storage"></a>Planowanie hello tooPremium migracji magazynu
W tej sekcji gwarantuje, że są gotowe toofollow hello kroki migracji opisane w tym artykule i ułatwia toomake hello najlepszych decyzji w typach maszyny Wirtualnej i dysku.

### <a name="prerequisites"></a>Wymagania wstępne
* Konieczne będzie subskrypcji platformy Azure. Jeśli nie masz, możesz utworzyć jeden miesiąc [bezpłatnej wersji próbnej](https://azure.microsoft.com/pricing/free-trial/) subskrypcji lub odwiedź stronę [cennik usługi Azure](https://azure.microsoft.com/pricing/) wyświetlić więcej opcji.
* tooexecute poleceń cmdlet programu PowerShell, należy hello modułu Microsoft Azure PowerShell. Zobacz [jak tooinstall i konfigurowanie programu Azure PowerShell](/powershell/azure/overview) hello zainstalować instrukcje instalacji i punktu.
* Planując maszyn wirtualnych Azure toouse pracujących na magazyn w warstwie Premium, należy toouse hello maszyn wirtualnych z funkcją Magazyn w warstwie Premium. Dyski w wersjach Standard i Premium Storage służy magazyn w warstwie Premium obsługuje maszyn wirtualnych. Dyski magazynu Premium będą dostępne z większą liczbę typów w przyszłości hello maszyny Wirtualnej. Aby uzyskać więcej informacji na wszystkich dostępnych typów dysku maszyny Wirtualnej platformy Azure i rozmiarów, zobacz [rozmiary maszyn wirtualnych](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) i [rozmiary dla usług w chmurze](../../cloud-services/cloud-services-sizes-specs.md).

### <a name="considerations"></a>Zagadnienia do rozważenia
Maszyny Wirtualnej platformy Azure obsługuje dołączanie kilka dysków Premium Storage, dzięki czemu aplikacji może zawierać maksymalnie too256 TB pamięci masowej dla maszyny Wirtualnej. Z magazyn w warstwie Premium aplikacje można osiągnąć 80 000 IOPS (operacje wejścia/wyjścia na sekundę) dla maszyny Wirtualnej i 2000 MB na drugi przepływność dysku dla maszyny Wirtualnej z bardzo małych opóźnień operacji odczytu. Dostępne są opcje wiele maszyn wirtualnych i dysków. Ta sekcja ma toohelp toofind opcję najlepiej pasującą do obciążenia.

#### <a name="vm-sizes"></a>Rozmiary maszyn wirtualnych
specyfikacje rozmiaru maszyny Wirtualnej Azure Hello są wymienione w [rozmiary maszyn wirtualnych](../../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Przejrzyj hello charakterystyki wydajności maszyn wirtualnych, które pracować z magazyn w warstwie Premium i wybierz polecenie hello najbardziej odpowiedni rozmiar maszyny Wirtualnej najlepiej pasujące do obciążenia. Upewnij się, czy Brak dostępnej wystarczającą przepustowość na ruchu dysku hello toodrive maszyny Wirtualnej.

#### <a name="disk-sizes"></a>Rozmiary dysków
Istnieje pięć typów dysków, które mogą być używane z maszyny Wirtualnej, a każdy ma określonych IOPs i przepływność limity. Wziąć pod uwagę następujące limity gdy wybieranie hello typu dysku do maszyny Wirtualnej na podstawie hello potrzeb aplikacji pod względem wydajności, wydajności, skalowalności i ładuje godzinami szczytu.

| Typ dysków Premium  | P10   | P20   | P30            | P40            | P50            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| Rozmiar dysku           | 128 GB| 512 GB| 1024 GB (1 TB) | 2048 GB (2 TB) | 4095 GB (4 TB) | 
| Liczba operacji wejścia/wyjścia na sekundę na dysk       | 500   | 2300  | 5000           | 7500           | 7500           | 
| Przepływność na dysk | 100 MB na sekundę | 150 MB na sekundę | 200 MB / s | 250 MB na sekundę | 250 MB na sekundę |

W zależności od obciążenia należy sprawdzić, czy dyski dodatkowe dane są niezbędne dla maszyny Wirtualnej. Możesz dołączyć kilka tooyour dysków danych maszyny Wirtualnej. W razie potrzeby można paskowych między hello dysków tooincrease hello pojemność i wydajność hello woluminu. (Zobacz, co rozkładanie [tutaj](storage-premium-storage-performance.md#disk-striping).) Jeśli paskowych magazyn w warstwie Premium dysków danych za pomocą [miejsca do magazynowania][4], należy ją skonfigurować z jedną kolumną dla każdego dysku, który jest używany. W przeciwnym razie hello ogólnej wydajności hello rozkładane woluminu może być niższa niż oczekiwano powodu dystrybucji toouneven ruchu na dyskach hello. W przypadku maszyn wirtualnych systemu Linux można użyć hello *mdadm* tooachieve narzędzie hello takie same. Zobacz artykuł [skonfigurować RAID oprogramowania w systemie Linux](../../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) szczegółowe informacje.

#### <a name="storage-account-scalability-targets"></a>Wartości docelowe skalowalności konta magazynu
Konta Premium magazynu ma następujące wartości docelowe skalowalności w toohello dodanie hello [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md). Wymagania aplikacji przekracza hello wartości docelowe skalowalności konta magazynu pojedynczego, kompilacji toouse Twojej aplikacji z wielu kont magazynu i partycji danych przez tych kont magazynu.

| Konto łączna pojemność | Przepustowość konto magazyn lokalnie nadmiarowy |
|:--- |:--- |
| Pojemność dysku: 35TB<br />Migawki pojemności: 10 TB |Zapasowej too50 gigabity na sekundę dla ruchu przychodzącego i wychodzącego |

Dla hello więcej informacji na temat specyfikacji magazyn w warstwie Premium, zapoznaj się z [skalowalność i cele wydajności przy użyciu magazyn w warstwie Premium](storage-premium-storage.md#scalability-and-performance-targets).

#### <a name="disk-caching-policy"></a>Dyskowej pamięci podręcznej zasad
Domyślnie jest dyskowej pamięci podręcznej zasad *tylko do odczytu* dla wszystkich hello dysków danych w warstwie Premium i *odczytu i zapisu* dla dysku systemu operacyjnego Premium hello dołączony toohello maszyny Wirtualnej. To ustawienie konfiguracji jest zalecane tooachieve hello optymalnej wydajności dla aplikacji systemu IOs. W przypadku dysków ciężki zapisu lub w trybie tylko do zapisu danych (takich jak pliki dziennika programu SQL Server) Wyłącz buforowanie dysku, dzięki czemu można osiągnąć lepszą wydajność aplikacji. ustawienia pamięci podręcznej Hello istniejących dysków danych można zaktualizować przy użyciu [Azure Portal](https://portal.azure.com) lub hello *- HostCaching* parametru hello *AzureDataDisk zestawu* polecenia cmdlet.

#### <a name="location"></a>Lokalizacja
Wybierz lokalizację, gdzie dostępna jest usługa Azure Premium Storage. Zobacz [regionów platformy Azure](https://azure.microsoft.com/regions/#services) aktualne informacje o dostępnych lokalizacji. Maszyny wirtualne znajdujące się w hello sam region jako hello konta magazynu, czy magazyny hello dysków dla maszyny Wirtualnej hello zapewni znacznie lepszą wydajność niż jeśli znajdują się w oddzielnych regionach.

#### <a name="other-azure-vm-configuration-settings"></a>Inne ustawienia konfiguracji maszyny Wirtualnej Azure
Podczas tworzenia maszyny Wirtualnej platformy Azure, użytkownik będzie proszony tooconfigure niektórych ustawień maszyny Wirtualnej. Należy pamiętać, że w ustaleniu ustawień kilka hello czas ich istnienia hello maszyny Wirtualnej, podczas gdy można zmodyfikować lub dodać inne później. Przejrzyj te ustawienia konfiguracji maszyny Wirtualnej platformy Azure i upewnij się, że są one poprawnie skonfigurowane, toomatch wymagań obciążenia.

### <a name="optimization"></a>Optymalizacja
[Usługa Azure Premium Storage: Projekt o wysokiej wydajności](storage-premium-storage-performance.md) zawiera wskazówki dotyczące tworzenia aplikacji wysokiej wydajności za pomocą usługi Azure Premium Storage. Można użyć wskazówki hello połączone z wydajności najlepszych praktyk stosowanych tootechnologies używanych przez aplikację.

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Przygotowanie i skopiuj wirtualne dyski twarde (VHD) tooPremium magazynu
powitania po sekcji wskazówki przygotowania wirtualne dyski twarde z maszyny Wirtualnej i kopiowanie wirtualnych dysków twardych tooAzure magazynu.

* [Scenariusz 1: "I am migracji istniejących maszyn wirtualnych Azure tooAzure magazyn w warstwie Premium."](#scenario1)
* [Scenariusz 2: "I am Migrowanie maszyn wirtualnych z innych platform tooAzure magazyn w warstwie Premium."](#scenario2)

### <a name="prerequisites"></a>Wymagania wstępne
Witaj tooprepare wirtualne dyski twarde do migracji, będą potrzebne:

* Subskrypcja platformy Azure, konta magazynu i kontener, w tym magazynie konta toowhich kopiujesz dysk VHD. Należy pamiętać, że konto magazynu docelowego hello może być kontem Standard lub Premium Storage, w zależności od wymagań.
* Witaj toogeneralize narzędzie wirtualnego dysku twardego, jeśli planujesz toocreate wielu wystąpień maszyny Wirtualnej z niego. Na przykład, program sysprep dla systemu Windows lub programu sysprep virt dla Ubuntu.
* Narzędzie tooupload hello wirtualnego dysku twardego pliku toohello konta magazynu. Zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md) lub użyj [Eksploratora usługi Azure storage](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx). Ten przewodnik zawiera opis kopiowanie dysk VHD za pomocą narzędzia AzCopy hello.

> [!NOTE]
> Jeśli wybierzesz opcję synchronicznych kopii z narzędzia AzCopy, aby uzyskać optymalną wydajność, skopiuj dysk VHD, uruchamiając jeden z tych narzędzi z maszyny Wirtualnej platformy Azure, który znajduje się w hello tego samego regionu co konto magazynu docelowego hello. Jeśli kopiujesz dysk VHD maszyny Wirtualnej platformy Azure w innym regionie, wydajność może przebiegać wolniej.
>
> W przypadku kopiowania dużych ilości danych w ograniczonej przepustowości, rozważ [przy użyciu hello Import/Eksport Azure usługa tootransfer danych tooBlob magazynu](../storage-import-export-service.md); umożliwia tootransfer danych przez dysk twardy wysyłki dyski tooan Azure Centrum danych. Możesz użyć hello Import/Eksport Azure usługa toocopy danych tooa konta standard storage tylko. Po hello danych na koncie magazynu w warstwie standardowa, można użyć albo hello [kopiowania obiektu Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx) lub konto magazynu premium tooyour danych AzCopy tootransfer hello.
>
> Należy pamiętać, że Microsoft Azure obsługuje tylko pliki wirtualnego dysku twardego o stałym rozmiarze. Pliki VHDX lub dynamiczne wirtualne dyski twarde nie są obsługiwane. Jeśli masz dynamicznego wirtualnego dysku twardego, możesz przekonwertować ją przy użyciu hello rozmiar toofixed [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) polecenia cmdlet.
>
>

### <a name="scenario1"></a>Scenariusz 1: "I am migracji istniejących maszyn wirtualnych Azure tooAzure magazyn w warstwie Premium."
W przypadku migracji istniejących maszyn wirtualnych platformy Azure, hello Zatrzymaj maszynę Wirtualną, przygotowanie dysków VHD na typ hello ma wirtualnego dysku twardego, a następnie skopiuj hello wirtualnego dysku twardego z narzędzia AzCopy lub środowiska PowerShell.

Witaj maszyny Wirtualnej musi toobe całkowicie dół toomigrate stanu czystego. Będzie przestoju dopiero po zakończeniu migracji hello.

#### <a name="step-1-prepare-vhds-for-migration"></a>Krok 1. Przygotowanie do migracji dysków VHD
W przypadku migracji istniejących maszyn wirtualnych platformy Azure tooPremium magazynu, może być dysk VHD:

* Obraz systemu operacyjnego ogólnych
* Dysk systemu operacyjnego
* Dysk z danymi

Poniżej opisano firma Microsoft za pośrednictwem tych scenariuszy 3 przygotowania dysk VHD.

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a>Użyj ogólnych toocreate wirtualnego dysku twardego systemu operacyjnego wielu wystąpień maszyny Wirtualnej
Podczas przekazywania wirtualnego dysku twardego, który ma być używane toocreate wiele ogólnych wystąpień maszyny Wirtualnej platformy Azure, musi najpierw generalize plik VHD za pomocą narzędzia sysprep. Dotyczy to tooa wirtualnego dysku twardego, który jest lokalnie lub w chmurze hello. Program Sysprep usuwa wszystkie informacje dotyczące komputera hello wirtualnego dysku twardego.

> [!IMPORTANT]
> Utwórz migawkę lub kopii zapasowej maszyny Wirtualnej przed jej uogólnianie. Uruchomiony program sysprep spowoduje zatrzymanie i deallocate hello wystąpienia maszyny Wirtualnej. Wykonaj kroki opisane poniżej toosysprep wirtualnego dysku twardego systemu operacyjnego Windows. Należy pamiętać, że polecenia Sysprep hello będzie wymagać tooshut maszynę wirtualną hello. Aby uzyskać więcej informacji na temat narzędzia Sysprep, zobacz [Omówienie narzędzia Sysprep](http://technet.microsoft.com/library/hh825209.aspx) lub [techniczne dotyczące narzędzia Sysprep](http://technet.microsoft.com/library/cc766049.aspx).
>
>

1. Otwórz okno wiersza polecenia z uprawnieniami administratora.
2. Wprowadź powitania po tooopen polecenia Sysprep:

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. Hello narzędzie przygotowania systemu, wybierz opcję Wprowadź systemu Out-of-Box (OOBE Experience), hello zaznacz pole wyboru Generalize, wybierz **zamknięcia**, a następnie kliknij przycisk **OK**, jak pokazano w poniższym obrazie hello. Narzędzie Sysprep będzie uogólnienia systemu operacyjnego hello i zamknij hello system.

    ![][1]

Dla maszyny Wirtualnej systemu Ubuntu Użyj narzędzia sysprep virt tooachieve hello takie same. Zobacz [virt sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) więcej szczegółów. Zobacz też niektóre typu hello open source [rozbudowy serwerów Linux oprogramowania](http://www.cyberciti.biz/tips/server-provisioning-software.html) dla innych systemów operacyjnych Linux.

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a>Użyj unikatowy toocreate wirtualnego dysku twardego systemu operacyjnego jedno wystąpienie maszyny Wirtualnej
Jeśli masz aplikacji działających na powitania maszyny Wirtualnej, co wymaga dane dotyczące określonego komputera hello nie generalize hello wirtualnego dysku twardego. Uogólniony wirtualny dysk twardy może być używane toocreate unikatowego wystąpienia maszyny Wirtualnej platformy Azure. Na przykład jeśli kontroler domeny na dysk VHD, wykonywanie programu sysprep, spowoduje to nieefektywne jako kontroler domeny. Przejrzyj hello aplikacji działających w sieci maszyny Wirtualnej i hello wpływ program sysprep na nich przed uogólnianie hello wirtualnego dysku twardego.

##### <a name="register-data-disk-vhd"></a>Zarejestruj dane dysku VHD
Jeśli masz migracji dysków z danymi w Azure toobe, należy upewnić się, że maszyny wirtualne hello korzystających z tych danych, które dyski są zamknięte.

Wykonaj kroki hello opisanych poniżej toocopy wirtualnego dysku twardego tooAzure magazyn w warstwie Premium i zarejestrowanie go jako dysk danych elastycznie.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Krok 2. Utwórz lokalizację docelową hello dysk VHD
Utwórz konto magazynu do przechowywania dyski VHD. Należy wziąć pod uwagę następujące punkty podczas planowania miejsca hello toostore dyski VHD:

* obiekt docelowy Hello konta magazynu w warstwie Premium.
* Lokalizacja konta magazynu Hello musi być taki sam jak magazyn w warstwie Premium obsługuje maszyny wirtualne Azure utworzysz w ostatnim etapie hello. Można skopiować nowego konta magazynu tooa lub hello toouse planu tego samego konta magazynu na podstawie Twoich potrzeb.
* Skopiuj i Zapisz klucz konta magazynu hello konto magazynu docelowego hello hello następny etap.

Dla dysków z danymi można wybrać tookeep niektóre dyski danych w ramach konta magazynu w warstwie standardowa (na przykład dysków, które mają lodówki magazynu), ale zdecydowanie zalecamy przeniesienie wszystkich danych magazyn w warstwie premium toouse obciążeń produkcyjnych.

#### <a name="copy-vhd-with-azcopy-or-powershell"></a>Krok 3. Skopiuj wirtualny dysk twardy z narzędzia AzCopy lub programu PowerShell
Konieczne będzie toofind Twojego ścieżka kontenera i dowolna z tych dwóch opcji konta tooprocess klucza magazynu. Kontener ścieżki i przechowywania klucza konta znajdują się w **Azure Portal** > **magazynu**. adresu URL kontenera Hello będzie takie jak "https://myaccount.blob.core.windows.net/mycontainer/".

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a>Opcja 1: Skopiuj dysk VHD o AzCopy (asynchroniczne kopia)
Przy użyciu narzędzia AzCopy, możesz wysłać hello wirtualnego dysku twardego za pośrednictwem hello Internet. W zależności od rozmiaru hello hello wirtualne dyski twarde to może potrwać. Należy pamiętać limity konta magazynu toocheck hello w wejście/wyjście, korzystając z tej opcji. Zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md) szczegółowe informacje.

1. Pobierz i zainstaluj narzędzie AzCopy stąd: [najnowszą wersję programu AzCopy](http://aka.ms/downloadazcopy)
2. Otwórz program Azure PowerShell i folder przejdź toohello, w którym zainstalowano narzędzia AzCopy.
3. Użyj hello następujące polecenie plik VHD hello toocopy z "Source" za "Miejsce docelowe".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Przykład:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    Poniżej przedstawiono opisy parametrów hello używana w hello polecenia programu AzCopy:

   * **/ Źródło:  *&lt;źródła&gt;:***  lokalizację folderu hello lub adresu URL kontenera magazynu zawierającego hello wirtualnego dysku twardego.
   * **/ SourceKey:  *&lt;źródła konta klucza&gt;:***  klucz konta magazynu z konta magazynu źródłowego hello.
   * **/ Dest:  *&lt;docelowego&gt;:***  toocopy adresu URL kontenera magazynu hello wirtualnego dysku twardego.
   * **/ DestKey:  *&lt;dest konta klucza&gt;:***  klucz konta magazynu konto magazynu docelowego hello.
   * **/ Wzorzec:  *&lt;nazwę pliku&gt;:***  Określ nazwę pliku hello hello toocopy wirtualnego dysku twardego.

Aby uzyskać więcej informacji na temat używania narzędzia AzCopy narzędzie, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md).

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a>Opcja 2: Kopiować dysku VHD przy użyciu programu PowerShell (Synchronized kopia)
Można także skopiować hello plik VHD za pomocą polecenia cmdlet programu PowerShell hello Start AzureStorageBlobCopy. Użyj hello następujące polecenia na toocopy programu Azure PowerShell wirtualnego dysku twardego. Zastąp wartości hello <> odpowiednie wartości w ramach konta magazynu źródłowego i docelowego. toouse to polecenie musi mieć kontener o nazwie wirtualne dyski twarde na koncie magazynu docelowego. Jeśli hello kontener nie istnieje, utwórz je przed uruchomieniem polecenia hello.

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

Przykład:

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a>Scenariusz 2: "I am Migrowanie maszyn wirtualnych z innych platform tooAzure magazyn w warstwie Premium."
W przypadku migracji z tooAzure — z usługi Azure Cloud Storage wirtualnego dysku twardego, należy wyeksportować hello katalogu lokalnego tooa wirtualnego dysku twardego. Ścieżka źródłowej pełną hello hello katalogu lokalnego wirtualnego dysku twardego przechowywania przydatną i przy użyciu narzędzia AzCopy tooupload on tooAzure magazynu.

#### <a name="step-1-export-vhd-tooa-local-directory"></a>Krok 1. Eksportowanie katalogu lokalnego tooa wirtualnego dysku twardego
##### <a name="copy-a-vhd-from-aws"></a>Skopiuj wirtualny dysk twardy z usług AWS
1. Jeśli używasz usług AWS wyeksportować hello EC2 wystąpienia tooa wirtualnego dysku twardego w zasobniku Amazon S3. Hello kroków opisanych w hello Amazon dokumentacji eksportowanie wystąpień EC2 Amazon tooinstall hello Amazon EC2 interfejsu wiersza polecenia (CLI) narzędzie i uruchom plik VHD tooa hello-wystąpienie export-polecenia Utwórz zadanie tooexport hello EC2 wystąpienia. Należy się toouse **wirtualnego dysku twardego** dla hello dysku &#95; obraz &#95; FORMAT zmiennej podczas uruchamiania hello **tworzenie — wystąpienie export zadania** polecenia. Witaj wyeksportowany plik wirtualnego dysku twardego jest zapisywany w zasobniku hello Amazon S3, którą określisz podczas tego procesu.

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. Pobierz plik VHD hello z hello przedział S3. Plik VHD wybierz hello, następnie **akcje** > **Pobierz**.

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a>Skopiuj wirtualny dysk twardy z innych chmury Azure z systemem innym niż
W przypadku migracji z tooAzure — z usługi Azure Cloud Storage wirtualnego dysku twardego, należy wyeksportować hello katalogu lokalnego tooa wirtualnego dysku twardego. Skopiować hello źródła pełną ścieżkę katalogu lokalnego hello przechowywania wirtualnego dysku twardego.

##### <a name="copy-a-vhd-from-on-premises"></a>Skopiuj wirtualny dysk twardy z lokalnymi
W przypadku migracji ze środowiska lokalnego wirtualnego dysku twardego, konieczne będzie ścieżki źródłowej pełną hello przechowywania wirtualnego dysku twardego. Ścieżka źródłowa Hello może być serwerem lokalizacji lub w udziale plików.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Krok 2. Utwórz lokalizację docelową hello dysk VHD
Utwórz konto magazynu do przechowywania dyski VHD. Należy wziąć pod uwagę następujące punkty podczas planowania miejsca hello toostore dyski VHD:

* Witaj docelowe konto magazynu może być standard lub premium magazynu w zależności od wymagań aplikacji.
* region konta magazynu Hello musi być taki sam jak magazyn w warstwie Premium obsługuje maszyny wirtualne Azure utworzysz w ostatnim etapie hello. Można skopiować nowego konta magazynu tooa lub hello toouse planu tego samego konta magazynu na podstawie Twoich potrzeb.
* Skopiuj i Zapisz klucz konta magazynu hello konto magazynu docelowego hello hello następny etap.

Stanowczo zaleca się możesz przeniesienie wszystkich danych magazyn w warstwie premium toouse obciążeń produkcyjnych.

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a>Krok 3. Przekaż hello wirtualnego dysku twardego tooAzure magazynu
Teraz, gdy dysk VHD znajdują się w katalogu lokalnym hello, można użyć narzędzia AzCopy lub AzurePowerShell tooupload hello VHD pliku tooAzure magazynu. Obie te opcje są dostępne w tym miejscu:

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a>Opcja 1: Przy użyciu programu Azure PowerShell Add-AzureVhd tooupload hello pliku VHD

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

Przykład <Uri> może być ***"https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd"***. Przykład <FileInfo> może być ***"C:\path\to\upload.vhd"***.

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a>Opcja 2: Przy użyciu pliku VHD hello tooupload AzCopy
Przy użyciu narzędzia AzCopy, możesz wysłać hello wirtualnego dysku twardego za pośrednictwem hello Internet. W zależności od rozmiaru hello hello wirtualne dyski twarde to może potrwać. Należy pamiętać limity konta magazynu toocheck hello w wejście/wyjście, korzystając z tej opcji. Zobacz [cele dotyczące wydajności i skalowalności magazynu Azure](storage-scalability-targets.md) szczegółowe informacje.

1. Pobierz i zainstaluj narzędzie AzCopy stąd: [najnowszą wersję programu AzCopy](http://aka.ms/downloadazcopy)
2. Otwórz program Azure PowerShell i folder przejdź toohello, w którym zainstalowano narzędzia AzCopy.
3. Użyj hello następujące polecenie plik VHD hello toocopy z "Source" za "Miejsce docelowe".

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Przykład:

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    Poniżej przedstawiono opisy parametrów hello używana w hello polecenia programu AzCopy:

   * **/ Źródło:  *&lt;źródła&gt;:***  lokalizację folderu hello lub adresu URL kontenera magazynu zawierającego hello wirtualnego dysku twardego.
   * **/ SourceKey:  *&lt;źródła konta klucza&gt;:***  klucz konta magazynu z konta magazynu źródłowego hello.
   * **/ Dest:  *&lt;docelowego&gt;:***  toocopy adresu URL kontenera magazynu hello wirtualnego dysku twardego.
   * **/ DestKey:  *&lt;dest konta klucza&gt;:***  klucz konta magazynu konto magazynu docelowego hello.
   * **/ BlobType: strony:** Określa, że docelowy hello stronicowych obiektów blob.
   * **/ Wzorzec:  *&lt;nazwę pliku&gt;:***  Określ nazwę pliku hello hello toocopy wirtualnego dysku twardego.

Aby uzyskać więcej informacji na temat używania narzędzia AzCopy narzędzie, zobacz [Transfer danych za pomocą wiersza polecenia Azcopy hello](storage-use-azcopy.md).

##### <a name="other-options-for-uploading-a-vhd"></a>Inne opcje przekazywanie wirtualnego dysku twardego
Możesz również przekazywać przy użyciu jednej z powitania po oznacza, że konto magazynu wirtualnego dysku twardego tooyour:

* [Obiektu Blob magazynu Azure kopiowania interfejsu API](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [Obiekty BLOB magazynu Azure Explorer przekazywania](https://azurestorageexplorer.codeplex.com/)
* [Dokumentacja interfejsu API REST usługi Import/Eksport magazynu](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> Zaleca się za pomocą usługi Import/eksport, jeśli szacowany czas przekazywania jest dłuższa niż 7 dni. Można użyć [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello czasu z jednostki rozmiaru i transferu danych.
>
> Import/Eksport można używać konta standard storage tooa toocopy. Konieczne będzie toocopy z konta magazynu toopremium standard storage przy użyciu narzędzia, takiego jak narzędzie AzCopy.
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a>Tworzenie maszyn wirtualnych platformy Azure przy użyciu magazyn w warstwie Premium
Po hello wirtualnego dysku twardego jest przekazany lub kopiowane toohello żądanego konta magazynu, wykonaj instrukcje hello w tej sekcji tooregister hello wirtualnego dysku twardego jako obraz systemu operacyjnego lub dysku systemu operacyjnego, w zależności od scenariusza, a następnie utwórz wystąpienie maszyny Wirtualnej z niego. dysk danych Hello wirtualnego dysku twardego może być dołączone toohello maszyny Wirtualnej, po jego utworzeniu.
Przykładowy skrypt migracji znajduje się na końcu hello w tej sekcji. Ten prosty skrypt nie jest zgodna wszystkie scenariusze. Może być konieczne tooupdate hello skryptu toomatch z konkretnego scenariusza. poniżej toosee, jeśli ten skrypt stosuje scenariuszu tooyour [A przykładowy skrypt migracji](#a-sample-migration-script).

### <a name="checklist"></a>Lista kontrolna
1. Zaczekaj na wszystkie dyski VHD hello Kopiowanie zostało ukończone.
2. Upewnij się, że magazyn w warstwie Premium jest dostępna w regionie hello, które w przypadku migracji do.
3. Zdecyduj, hello nowej serii maszyn wirtualnych, które będą używane. Powinna być funkcją Magazyn w warstwie Premium i hello rozmiar powinien mieścić się w zależności od dostępności hello w regionie hello i zgodnie z potrzebami.
4. Zdecyduj, hello dokładny rozmiar maszyny Wirtualnej, który będzie używany. Rozmiar maszyny Wirtualnej musi toobe toosupport wystarczająco duży hello liczba dysków danych, do których masz. Na przykład Jeśli masz 4 dyski danych hello maszyna wirtualna musi mieć co najmniej 2 rdzeni. Należy również rozważyć przetwarzania zasilania, pamięci i musi przepustowości sieci.
5. Tworzenie konta Premium Storage w obszarze docelowym hello. To jest konto hello użyjesz hello nowej maszyny Wirtualnej.
6. Ma hello wirtualna szczegóły bieżącej przydatną tym hello listę dysków i odpowiednie obiekty BLOB dysków VHD.

Przygotowanie aplikacji dla przestoju. toodo czystą migracji należy toostop przetwarzania hello w bieżącym systemie hello. Następnie możesz pobrać go tooconsistent stanu, które można migrować toohello na nowej platformie. Czas trwania przestoju będzie zależeć od hello ilości danych w hello toomigrate dysków.

> [!NOTE]
> W przypadku tworzenia maszyny Wirtualnej platformy Azure Resource Manager z specjalne dysku VHD, można znaleźć zbyt[ten szablon](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) wdrażania Menedżera zasobów maszyny Wirtualnej przy użyciu istniejącego dysku.
>
>

### <a name="register-your-vhd"></a>Zarejestruj dysk VHD
toocreate Maszynę wirtualną z wirtualnego dysku twardego systemu operacyjnego lub tooattach tooa dysku danych nowej maszyny Wirtualnej, najpierw należy zarejestrować je. Wykonaj poniższe kroki w zależności od scenariusza z wirtualnego dysku twardego.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Uogólniony wirtualny dysk twardy systemu operacyjnego toocreate wielu wystąpień maszyny Wirtualnej Azure
Po uogólniony obraz systemu operacyjnego, wirtualny dysk twardy jest przekazywane toohello konta magazynu, należy zarejestrować go w formie **obrazu maszyny Wirtualnej Azure** tak, aby z niego można utworzyć co najmniej jedno wystąpienie maszyny Wirtualnej. Użyj powitania po tooregister poleceń cmdlet programu PowerShell dysk VHD jako obrazu systemu operacyjnego maszyny Wirtualnej Azure. Podaj adres URL ukończenia kontenera hello gdzie wirtualnego dysku twardego został skopiowany do.

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

Skopiuj i Zapisz nazwę hello tego nowego obrazu maszyny Wirtualnej Azure. W powyższym przykładzie hello, jest *OSImageName*.

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Unikatowy wirtualnego dysku twardego systemu operacyjnego toocreate jedno wystąpienie maszyny Wirtualnej Azure
Hello unikatowy wirtualnego dysku twardego systemu operacyjnego — po magazynu przekazana toohello konto, zarejestruj go w formie **dysk systemu operacyjnego Azure** tak, aby z niego można utworzyć wystąpienia maszyny Wirtualnej. Użyj tych tooregister poleceń cmdlet programu PowerShell dysk VHD jako dysk systemu operacyjnego Azure. Podaj adres URL ukończenia kontenera hello gdzie wirtualnego dysku twardego został skopiowany do.

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

Skopiuj i Zapisz nazwę hello ten nowy dysk systemu operacyjnego Azure. W powyższym przykładzie hello, jest *OSDisk*.

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a>Dane dysku VHD toobe dołączony toonew wystąpienia maszyny Wirtualnej Azure
Po hello danych dysk wirtualny dysk twardy jest przekazany konta toostorage, zarejestruj go jako dysk danych Azure, dzięki czemu mogą być dołączone tooyour nowej serii DS, DSv2 serii lub wystąpienie maszyny Wirtualnej Azure serii GS.

Użyj tych tooregister poleceń cmdlet programu PowerShell dysk VHD jako dysk danych Azure. Podaj adres URL ukończenia kontenera hello gdzie wirtualnego dysku twardego został skopiowany do.

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

Skopiuj i Zapisz nazwę hello ten nowy dysk danych Azure. W powyższym przykładzie hello, jest *DataDisk*.

### <a name="create-a-premium-storage-capable-vm"></a>Tworzenie maszyny Wirtualnej obsługuje magazyn w warstwie Premium
Raz hello obrazu systemu operacyjnego lub dysku systemu operacyjnego są rejestrowane, tworzenie nowej serii DS, dsv2 lub GS-series maszyny Wirtualnej. Będziesz używać obrazu systemu operacyjnego hello lub nazwa dysku systemu operacyjnego, który został zarejestrowany. Wybierz hello typu maszyny Wirtualnej z warstwy Premium Storage hello. W poniższym przykładzie użyto hello *Standard_DS2* rozmiar maszyny Wirtualnej.

> [!NOTE]
> Zaktualizuj toomake rozmiar dysku hello taka sama pojemność i wydajność wymagań i hello rozmiary dysku platformy Azure.
>
>

Polecenia cmdlet programu PowerShell krok po kroku hello wykonaj poniżej toocreate hello nowej maszyny Wirtualnej. Najpierw należy ustawić hello typowe parametry:

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

Najpierw należy utworzyć usługi w chmurze w którym będą obsługiwać nowych maszyn wirtualnych.

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

Następnie w zależności od scenariusza, utworzyć wystąpienie maszyny Wirtualnej Azure hello hello obrazu systemu operacyjnego lub dysku systemu operacyjnego, który został zarejestrowany.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Uogólniony wirtualny dysk twardy systemu operacyjnego toocreate wielu wystąpień maszyny Wirtualnej Azure
Utwórz co najmniej jednego nowego wystąpienia maszyny Wirtualnej Azure serii DS przy użyciu hello hello **obrazu systemu operacyjnego Azure** który został zarejestrowany. Określ nazwę tego obrazu systemu operacyjnego w konfiguracji maszyny Wirtualnej hello, podczas tworzenia nowej maszyny Wirtualnej, jak pokazano poniżej.

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Unikatowy wirtualnego dysku twardego systemu operacyjnego toocreate jedno wystąpienie maszyny Wirtualnej Azure
Utwórz wystąpienie maszyny Wirtualnej Azure nowej serii DS przy użyciu hello **dysk systemu operacyjnego Azure** który został zarejestrowany. Określ w konfiguracji maszyny Wirtualnej hello ta nazwa dysku systemu operacyjnego, podczas tworzenia hello nowej maszyny Wirtualnej, jak pokazano poniżej.

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

Określ inne informacje maszyny Wirtualnej platformy Azure, takich jak usługi w chmurze, region, konta magazynu, zestawu dostępności i zasad buforowania. Zauważ, że hello wystąpienia maszyny Wirtualnej musi być wspólnie z skojarzonego z nim systemu operacyjnego lub dysków z danymi, więc hello wybrane chmury usługi, regionu i konto magazynu muszą być wartościami hello tej samej lokalizacji co hello podstawowych dysków VHD tych dysków.

### <a name="attach-data-disk"></a>Dołączanie dysku danych
Ponadto jeśli zarejestrowano danych na dysku VHD, dołącz je toohello nowy magazyn w warstwie Premium obsługuje maszyny Wirtualnej platformy Azure.

Skorzystaj z następujących PowerShell polecenia cmdlet tooattach danych dysku toohello nowej maszyny Wirtualnej i określ hello zasad buforowania. W przykładzie poniżej hello zasad buforowania ustawiono zbyt*tylko do odczytu*.

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> Może być konieczne toosupport dodatkowe kroki aplikacji, która jest nie obejmuje się w tym przewodniku.
>
>

### <a name="checking-and-plan-backup"></a>Sprawdzanie i Planowanie tworzenia kopii zapasowej
Raz powitalne nowej maszyny Wirtualnej jest uruchomiony i działa, hello przy użyciu tego samego identyfikatora logowania i hasło dostępu do jako hello oryginalna maszyna wirtualna, a następnie sprawdź, czy wszystko działa zgodnie z oczekiwaniami. Wszystkie ustawienia hello, w tym woluminy rozłożone hello będą obecne w hello nowej maszyny Wirtualnej.

ostatni krok Hello jest harmonogram tworzenia kopii zapasowej i konserwacji tooplan powitalne nowej maszyny Wirtualnej na podstawie aplikacji hello potrzeb.

### <a name="a-sample-migration-script"></a>Przykładowy skrypt migracji
Jeśli masz wiele maszyn wirtualnych toomigrate automatyzacji za pomocą skryptów środowiska PowerShell będą przydatne. Oto przykładowy skrypt, który zautomatyzuje hello migracji maszyny wirtualnej. Uwaga poniżej skryptu jest tylko przykładem, a istnieje kilka założeń dotyczących hello bieżącego dysków maszyny Wirtualnej. Może być konieczne tooupdate hello skryptu toomatch z konkretnego scenariusza.

założenia Hello są:

* Tworzysz klasycznych maszyn wirtualnych platformy Azure.
* Źródła dysków systemu operacyjnego i dysków danych źródłowych znajdują się w tym samym koncie magazynu i tego samego kontenera. Jeśli dysków systemu operacyjnego i dysków z danymi nie znajdują się w hello same Umieść, można użyć narzędzia AzCopy lub Azure PowerShell toocopy dysków VHD za pośrednictwem konta magazynu i kontenerów. Zobacz poprzedni krok toohello: [kopii wirtualnego dysku twardego z narzędzia AzCopy lub środowiska PowerShell](#copy-vhd-with-azcopy-or-powershell). Edytowanie toomeet tego skryptu innym rozwiązaniem jest scenariusz, ale zaleca się użycie narzędzia AzCopy lub programu PowerShell, ponieważ jest łatwiejsze i szybsze.

skrypt automatyzacji Hello podano poniżej. Zastąp tekst z informacjami i zaktualizuj hello toomatch skryptu z konkretnego scenariusza.

> [!NOTE]
> Przy użyciu istniejącego skryptu hello nie zachowa konfiguracji sieci hello źródła maszyny Wirtualnej. Potrzebujesz ustawień sieciowych hello toore-config na zmigrowanych maszyn wirtualnych.
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a>Optymalizacja
Bieżąca konfiguracja maszyny Wirtualnej można dostosować w szczególności toowork prawidłowo w przypadku standardowych dysków. Na przykład tooincrease hello wydajności przy użyciu wielu dysków w woluminy rozłożone. Na przykład zamiast 4 dyski osobno na magazyn w warstwie Premium, może być możliwe toooptimize hello koszt przez jednego dysku. Optymalizacje, takich jak ta toobe konieczność obsługi na podstawie przypadku i wymagają niestandardowej czynności po migracji hello. Należy również zauważyć, że ten proces może nie również działać dla baz danych i aplikacji, które są zależne od układ dysku hello zdefiniowane w Instalatorze hello.

##### <a name="preparation"></a>Przygotowanie
1. Zakończenie hello proste migracji, zgodnie z opisem w hello wcześniej sekcji. Optymalizacje zostaną wykonane na powitania nowej maszyny Wirtualnej po migracji hello.
2. Zdefiniuj hello nowe rozmiary dysku wymagane do konfiguracji hello zoptymalizowane.
3. Należy określić mapowanie specyfikacji hello bieżącego dysków/woluminów toohello nowego dysku.

##### <a name="execution-steps"></a>Wykonanie czynności
1. Utwórz hello nowe dyski o odpowiednim rozmiarze hello na powitania Premium magazynu z maszyny Wirtualnej.
2. Toohello maszyny Wirtualnej i skopiuj hello dane logowania z hello bieżącego woluminu toohello nowego dysku mapowanego toothat woluminu. W tym wszystkie woluminy bieżącego hello, które wymagają toomap tooa nowego dysku.
3. Następnie zmienić hello aplikacji ustawienia tooswitch toohello nowe dyski i odłączyć hello starszych woluminów.

Dostrajanie aplikacji hello w celu zapewnienia lepszej wydajności dysku, można znaleźć w artykule zbyt[optymalizacji wydajności aplikacji](storage-premium-storage-performance.md#optimizing-application-performance).

### <a name="application-migrations"></a>Migracja aplikacji
Baz danych i innych złożonych aplikacji może wymagać specjalne kroki zgodnie z definicją w dostawcy aplikacji hello hello migracji. Można znaleźć w dokumentacji aplikacji toorespective. Na przykład zwykle baz danych można poddać migracji za pomocą kopii zapasowej i przywracania.

## <a name="next-steps"></a>Następne kroki
Zobacz następujące zasoby w określonych scenariuszach migracji maszyn wirtualnych hello:

* [Migrowanie maszyn wirtualnych platformy Azure między kontami magazynu](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Tworzenie i przekazywanie tooAzure wirtualnego dysku twardego z systemem Windows Server.](../../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Tworzenie i przekazywanie wirtualnego dysku twardego zawierający hello System operacyjny Linux](../../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migrowanie maszyn wirtualnych z usług AWS Amazon tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Zobacz też hello następujące zasoby toolearn więcej informacji na temat usługi Azure Storage i maszyn wirtualnych platformy Azure:

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Maszyny wirtualne platformy Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Premium Storage: magazyn o wysokiej wydajności dla obciążeń maszyn wirtualnych platformy Azure](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
