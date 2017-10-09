
## <a name="about-vhds"></a>Informacje o wirtualnych dyskach twardych

Witaj dysków VHD używana w usłudze Azure są pliki VHD przechowywany jako stronicowe obiekty BLOB na koncie magazynu standard lub premium na platformie Azure. Aby uzyskać informacje na temat stronicowych obiektów blob, zobacz [Understanding block blobs and page blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs/) (Omówienie blokowych i stronicowych obiektów blob). Aby uzyskać szczegółowe informacje na temat magazynu w warstwie Premium, zobacz [High-performance premium storage and Azure VMs](../articles/storage/common/storage-premium-storage.md) (Magazyn w warstwie Premium o wysokiej wydajności i maszyny wirtualne platformy Azure).

Azure obsługuje hello stały format dysku VHD. Określa format Hello stałej hello dysku logicznego limit liniowo w pliku hello, więc ten dysk Przesunięcie X jest przechowywany przy przesunięciu obiektu blob X. Mała stopkę na końcu obiektu blob hello hello opisuje właściwości hello hello wirtualnego dysku twardego. Często hello ustalonym formacie marnuje miejsce, ponieważ większość dyski mają duże zakresy nieużywane w nich. Jednak Azure przechowuje pliki VHD w formacie rozrzedzonych, co otrzymasz hello zalet obu hello stałej i dynamiczne dyski na powitania sam czas. Aby uzyskać więcej szczegółów, zobacz [Getting started with virtual hard disks](https://technet.microsoft.com/library/dd979539.aspx) (Pierwsze kroki z wirtualnymi dyskami twardymi).

Wszystkie pliki VHD na platformie Azure, czy ma być toouse dysków toocreate źródłowych lub obrazy są tylko do odczytu. Po utworzeniu dysku lub obrazie Azure tworzy kopie hello pliki VHD. Te kopie mogą być tylko do odczytu lub odczytu i zapisu, w zależności od tego, jak używasz hello wirtualnego dysku twardego.

Po utworzeniu maszyny wirtualnej z obrazu Azure tworzy dysku dla maszyny wirtualnej hello, który jest kopią hello źródłowego pliku VHD. tooprotect przed przypadkowym usunięciem, Azure umieszcza dzierżawę na każdego pliku VHD źródła, który został użyty toocreate obrazu, dysk systemu operacyjnego lub dysku danych.

Przed usunięciem pliku VHD źródła należy tooremove hello dzierżawy przez usunięcie dysku hello lub obrazu. toodelete pliku VHD, który jest używany przez maszynę wirtualną jako dysk systemu operacyjnego, można usunąć maszyny wirtualnej hello, dysk systemu operacyjnego hello i plik VHD źródłowy hello jednocześnie przez usunięcie hello maszyny wirtualnej i usunięcie wszystkich skojarzonych dysków. Usunięcie pliku vhd będącego źródłem dysku danych wymaga jednak wykonania kilku kroków w ustalonej kolejności. Najpierw odłączyć dysku hello z hello maszyny wirtualnej, a następnie usuń hello dysku, a następnie usuń hello pliku VHD.

> [!WARNING]
> Jeśli usuniesz źródłowy plik vhd z magazynu albo usuniesz swoje konto magazynu, firma Microsoft nie będzie mogła odzyskać usuniętych danych.
> 

## <a name="types-of-disks"></a>Typy dysków 

Dyski platformy Azure zaprojektowano tak, aby zapewniały 99,999% dostępności. Dysku systemu Azure zostały spójnie dostarczone trwałości korporacyjnej, z branży, ZERO % Annualized częstość niepowodzeń.

Do wyboru podczas tworzenia dysków są dwie warstwy wydajności — magazyny Standard Storage i Premium Storage. Ponadto istnieją dwa typy dysków — niezarządzane i zarządzane — mogące występować w obu warstwach wydajności.


### <a name="standard-storage"></a>Standard Storage 

Magazyn Standard Storage bazuje na dyskach twardych (HDD) i stanowi ekonomiczne, chociaż wciąż wydajne rozwiązanie. Magazyn Standard Storage może być replikowany lokalnie w jednym centrum danych albo być objęty nadmiarowością geograficzną z głównym i dodatkowym centrum danych. Aby uzyskać więcej informacji na temat replikowania magazynu, zobacz [Replikacja usługi Azure Storage](../articles/storage/common/storage-redundancy.md). 

Aby uzyskać więcej informacji na temat korzystania z magazynu Standard Storage z dyskami maszyn wirtualnych, zobacz [Standard Storage and Disks](../articles/storage/common/storage-standard-storage.md) (Magazyn Standard Storage i dyski).

### <a name="premium-storage"></a>Premium Storage 

Magazyn Premium Storage bazuje na dyskach półprzewodnikowych (SSD) i oferuje dyski o wysokiej wydajności i małych opóźnieniach dla maszyn wirtualnych, na których działają obciążenia intensywnie korzystające z operacji wejścia/wyjścia. Magazyn w warstwie Premium mogą używających DS, DSv2, GS, Ls lub maszynach wirtualnych platformy Azure serii FS. Aby uzyskać więcej informacji, zobacz [Premium Storage](../articles/storage/common/storage-premium-storage.md).

### <a name="unmanaged-disks"></a>Dyski niezarządzane

Niezarządzane dyski są hello tradycyjnych typów dysków, które były używane przez maszyny wirtualne. Z tych opcji Tworzenie konta magazynu i konto magazynu można określić podczas tworzenia dysku hello. Masz toomake się, że zbyt wiele dysków nie umieszczaj hello tego samego konta magazynu, ponieważ mogła przekroczyć hello [wartości docelowe skalowalności](../articles/storage/common/storage-scalability-targets.md) hello konta magazynu (20 000 IOPS, na przykład), co powoduje hello ograniczane maszyn wirtualnych. W przypadku niezarządzanych dysków masz toofigure się, jak używać toomaximize hello z co najmniej jeden magazyn kont tooget hello najlepszą wydajność poza maszyn wirtualnych.

### <a name="managed-disks"></a>Dyski zarządzane 

Zarządzane uchwytów dyski magazynu hello uwzględnić tworzenia i zarządzania nimi w tle hello i sprawia, że nie mogą tooworry dotyczących ograniczeń skalowalności hello hello konta magazynu. Po prostu określić rozmiar dysku hello i warstwę wydajności hello (Standard/Premium) i Azure tworzy i zarządza hello dysku. Również w przypadku dodawania dysków lub skalować hello maszyny Wirtualnej w górę i w dół, nie masz tooworry o magazyn hello jest używany. 

Można również zarządzać niestandardowych obrazów w jedno konto magazynu na region platformy Azure i używać ich toocreate setki maszyn wirtualnych w hello tej samej subskrypcji. Aby uzyskać więcej informacji o dyskach zarządzanych, zobacz hello [omówienie dysków zarządzanych](../articles/virtual-machines/windows/managed-disks-overview.md).

Firma Microsoft zaleca użycia dysków zarządzanych Azure dla nowych maszyn wirtualnych i przekonwertować poprzedniej dysków toomanaged niezarządzane dysków, tootake zaletą hello wiele funkcji dostępnych w przypadku dysków zarządzanych.

### <a name="disk-comparison"></a>Porównanie dysków

Witaj w poniższej tabeli zapewnia porównanie Premium vs Standard zarówno niezarządzane, a zarządzane zdecyduj, jakie toouse toohelp dysków.

|    | Dysk platformy Azure w warstwie Premium | Dysk platformy Azure w warstwie Standardowa |
|--- | ------------------ | ------------------- |
| Typ dysku | Dyski półprzewodnikowe (SSD) | Dyski twarde (HDD)  |
| Omówienie  | Pamięć dyskowa o wysokiej wydajności i małych opóźnieniach, bazująca na dyskach SSD, przeznaczona dla maszyn wirtualnych uruchamiających obciążenia intensywnie korzystające z operacji wejścia/wyjścia lub hostujących środowisko produkcyjne o znaczeniu krytycznym | Ekonomiczna pamięć dyskowa oparta na dyskach HDD, przeznaczona dla scenariuszy z maszynami wirtualnymi do programowania i testowania |
| Scenariusz  | Obciążenia produkcyjne i wrażliwe na wydajność | Programowanie i testowanie, zastosowania niekrytyczne <br>Rzadki dostęp |
| Rozmiar dysku | P4: 32 GB (tylko w przypadku dysków zarządzane)<br>P6: 64 GB (tylko w przypadku dysków zarządzane)<br>P10: 128 GB<br>P20: 512 GB<br>P30: 1024 GB<br>P40: 2048 GB<br>P50: GB 4095 | Niezarządzane dysków: 1 GB – 4 TB (4095 GB) <br><br>Dyski zarządzane:<br> S4: 32 GB <br>S6: 64 GB <br>S10: 128 GB <br>S20: 512 GB <br>S30: 1024 GB <br>S40: 2048 GB<br>S50: GB 4095| 
| Maksymalna przepływność na dysk | 250 MB/s | 60 MB/s | 
| Maksymalna liczba operacji wejścia/wyjścia na dysk | 7500 IOPS | 500 IOPS | 

