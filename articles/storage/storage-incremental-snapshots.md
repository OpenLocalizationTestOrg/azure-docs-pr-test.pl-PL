---
title: "aaaUse migawki przyrostowych kopii zapasowych i odzyskiwania niezarządzane dysków maszyny Wirtualnej platformy Azure | Dokumentacja firmy Microsoft"
description: "Tworzenie niestandardowego rozwiązania do tworzenia kopii zapasowych i odzyskiwania dysków maszyny wirtualnej platformy Azure przy użyciu przyrostowej migawki."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: 3524b987-bd65-4e35-83e7-fbc2136643e5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: aungoo
ms.openlocfilehash: 6d3e6d78e953f77a1028ac35dcde1ef046dbc3bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pl-PL
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>Tworzenie kopii zapasowej Azure niezarządzane dysków maszyny Wirtualnej z migawkami przyrostowe
## <a name="overview"></a>Omówienie
Usługa Azure Storage udostępnia możliwość hello migawki tootake obiektów blob. Migawki przechwytywania stanu obiektu blob hello w danym momencie. W tym artykule firma Microsoft opisano scenariusz jak może przechowywać kopie zapasowe przy użyciu migawek dysków maszyny wirtualnej. Po wybraniu toouse nie można użyć tej metody kopia zapasowa Azure i usługi odzyskiwania i chcą toocreate niestandardowych strategii tworzenia kopii zapasowych dysków maszyny wirtualnej.

Dyski maszyny wirtualnej platformy Azure są przechowywane jako stronicowe obiekty BLOB w usłudze Azure Storage. Ponieważ firma Microsoft mówimy więc o strategii tworzenia kopii zapasowych dysków maszyny wirtualnej w tym artykule, firma Microsoft będzie odwołanie toosnapshots w kontekście hello stronicowych obiektów blob. toolearn więcej informacji na temat migawek, zobacz zbyt[tworzenia migawki obiektu Blob](https://msdn.microsoft.com/library/azure/hh488361.aspx).

## <a name="what-is-a-snapshot"></a>Co to jest migawkę?
Migawki obiektu blob jest tylko do odczytu wersji obiektu blob przechwyconych w punkcie w czasie. Po utworzeniu migawki, to można można odczytać, kopiowane, lub usunięte, ale nie został zmodyfikowany. Migawki zapewniają tooback sposób się obiektu blob znajduje się na chwilę w czasie. Do POZOSTAŁEJ wersji 2015-04-05, trzeba było hello możliwości toocopy pełnej migawki. Z hello REST wersji 2015-07-08 lub wyższej, możesz również skopiować przyrostowe migawki.

## <a name="full-snapshot-copy"></a>Pełna migawka kopii
Migawki mogą być kopiowane konta magazynu tooanother jako zapasowe tookeep obiektów blob, hello podstawowego obiektu blob. Można także skopiować migawki przez blob podstawowej, czyli jak przywracanie tooan obiektu blob hello starszej wersji. Gdy migawki zostaną skopiowane z jednego tooanother konta magazynu, zajmie hello sam obszar jako obiektu blob strony podstawowej hello. W związku z tym Kopiowanie całego migawki z jednego tooanother konta magazynu będzie zajmować dużo czasu i będą korzystać z dużej ilości miejsca w hello docelowe konto magazynu.

> [!NOTE]
> Po skopiowaniu hello podstawowego obiektu blob tooanother docelowego migawki hello hello obiektu blob nie są kopiowane wraz z jej. Podobnie jeśli podstawowego obiektu blob zastąpić kopii, migawki skojarzone z obiektem blob podstawowej hello nie dotyczy i pozostać bez zmian w obszarze nazwy podstawowe obiektu blob.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>Wykonywanie kopii zapasowych dysków przy użyciu migawek
Jako strategii tworzenia kopii zapasowej dla dysków maszyny wirtualnej można migawek hello obiektu blob dysku lub stronę i skopiuj je tooanother konto magazynu przy użyciu narzędzia, takie jak [kopiowania obiektu Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) operacji lub [AzCopy](storage-use-azcopy.md). Można skopiować obiektu blob strony migawki tooa docelowy o innej nazwie. Obiekt blob Hello wynikowy docelowej strony jest zapisywalny stronicowy obiekt blob i nie migawki. W dalszej części tego artykułu możemy opisano kroki tootake kopie zapasowe przy użyciu migawek dysków maszyny wirtualnej.

### <a name="restore-disks-using-snapshots"></a>Przywracanie dysków za pomocą migawek
Gdy nadejdzie czas toorestore dysku tooa poprzedniej wersji stabilnej przechwycone w jednym z hello migawek kopii zapasowych, możesz skopiować migawki za pośrednictwem obiektu blob strony podstawowej hello. Po migawki hello jest awansowana toohello blob strony podstawowej, hello pozostaje migawki, ale jego źródło jest zastępowany kopii, którą można zarówno Odczyt i zapis. W dalszej części tego artykułu możemy opisano kroki toorestore poprzednią wersję dysku z jej migawek.

### <a name="implementing-full-snapshot-copy"></a>Implementowanie pełna migawka kopii
Wykonując poniższe polecenie hello, można zaimplementować pełna migawka kopii

* Najpierw Utwórz migawkę hello blob podstawowej za pomocą hello [migawki obiektu Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx) operacji.
* Następnie kopiowania hello migawki tooa docelowym magazynu konta za pomocą [kopiowania obiektu Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx).
* Powtórz ten proces toomaintain kopie zapasowe z podstawowego obiektu blob.

## <a name="incremental-snapshot-copy"></a>Kopiuj przyrostowe migawki
Nowa funkcja Hello w [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx) interfejs API udostępnia znacznie lepszą tooback sposób zapasowej migawki hello stronicowych obiektów blob lub dysków. Hello interfejsu API zwraca listę hello zmiany między hello podstawowej obiektów blob i hello migawki. Zmniejsza to hello ilość miejsca używanego na powitania konto kopii zapasowej. Hello interfejs API obsługuje stronicowych obiektów blob na magazyn w warstwie Premium, a także magazynu w warstwie standardowa. Przy użyciu tego interfejsu API, można teraz tworzyć szybsze i wydajne rozwiązania kopii zapasowej dla maszyn wirtualnych platformy Azure. Są to dostępnych hello REST wersji 2015-07-08 i wyższych.

Przyrostowa kopia migawki umożliwia toocopy z jednego magazynu konta tooanother hello różnicy między,

* Podstawowy obiektów blob i jego migawki lub
* Wszystkie migawki dwóch hello podstawowego obiektu blob

Podana hello następujące warunki są spełnione,

* Obiekt blob Hello utworzono Jan-1-2016 lub nowszy.
* Hello obiektu blob nie zostało zastąpione [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) lub [kopiowania obiektu Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) między dwiema migawkami.

**Uwaga**: Ta funkcja jest dostępna dla Premium i standardowa Azure stronicowe obiekty BLOB.

Jeśli masz niestandardowe strategii tworzenia kopii zapasowej, która korzysta z migawki, kopiowanie migawek hello z jednego tooanother konta magazynu może być bardzo wolno i zużywa dużo miejsca do magazynowania. Zamiast kopiować konta magazynu kopii zapasowej tooa cały migawki hello, można napisać hello różnica między blob kopii zapasowej strony tooa kolejnych migawek. W ten sposób hello czasu toocopy miejsca toostore kopii zapasowych i znacznie zmniejszyć.

### <a name="implementing-incremental-snapshot-copy"></a>Implementowanie kopiowania przyrostowe migawki
Można zaimplementować przyrostowe migawki kopii następujący hello

* Utwórz migawkę przy użyciu podstawowego obiektu blob hello [migawki obiektu Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx).
* Kopiuj hello migawki toohello docelowej magazynu kopii zapasowej konta przy użyciu [kopiowania obiektu Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx). Są to hello blob kopii zapasowej strony. Utworzenie migawki tej kopii zapasowej stronicowych obiektów blob i przechowywać w konto kopii zapasowej.
* Utwórz kolejną migawkę podstawowego obiektu blob hello za pomocą migawki obiektu Blob.
* Pobierz hello różnica między pierwszego i drugiego migawki za pomocą podstawowego obiektu blob [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx). Użyj nowego parametru hello **prevsnapshot** toospecify hello wartość DateTime ma różnicy hello tooget z migawki hello. Jeśli ten parametr jest obecny, hello odpowiedzi REST uwzględni tylko stron hello, które zostały zmienione między migawki docelowej i poprzednią migawkę tym wyczyść strony.
* Użyj [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) tooapply te zmiany toohello kopii zapasowej stronicowych obiektów blob.
* Na koniec migawki obiektu blob kopii zapasowej strony hello i zapisze go na koncie magazynu kopii zapasowej hello.

W następnej sekcji hello możemy opisano szczegółowo w sposób umożliwiający obsługę kopii zapasowych dysków przy użyciu przyrostowej migawki kopii

## <a name="scenario"></a>Scenariusz
W tej sekcji możemy opisano scenariusz, który obejmuje niestandardowych strategii tworzenia kopii zapasowej przy użyciu migawek dysków maszyny wirtualnej.

Rozważ premium magazynu P30 dysku maszyny Wirtualnej Azure serii DS. Witaj P30 dysk o nazwie *mypremiumdisk* są przechowywane na koncie magazynu premium o nazwie *mypremiumaccount*. Konto magazynu w warstwie standardowa nazywane *mybackupstdaccount* będzie służyć do przechowywania kopii zapasowej hello *mypremiumdisk*. Chcielibyśmy tookeep migawki z *mypremiumdisk* co 12 godzin.

toolearn dotyczące tworzenia konta magazynu i dyski, można znaleźć zbyt[kont magazynu Azure o](storage-create-storage-account.md).

toolearn o tworzeniu kopii zapasowych maszyn wirtualnych platformy Azure, zobacz zbyt[kopii zapasowych maszyny Wirtualnej Azure Planowanie](../backup/backup-azure-vms-introduction.md).

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>Kopie zapasowe toomaintain kroki dysk przy użyciu przyrostowej migawki
Hello opisane poniżej będzie migawek *mypremiumdisk* i obsługa kopii zapasowych hello w *mybackupstdaccount*. Witaj kopia zapasowa będzie standardowy stronicowy obiekt blob o nazwie *mybackupstdpageblob*. Witaj kopii zapasowej stronicowych obiektów blob będzie zawsze odzwierciedla hello sam stan jako ostatnia migawka hello z *mypremiumdisk*.

1. Najpierw utwórz hello kopii zapasowej stronicowych obiektów blob dla dysku magazynu premium. toodo, wykonaj migawki *mypremiumdisk* o nazwie *mypremiumdisk_ss1*.
2. Skopiuj to toomybackupstdaccount migawki jako stronicowy obiekt blob o nazwie *mybackupstdpageblob*.
3. Utwórz migawkę *mybackupstdpageblob* o nazwie *mybackupstdpageblob_ss1*za pomocą [migawki obiektu Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx) i zapisze go w *mybackupstdaccount*.
4. Podczas hello okna kopii zapasowej, Utwórz kolejną migawkę z *mypremiumdisk*, powiedz *mypremiumdisk_ss2*i zapisz go w *mypremiumaccount*.
5. Pobrać hello przyrostowe zmiany między migawki hello dwa *mypremiumdisk_ss2* i *mypremiumdisk_ss1*za pomocą [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx) na  *mypremiumdisk_ss2* z **prevsnapshot** toohello sygnaturę czasową ustawiono parametru *mypremiumdisk_ss1*. Zapisać te zmiany przyrostowe toohello kopii zapasowej stronicowych obiektów blob *mybackupstdpageblob* w *mybackupstdaccount*. W przypadku usunięto zakresów w hello przyrostowe zmiany, muszą zostać wyczyszczone z obiektu blob kopii zapasowej strony hello. Użyj [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) toowrite zmiany przyrostowe toohello kopii zapasowej strony blob.
6. Utworzenie migawki obiektu blob kopii zapasowej strony hello *mybackupstdpageblob*o nazwie *mybackupstdpageblob_ss2*. Usunąć poprzednią migawkę hello *mypremiumdisk_ss1* z konta magazynu premium.
7. Powtórz kroki 4 – 6 co okna kopii zapasowej. W ten sposób można zachować kopie zapasowe *mypremiumdisk* w ramach konta magazynu w warstwie standardowa.

![Tworzenie kopii zapasowej dysku przy użyciu przyrostowej migawki](./media/storage-incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>Kroki toorestore dysku z migawki
Witaj opisane poniżej spowoduje przywrócenie dysku premium *mypremiumdisk* tooan wcześniej migawki z konta magazynu kopii zapasowych hello *mybackupstdaccount*.

1. Zidentyfikuj hello punktu w czasie, którego chcesz toorestore hello premium dysku. Załóżmy, że utworzenie migawki *mybackupstdpageblob_ss2*, który jest przechowywany na koncie magazynu kopii zapasowej hello *mybackupstdaccount*.
2. W mybackupstdaccount, podwyższyć poziom migawki hello *mybackupstdpageblob_ss2* jako obiekt blob hello nowej strony podstawowej kopii zapasowej *mybackupstdpageblobrestored*.
3. Utworzenie migawki tej przywróconej kopii zapasowej stronicowych obiektów blob, nazywany *mybackupstdpageblobrestored_ss1*.
4. Kopiuj hello przywrócić stronicowych obiektów blob *mybackupstdpageblobrestored* z *mybackupstdaccount* za*mypremiumaccount* jako nowego dysku premium hello  *mypremiumdiskrestored*.
5. Utwórz migawkę *mypremiumdiskrestored*o nazwie *mypremiumdiskrestored_ss1* dokonywania przyszłych przyrostowych kopii zapasowych.
6. Wskaż serii hello DS dysku toohello przywrócić maszyny Wirtualnej *mypremiumdiskrestored* i odłączania hello starego *mypremiumdisk* z hello maszyny Wirtualnej.
7. Rozpocząć proces tworzenia kopii zapasowej hello opisanego w poprzedniej sekcji hello przywrócić dysku *mypremiumdiskrestored*, przy użyciu hello *mybackupstdpageblobrestored* jako hello blob kopii zapasowej strony.

![Przywracanie z migawki dysku](./media/storage-incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>Następne kroki
Dowiedz się więcej o tworzeniu migawki obiektu blob i planowania infrastruktury kopii zapasowych maszyn wirtualnych przy użyciu poniższych łączy hello.

* [Utworzenie migawki obiektu Blob](https://msdn.microsoft.com/library/azure/hh488361.aspx)
* [Zaplanuj infrastrukturę kopii zapasowej maszyny Wirtualnej](../backup/backup-azure-vms-introduction.md)

